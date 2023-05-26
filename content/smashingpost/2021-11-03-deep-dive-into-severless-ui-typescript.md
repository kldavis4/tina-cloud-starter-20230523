---
title: 'A Deep Dive Into Serverless UI With TypeScript'
slug: deep-dive-into-serverless-ui-typescript
author: ikeh-akinyemi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/aff46dfe-164d-4bf7-8e14-057470001b41/deep-dive-into-serverless-ui-typescript.jpg
date: 2021-11-03T11:30:00.000Z
summary: >-
  Serverless UI is simply a free, open-source command-line utility for quickly building and deploying serverless applications on the AWS platform. In this article, we will learn and cover everything needed on using Serverless UI to deploy our projects or serverless applications to cloud services providers. 
description: >-
  Serverless UI is simply a free, open-source command-line utility for quickly building and deploying serverless applications on the AWS platform. In this article, we will learn and cover everything needed on using Serverless UI to deploy our projects or serverless applications to cloud services providers.
categories:
  - Apps
  - Tools
  - TypeScript
  - Serverless
---

If you’ve been looking for a clear explanation of how applications can be developed and deployed to AWS with less configuration as possible, then I’ve prepared just the article for you. We’ll be breaking it all down into two parts: deploying a static web application (in this case a Notes application), and then a serverless web application to CloudFront using the Serverless UI library.

**Note**: *To follow along, you’ll need a basic understanding of AWS and web development in order to understand how the TypeScript project is built and used to deploy to AWS.*

## Requirements

Before starting to build our project, the following requirements need to be met:

- Basic knowledge of React, React Hooks, and Material UI;
- Good knowledge of TypeScript;
- Node.js version &gt;= `12.x.x` installed on your local machine;
- Have an AWS verified account;
- Configured your AWS CLI with local credentials;
- Ensure that `npm` or `yarn` is also installed as the package manager.

## Introduction

We’ll start with a few introductions on Serverless UI, but at the end of this tutorial, you should be able to comfortably use Serverless UI in your applications &mdash; from installing to understanding the concepts and implementing it in your very own projects. According to the [docs](https://github.com/JakePartusch/serverlessui) on GitHub:

<blockquote>“Serverless UI is simply a free, open-source command-line utility for quickly building and deploying serverless applications on the AWS platform.”</blockquote>

As stated, it’s a lightweight library that’s quickly installed over the terminal, and can be used to set up configure-domain, deploy static or serverless websites &mdash; all done on the terminal. This permits you to easily couple any choice of front-end framework with Serverless UI to deploy existing and new applications to AWS stress-free.

Serverless UI also works great with any static website, and websites that use serverless functions to handle requests to some sort of API. This makes it great for building serverless back-end applications. The deploy process through Serverless UI gives you the control to automatically deploy each part or in better words, iteration of your application with a different and separate URL. Though, this means you get to monitor the continuous integration and testing of your application with confidence in real-time. 

Using Serverless UI in production, you can choose to have your project or serverless functions written in native JavaScript or TypeScript. Either way, they’ll be bundled down extremely quickly and your functions deployed as Node.js 14 Lambda functions. Your functions within the `./functions` folder are deployed automatically as serverless functions on AWS. This approach means that we’ll be writing our code in the form of functions that will handle different tasks or requests within the application. So when we deploy our functions, we’ll invoke them in the format of an event. 

Then the need for a fast and very small application file size makes the Serverless UI be of good essence within our application. Being a command-line tool, it doesn’t need to be bundled inside the application &mdash; it can be installed globally, `npm install -g @serverlessui/cli` or as a `devDependency` within our application. This means no file size was added to our application, giving us the benefit of having only the code needed for our application to function. No extra added bundle size to our application. As with any migration, we developers know that migrating existing applications can be tough and troubling without downtime for our users, but it is doable depending on the use case.

{{% feature-panel %}} 

## Pros And Cons Of Using Serverless UI

Using Serverless UI within our projects, whether existing or new project has some **benefits** that it gives us:

- There are no middleman services unlike others; Serverless UI gives you out-of-the-box benefits of a pre-configured infrastructure without having to go through a middleman.
- It supports and works in almost any CI (**Continuous Integration**) environment owing that it’s a command-line tool readily available via npm. This is a plus for the backend and infrastructure setup.
- For already existing serverless applications or those that may have additional CloudFormation and/or CDK infrastructure, there is a full provision of CDK constructs for each of the CLI actions.
- Serverless UI provides almost any option during deploying your application &mdash; deploy your static website, Lambda functions or production code.
- Almost all configurations (such as `configure-domain` and deploying applications) are all done on the command line.
- Front-end frameworks like React, Svelte, Vue, or JQuery are all supported, as long as it compiles down to static code.
- Gives serverless applications the ability to scale dynamically per request, and won’t require any capacity planning or provisioning for the application.

These are some **downsides of Serverless UI** that we should consider before deciding to use it within our projects:

- There is only support for projects built using TypeScript or JavaScript within the project.
- Within recent time, the library core infrastructure is written with `aws-cdk`, which means the only platform our applications could be deployed to is AWS.

**Recommended Reading**: [*Local Testing A Serverless API (API Gateway And Lambda)*](https://www.smashingmagazine.com/2021/10/local-testing-serverless-api-gateway-lambda/)

## Setting Up The Notes Application

Nowadays, several tools are available for developers to efficiently manage infrastructures, for example, the **Serverless UI**, the console, or one of the frameworks available online. As explained above, our goal is to set up a simple demo of a Notes application in TypeScript, which will quickly help us to demonstrate how Serverless UI could be used in hosting it, so you can quickly grasp and implement it within your own projects.

For this tutorial, we’ll quickly explore and explain the different parts of a Notes application, then install **Serverless UI** library to host the application on AWS. 

We proceed to clone the remote repository on our local machine and run the command that will install all the dependencies.

<pre><code class="language-bash">git clone https://github.com/smashingmagazine/serverless-UI-typescript.git

yarn install</code></pre>

The above command clones a Note application that has the functional components built already, and then goes ahead to install the dependencies that are needed for the components to function. Here’s the list of the dependencies that are required for this Notes application to function:

<pre><code class="language-javascript">{
  ...
  "dependencies": {
    "@testing-library/jest-dom": "^5.11.4",
    "@testing-library/react": "^11.1.0",
    "@testing-library/user-event": "^12.1.10",
    "@types/jest": "^26.0.15",
    "@types/node": "^12.0.0",
    "@types/react": "^17.0.0",
    "@types/react-dom": "^17.0.0",
    "react": "^17.0.1",
    "react-dom": "^17.0.1",
    "react-scripts": "4.0.3",
    "typescript": "^4.1.2",
    "web-vitals": "^1.0.1"
  },
  ...
}
</code></pre>

The above list contains dependencies and their type definitions to work optimally with TypeScript. We proceed to explain the working parts of the application. But let’s first define interfaces for the Note data and the Props argument that will be passed down into our functions. Create a `/src/interfaces.ts` file and include the following:

<pre><code class="language-javascript">export interface INote {
  note: string;
}
export interface Props {
  content: INote;
  delContent(noteToDelete: string): void;
}</code></pre>

Here we’re defining the type structure that acts as a syntax contract between our components and the props passed within them. Also defines the unit data of our application state, `INote`.

For this application, we’ll focus mainly on the `/src/components` folder and the `/src/App.tsx` file. We’ll start from the `components` folder then gradually explain the rest of the application.

**Note:** *The styles defined and used throughout this Notes application can be found in the `/src/App.css` file.*

The `components` folder contains one file, the `Note.tsx` file; which will define the UI structure of each Note data we create. 

<pre><code class="language-javascript">import { INote } from "../Interfaces";

interface Props {
  content: INote;
  delContent(noteToDelete: number): void;
}

const Note = ({ content, delContent }: Props) =&gt; {
  return (
    &lt;div className="note"&gt;
      &lt;div className="content"&gt;
        &lt;span&gt;{content.note}&lt;/span&gt;
      &lt;/div&gt;
      &lt;button
        onClick={() =&gt; {
          delContent(content.id);
        }}
      &gt;
        X
      &lt;/button&gt;
    &lt;/div&gt;
  );
};
export default Note;
</code></pre>

Within the `Note` function, we’re destructuring a props parameter that has the data type definition of `Props`, and contains the `content` and `delContent` fields. The `content` field further contains the `note` field whose value will be the input value of our users. While the `delContent` field is a function to delete `content` from the application. 

We’ll proceed to build the general UI of the application, defining its two sections; one for creating the notes and the other to contain the list of notes already created:

<pre><code class="language-javascript">const App: FC = () =&gt; {
  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
      &lt;/div&gt;

      &lt;div className="noteList"&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default App;</code></pre>

The `div` tag with the **header** class contains the input and the button elements for creating and adding notes to the application:

<pre><code class="language-javascript">const App: FC = () =&gt; {
  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
        &lt;div className="inputContainer"&gt;
          &lt;input
            type="text"
            placeholder="Add Note..."
            name="note"
            value={noteContent}
            onChange={handleChange}
          /&gt;
        &lt;/div&gt;
        &lt;button onClick={addNote}&gt;Add Note&lt;/button&gt;
      &lt;/div&gt;

      ...
    &lt;/div&gt;
  );
};
export default App;</code></pre>

In the above code we recorded a new state, `noteContent`, for the `input` element’s value. Also an `onChange` event to update the **input** value. The `button` element has `onClick` event that will handle generating new content from the input’s value and adding it to the application. The above UI markup coupled with the already defined styles will look like:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b7b12a-581c-49ef-8ca3-00b55baaa71e/2-deep-dive-into-severless-ui-typescript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b7b12a-581c-49ef-8ca3-00b55baaa71e/2-deep-dive-into-severless-ui-typescript.png" width="800" height="250" sizes="100vw" caption="Header component. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/37b7b12a-581c-49ef-8ca3-00b55baaa71e/2-deep-dive-into-severless-ui-typescript.png'>Large preview</a>)" alt="The header component" >}}

Now let’s define the new states, `noteContent` and `noteList`, then the two events, `handleChange` and `addNote` functions to update our application functionalities:
 

<pre><code class="language-javascript">import { FC, ChangeEvent, useState } from "react";
import "./App.css";
import { INote } from "./Interfaces";

const App: FC = () =&gt; {
  const [noteContent, setNoteContent] = useState&lt;string&gt;("");
  const [noteList, setNoteList] = useState&lt;INote[]&gt;([]);

  const handleChange = (event: ChangeEvent&lt;HTMLInputElement&gt;) =&gt; {
      setNoteContent(event.target.value.trim());
  };

  const addNote = (): void =&gt; {
    const newContent = { Date.now(), note: noteContent };
    setNoteList([...noteList, newContent]);
    setNoteContent("");
  };
  
  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
        &lt;div className="inputContainer"&gt;
          &lt;input
            type="text"
            placeholder="Add Note..."
            name="note"
            value={noteContent}
            onChange={handleChange}
          /&gt;
        &lt;/div&gt;
        &lt;button onClick={addNote}&gt;Add Note&lt;/button&gt;
      &lt;/div&gt;

      ...
    &lt;/div&gt;
  );
};
export default App;
</code></pre>

The `noteList` state contains all the notes created within the application. We add and remove from it to update the UI with more notes created. Within the `handleChange` function, we’re regularly updating `noteContent` with the changes made to the input field using the `setNoteContent` function. The `addNote` function creates a `newContent` object with a `note` field whose value is gotten from `noteContent`. It then calls the `setNoteList` functions and creates a new `noteList` array from its previous state and `newContent`.

Next is to update the second section of the `App` function with the JSX code to contain the list of notes created:

<div class="break-out">

<pre><code class="language-javascript">...

import Note from "./Components/Note";

const App: FC = () =&gt; {
  ...

  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
        ...
      &lt;/div&gt;

      &lt;div className="noteList"&gt;
        {noteList.map((content: INote) =&gt; {
          return &lt;Note key={content.id} content={content} delContent={delContent} /&gt;;
        })}
      &lt;/div&gt;
    &lt;/div&gt;
  );
};

export default App;
</code></pre>
</div>

We’re looping through the `noteList` using the `Array.prototype.map` method to create the dump of notes within our application. Then we imported the `Note` component which defines the UI of our note, passing the `key`, `content` and `delContent` props into it. The `delContent` function as discussed earlier deletes `content` from the application:

<div class="break-out">

<pre><code class="language-javascript">...
import Note from "./Components/Note";

const App: FC = () =&gt; {
  ...
  const [noteList, setNoteList] = useState&lt;INote[]&gt;([]);

  ...

  const delContent = (noteID: number) =&gt; {
    setNoteList(
      noteList.filter((content) =&gt; {
        return content.id !== noteID;
      })
    );
  };
  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
        ...
      &lt;/div&gt;

      &lt;div className="noteList"&gt;
        {noteList.map((content: INote) =&gt; {
          return &lt;Note key={content.id} content={content} delContent={delContent} /&gt;;
        })}
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default App;</code></pre>
</div>

The `delContent` function filters out of `noteList` the `content`s that are not in any way equivalent to the `noteToDelete` argument. The `noteToDelete` is equivalent to `content.note` but gets passed down to `delContent` whenever a note is created by calling the `Note` component.

Coupling the two sections of the `App` component together, your code should look like the below:

<div class="break-out">

<pre><code class="language-javascript">import { FC, ChangeEvent, useState } from "react";
import "./App.css";
import Note from "./Components/Note";
import { INote } from "./Interfaces";

const App: FC = () =&gt; {
  const [noteContent, setNoteContent] = useState&lt;string&gt;("");
  const [noteList, setNoteList] = useState&lt;INote[]&gt;([]);

  const handleChange = (event: ChangeEvent&lt;HTMLInputElement&gt;) =&gt; {
      setNoteContent(event.target.value.trim());
  };

  const addNote = (): void =&gt; {
    const newContent = { id: Date.now(), note: noteContent };
    setNoteList([...noteList, newContent]);
    setNoteContent("");
  };

  const delContent = (noteID: number): void =&gt; {
    setNoteList(
      noteList.filter((content) =&gt; {
        return content.id !== noteID;
      })
    );
  };

  return (
    &lt;div className="App"&gt;
      &lt;div className="header"&gt;
        &lt;div className="inputContainer"&gt;
          &lt;input
            type="text"
            placeholder="Add Note..."
            name="note"
            value={noteContent}
            onChange={handleChange}
          /&gt;
        &lt;/div&gt;
        &lt;button onClick={addNote}&gt;Add Note&lt;/button&gt;
      &lt;/div&gt;

      &lt;div className="noteList"&gt;
        {noteList.map((content: INote) =&gt; {
          return &lt;Note key={content.id} content={content} delContent={delContent} /&gt;;
        })}
      &lt;/div&gt;
    &lt;/div&gt;
  );
};
export default App;
</code></pre>
</div>

And if we go ahead and add a few notes to our application, then our final UI will look like this:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09655bb-b586-4a73-8e69-069a57b90ebb/3-deep-dive-into-severless-ui-typescript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09655bb-b586-4a73-8e69-069a57b90ebb/3-deep-dive-into-severless-ui-typescript.png" width="800" height="397" sizes="100vw" caption="Notes application. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b09655bb-b586-4a73-8e69-069a57b90ebb/3-deep-dive-into-severless-ui-typescript.png'>Large preview</a>)" alt="The Notes application" >}}

Now we have created a simple Notes application that we can add and delete Notes, let’s move on to using Serverless UI to deploy this application to AWS and as well deploy a serverless back-end application (serverless functions).

{{% ad-panel-leaderboard %}}

### Deploying Notes Application With Serverless UI

Now we’re done explaining the components that make up our Notes application, it’s time to deploy our application using **Serverless UI** on the terminal. The first step in deploying our application to AWS is to configure the AWS CLI on our machine. Check [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) for comprehensive steps to take.

Next is to install the **Serverless UI library** globally on our local machine:

<pre><code class="language-bash">npm install -g @serverlessui/cli</code></pre>

This installs the package globally, meaning no extra file size was added within the build code.

Next is to make a `build` folder of the project, this is the folder we’ll reference within our terminal:

<pre><code class="language-bash">sui deploy --dir="build"
...
❯ Website Url: https://xxxxx.cloudfront.net</code></pre>

But for our project, we’ll run the `yarn` command that builds our application into a static website within the `build` folder, after which we run the **Serverless UI** command to deploy the application:

<div class="break-out">

<pre><code class="language-bash">yarn build 
...
Done in 80.63s.

sui deploy --dir="build"
...

✅  ServerlessUIAppPreview1c9ec9f1

Outputs:
ServerlessUIAppPreview1c9ec9f1.ServerlessUIBaseUrlCA2DC891 = https://dal254gl37fow.cloudfront.net

Stack ARN:
arn:aws:cloudformation:us-west-2:261955174750:stack/ServerlessUIAppPreview1c9ec9f1/e4dc82e0-fe44-11eb-b959-064619847e85
</code></pre>
</div>

Our application was successfully deployed, and the total time it took to deploy was less than five minutes. The application was deployed to Cloudfront [here](https://dal254gl37fow.cloudfront.net).

{{% ad-panel-leaderboard %}}

## Deploying Serverless Functions With Serverless UI

Here, we’ll focus on deploying Lambda functions written in our local environment, other than on the IDE provided on the AWS web platform. With Serverless UI, we’ll remove the hassle of doing a lot of configuration and set up before deploying it on AWS.

You’ll also want to ensure your local environment is as close to the production environment as possible. This includes the runtime, Node.js version. As a reminder, you need to install a version of Node.js supported by AWS Lambda.

The code or the `/serverless` folder used within this part of the article can be found [here](https://github.com/smashingmagazine/serverless-UI-typescript/tree/main/serverless). This folder contains the source file, that makes a request to an API to get a random note; a joke.

<pre><code class="language-javascript">const nodefetch = require("node-fetch");

exports.handler = async (event, context) =&gt; {
  const url = "https://icanhazdadjoke.com/";
  try {
    const jokeStream = await nodefetch(url, {
      headers: {
        Accept: "application/json"
      }
    });
    const jsonJoke = await jokeStream.json();
    return {
      statusCode: 200,
      body: JSON.stringify(jsonJoke)
    };
  } catch (err) {
    return { statusCode: 422, body: err.stack };
  }
};</code></pre>

Before we deploy the `serverless` folder, we’ll need to install `esbuild` library. This will help make bundling of the application files more fast and accessible.

<pre><code class="language-bash">npm install esbuild --save-dev</code></pre>

The next step to deploy the serverless function on AWS is by specifying the folder location with the `--functions` flag as we previously did with the `--dist` flag when deploying our static website.

<pre><code class="language-bash">sui deploy --functions="serverless"</code></pre>

While the above command helps us build our application, the serverless function successfully deploys it:

<div class="break-out">

<pre><code class="language-bash">...
 
✅  ServerlessUIAppPreview560dbd41

Outputs:
ServerlessUIAppPreview560dbd41.ServerlessUIFunctionPathjokesD9F032B9 = https://dwh6k64yrlqcn.cloudfront.net/api/jokes

Stack ARN:
arn:aws:cloudformation:us-west-2:261955174750:stack/ServerlessUIAppPreview560dbd41/21de6780-fb93-11eb-a0fb-061a2a83f0b9</code></pre>
</div>
 
- *The serverless function is now deployed to Cloudfront [here](https://dwh6k64yrlqcn.cloudfront.net/api/jokes).*

As a side note, we should be able to reference our API URL by relative path in our UI code like `/api/jokes` instead of the full URL if deployed at the same time with the `/dist` or `/build` folder. This should always work &mdash; even with CORS &mdash; since the UI and API are on the same domain.

But by default, Serverless Ui will create a new stack for every preview deployed, which means each URL will be different and unique. In order to deploy to the same URL multiple times, the `--prod` flag needs to be passed. 

<pre><code class="language-bash">sui deploy --prod --dir="dist" --functions="serverless"</code></pre>

Let’s create a `/src/components/Quote` folder and inside it create an `index.tsx` file. This contains the JSX code to house the quotes.

<pre><code class="language-javascript">import { useState } from "react";

const Quote = () =&gt; {
  const [joke, setJoke] = useState&lt;string&gt;();
  return (
    &lt;div className="container"&gt;
      &lt;p className="fade-in"&gt;{joke}&lt;/p&gt;
    &lt;/div&gt;
  );
};
export default Quote;</code></pre>

Next, we will make a request to the deployed serverless functions to retrieve a joke from it within a set interval of time. This way the note, i.e the joke, within the `<p className="fade-in">{joke}</p>` JSX markup gets updated every 2000 milliseconds.

<div class="break-out">

<pre><code class="language-javascript">import { useEffect, useState } from "react";

const Quote = () =&gt; {
  const [joke, setJoke] = useState&lt;string&gt;();

  useEffect(() =&gt; {
    const getRandomJokeEveryTwoSeconds = setInterval(async () =&gt; {
      const url = process.env.API_LINK || "https://dwh6k64yrlqcn.cloudfront.net/api/jokes";
      const jokeStream = await fetch(url);
      const res = await jokeStream.json();
      const joke = res.joke;
      setJoke(joke);
    }, 2000);
    return () =&gt; {
      clearInterval(getRandomJokeEveryTwoSeconds);
    };
  }, []);

  return (
    &lt;div className="container"&gt;
      &lt;p className="fade-in"&gt;{joke}&lt;/p&gt;
    &lt;/div&gt;
  );
};
export default Quote;</code></pre>
</div>

The code snippet added to the above source code will use `useEffect` hook to make API calls to the serverless functions, updating the UI with the jokes returned from the request by using the `setJoke` function provided from the `useState` hook.

Let’s restart our local development server to see the new changes added to our UI:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606e8d06-6c97-4e3f-9caf-60d771648df1/1-deep-dive-into-severless-ui-typescript.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606e8d06-6c97-4e3f-9caf-60d771648df1/1-deep-dive-into-severless-ui-typescript.png" width="800" height="417" sizes="100vw" caption="Notes application with a serverless function running on it. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/606e8d06-6c97-4e3f-9caf-60d771648df1/1-deep-dive-into-severless-ui-typescript.png'>Large preview</a>)" alt="Incorporated a serverless function that runs every two seconds in the Notes application" >}}

Before deploying the updates to your existing application, you can set up a custom domain, and using Serverless UI deploy and push subsequent code updates to this custom domain.

## Configure Domain With Serverless UI

We can deploy our serverless application to our custom domain rather than the default one provided by CloudFront. Configuring and deploying to our custom domain may take 20 &ndash; 48 hours to fully propagate but only needs to be completed once. Navigate into your project directory and run the command:

<pre><code class="language-bash">sui configure-domain --domain="&lt;custom-domain.com&gt;"</code></pre>

Replace the above value of the `--domain` flag with your own custom URL. Then you can continuously update the already deployed project by adding the `--prod` flag when using the `sui deploy` command again.

**Recommended Reading**: [*Building A Serverless Contact Form For Your Static Site*](https://www.smashingmagazine.com/2018/05/building-serverless-contact-form-static-website/)

## Conclusion

In this article, we introduced Serverless UI by discussing different merits that make it a good fit for deploying your application with it. Also, we created a demo of a simple Notes application and deployed it with the library. You can further build back-end serverless functions that are triggered by events happening with the application, and deploy them to your AWS lambda.

For the advanced use case of Serverless UI, we configured the default domain provided by CloudFront with our own custom domain name using **Serverless UI.** And for existing serverless projects or those that may have additional CloudFormation and/or CDK infrastructure, Serverless UI provides CDK constructs for each of the CLI actions. And with Serverless UI, we can easily configure a private S3 bucket &mdash; an extra desired feature for enhanced security on our serverless applications. Click [here](https://github.com/JakePartusch/serverlessui#configure-domain) to read up more on it.

- *The code used within this article can be found on [Github](https://github.com/smashingmagazine/serverless-UI-typescript).*

### Resources

- [Serverless UI Official documentation](https://github.com/JakePartusch/serverlessui)
- [Setting up AWS CLI](https://github.com/JakePartusch/serverlessui)

{{< signature "ks, vf, yk, il" >}}
