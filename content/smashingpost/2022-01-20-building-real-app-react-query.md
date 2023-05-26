---
title: 'Building The Real App With React Query'
slug: building-real-app-react-query
author: georgii-perepecho
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb299a88-9204-4579-bfb0-f9d8dac84014/building-real-app-react-query.jpg
date: 2022-01-20T14:30:00.000Z
summary: >-
  In this article, Georgii Perepecho explains the most common React Query features that you need to be familiar with when creating a real-life application that is stable when testing.
description: >-
  In this article, Georgii Perepecho explains the most common React Query features that you need to be familiar with when creating a real-life application that is stable when testing.
categories:
  - React
  - Apps
  - Workflow
  - Techniques
  - TypeScript
---

If you have ever built React applications that use asynchronous data you probably know how annoying it could be to handle different states (loading, error, and so on), share the state between components using the same API endpoint, and keep the synchronized state in your components. 

In order to refresh data, we should do a lot of actions: define `useState` and `useEffect` hooks, fetch data from the API, put the updated data to the state, change the loading state, handle errors, and so on. Fortunately, we have React Query, i.e. a library that makes fetching, caching, and managing the data easier.

## Benefits Of Using The New Approach

React Query has an impressive list of features:

- caching;
- deduping multiple requests for the same data into a single request;
- updating “out of date” data in the background (on windows focus, reconnect, interval, and so on);
- performance optimizations like pagination and lazy loading data;
- memoizing query results;
- prefetching the data;
- mutations, which make it easy to implement optimistic changes.

To demonstrate these features I’ve implemented an example application, where I tried to cover all cases for those you would like to use React Query. The application is written in TypeScript and uses CRA, React query, Axios mock server and material UI for easier prototyping.

## Demonstration The Example Application

Let’s say we would like to implement the car service system. It should be able to:

- log in using email and password and indicate the logged user;
- show the list of next appointments with load more feature;
- show information about one particular appointment;
- save and view changes history;
- prefetch additional information;
- add and amend required jobs.

{{% feature-panel %}}

## Client-Side Interaction

As we don’t have a real backend server, we will use `axios-mock-adapter`. I prepared some kind of `REST API` with get/post/patch/delete endpoints. To store data, we will use fixtures. Nothing special &mdash; just variables which we will mutate.

Also, in order to be able to view state changes, I’ve set the delay time as 1 second per request.

## Preparing React Query For Using

Now we are ready to set up React Query. It’s pretty straightforward.

First, we have to wrap our app with the provider:

<pre><code class="language-javascript">const queryClient = new QueryClient();

ReactDOM.render(
 &lt;React.StrictMode&gt;
   &lt;Router&gt;
     &lt;QueryClientProvider client={queryClient}&gt;
       &lt;App /&gt;
       &lt;ToastContainer /&gt;
     &lt;/QueryClientProvider&gt;
   &lt;/Router&gt;
 &lt;/React.StrictMode&gt;,
 document.getElementById('root')
);</code></pre>

In `QueryClient()`, we could specify some global defaults.

For easier development, we will create our own abstractions for React Query hooks. To be able to subscribe to a query we have to pass a unique key. The easiest way to use strings, but it’s possible to use array-like keys.

In the official documentation, they use string keys, but I found it a bit redundant as we already have URLs for calling API requests. So, we could use the URL as a key, so that we don’t need to create new strings for keys.

However there are some restrictions: if you are going to use different URLs for `GET/PATCH`, for example, you have to use the same key, otherwise, React Query will not be able to match these queries. 

Also, we should keep in mind that it’s important to include not only the URL but also all parameters which we are going to use to make requests to the backend. A combination of URL and params will create a solid key which the React Query will use for caching.  

As a fetcher, we will use Axios where we pass a URL and params from `queryKey`. 

<pre><code class="language-javascript">export const useFetch = &lt;T&gt;(
 url: string | null,
 params?: object,
 config?: UseQueryOptions&lt;T, Error, T, QueryKeyT&gt;
) =&gt; {
 const context = useQuery&lt;T, Error, T, QueryKeyT&gt;(
   [url!, params],
   ({ queryKey }) =&gt; fetcher({ queryKey }),
   {
     enabled: !!url,
     ...config,
   }
 );

 return context;
};

export const fetcher = &lt;T&gt;({
 queryKey,
 pageParam,
}: QueryFunctionContext&lt;QueryKeyT&gt;): Promise&lt;T&gt; =&gt; {
 const [url, params] = queryKey;
 return api
   .get&lt;T&gt;(url, { params: { ...params, pageParam } })
   .then((res) =&gt; res.data);
};</code></pre>

Where `[url!, params]` is our key, setting `enabled: !!url` we use for pausing requests if there is no key (I’ll talk about that a bit later). For fetcher we could use anything &mdash; it doesn’t matter. For this case, I chose Axios.

For a smoother developer experience, it’s possible to use React Query Devtools by adding it to the root component.

<pre><code class="language-javascript">import { ReactQueryDevtools } from 'react-query/devtools';

ReactDOM.render(
 &lt;React.StrictMode&gt;
   &lt;Router&gt;
     &lt;QueryClientProvider client={queryClient}&gt;
       &lt;App /&gt;
       &lt;ToastContainer /&gt;
       &lt;ReactQueryDevtools initialIsOpen={false} /&gt;
     &lt;/QueryClientProvider&gt;
   &lt;/Router&gt;
 &lt;/React.StrictMode&gt;,
 document.getElementById('root')
);</code></pre>

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30ee2b9-752c-40c0-83c4-f610a19bc243/react-query-devtools.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30ee2b9-752c-40c0-83c4-f610a19bc243/react-query-devtools.png" width="800" height="224" sizes="100vw" caption="React Query devtools. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b30ee2b9-752c-40c0-83c4-f610a19bc243/react-query-devtools.png'>Large preview</a>)" alt="React Query devtools" >}}

Nice one!

## Authentication

To be able to use our app, we should log in by entering the email and password. The server returns the token and we store it in cookies (in the example app any combination of email/password works). When a user goes around our app we attach the token to each request.

Also, we fetch the user profile by the token. On the header, we show the user name or the loading if the request is still in progress. The interesting part is that we can handle a redirect to the login page in the root `App` component, but show the user name in the separate component. 

This is where the React Query magic starts. By using hooks, we could easily share data about a user without passing it as props.

`App.tsx`:

<pre><code class="language-javascript">const { error } = useGetProfile();

useEffect(() =&gt; {
 if (error) {
   history.replace(pageRoutes.auth);
 }
}, [error]);</code></pre>

`UserProfile.tsx`:

<pre><code class="language-javascript">const UserProfile = ({}: Props) =&gt; {
 const { data: user, isLoading } = useGetProfile();

 if (isLoading) {
   return (
     &lt;Box display="flex" justifyContent="flex-end"&gt;
       &lt;CircularProgress color="inherit" size={24} /&gt;
     &lt;/Box&gt;
   );
 }

 return (
   &lt;Box display="flex" justifyContent="flex-end"&gt;
     {user ? `User: ${user.name}` : 'Unauthorized'}
   &lt;/Box&gt;
 );
};</code></pre>

And the request to the API will be called just once (it is called deduping requests, and I’ll talk about it a bit more in the next section).

Hook to fetch the profile data:

<pre><code class="language-javascript">export const useGetProfile = () =&gt; {
 const context = useFetch&lt;{ user: ProfileInterface }&gt;(
   apiRoutes.getProfile,
   undefined,
   { retry: false }
 );
 return { ...context, data: context.data?.user };
};</code></pre>

We use the `retry: false` setting here because we don’t want to retry this request. If it fails, we believe that the user is unauthorized and do the redirect.

When users enter their login and password we send a regular `POST` request. Theoretically, we could use React Query mutations here, but in this case, we don’t need to specify `const [btnLoading, setBtnLoading] = useState(false);` state and manage it, but I think it would be unclear and probably over complicated in this particular case.

If the request is successful, we invalidate all queries to get fresh data. In our app it would be just 1 query: user profile to update the name in the header, but just to be sure we invalidate everything.

<pre><code class="language-javascript">if (resp.data.token) {
 Cookies.set('token', resp.data.token);
 history.replace(pageRoutes.main);
 queryClient.invalidateQueries();
}</code></pre>

If we wanted to invalidate just a single query we would use `queryClient.invalidateQueries(apiRoutes.getProfile);`.

{{< vimeo id="665979322" caption="A sign-in page and a user name loading." breakout="true" >}}

{{% ad-panel-leaderboard %}}

## More About Deduping Requests

Let’s assume that we have two different (or even the same) components on the page which use the same API endpoint. Usually, we would have to make two requests, which are actually the same, and it’s just a waste of the backend resources. Using React Query, we could dedupe API calls with the same params. This means that if we have components that call the same requests, the request will be made just once. 

In our app, we have two components: showing total appointments and the list. 

Total appointments component:

<pre><code class="language-javascript">const UsersSummary = () =&gt; {
 const { data: list, isLoading } = useGetAppointmentsList();

 if (!isLoading && !list) {
   return null;
 }

 return (
   &lt;Box mb={2}&gt;
     &lt;Card&gt;
       &lt;Box p={2}&gt;
         &lt;Typography&gt;
           Total appointments:{' '}
           {isLoading ? (
             &lt;Skeleton
               animation="wave"
               variant="rectangular"
               height={15}
               width="60%"
             /&gt;
           ) : (
             list!.pages[0].count
           )}
         &lt;/Typography&gt;
       &lt;/Box&gt;
     &lt;/Card&gt;
   &lt;/Box&gt;
 );
};</code></pre>

Users list component:

<pre><code class="language-javascript">const UsersList = () =&gt; {
 const {
   data: list,
   isLoading,
   fetchNextPage,
   hasNextPage,
   isFetchingNextPage,
 } = useGetAppointmentsList();

 return (
   &lt;&gt;
     &lt;Card&gt;
       {isLoading ? (
         &lt;List&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
         &lt;/List&gt;
       ) : (
         &lt;List&gt;
           {list!.pages.map((page) =&gt; (
             &lt;React.Fragment key={page.nextId || 0}&gt;
               {page.data.map((item) =&gt; (
                 &lt;UserItem
                   key={item.id}
                   id={item.id}
                   name={item.name}
                   date={item.appointment_date}
                 /&gt;
               ))}
             &lt;/React.Fragment&gt;
           ))}
         &lt;/List&gt;
       )}
     &lt;/Card&gt;
     {hasNextPage && (
       &lt;Box mt={2}&gt;
         &lt;Button
           variant="contained"
           color="primary"
           onClick={() =&gt; {
             fetchNextPage();
           }}
           disabled={isFetchingNextPage}
         &gt;
           {isFetchingNextPage ? 'Loading more...' : 'Load more users'}
         &lt;/Button&gt;
       &lt;/Box&gt;
     )}
   &lt;/&gt;
 );
};</code></pre>

They use the same hook `useGetAppointmentsList()` where we send the request to the API. As we could see, the request `GET /api/getUserList` was called just once.

{{< vimeo id="665980714" caption="Deduping requests for the same endpoint." breakout="true" >}}
  
## Load More List

In our app, we have an infinite list with a `Load more` button. We cannot implement that using a regular `useQuery` hook, that’s why we have `useInfiniteQuery`  hook, it makes it possible to handle pagination, using `fetchNextPage` function.

<pre><code class="language-javascript">export const useGetAppointmentsList = () =&gt;
 useLoadMore&lt;AppointmentInterface[]&gt;(apiRoutes.getUserList);</code></pre>

We have our own abstraction for the React Query hook:

<div class="break-out">

<pre><code class="language-javascript">export const useLoadMore = &lt;T&gt;(url: string | null, params?: object) =&gt; {
 const context = useInfiniteQuery&lt;
   GetInfinitePagesInterface&lt;T&gt;,
   Error,
   GetInfinitePagesInterface&lt;T&gt;,
   QueryKeyT
 &gt;(
   [url!, params],
   ({ queryKey, pageParam = 1 }) =&gt; fetcher({ queryKey, pageParam }),
   {
     getPreviousPageParam: (firstPage) =&gt; firstPage.previousId ?? false,
     getNextPageParam: (lastPage) =&gt; {
       return lastPage.nextId ?? false;
     },
   }
 );

 return context;
};</code></pre>
</div>

It’s pretty much the same that we have for `useFetch` hook, just here we specify `getPreviousPageParam` and `getNextPageParam` functions, based on the API response, and also we pass `pageParam` property to the fetcher function.

<pre><code class="language-javascript">const UsersList = () =&gt; {
 const {
   data: list,
   isLoading,
   fetchNextPage,
   hasNextPage,
   isFetchingNextPage,
 } = useGetAppointmentsList();

 return (
   &lt;&gt;
     &lt;Card&gt;
       {isLoading ? (
         &lt;List&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;UserItemSkeleton /&gt;
           &lt;/Box&gt;
         &lt;/List&gt;
       ) : (
         &lt;List&gt;
           {list!.pages.map((page) =&gt; (
             &lt;React.Fragment key={page.nextId || 0}&gt;
               {page.data.map((item) =&gt; (
                 &lt;UserItem
                   key={item.id}
                   id={item.id}
                   name={item.name}
                   date={item.appointment_date}
                 /&gt;
               ))}
             &lt;/React.Fragment&gt;
           ))}
         &lt;/List&gt;
       )}
     &lt;/Card&gt;
     {hasNextPage && (
       &lt;Box mt={2}&gt;
         &lt;Button
           variant="contained"
           color="primary"
           onClick={() =&gt; {
             fetchNextPage();
           }}
           disabled={isFetchingNextPage}
         &gt;
           {isFetchingNextPage ? 'Loading more...' : 'Load more users'}
         &lt;/Button&gt;
       &lt;/Box&gt;
     )}
   &lt;/&gt;
 );
};</code></pre>

`useInfiniteQuery` hook has several additional fields like `fetchNextPage`, `hasNextPage`, `isFetchingNextPage`, which we could use to handle our load more list. And methods `fetchNextPage`, `fetchPreviousPage`.

{{< vimeo id="665981134" caption="A load more list." breakout="true" >}}

## Background Fetching Indicator/Refetching

One of the most interesting features for me is refetching data if we change window focus, like switching between tabs. For example, it could be useful if data could be changed by several authors. In this case, if we keep the browser tab opened we don’t have to reload the page. We will see the actual data when we focus on the window. Moreover, we could use a flag, to indicate that fetching is in progress. React Query has several settings in case you don’t need it:

- `refetchInterval`,
- `refetchIntervalInBackground`,
- `refetchOnMount`,
- `refetchOnReconnect`,
- `refetchOnWindowFocus`.

Also it’s possible to disable/enable options globally:

<pre><code class="language-javascript">const queryClient = new QueryClient({
 defaultOptions: {
   queries: {
     refetchOnWindowFocus: false,
   },
 },
});</code></pre>

To indicate re-fetching we have `isFetching` flag to show loading state:

{{< vimeo id="665981692" caption="Background fetching after switching the tab." breakout="true" >}}

## Making Conditional Requests

As we use hooks to fetch the data it could be confusing how we can avoid making requests. As you know, we cannot use conditional statements with hooks, for example we cannot code like that:

<pre><code class="language-javascript">if (data?.hasInsurance) {
 const { data: insurance } = useGetInsurance(
   data?.hasInsurance ? +id : null
 );
}</code></pre>

Let’s assume in our app we should make an additional request to get insurance details, based on the appointment endpoint response.

If we want to make a request, we pass a key, otherwise we pass null.  

<div class="break-out">

<pre><code class="language-javascript">const { data: insurance } = useGetInsurance(data?.hasInsurance ? +id : null);

export const useGetInsurance = (id: number | null) =&gt;
 useFetch&lt;InsuranceDetailsInterface&gt;(
   id ? pathToUrl(apiRoutes.getInsurance, { id }) : null
 );</code></pre>
</div>

In our `useFetch` abstraction, we set enabled the property in the config as false in case we don’t have a key. In this case, React Query just pauses making requests.

For an appointment with `id = 1`, we have `hasInsurance = true`. Next, we make another request and show a check icon next to the name. This means that we received an `allCovered` flag from the `getInsurance` endpoint.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb338315-07fc-4110-ba76-52b57bb23f45/cancel-requests.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb338315-07fc-4110-ba76-52b57bb23f45/cancel-requests.png" width="800" height="426" sizes="100vw" caption="The request has been made. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bb338315-07fc-4110-ba76-52b57bb23f45/cancel-requests.png'>Large preview</a>)" alt="The request has been made." >}}

For an appointment with `id = 2` we have `hasInsurance = false`, and we don’t make requests for the insurance details.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d439a7e3-6f60-41a5-9398-30c1176bbb42/cancel-requests-1.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d439a7e3-6f60-41a5-9398-30c1176bbb42/cancel-requests-1.png" width="800" height="437" sizes="100vw" caption="The request has not been made. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d439a7e3-6f60-41a5-9398-30c1176bbb42/cancel-requests-1.png'>Large preview</a>)" alt="The request has not been made." >}}
  
## Simple Mutation With Data Invalidation

To create/update/delete data in React Query we use mutations. It means we send a request to the server, receive a response, and based on a defined updater function we mutate our state and keep it fresh without making an additional request.

We have a genetic abstraction for these actions.

<div class="break-out">

<pre><code class="language-javascript">const useGenericMutation = &lt;T, S&gt;(
 func: (data: S) =&gt; Promise&lt;AxiosResponse&lt;S&gt;&gt;,
 url: string,
 params?: object,
 updater?: ((oldData: T, newData: S) =&gt; T) | undefined
) =&gt; {
 const queryClient = useQueryClient();

 return useMutation&lt;AxiosResponse, AxiosError, S&gt;(func, {
   onMutate: async (data) =&gt; {
     await queryClient.cancelQueries([url!, params]);

     const previousData = queryClient.getQueryData([url!, params]);

queryClient.setQueryData&lt;T&gt;([url!, params], (oldData) =&gt; {
 return updater ? (oldData!, data) : data;
});


     return previousData;
   },
   // If the mutation fails, use the context returned from onMutate to roll back
   onError: (err, &#95;, context) =&gt; {
     queryClient.setQueryData([url!, params], context);
   },

   onSettled: () =&gt; {
     queryClient.invalidateQueries([url!, params]);
   },
 });
};</code></pre>
</div>

Let’s have a look in more detail. We have several `callback` methods: 

`onMutate` (if the request is successful):

1. Cancel any ongoing requests.
2. Save the current data into a variable.
3. If defined, we use an `updater` function to mutate our state by some specific logic, if not, just override the state with the new data. In most cases, it makes sense to define the `updater` function.
4. Return the previous data.

`onError` (if the request is failed):

1. Roll back the previous data.

`onSettled` (if the request is either successful or failed):

1. Invalidate the query to keep the fresh state.

This abstraction we will use for all mutation actions.

<pre><code class="language-javascript">export const useDelete = &lt;T&gt;(
 url: string,
 params?: object,
 updater?: (oldData: T, id: string | number) =&gt; T
) =&gt; {
 return useGenericMutation&lt;T, string | number&gt;(
   (id) =&gt; api.delete(`${url}/${id}`),
   url,
   params,
   updater
 );
};

export const usePost = &lt;T, S&gt;(
 url: string,
 params?: object,
 updater?: (oldData: T, newData: S) =&gt; T
) =&gt; {
 return useGenericMutation&lt;T, S&gt;(
   (data) =&gt; api.post&lt;S&gt;(url, data),
   url,
   params,
   updater
 );
};

export const useUpdate = &lt;T, S&gt;(
 url: string,
 params?: object,
 updater?: (oldData: T, newData: S) =&gt; T
) =&gt; {
 return useGenericMutation&lt;T, S&gt;(
   (data) =&gt; api.patch&lt;S&gt;(url, data),
   url,
   params,
   updater
 );
};</code></pre>

That’s why it’s very important to have the same set of `[url!, params]` (which we use as a key) in all hooks. Without that the library will not be able to invalidate the state and match the queries. 

Let’s see how it works in our app: we have a `History` section, clicking by `Save` button we send a `PATCH` request and receive the whole updated appointment object. 

First, we define a mutation. For now, we are not going to perform any complex logic, just returning the new state, that’s why we are not specifying the `updater` function.

<pre><code class="language-javascript">const mutation = usePatchAppointment(+id);

export const usePatchAppointment = (id: number) =&gt;
 useUpdate&lt;AppointmentInterface, AppointmentInterface&gt;(
   pathToUrl(apiRoutes.appointment, { id })
 );</code></pre>

**Note:** It uses our generic `useUpdate` hook.

Finally, we call the `mutate` method with the data we want to patch: `mutation.mutate([data!]);`.

{{< vimeo id="665985180" caption="Simple data mutation with invalidation." breakout="true" >}}

**Note**: In this component, we use an `isFetching` flag to indicate updating data on window focus (check `Background` fetching section), so, we show the loading state each time when the request is in-flight. That’s why when we click `Save`, mutate the state and fetch the actual response we show the loading state as well. Ideally, it shouldn’t be shown in this case, but I haven’t found a way to indicate a background fetching, but don’t indicate fetching when loading the fresh data.

<div class="break-out">

<pre><code class="language-javascript">const History = ({ id }: Props) =&gt; {
 const { data, isFetching } = useGetAppointment(+id);
 const mutation = usePatchAppointment(+id);

 if (isFetching) {
   return (
     &lt;Box&gt;
       &lt;Box pt={2}&gt;
         &lt;Skeleton animation="wave" variant="rectangular" height={15} /&gt;
       &lt;/Box&gt;
       &lt;Box pt={2}&gt;
         &lt;Skeleton animation="wave" variant="rectangular" height={15} /&gt;
       &lt;/Box&gt;
       &lt;Box pt={2}&gt;
         &lt;Skeleton animation="wave" variant="rectangular" height={15} /&gt;
       &lt;/Box&gt;
     &lt;/Box&gt;
   );
 }

 const onSubmit = () =&gt; {
   mutation.mutate(data!);
 };

 return (
   &lt;&gt;
     {data?.history.map((item) =&gt; (
       &lt;Typography variant="body1" key={item.date}&gt;
         Date: {item.date} &lt;br /&gt;
         Comment: {item.comment}
       &lt;/Typography&gt;
     ))}

     {!data?.history.length && !isFetching && (
       &lt;Box mt={2}&gt;
         &lt;span&gt;Nothing found&lt;/span&gt;
       &lt;/Box&gt;
     )}
     &lt;Box mt={3}&gt;
       &lt;Button
         variant="outlined"
         color="primary"
         size="large"
         onClick={onSubmit}
         disabled={!data || mutation.isLoading}
       &gt;
         Save
       &lt;/Button&gt;
     &lt;/Box&gt;
   &lt;/&gt;
 );
};</code></pre>
</div>

{{% ad-panel-leaderboard %}}

## Mutation With Optimistic Changes

Now let’s have a look at the more complex example: in our app, we want to have a list, where we should be able to add and remove items. Also, we want to make the user experience as smooth as we can. We are going to implement optimistic changes for creating/deleting jobs.

Here are the actions:

1. User inputs the job name and clicks `Add` button.
2. We immediately add this item to our list and show the loader on the `Add` button.
3. In parallel we send a request to the API.
4. When the response is received we hide the loader, and if it succeeds we just keep the previous entry, update its id in the list, and clear the input field.
5. If the response is failed we show the error notification, remove this item from the list, and keep the input field with the old value.
6. In both cases we send `GET` request to the API to make sure we have the actual state.

All our logic is:

<div class="break-out">

<pre><code class="language-javascript">const { data, isLoading } = useGetJobs();

const mutationAdd = useAddJob((oldData, newData) =&gt; [...oldData, newData]);
const mutationDelete = useDeleteJob((oldData, id) =&gt;
 oldData.filter((item) =&gt; item.id !== id)
);

const onAdd = async () =&gt; {
 try {
   await mutationAdd.mutateAsync({
     name: jobName,
     appointmentId,
   });
   setJobName('');
 } catch (e) {
   pushNotification(`Cannot add the job: ${jobName}`);
 }
};

const onDelete = async (id: number) =&gt; {
 try {
   await mutationDelete.mutateAsync(id);
 } catch (e) {
   pushNotification(`Cannot delete the job`);
 }
};</code></pre>
</div>

In this example we define our own `updater` functions to mutate the state by custom logic: for us, it’s just creating an array with the new item and filtering by `id` if we want to delete the item. But the logic could be any, it depends on your tasks.

React Query takes care of changing states, making requests, and rolling back the previous state if something goes wrong.

In the console you could see which requests axios makes to our mock API. We could immediately see the updated list in the UI, then we call `POST` and finally we call `GET`. It works because we defined `onSettled` callback in `useGenericMutation` hook, so after success or error we always refetch the data:

<pre><code class="language-javascript">onSettled: () =&gt; {
 queryClient.invalidateQueries([url!, params]);
},</code></pre>

{{< vimeo id="665985636" caption="Optimistic changes with background requests and data invalidation." breakout="true" >}}

**Note:** When I highlight the lines in the dev tools you could see a lot of made requests. This is because we change the window focus when we click on the Dev Tools window, and React Query invalidates the state.

If the backend returned the error, we would rollback the optimistic changes, and show the notification. It works because we defined `onError` callback in `useGenericMutation` hook, so we set previous data if an error happened:

<pre><code class="language-javascript">onError: (err, _, context) =&gt; {
 queryClient.setQueryData([url!, params], context);
},</code></pre>

{{< vimeo id="665985934" caption="Optimistic changes and rollback the data due to the error." breakout="true" >}}

## Prefetching

Prefetching could be useful if we want to have the data in advance and if there is a high possibility that a user will request this data in the near future.

In our example, we will prefetch the car details if the user moves the mouse cursor in the `Additional` section area.

{{< vimeo id="665986276" caption="Prefetching data if a user moves the cursor into the area." breakout="true" >}}

When the user clicks the `Show` button we will render the data immediately, without calling the API (despite having a 1-second delay).

<pre><code class="language-javascript">const prefetchCarDetails = usePrefetchCarDetails(+id);

onMouseEnter={() =&gt; {
 if (!prefetched.current) {
   prefetchCarDetails();
   prefetched.current = true;
 }
}}

export const usePrefetchCarDetails = (id: number | null) =&gt;
 usePrefetch&lt;InsuranceDetailsInterface&gt;(
   id ? pathToUrl(apiRoutes.getCarDetail, { id }) : null
 );</code></pre>

We have our abstraction hook for the prefetching: 

<pre><code class="language-javascript">export const usePrefetch = &lt;T&gt;(url: string | null, params?: object) =&gt; {
 const queryClient = useQueryClient();

 return () =&gt; {
   if (!url) {
     return;
   }

   queryClient.prefetchQuery&lt;T, Error, T, QueryKeyT&gt;(
     [url!, params],
     ({ queryKey }) =&gt; fetcher({ queryKey })
   );
 };
};</code></pre>

To render the car details we use `CarDetails` component, where we define a hook to retrieve data.

<pre><code class="language-javascript">const CarDetails = ({ id }: Props) =&gt; {
 const { data, isLoading } = useGetCarDetail(id);

 if (isLoading) {
   return &lt;CircularProgress /&gt;;
 }

 if (!data) {
   return &lt;span&gt;Nothing found&lt;/span&gt;;
 }

 return (
   &lt;Box&gt;
     &lt;Box mt={2}&gt;
       &lt;Typography&gt;Model: {data.model}&lt;/Typography&gt;
     &lt;/Box&gt;

     &lt;Box mt={2}&gt;
       &lt;Typography&gt;Number: {data.number}&lt;/Typography&gt;
     &lt;/Box&gt;
   &lt;/Box&gt;
 );
};

export const useGetCarDetail = (id: number | null) =&gt;
 useFetch&lt;CarDetailInterface&gt;(
   pathToUrl(apiRoutes.getCarDetail, { id }),
   undefined,
   { staleTime: 2000 }
 );</code></pre>

Good point that we don’t have to pass additional props to this component, so in the `Appointment` component we prefetch the data and in the `CarDetails` component we use `useGetCarDetail` hook to retrieve the prefetched data.

By setting extended `staleTime`, we allow users to spend a bit more time before they click on the `Show` button. Without this setting, the request could be called twice if it takes too long between moving the cursor on the prefetching area and clicking the button.

## Suspense

Suspense is an experimental React feature that makes it possible to wait for some code in a declarative way. In other words, we could call the Suspense component and define the `fallback` component, which we want to show while we are waiting for the data. We don't even need the `isLoading` flag from React Query. For more information please refer to the [official documentation](https://reactjs.org/docs/concurrent-mode-suspense.html).

Let’s say we have a `Service` list, and we want to show the error, and `Try again` button if something went wrong.

To get the new developer experience let’s use Suspense, React Query and Error Boundaries together. For the last one, we will use `react-error-boundary`
Library.

<pre><code class="language-javascript">&lt;QueryErrorResetBoundary&gt;
 {({ reset }) =&gt; (
   &lt;ErrorBoundary
     fallbackRender={({ error, resetErrorBoundary }) =&gt; (
       &lt;Box width="100%" mt={2}&gt;
         &lt;Alert severity="error"&gt;
           &lt;AlertTitle&gt;
             &lt;strong&gt;Error!&lt;/strong&gt;
           &lt;/AlertTitle&gt;
           {error.message}
         &lt;/Alert&gt;

         &lt;Box mt={2}&gt;
           &lt;Button
             variant="contained"
             color="error"
             onClick={() =&gt; resetErrorBoundary()}
           &gt;
             Try again
           &lt;/Button&gt;
         &lt;/Box&gt;
       &lt;/Box&gt;
     )}
     onReset={reset}
   &gt;
     &lt;React.Suspense
       fallback={
         &lt;Box width="100%"&gt;
           &lt;Box mb={1}&gt;
             &lt;Skeleton variant="text" animation="wave" /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;Skeleton variant="text" animation="wave" /&gt;
           &lt;/Box&gt;
           &lt;Box mb={1}&gt;
             &lt;Skeleton variant="text" animation="wave" /&gt;
           &lt;/Box&gt;
         &lt;/Box&gt;
       }
     &gt;
       &lt;ServicesCheck checked={checked} onChange={onChange} /&gt;
     &lt;/React.Suspense&gt;
   &lt;/ErrorBoundary&gt;
 )}
&lt;/QueryErrorResetBoundary&gt;</code></pre>

Within the Suspense component, we render our `ServiceCheck` component, where we call the API endpoint for the service list.

<pre><code class="language-javascript">const { data } = useGetServices();</code></pre>

In the hook, we set `suspense: true` and `retry: 0`.

<div class="break-out">

<pre><code class="language-javascript">export const useGetServices = () =&gt;
 useFetch&lt;ServiceInterface[]&gt;(apiRoutes.getServices, undefined, {
   suspense: true,
   retry: 0,
 });</code></pre>
</div>

On the mock server, we send a response of either `200` or `500` status codes randomly.

<pre><code class="language-javascript">mock.onGet(apiRoutes.getServices).reply((config) =&gt; {
 if (!getUser(config)) {
   return [403];
 }

 const failed = !!Math.round(Math.random());

 if (failed) {
   return [500];
 }

 return [200, services];
});</code></pre>

{{< vimeo id="665986628" caption="Handling the errors by using React Query, Suspense and ErrorBoundary." breakout="true" >}}

So, if we receive some error from the API, and we don't handle it, we show the red notification with the message from the response. Clicking on the `Try again` button we call `resetErrorBoundary()` method, which tries to call the request again. In React Suspense fallback, we have our loading skeleton component, which renders when we are making the requests.

As we could see, this is a convenient and easy way to handle async data, but keep in mind that this is unstable, and probably shouldn’t be used in production right now.

## Testing

Testing applications using React Query is almost the same as testing a regular application. We will use React Testing Library and Jest. 

First, we create an abstraction for the rendering components.

<div class="break-out">

<pre><code class="language-javascript">export const renderComponent = (children: React.ReactElement, history: any) =&gt; {
 const queryClient = new QueryClient({
   defaultOptions: {
     queries: {
       retry: false,
     },
   },
 });
 const options = render(
   &lt;Router history={history}&gt;
     &lt;QueryClientProvider client={queryClient}&gt;{children}&lt;/QueryClientProvider&gt;
   &lt;/Router&gt;
 );

 return {
   ...options,
   debug: (
     el?: HTMLElement,
     maxLength = 300000,
     opt?: prettyFormat.OptionsReceived
   ) =&gt; options.debug(el, maxLength, opt),
 };
};</code></pre>
</div>

We set `retry: false` as a default setting in `QueryClient` and wrap a component with `QueryClientProvider`.

Now, let’s test our `Appointment` component.

We start with the easiest one: just checking that the component renders correctly.

<div class="break-out">

<pre><code class="language-javascript">test('should render the main page', async () =&gt; {
 const mocked = mockAxiosGetRequests({
   '/api/appointment/1': {
     id: 1,
     name: 'Hector Mckeown',
     appointment_date: '2021-08-25T17:52:48.132Z',
     services: [1, 2],
     address: 'London',
     vehicle: 'FR14ERF',
     comment: 'Car does not work correctly',
     history: [],
     hasInsurance: true,
   },
   '/api/job': [],
   '/api/getServices': [
     {
       id: 1,
       name: 'Replace a cambelt',
     },
     {
       id: 2,
       name: 'Replace oil and filter',
     },
     {
       id: 3,
       name: 'Replace front brake pads and discs',
     },
     {
       id: 4,
       name: 'Replace rare brake pads and discs',
     },
   ],
   '/api/getInsurance/1': {
     allCovered: true,
   },
 });
 const history = createMemoryHistory();
 const { getByText, queryByTestId } = renderComponent(
   &lt;Appointment /&gt;,
   history
 );

 expect(queryByTestId('appointment-skeleton')).toBeInTheDocument();

 await waitFor(() =&gt; {
   expect(queryByTestId('appointment-skeleton')).not.toBeInTheDocument();
 });

 expect(getByText('Hector Mckeown')).toBeInTheDocument();
 expect(getByText('Replace a cambelt')).toBeInTheDocument();
 expect(getByText('Replace oil and filter')).toBeInTheDocument();
 expect(getByText('Replace front brake pads and discs')).toBeInTheDocument();
 expect(queryByTestId('DoneAllIcon')).toBeInTheDocument();
 expect(
   mocked.mock.calls.some((item) =&gt; item[0] === '/api/getInsurance/1')
 ).toBeTruthy();
});</code></pre>
</div>

We have prepared helpers to mock Axios requests. In the tests, we could specify URL and mock data.

<pre><code class="language-javascript">const getMockedData = (
 originalUrl: string,
 mockData: { [url: string]: any },
 type: string
) =&gt; {
 const foundUrl = Object.keys(mockData).find((url) =&gt;
   originalUrl.match(new RegExp(`${url}$`))
 );

 if (!foundUrl) {
   return Promise.reject(
     new Error(`Called unmocked api ${type} ${originalUrl}`)
   );
 }

 if (mockData[foundUrl] instanceof Error) {
   return Promise.reject(mockData[foundUrl]);
 }

 return Promise.resolve({ data: mockData[foundUrl] });
};

export const mockAxiosGetRequests = &lt;T extends any&gt;(mockData: {
 [url: string]: T;
}): MockedFunction&lt;AxiosInstance&gt; =&gt; {
 // @ts-ignore
 return axios.get.mockImplementation((originalUrl) =&gt;
   getMockedData(originalUrl, mockData, 'GET')
 );
};</code></pre>

Then, we check there is a loading state and next, wait for the unmounting of the loading component.

<div class="break-out">

<pre><code class="language-javascript">expect(queryByTestId('appointment-skeleton')).toBeInTheDocument();

 await waitFor(() =&gt; {
   expect(queryByTestId('appointment-skeleton')).not.toBeInTheDocument();
 });</code></pre>
</div>

Next, we check that there are necessary texts in the rendered component, and finally check that the API request for the insurance details has been called.

<div class="break-out">

<pre><code class="language-javascript">expect(
   mocked.mock.calls.some((item) =&gt; item[0] === '/api/getInsurance/1')
 ).toBeTruthy();</code></pre>
</div>

It checks that loading flags, fetching data and calling endpoints work correctly.

In the next text, we check that we do not call request for the insurance details if we don’t need it (remember in the component we have a condition, that if in the response from appointment endpoint there is a flag `hasInsurance: true` we should call the insurance endpoint, otherwise we shouldn’t).

<div class="break-out">

<pre><code class="language-javascript">test('should not call and render Insurance flag', async () =&gt; {
 const mocked = mockAxiosGetRequests({
   '/api/appointment/1': {
     id: 1,
     name: 'Hector Mckeown',
     appointment_date: '2021-08-25T17:52:48.132Z',
     services: [1, 2],
     address: 'London',
     vehicle: 'FR14ERF',
     comment: 'Car does not work correctly',
     history: [],
     hasInsurance: false,
   },
   '/api/getServices': [],
   '/api/job': [],
 });
 const history = createMemoryHistory();
 const { queryByTestId } = renderComponent(&lt;Appointment /&gt;, history);

 await waitFor(() =&gt; {
   expect(queryByTestId('appointment-skeleton')).not.toBeInTheDocument();
 });

 expect(queryByTestId('DoneAllIcon')).not.toBeInTheDocument();

 expect(
   mocked.mock.calls.some((item) =&gt; item[0] === '/api/getInsurance/1')
 ).toBeFalsy();
});</code></pre>
</div>

This test checks that if we have `hasInsurance: false` in the response, we will not call the insurance endpoint and render the icon.

Last, we are going to test mutations in our `Jobs` component. The whole test case:

<div class="break-out">

<pre><code class="language-javascript">test('should be able to add and remove elements', async () =&gt; {
 const mockedPost = mockAxiosPostRequests({
   '/api/job': {
     name: 'First item',
     appointmentId: 1,
   },
 });

 const mockedDelete = mockAxiosDeleteRequests({
   '/api/job/1': {},
 });

 const history = createMemoryHistory();
 const { queryByTestId, queryByText } = renderComponent(
   &lt;Jobs appointmentId={1} /&gt;,
   history
 );

 await waitFor(() =&gt; {
   expect(queryByTestId('loading-skeleton')).not.toBeInTheDocument();
 });

 await changeTextFieldByTestId('input', 'First item');

 await clickByTestId('add');

 mockAxiosGetRequests({
   '/api/job': [
     {
       id: 1,
       name: 'First item',
       appointmentId: 1,
     },
   ],
 });

 await waitFor(() =&gt; {
   expect(queryByText('First item')).toBeInTheDocument();
 });

 expect(
   mockedPost.mock.calls.some((item) =&gt; item[0] === '/api/job')
 ).toBeTruthy();

 await clickByTestId('delete-1');

 mockAxiosGetRequests({
   '/api/job': [],
 });

 await waitFor(() =&gt; {
   expect(queryByText('First item')).not.toBeInTheDocument();
 });

 expect(
   mockedDelete.mock.calls.some((item) =&gt; item[0] === '/api/job/1')
 ).toBeTruthy();
});</code></pre>
</div>

Let’s see what is happening here.

1. We mock requests for `POST` and `DELETE`.
2. Input some text in the field and press the button.
3. Mock `GET` endpoint again, because we assume that `POST` request has been made, and the real server should send us the updated data; in our case, it’s a list with 1 item.
4. Wait for the updated text in the rendered component.
5. Check that the `POST` request to `api/job` has been called.
6. Click the `Delete` button.
7. Mock `GET` endpoint again with an empty list (like in the previous case we assume the server sent us the updated data after deleting).
8. Check that deleted item doesn’t exist in the document.
9. Check that the `DELETE` request to `api/job/1` has been called.

**Important Note:** *We need to clear all mocks after each test to avoid mixing them up.*

<pre><code class="language-javascript">afterEach(() =&gt; {
 jest.clearAllMocks();
});</code></pre>

## Conclusion

With the help of this real-life application, we went through all of the most common React Query features: how to fetch data, manage states, share between components, make it easier to implement optimistic changes and infinite lists, and learned how to make the app stable with tests.

I hope I could interest you in trying out this new approach in your current or upcoming projects.

### Resources

- [Example app](https://github.com/horprogs/react-query) used in the article
- [Official documentation](https://react-query.tanstack.com/)
- [`Axios-mock-adapter`](https://github.com/ctimmerm/axios-mock-adapter)

{{< signature "vf, yk, il" >}}
