---
title: 'Smashing Podcast Episode 31 With Eve Porcello: What Is GraphQL?'
slug: smashing-podcast-episode-31
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8f3309f1-4454-444b-acf0-953697c2fe7a/smashing-podcast-episode-31.png
date: 2020-12-15T05:00:00.000Z
summary: >-
  In this episode, we’re talking about GraphQL. What is it, and how does solve some common API problems? Drew McLellan talks to expert Eve Porcello to find out.
description: >-
  In this episode, we’re talking about GraphQL. What is it, and how does solve some common API problems? Drew McLellan talks to expert Eve Porcello to find out.
categories:
  - Smashing Podcast
  - GraphQL
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

In this episode, we’re talking about GraphQL. What is it, and how does solve some common API problems? I spoke with expert Eve Porcello to find out.

<iframe src="https://share.transistor.fm/e/7e0f9d66/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- Eve [on Twitter](https://twitter.com/eveporcello)
- Eve’s company [Moon Highway](https://moonhighway.com)
- [Learning GraphQL](https://www.oreilly.com/library/view/learning-graphql/9781492030706/) from O’Reilly
- [Discover Your Path Through The GraphQL Wilderness](https://www.graphqlworkshop.com) - Eve’s GraphQL workshop launching early 2021

### Weekly Update

- [How To Use MDX Stored In Sanity In A Next.js Website](https://www.smashingmagazine.com/2020/12/mdx-stored-sanity-next-js-website/)  
*written by Jason Lengstorf*
- [Building A Conversational N.L.P Enabled Chatbot Using Google’s Dialogflow](https://www.smashingmagazine.com/2020/12/conversational-nlp-enabled-chatbot-google-dialogflow/)  
*written by Nwani Victory*
- [Ethical Considerations In UX Research: The Need For Training And Review](https://www.smashingmagazine.com/2020/12/ethical-considerations-ux-research/)  
*written by Victor Yocco*
- [Making Websites Easier To Talk To](https://www.smashingmagazine.com/2020/12/making-websites-accessible/)  
*written by Frederick O’Brien*
- [How To Design A Simple UI When You Have A Complex Solution](https://www.smashingmagazine.com/2020/12/design-simple-ui-complex-solution/)  
*written by Suzanne Scacca*

## Transcript

<p><a href="https://twitter.com/eveporcello"><img loading="lazy" decoding="async" style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/dc83c308-c1aa-4c26-8e5b-80e9c7f51281/eve-porcello-250x250.jpg" width="200" height="200" alt="Photo of Eve Porcello" /></a><span class="smashing-tv-host">Drew McLellan:</span> She’s a software engineer, instructor, author, and co-founder of training and curriculum development company, Moon Highway. Her career started writing technical specifications and creating UX designs for web projects. Since starting Moon Highway in 2012, she’s created video content for egghead.io and LinkedIn Learning, and has co-authored the books Learning React and Learning GraphQL for O’Reilly’s Media.</p>

<span class="smashing-tv-host">Drew:</span> She’s also a frequent conference speaker, and has presented at conferences including React Rally, GraphQL Summit, and OSCON. So we know she’s an expert in GraphQL, but did you know she once taught a polar bear to play chess? My smashing friends, please welcome Eve Porcello.

<span class="smashing-tv-host">Drew:</span> Hi Eve, how are you?

<span class="smashing-tv-speaker">Eve Porcello:</span> I’m smashing.

<span class="smashing-tv-host">Drew:</span> As I mentioned there, you’re very much an educator in things like JavaScript and React, but I wanted to talk to you today about one of your other specialist areas, GraphQL. Many of us will have heard of GraphQL in some capacity, but might not be completely sure what it is, or what it does, and in particular, what sort of problem it solves in the web stack.

<span class="smashing-tv-host">Drew:</span> So set the stage for us, if you will, if I’m a front end developer, where does GraphQL slot into the ecosystem and what function does it perform for me?

<span class="smashing-tv-speaker">Eve:</span> Yeah. GraphQL kind of fits between the front end and the backend. It’s kind of living in the middle between the two and gives a lot of benefits to front end developers and back end developers.

<span class="smashing-tv-speaker">Eve:</span> If you’re a front end developer, you can define all of your front ends data requirements. So if you have a big list of React components, for example, you could write a query. And that’s going to define all of the fields that you would need to populate the data for that page.

<span class="smashing-tv-speaker">Eve:</span> Now with the backend piece, it’s really own, because we can collect a lot of data from a lot of different sources. So we have data in REST APIs, and databases, and all these different places. And GraphQL provides us this nice little orchestration layer to really make sense of the chaos of where all of our data is. So it’s a really useful for kind of everybody all over the stack.

<span class="smashing-tv-host">Drew:</span> So it’s basically an API based technology, isn’t it? It sits between your front end and your back end and provide some sort of API, is that correct?

<span class="smashing-tv-speaker">Eve:</span> Yeah, that’s exactly right. Exactly.

<span class="smashing-tv-host">Drew:</span> I think, over the last decade, the gold standard for APIs has been rest. So if you have a client side app and you need to populate it with data from the backend, you would build a REST API endpoint and you’d query that. So where does that model fall down? And when might we need GraphQL to come in and solve that for us?

<span class="smashing-tv-speaker">Eve:</span> Well, the problem that GraphQL really helps us with, kind of the golden problem, the golden solution, I guess, that GraphQL provides is that with REST we’re over fetching a lot of data. So if I have slash users or slash products, that’s going to give me back all of the data every time I hit route.

<span class="smashing-tv-speaker">Eve:</span> With GraphQL, we can be a little bit pickier about what data we want. So if I only need four fields from an object that has a hundred, I’m going to be able to really pinpoint those fields and not have to load data into, or load all of that data I should say, into your device, because that’s a lot of extra legwork, for your phone especially.

<span class="smashing-tv-host">Drew:</span> I’ve seen and worked with REST APIs in the past that have an optional field where you can pass in a list of the data that you want back, or you can augment what comes back with extra things. And so I guess that’s identifying this problem, isn’t it? That’s saying, you don’t always want the same data back every time. So is it that GraphQL formalizes that approach of allowing the front end to specify what the backend is going to return, in terms of data?

<span class="smashing-tv-speaker">Eve:</span> Yeah, exactly. So your query then becomes how you ask, how you filter, how you grasp for any sort of information from anywhere.

<span class="smashing-tv-speaker">Eve:</span> I also think it’s important to note that we don’t have to tear down all of our REST APIs in order to work with GraphQL really successfully. A lot of the most successful implementations of GraphQL I’ve seen out there, it’s wrappers around REST APIs. And the GraphQL query really gives you a way to think about what data you need. And then maybe some of your data comes from our users and products, examples, some of the data comes from REST, some of it comes from a database.

<span class="smashing-tv-host">Drew:</span> I guess the familiar scenario is, you might have an endpoint on your website that returns information about a user to display the header. It might give you their username and their avatar. And you cull that on every page and populate the data, but then you find somewhere else in your app you need to display their full name.

<span class="smashing-tv-host">Drew:</span> So you add that to the endpoint and it starts returning that. And then you do your account management section, and you need like their mailing address. So that gets returned by that endpoint as well.

<span class="smashing-tv-host">Drew:</span> And before you know it, that endpoint is returning a whole heavy payload that costs quite a lot on the backend to put together, and obviously a lot to download.

<span class="smashing-tv-host">Drew:</span> And that’s been culled on every single page just to show an avatar. So I guess that’s the sort of problem that grows over time, that was so easy to fall into, particularly in big teams, that GraphQL, it’s on top of that problem. It knows how to solve that, and it’s designed around solving that.

<span class="smashing-tv-speaker">Eve:</span> Exactly. And yeah, I think that whole idea of a GraphQL Schema, I think is a really, it’s kind of less talked about than the query language part of GraphQL. But I really feel like the Schema in particular gives us this nice type system for API.

<span class="smashing-tv-speaker">Eve:</span> So anybody on the team, managers, front end developers, back end developers, anybody who is really dealing with data can come together, coalesce around what data we actually want to serve up on this API, and then everyone knows what that source of truth is, they can go build their own parts of the app based on that.

<span class="smashing-tv-speaker">Eve:</span> So there’s some tricky Schema management things that come up with that too. But as far as moving from microservices back to monoliths, we’re sort of doing that, but getting all of the benefits we like out of microservices still.

<span class="smashing-tv-host">Drew:</span> And do I understand correctly that the typical way of setting up a GraphQL system is that you’d have basically one route, which is the endpoint that you send all your queries to so you’re not having to... Often one of the most difficult things is working out what to name, and what the path should be that this particular query should be at. It’s returning users and products, should it be it slash users something, or slash product something?

<span class="smashing-tv-host">Drew:</span> With GraphQL you just have one endpoint that you just fire your queries to and you get back an appropriate response.

<span class="smashing-tv-speaker">Eve:</span> Exactly. Yeah. It’s a single endpoint. I guess, you still are dealing with problems of naming because you’re naming everything in the Schema. But as far as, I feel like a lot of companies who have made big bets on microservices, everyone’s like, what endpoints do we have? Where are they? How are they documented? And with GraphQL, we have one place, one kind of dictionary to look up anything that we want to find out about how the API works.

<span class="smashing-tv-host">Drew:</span> So, I’m very familiar with other query languages, like SQL is an obvious example of a query language that a lot of web developers will know. And the queries in that take the form of almost like a command. It’s a text string, isn’t it, Select this from that, where, whatever. What format do the queries take with GraphQL?

<span class="smashing-tv-speaker">Eve:</span> It’s still a tech string, but it doesn’t define where that logic comes from. And a lot of the logic is moved back to the server. So the GraphQL server, the GraphQL API is really responsible for saying, "Go get this data from where it is, filter it based on these parameters."

<span class="smashing-tv-speaker">Eve:</span> But in the query language, it’s very field oriented. So we just add fields for anything that we want to retrieve. We can put filters on those queries, of course, too. But I think it’s a little less direct about where that information comes from. A lot of the functionality is built into the server.

<span class="smashing-tv-host">Drew:</span> So you can mix and match in a query. You can make a request that brings back lots of different types of data in one request. Is that right?

<span class="smashing-tv-speaker">Eve:</span> Yeah, that’s absolutely right. So you could send a query for as many fields as your server would allow, and bring back all sorts of nested data. But that’s really how it works, we connect different types on fields. So I guess we’ll recycle my users and products idea, but the user might have a products field that returns a list of products. All of those are associated with other types as well. So as deeply nested as we want the query to go, we can.

<span class="smashing-tv-host">Drew:</span> So does that mean to retrieve the data for a typical view in your web application that might have all sorts of things going on, that you can just make one request to the backend and get that all in one go without needing to make different queries to different endpoints, because it’s all just one thing?

<span class="smashing-tv-speaker">Eve:</span> Yeah. That’s exactly the whole goal, is just a single query, define every field that you want, and then return it in one response.

<span class="smashing-tv-host">Drew:</span> And the queries are JSON based, is that right?

<span class="smashing-tv-speaker">Eve:</span> The query itself is a text string, but it typically returns JSON data. So if I have the fields, then my JSON response matches exactly, and so it’s really clear what you’re getting when you send that query, because the data response looks exactly the same.

<span class="smashing-tv-host">Drew:</span> A lot of the queries it seems like are for almost like bare objects, like a customer or a product. Is there a way to specify more complex queries where business logic is controlled at the backend? Say I want to get a list of teams for a user, but only where that user is an admin of a team and where the team plan hasn’t expired, and all those sorts of real constraints that we face in everyday web application development. Can that be achieved with GraphQL?

<span class="smashing-tv-speaker">Eve:</span> Absolutely. So that’s the real exciting, powerful thing about GraphQL is, you can move a lot of that logic to the server. If you had a complex query, some really specific type of user that you wanted to get, all you’d need to do in the Schema is say, "Get complicated user", and then on the server, there would be a function where you could write all of the logic in whatever language you wanted to. JavaScript is kind of the most popular GraphQL implementation language, but you don’t have to use that at all. So Python, Go, C++, whatever you want to use, you can build a GraphQL server with that. But yeah, you can define as complex a query as you’d like to.

<span class="smashing-tv-host">Drew:</span> And I guess that enables you to encapsulate a lot of business logic then in new types of objects. Is that fair? You know, you set up a complicated user and then you don’t need to think what a complicated user is, but you can just keep using that complicated user and know that the business logic is implemented on that. Is that right?

<span class="smashing-tv-speaker">Eve:</span> That’s exactly right. So I think this is really nice for front end folks because they can start to prototype based on that. And then the backend team could go implement those functions to make that work. And then there’s kind of this shared understanding for what that type actually is and who they are, and, "What are the fields on that type?" And everything can be handled by wherever in the stack GraphQL is working. And that’s why it’s not really a front end or a back end technology. It’s really kind of both, and neither.

<span class="smashing-tv-host">Drew:</span> It sounds like it’s sort of formalizing the API and the relationship between front end and backend, so everybody’s getting a predictable interface that is standardized.

<span class="smashing-tv-speaker">Eve:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> Which I guess in organizations where the front end and the backend are owned by different teams, which isn’t at all uncommon, I guess this approach also enables changes to be made, say, on the front end, it might require different data, without needing somebody who works on the backend to make the changes that correspond to that. You’ve still got this almost infinitely customizable API without requiring any work to be done to change it if you need new data.

<span class="smashing-tv-speaker">Eve:</span> Yeah, exactly right.

<span class="smashing-tv-host">Drew:</span> So is the GraphQL server responsible for formatting the response, or do you need to do that in your server side logic?

<span class="smashing-tv-speaker">Eve:</span> So the GraphQL server defines two things. It defines the Schema itself that lives on the server, and then it defines the resolver functions. Those are functions that go get the data from wherever it is. So if I have a REST API that I’m wrapping with GraphQL, the resolver would fetch from that API, transform the data however it needed to be, and then return it to the client in that function. You can use any sort of database functions you’d like to on that server as well. So if you have data in a bunch of different places, this is a really nice cohesive spot to put all of that data in and to kind of design all the logic around, "Where’s that data coming? How do we want to transform it?"

<span class="smashing-tv-host">Drew:</span> The client says, "I want a complex user", the server receives that in a query and could say, "Right, I’m going to look up the complex user resolver." Is that right?

<span class="smashing-tv-speaker">Eve:</span> Mm-hmm (affirmative).

<span class="smashing-tv-host">Drew:</span> Which is the function, and then you write your logic that your backend team, or whoever writes the logic inside that function, to do whatever is necessary to return a complex user.

<span class="smashing-tv-speaker">Eve:</span> Yeah, exactly.

<span class="smashing-tv-host">Drew:</span> So that could be calling other APIs, it could be querying a database, it could be looking stuff up in cache, or pretty much anything.

<span class="smashing-tv-speaker">Eve:</span> Pretty much anything. And then, as long as that return from the function matches the requirements of the Schema, matches what fields, what types, were returning there, then everything will work nice and harmoniously.

<span class="smashing-tv-host">Drew:</span> I guess it gives you a consistent response format across your entire API just by default. You don’t have to design what that looks like. You just get a consistent result.

<span class="smashing-tv-speaker">Eve:</span> Yeah, exactly.

<span class="smashing-tv-host">Drew:</span> I think that could be quite a win really, because it can be really difficult to maintain consistency across a big range of API end points, especially in larger teams. Different people are working on different things. Unless you have quite strict governance in place, it can get really complex really quickly, can’t it?

<span class="smashing-tv-speaker">Eve:</span> Yeah, absolutely. And I think that Schema is just such a nice little document to describe everything. You get the automatic benefit of being able to see all of the fields in that Schema whenever you’re trying to send queries to it, because you can send introspection queries and there’s all sorts of nice tools for that, like GraphQL and GraphQL Playground, little tools that you can use to interact with the API’s data.

<span class="smashing-tv-speaker">Eve:</span> But also, if you’ve ever played around with Postman, like to ping a REST API, a lot of those, the documentation doesn’t really exist or it’s tough to find, or things like that. GraphQL really gives you that nice cohesive layer to describe everything that might be part of that API.

<span class="smashing-tv-host">Drew:</span> Practically, how do things work on the server side? I mean, I guess you need to run a GraphQL service as part of your infrastructure, but what form does that take? Is it an entire server running on its own port? Or is it just like a library you integrate into your existing Express or Apache or whatever with a route that resolves to that service? How do you implement it?

<span class="smashing-tv-speaker">Eve:</span> Yeah, it’s an actual server. So kind of the most popular GraphQL implementations are Node.js servers. When GraphQL as a spec was released, the team released this reference implementation in JavaScript, kind of a Node server that served as the guidelines for all these other ones who have popped up. But yeah, you can run these servers on their own instances. You can put them on Lambda. So there’s Apollo Server Express, there’s Apollo Server Lambda; all sorts of different types of implementations that you can use to actually run this thing.

<span class="smashing-tv-host">Drew:</span> So you mentioned briefly before the concept of a Schema that the server has.

<span class="smashing-tv-speaker">Eve:</span> Yeah.

<span class="smashing-tv-host">Drew:</span> That gives you the ability to describe your types more strictly than just, you know, mapping a name to a resolver. There’s more involved there, is there?

<span class="smashing-tv-speaker">Eve:</span> Yeah. There’s a full language. So I’ve referenced the spec and I didn’t describe what it is. GraphQL itself is a spec that describes the query language and the Schema definition language. So it has its own syntax. It has its own rules for defining these types.

<span class="smashing-tv-speaker">Eve:</span> When you’re using the Schema definition language, you basically use all of the features of that language to think about, what are the types that are part of the API? It’s also where you define the queries, the mutations, which are the verbs, like the actions, create account login, things like that. And even GraphQL subscriptions, which are another cool thing, real time GraphQL that you can define right there in the Schema.

<span class="smashing-tv-speaker">Eve:</span> So yeah, the Schema really is super important. And I think that it gives us this nice type enforcement across our full Stack application, because as soon as you start to deviate from those fields and from those types, you start to see errors, which is, in that case, good, because you’re following the rules of the Schema.

<span class="smashing-tv-host">Drew:</span> Is there any crossover between that and TypeScript? Is there a sort of synergy between the two there?

<span class="smashing-tv-speaker">Eve:</span> Absolutely. So if you’re a person who talks about GraphQL a lot, sometimes people will tell you that it’s bad, and they’ll come up to you publicly, when you could do that, and talk about how GraphQL is no good. But a lot of times they skip out on the cool stuff you get from types. So as far as synergy with TypeScript goes, absolutely, you can auto-generate types for your front end application using the types from the Schema. So that’s a huge win because you can not only generate it the first time, which gives you great interoperability with your front end application, but also, as things change, you can regenerate types and then build to reflect those changes. So yeah, I think those things fit really nicely together as types start to be kind of the defacto rule.

<span class="smashing-tv-speaker">Eve:</span> ... to be kind of the defacto rule in JavaScript, they fit nicely together.

<span class="smashing-tv-host">Drew:</span> It seems to be a sort of ongoing theme with the way that TypeScript has been designed ... that’s not TypeScript, sorry. GraphQL has been designed that there’s a lot of about formalizing the interaction between the front end and the back end. And it’s coming as a solution in between the just creates consistency and a formalization of what so far has been otherwise a fairly scrappy experience with rest for a lot of people. One thing that we always have to keep in mind when writing client-side apps is that the code is subject to inspection and potentially modification. And having an API where the client can just request data could be dangerous. Now, if you can specify what fields you want, maybe that could be dangerous. Where in the sort of the whole stack, would you deal with the authorization of users and making sure that the business rules around your data enforced?

<span class="smashing-tv-speaker">Eve:</span> You would deal with that all on the server. So, that could happen in many different ways. You don’t have to use one off strategy, but your resolvers will handle your authorization. So that could mean wrapping an existing off REST API, like a service like Auth0 or something you’ve built on your own. That could mean interacting with an OAuth, like GitHub or Facebook or Google login, those types of things that involves kind of passing tokens back and forth with resolvers. But oftentimes that will be built directly into the Schema. So the Schema will say, I don’t know, we’ll create a login mutation. And then I send that mutation with my credentials and then on the server, all of those credentials are verified. So the client doesn’t have to worry so much, maybe a little bit of passing tokens and things like that. But most of that is just built into the server.

<span class="smashing-tv-host">Drew:</span> So essentially, that doesn’t really change compared to how we’re building rest endpoints at the moment. Rest as a technology, well, it doesn’t really deal with authorization either and we have middleware and things on the server that deals with it. And it’s just the same with GraphQL. You just deal with it. Are there any conventions in GraphQL community for doing that? Are there common approaches or is it all over the place for how people choose to implement it?

<span class="smashing-tv-speaker">Eve:</span> It’s honestly all over the place. I think most times you’ll see folks building off into the Schema and by that I mean, representing those types and authorized users versus regular users building those types into the Schema itself. But you’ll also see a lot of folks using third-party solutions. I mentioned Auth0. A lot of folks will kind of offload their authorization on to companies who are more focused on it, particularly smaller companies, startups, things like that. But you’ll also see bigger companies starting to create solutions for this. So AWS, Amazon has AppSync, which is their flavor of GraphQL, and they have author rolls built directly into AppSync. And that’s kind of cool just to be able to, I don’t know, not have to worry about all of that stuff or at least provide an interface for working with that. So a lot of these ecosystem tools have, I think authorization is such a big topic in GraphQL. They’ve seen kind of the need, the demand for auth solutions and standard approaches to handling auth on the graph.

<span class="smashing-tv-host">Drew:</span> I guess there’s hardly a, an implementation out there that doesn’t need some sort of authorization. So yeah, it’s going to be a fairly common requirement. We’re all sort of increasingly building componentized applications, particularly when we’re using things React and View and what have you. And the principle of loose coupling leaves us with lots of components that don’t necessarily know what else is running on the page around them. Is there a danger as a result of that, you could end up with lots of components querying for the same data and making multiple requests? Or is it just an architectural problem in your app that you need to solve for that? Are there sort of well-trodden solutions for dealing with that?

<span class="smashing-tv-speaker">Eve:</span> Well, I think because GraphQL for the most part, not 100% of the solutions, but almost every GraphQL query is sent over HTTP. So if you want to track down where those multiple requests are happening, it’s probably a fairly familiar problem to folks who are using rest data for their applications. So there are some tools like Paulo Client Dev Tools and Urkel Dev Tools for front end developers who are like, "What’s going on? Which queries are on this page?" That gives you really clear insights into what’s happening. There’s kind of several schools of thought with that. Do we create one big, huge query for all of the data for the page? Or do we create smaller queries to load data for different parts of the app? Both as you might imagine, they have their own drawbacks, just because if you have a big query, you’re waiting for more fields.

<span class="smashing-tv-speaker">Eve:</span> If you have smaller queries, there may be collisions between what data you’re requiring. But I think, and not to go off on too much of a tangent, but I’m there already. So the there’s something called the Deferred Directive that’s coming to the GraphQL spec and the Deferred Directive is going to help with kind of secondarily loading content. So let’s say you have some content at the top of the page, the super important content that you want to load first. If you add that to your query and then any subsequent fields get the deferred directive on that. It’s just a little decorator that you would add to a field, that will then say, "All right, load the important data first, then hold up and load the second data second." And it kind of gives you this, it’s the appearance of kind of streaming data to your front end, so that there’s perceived performance, there’s interactivity. People are seeing data right away versus waiting for every single field to load for the page, which yeah, it could be a problem.

<span class="smashing-tv-host">Drew:</span> Yeah. I guess that enables you to architect pages where everything that’s ... we don’t like to talk too much about the viewport, but it is everything above the fold, you could prioritize, have that load in and then secondarily load in everything sort of further down. So, we’ve talked a lot about querying data. One of the main jobs of an API is sending new and modified data back to the server for persistence. You mentioned briefly mutations earlier. That’s the terminology that’s GraphQL uses for writing data back to the server?

<span class="smashing-tv-speaker">Eve:</span> Exactly. So any sort of changes we want to make to the data, anything we want to write back to the server, those are mutations, and those are all just like queries, they’re named operations that live on the server. So you can think about what are all the things we want our users to be able to do? Represent those with mutations. And then again on the server, write all the functions that make that stuff work.

<span class="smashing-tv-host">Drew:</span> And is that just as simple as querying for data? Calling a mutation is just as easy?

<span class="smashing-tv-speaker">Eve:</span> Yeah. It’s part of the query language. It looks pretty much identical. The only difference is, well, I guess queries take in filters. So mutations taken what looked like filters in the query itself. But those are responsible for actually changing data. An email and a password might get sent with a mutation, and then the server collects that and then uses that to authorize the user.

<span class="smashing-tv-host">Drew:</span> So, just as before, you’re creating a resolver on the backend to deal with that and to do whatever needs to be done. One common occurrence when writing data is that you want to commit your changes and then re-query to get the sort of current state of it. Does GraphQL have a good workflow for that?

<span class="smashing-tv-speaker">Eve:</span> It sort of lives in the mutation itself. So, a lot times when creating your Schema you’ll create the mutation operation. I’ll stick with log-in, takes in the email and the password. And the mutation itself returned something. So it could return something as simple as a Boolean, this went well, or this went badly, or it could return an actual type. So oftentimes you’ll see the mutation like the log-in mutation, maybe it returns a user. So you get all the information about the user once they’re logged in. Or you can create a custom object type that gives you that user plus what time the user logged in, and maybe a little more metadata about that transaction in the return object. So again, it’s kind of up to you to design that, but that pattern is really baked into GraphQL.

<span class="smashing-tv-host">Drew:</span> This all sounds pretty great, but every technical choice involves trade-offs. What are the downsides of using GraphQL? Are there any scenarios where it’d be a really poor choice?

<span class="smashing-tv-speaker">Eve:</span> I think that the place where a GraphQL might struggle is creating a one-to-one map of-

<span class="smashing-tv-speaker">Eve:</span> ... struggle is creating a one-to-one map of tabular data. So let’s say you have, I don’t know, think a database table with all sorts of different fields and, I don’t know, thousands of fields on a specific type, things like that, that type of data can be represented nicely with GraphQL, but sometimes when you run a process to generate a Schema on that data, you’re left with, in a Schema, the same problems that you had in the database, which is maybe too much data that goes beyond what the client actually requires. So I think those places, they’re potentially problems. I’ve talked to folks who have auto-generated Schemas based on their data and it’s become a million line long Schema or something like that, just thousands and thousands of lines of Schema code. And that’s where it becomes a little tricky, like how useful is this as a human readable document?

<span class="smashing-tv-speaker">Eve:</span> Yeah. So any sort of situation where you’re dealing with a client, it is a really nice fit as far as modeling every different type of data, it becomes a little tricky if your data sources too large.

<span class="smashing-tv-host">Drew:</span> So it sounds like anywhere where you’re going to carefully curate the responses in the fields and do it more by hand, you can get really powerful results. But if you’re auto-generating stuff because you’ve just got a massive Schema, then maybe it becomes a little unwieldy.

<span class="smashing-tv-speaker">Eve:</span> Yeah. And I think people are listening and disagreeing with me on that because there are good tools for that as well. But I think kind of the place where GraphQL really shines is that step of abstracting logic to the server, giving front end developers the freedom to define their components or their front ends data requirements, and really managing the Schema as a team.

<span class="smashing-tv-host">Drew:</span> Is there anything sort of built into the query language to deal with pagination of results, or is that down to a custom implementation as needed?

<span class="smashing-tv-speaker">Eve:</span> Yeah. Pagination, you would build first into the Schema, so you could define pagination for that. There’s a lot of guidelines that have sort of emerged in the community. A good example to look at if you’re newer to GraphQL or not, I look at this all the time, is the GitHub GraphQL API. They’ve basically recreated their API for v4 of their public facing API using GraphQL. So that’s a good spot to kind of look at how is a actual big company using this at scale. A lot of folks have big APIs running, but they don’t make it public to everybody. So pagination is built into that API really nicely and you can return, I don’t know, the first 50 repositories that you’ve ever created, or you can also use cursor based pagination for returning records based on ideas in your data. So cursor based pagination and kind of positional pagination like first, last records, that’s usually how people approach that, but there’s many techniques.

<span class="smashing-tv-host">Drew:</span> Are there any big gotchas we should know going into using GraphQL? Say I’m about to deploy a new GraphQL installation for my organization, we’re going to build all our new API endpoints using GraphQL going forward. What should I know? Is there anything lurking in the bushes?

<span class="smashing-tv-speaker">Eve:</span> Lurking in the bushes, always with technology, right? I think one of the things that isn’t built into GraphQL, but can be implemented without too much hassle is API security. So for example, you mentioned if I have a huge query, we talked about this with authorization, but it’s also scary to open up an API where someone could just send a huge nested query, friends of friends, friends of friends, friends of friends, down and down the chain. And then you’re basically allowing people to DDoS you with these huge queries. So there’s things that you can set up on the server to limit query depth and query complexity. You can put queries on a safe list. So maybe your front ends, you know what they all are and it’s not a public API. So you only want to let certain queries come over the wire to you. So I would say before rolling that out, that is definitely a possible gotcha with the GraphQL.

<span class="smashing-tv-host">Drew:</span> You do a lot of instruction and training around GraphQL, and you’ve co-written the O’Reilly ’animal’ book with Alex Banks called Learning GraphQL. But you’ve got something new that you’re launching early in 2021, is that right?

<span class="smashing-tv-speaker">Eve:</span> That’s right. So I have been collaborating with egghead.io to create a full stack GraphQL video course. We’re going to build an API and front end for a summer camp, so everything is summer camp themed. And yeah, we’re just going to get into how to work with Apollo server, Apollo client. We will talk about scaling GraphQL APIs with Apollo Federation. We’ll talk about authorization strategies and all sorts of different things. So it’s just kind of collecting the things that I’ve learned from teaching over the past, I don’t know, three or four years GraphQL and putting it into one spot.

<span class="smashing-tv-host">Drew:</span> So it’s a video course that... Is it all just self-directed, you can just work your way through at your own pace?

<span class="smashing-tv-speaker">Eve:</span> Yeah, exactly. So it’s a big hefty course so you can work through it at your own pace. Absolutely.

<span class="smashing-tv-host">Drew:</span> Oh, that sounds really good. And it’s graphqlworkshop.com, is that right?

<span class="smashing-tv-speaker">Eve:</span> Graphqlworkshop.com, exactly.

<span class="smashing-tv-host">Drew:</span> And I’m looking forward to seeing that released because I think that’s something that I might need. So I’ve been learning all about GraphQL. What have you been learning about lately?

<span class="smashing-tv-speaker">Eve:</span> I’ve also been looking into Rust lately. So I’ve been building a lot of Rust Hello Worlds, and figuring out what that is. I don’t know if I know what that is yet, but I have been having fun tinkering around with it.

<span class="smashing-tv-host">Drew:</span> If you dear listener, would like to hear more from Eve, you can find her on Twitter where she’s @eveporcello, and you can find out about her work at moonhighway.com. Her GraphQL workshop, discover your path through the GraphQL wilderness, is coming out early in 2021 and can be found at graphqlworkshop.com. Thanks for joining us today, Eve. Do you have any parting words?

<span class="smashing-tv-speaker">Eve:</span> Parting words, have fun with GraphQL, take the plunge, you’ll enjoy it, and thanks so much for having me. I appreciate it.

{{< signature "il" >}}
