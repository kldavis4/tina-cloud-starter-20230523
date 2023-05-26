---
title: 'How To Build A Node.js API For Ethereum Blockchain'
slug: nodejs-api-ethereum-blockchain
author: john-agbanusi
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e30b657d-50c0-40f3-b684-6eb5d98ef32f/nodejs-api-ethereum-blockchain.jpg
date: 2021-01-19T16:30:00.000Z
summary: >-
  In this article, John Agbanusi explains how you can build a Node.js API from scratch by building and deploying an Ethereum Blockchain for decentralization. He also shows you a step-by-step process of integrating both the API and blockchain into a single API called a “decentralized application API”.
description: >-
  In this article, John Agbanusi explains how you can build a Node.js API from scratch by building and deploying an Ethereum Blockchain for decentralization. He also shows you a step-by-step process of integrating both the API and blockchain into a single API called a “decentralized application API”.
categories:
  - API
  - Node.js
  - JavaScript
  - Blockchain
---

Blockchain technology has been on the rise in the past ten years, and has brought a good number of products and platforms to life such as [Chainalysis](https://www.chainalysis.com/) (finance tech), [Burstiq](https://www.burstiq.com/technology/) (health-tech), [Filament](https://www.iotevolutionworld.com/iot/articles/441809-filament-launches-new-blockcha-development-kit-iot-developers.htm) (IoT), [Opus](https://opus.audio/) (music streaming) and [Ocular](https://ocular.biz/cybersecurity/) (cybersecurity).

From these examples, we can see that blockchain cuts across many products and use cases &mdash; making it very essential and useful. In fintech (finance tech), it’s used as decentralized ledgers for security and transparency in places like Chain, Chainalysis, and is also useful in health tech for the security of sensitive health data in Burstiq and Robomed &mdash; not to forget media tech such as Opus and Audius that also use blockchain for royalties transparency and thus get full royalties.

Ocular uses security that comes with blockchain for identity management for biometric systems, while Filament uses blockchain ledgers for real-time encrypted communication. This goes to show how essential blockchain has become to us by making our lives better. But what *exactly* is a blockchain?

A blockchain is a **database** that is shared across a network of computers. Once a record has been added to the chain, it is quite difficult to change. To ensure that all the copies of the database are the same, the network makes constant checks.

So why do we *need* blockchain? Blockchain is a **safe way to record activities** and keep data fresh while maintaining a record of its history compared to the traditional records or databases where hacks, errors, and downtimes are very possible. The data can’t be corrupted by anyone or accidentally deleted, and you benefit from both a historical trail of data and an instantly up-to-date record that can’t be erased or become inaccessible due to downtime of a server.

Because the whole blockchain is duplicated across many computers, any user can view the entire blockchain. Transactions or records are processed not by one central administrator, but by a network of users who work to verify the data and achieve a consensus.

Applications that use blockchain are called **dApps** (Decentralised Applications). Looking around today, we’ll mostly find decentralized apps in fintech, but blockchain goes beyond decentralized finance. We have health platforms, music streaming/sharing platforms, e-commerce platforms, cybersecurity platforms, and  IOTs moving towards decentralized applications (dApps) as cited above.

So, when would it make sense to consider using blockchain for our applications, rather than a standard database or record?

{{% feature-panel %}}

## Common Applications Of Blockchain

*   **Managing And Securing Digital Relationships**  
Anytime you want to keep a long-term, transparent record of assets (for example, to record property or apartment rights), blockchain could be the ideal solution. Ethereum ‘Smart contracts’, in particular, are great for facilitating digital relationships. With a smart contract, automated payments can be released when parties in a transaction agree that their conditions have been met.
*   **Eliminating Middlemen/Gatekeepers**  
For example, most providers currently have to interact with guests via a centralized aggregator platform, like Airbnb or Uber (that, in turn, takes a cut on each transaction). Blockchain could change all that.<br />For example, TUI is so convinced of the power of blockchain that it is [pioneering ways to connect hoteliers and customers directly](https://www.forbes.com/sites/bernardmarr/2018/12/07/the-amazing-ways-tui-uses-blockchain-to-revolutionize-the-travel-industry/). That way, they can transact via blockchain in an easy, safe and consistent way, rather than via a central booking platform.
*   **Record Secure Transactions Between Partners To Ensure Trust**  
A traditional database may be good for recording simple transactions between two parties, but when things get more complicated, blockchain can help reduce bottlenecks and simplify relationships. What’s more, the added security of a decentralized system makes blockchain ideal for transactions in general.<br />An example is the University Of Melbourne that [started storing its records in blockchain](https://about.unimelb.edu.au/newsroom/news/2017/october/university-of-melbourne-to-issue-recipient-owned-blockchain-records). The most promising use case for blockchain in higher education is to transform the “record-keeping” of degrees, certificates, and diplomas. This saves a lot of cost from dedicated servers for storage or records.
*   **Keeping Records Of Past Actions For Applications Where Data Is In Constant Flux**  
Blockchain is a better, safer way to record the activity and keep data fresh while maintaining a record of its history. The data can’t be corrupted by anyone or accidentally deleted, and you benefit from both a historical trail of data, plus an instantly up-to-date record. An example of a good use case is blockchain in e-commerce, both blockchain and e-commerce involve transactions.<br />Blockchain makes these transactions safer and faster while e-commerce activities rely on them. Blockchain technology enables users to share and [securely store digital assets](https://cointelegraph.com/news/bringing-blockchain-technology-to-e-commerce-current-trends) both automatically and manually. This technology has the capacity to handle user activities such as payment processing, product searches, product purchases, and customer care. It also reduces the expenses spent on inventory management and payment processing.
*   **Decentralisation Makes It Possible To Be Used Anywhere**  
Unlike before where we have to restrict ourselves to a particular region due to various reasons like currency exchange policies, limitations of payment gateways makes access to financial resources of many countries not in your region or continent hard. With the rise and power of blockchain’s decentralization or peer-to-peer system, this becomes easier to work with other countries.<br />For example, an e-commerce store in Europe can have consumers in Africa and not require a middleman to process their payment requests. Furthermore, these technologies are opening doors for online retailers to make use of the consumer markets in faraway countries with bitcoin, i.e. a cryptocurrency.
*   **Blockhain Is Technology-Neutral**  
Blockchain works with all and any technology stack being used by a developer. You don’t have to learn Node as a Python dev to use blockchain or learn Golang. This makes blockchain very easy to use.<br />We can actually use it directly with our front-end apps in Vue/React with the blockchain acting as our sole database for simple uncomplicated tasks and use cases like uploading data or getting hashes for displaying records for our users, or building frontend games like casino games and betting games (in which a high amount of trust is needed). Also, with the power of web3, we can store data in the chain directly.

Now, we have seen quite a number of the advantages of using blockchain, but when should we not bother using a blockchain at all?

## Disadvantages Of Blockchain

*   **Reduced Speed For Digital Transaction**  
Blockchains require huge amounts of computing power, which tends to reduce the speed of digital transactions, though there are workarounds it is advisable to use centralized databases when in need of high-speed transactions in milliseconds.
*   **Data Immutability**  
Data immutability has always been one of the biggest disadvantages of the blockchain. It is clear that multiple systems benefit from it including supply chain, financial systems, and so on. However, it suffers from the fact that once data is written, it cannot be removed. Every person on the earth has the right to privacy. However, if the same person utilizes a digital platform that runs on blockchain technology, then he will be unable to remove its trace from the system when he doesn’t want it there. In simple words, there is no way that he can remove his trace &mdash; leaving privacy rights into pieces.
*   **Requires Expertise Knowledge**  
Implementing and managing a blockchain project is hard. It requires thorough knowledge to go through the whole process. This is why it is hard to come across blockchain specialists or experts because it takes a lot of time and effort to train a blockchain expert. Hence this article is a good place to start and a good guide if you have already started.
*   **Interoperability**  
Multiple blockchain networks working hard to solve the distributed ledger problem uniquely makes it hard to relate them or integrate them with each other. This makes communication between different chains hard.
*   **Legacy Applications Integration**  
Many businesses and applications still use legacy systems and architecture; adopting blockchain technology requires a complete overhaul of these systems which I must say is not feasible for many of them.

Blockchain is still evolving and maturing all the time so don’t be surprised if these cons mentioned today become transformed to a pro later on. Bitcoin which is a cryptocurrency is one popular example of a blockchain, a popular blockchain that has been on the rise aside from bitcoin cryptocurrency is Ethereum blockchain. Bitcoin focuses on cryptocurrencies while Ethereum focuses more on smart contracts which have been the major driving force for the new tech platforms.

<p><strong>Recommended reading</strong>: <em><a href="https://www.investopedia.com/articles/investing/031416/bitcoin-vs-ethereum-driven-different-purposes.asp">Bitcoin vs. Ethereum: What’s the Difference?</a></em></p>

## Let’s Start Building Our API

With a solid understanding of blockchain, now let's look at how to build an Ethereum blockchain and integrate it into a standard API in Node.js. The ultimate goal is to get a good understanding of how dApps and Blockchain platforms are being built.

Most dApps have similar architecture and structure. Basically, we have a user that interacts with the dApp frontend — either web or mobile — which then interacts with the backend APIs. The backend, then, on request interacts with the smart contract(s) or blockchain through public nodes; these either run Node.js applications or the backend uses blockchain by directly running the Node.js software. There are still so many things in between these processes from choosing to build a fully decentralized application or semi-decentralized application to choosing what should be decentralized and how to safely store private keys.

<p><strong>Recommended reading</strong>: <em><a href="https://www.freecodecamp.org/news/how-to-design-a-secure-backend-for-your-decentralized-application-9541b5d8bddb/">Decentralized Applications Architecture: Back End, Security and Design Patterns</a></em></p>

## Things We Should Know First

For this tutorial, we’re going to try to build the backend of a <strong>decentralized music store app</strong> that uses the power of Ethereum blockchain for storing music and sharing it for downloads or streaming.

The basic structure of the application we’re trying to build has three parts:

1. <strong>Authentication</strong>, which is done by email; of course we need to add an encrypted password to the app.
2. <strong>Storage of data</strong>, with the music data is first stored in [ipfs](https://ipfs.io/) and the storage address is stored in the blockchain for retrieval.
3.  <strong>Retrieval</strong>, with any authenticated user being able to access the stored data on our platform and use it.

We will be building this with Node.js, but you can also build with Python or any other programming language. We’ll also see how to store media data in [IPFS](https://ipfs.io/), get the address and write functions to store this address in — and retrieve this address from a blockchain with the Solidity programming language.

Here are some tools that we should have at our disposal for building or working with Ethereum and Node.js.

- **Node.js**  
The first requirement is a Node application. We are trying to build a Node.js app, so we need a compiler. Please make sure you have [Node.js](https://nodejs.org) installed — and please download the latest long term support binary (<em>LTS</em>).
- **Truffle Suite**  
Truffle is a contract development and testing environment, as well as an asset pipeline for Ethereum blockchain. It provides an environment for compiling, pipelining, and running scripts. Once you’re talking about developing blockchain, Truffle is a popular stop to go to. Check out about Truffle Suite on [Truffle Suite: Sweet Tools for Smart Contracts](https://www.trufflesuite.com/).
- **Ganache CLI**  
Another tool that works well in hand with Truffle is Ganache-CLI. It's built and maintained by the Truffle Suite team. After building and compiling, you need an emulator to develop and run blockchain apps, and then deploy smart contracts to be used. Ganache makes it easier for you to deploy a contract in an emulator without using actual money for transaction cost, recyclable accounts, and much more. Read more on Ganache CLI at [Ganache CLI](https://docs.nethereum.com/en/latest/ethereum-and-clients/ganache-cli/) and [Ganache](https://www.trufflesuite.com/ganache).
- **Remix**  
Remix is like an alternative to Ganache, but also comes with a GUI to help navigate deploying and testing of Ethereum smart contracts. You can learn more about it on [Remix &mdash; Ethereum IDE & community](https://remix-project.org/). All you have to do is to visit [https://remix.ethereum.org](https://remix.ethereum.org) and use the GUI to write and deploy smart contracts.
- **Web3**  
Web3 is a collection of libraries that allows you to interact with an Ethereum node. These could be local or remote nodes of the contract through HTTP, IPC or Web Sockets. [Intro to Web3.js · Ethereum Blockchain Developer Crash Course](https://www.dappuniversity.com/articles/web3-js-intro) is a good place to learn a bit about Web3.
- **IPFS**  
A core protocol that is being used in building dApps. The <em>InterPlanetary File System</em> (IPFS) is a protocol and peer-to-peer network for storing and sharing data in a distributed file system. [IPFS Powers the Distributed Web](https://ipfs.io/) explains more on IPFS and how it’s usually used.

{{% ad-panel-leaderboard %}}

## Creating A Backend API From Scratch

So first we have to create a backend to be used, and we’re using Node.js. When we want to create a new Node.js API, the first thing we’re going to do is initialize an npm package. As you probably know, [npm](https://www.npmjs.com/) stands for <em>Node Package Manager</em>, and it comes prepackaged with the Node.js binary. So we create a new folder and call it <em>“blockchain-music”</em>. We open the terminal in that folder directory, and then run the following command:

<pre><code class="language-bash">$ npm init -y && touch server.js routes.js
</code></pre>

This starts up the project with a *package.json* file and answers <em>yes</em> to all prompts. Then we also create a *server.js* file and a *routes.js* file for writing the `routes` functions in the API.

After all these, you will have to install packages that we need to make our build easy and straightforward. This process is a continuous one, i.e. you can install a package any time during the development of your project.

Let’s install the most important ones we need right now:

- [Express.js](https://expressjs.com/en/starter/installing.html)
- [@truffle/contract](https://github.com/trufflesuite/truffle/tree/master/packages/contract#readme)
- [Truffle.js](https://www.trufflesuite.com/docs/truffle/getting-started/installation)
- [web3.js](https://web3js.readthedocs.io/en/v1.3.0/getting-started.html#adding-web3-js)
- [dotenv](https://github.com/motdotla/dotenv#readme)
- [`short-id`](https://github.com/UmbraEngineering/short-id#readme)
- [MongoDB](https://docs.mongodb.com/guides/server/install/)
- [nodemon](https://nodemon.io/)

You’ll also have to install Truffle.js <em>globally</em>, so you can use it everywhere in your local environment. If you want to install all of them at once, run the following code in your Terminal:

<pre><code class="language-bash">$ npm install nodemon truffle-contract dotenv mongodb shortid express web3 --save && npm install truffle -g
</code></pre>

The `--save` flag is to save the package's name in the *package.json* file. The `-g` flag is to store this particular package globally, so that we can use it in any project we are going to work on.

We then create an *.env* file where we can store our MongoDB database secret URI for use. We do so by running *touch.env* in the Terminal. If you don’t have a database account with MongoDB yet, start with the [MongoDB page](https://www.mongodb.com/) first.

The <em>dotenv</em> package exports our stored variable to the Node.js process environment. Please make sure that you don’t push the *.env* file when pushing to public repositories to avoid leaking your passwords and private data.

Next, we have to add scripts for build and development phases of our project in our *package.json* file. Currently our *package.json* looks like this:

<pre><code class="language-json">{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "socket.io": "^2.3.0",
    "truffle-contract": "^4.0.31",
    "web3": "^1.3.0"
  }
}
</code></pre>

We’re then going to add a start script to the *package.json* file to use the nodemon server so that whenever we make change it restarts the server itself, and a build script that uses the node server directly, it could look like this:

<pre><code class="language-json">{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "server.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon server.js",
	"build": "node server.js"

  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "socket.io": "^2.3.0",
    "truffle-contract": "^4.0.31",
    "web3": "^1.3.0"
  }
}
</code></pre>

Next, we have to initialize Truffle for use in our smart contract by using the Truffle package we installed globally earlier. In the same folder of our projects, we run the following command below in our terminal:

<pre><code class="language-bash">$ truffle init
</code></pre>

Then we can start writing our code in our *server.js* file. Again, we’re trying to build a simple decentralized music store app, where customers can upload music for every other user to access and listen to.

Our *server.js* should be clean for easy coupling and decoupling of components, so routes and other functionalities will be put in other files like the *routes.js*. Our example *server.js* could be:

<div class="break-out">

 <pre><code class="language-javascript">require('dotenv').config();
const express= require('express')
const app =express()
const routes = require('./routes')
const Web3 = require('web3');
const mongodb = require('mongodb').MongoClient
const contract = require('truffle-contract');
app.use(express.json())

mongodb.connect(process.env.DB,{ useUnifiedTopology: true },(err,client)=>{
    const db =client.db('Cluster0')
    //home
    routes(app,db)
    app.listen(process.env.PORT || 8082, () => {
        console.log('listening on port 8082');
     })
})
</code></pre>
</div>

Basically, above we import the libraries that we need with <code>require</code>, then add a middleware that allows the use of JSON in our API using `app.use`, then connect to our MongoDB database and get the database access, and then we specify which database cluster we’re trying to access (for this tutorial it is <em>“Cluster0”</em>). After this, we call the function and import it from the *routes file*. Finally, we listen for any attempted connections on port `8082`.

This *server.js* file is just a barebone to get the application started. Notice that we imported *routes.js*. This file will hold the route endpoints for our API. We also imported the packages we needed to use in the *server.js* file and initialized them.

We’re going to create **five endpoints** for user consumption:

<ol>
	<li>Registration endpoint for registering users just via email. Ideally, we'd do so with an email and password, but as we just want to identify each user, we’re not going to venture into password security and hashing for the sake of the brevity of this tutorial.<br />

<pre><code class="language-bash">POST /register
Requirements: email
</code></pre>
</li>
<li>Login endpoint for users by email.<br />

<pre><code class="language-bash">POST /login
Requirements: email
</code></pre>
</li>
<li>Upload endpoint for users — the API that gets the data of the music file. The frontend will convert the MP3/WAV files to an audio buffer and send that buffer to the API.<br />

<pre><code class="language-bash">POST /upload
Requirements: name, title of music, music file buffer or URL stored
</code></pre>
</li>
<li>Access endpoint that will provide the music buffer data to any registered user that requests it, and records who accessed it.<br />

<pre><code class="language-bash">GET /access/{email}/{id}
Requirements: email, id
</code></pre>
</li>
<li>We also want to provide access to the entire music library and return the results to a registered user.<br />

<pre><code class="language-bash">GET /access/{email}
Requirements: email
</code></pre>
</li>
</ol>

Then we write our route functions in our *routes.js* file. We utilize the database storage and retrieval features, and then make sure we export the route function at the end of the file to make it possible to be imported in another file or folder.

<div class="break-out">

 <pre><code class="language-javascript">const shortid = require('short-id')
function routes(app, db){
    app.post('/register', (req,res)=>{
        let email = req.body.email
        let idd = shortid.generate()
        if(email){
            db.findOne({email}, (err, doc)=>{
                if(doc){
                    res.status(400).json({"status":"Failed", "reason":"Already registered"})
                }else{
                    db.insertOne({email})
                    res.json({"status":"success","id":idd})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.post('/login', (req,res)=>{
        let email = req.body.email
        if(email){
            db.findOne({email}, (err, doc)=>{
                if(doc){
                    res.json({"status":"success","id":doc.id})
                }else{
                    res.status(400).json({"status":"Failed", "reason":"Not recognised"})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.post('/upload', (req,res)=>{
        let buffer = req.body.buffer
        let name = req.body.name
        let title = req.body.title
        if(buffer && title){

        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.get('/access/:email/:id', (req,res)=>{
        if(req.params.id && req.params.email){


        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
}
module.exports = routes
</code></pre>
</div>

Inside this `route` function, we have many other functions called within both the `app` and `db` parameters. These are the API endpoint functions that enable users to specify an endpoint in the URL. Ultimately we choose one of these functions to be executed and provide results as response to incoming requests.

We have four major endpoint functions:

1. `get`: for reading record operations
2. `post`: for creating record operations
3. `put`: for updating record operations
4. `delete`: for deleting record operations

In this `routes` function, we used the `get` and `post` operations. We use `post` for registration, login, and upload operations, and `get` for accessing the data operations. For a little bit more explanation on that, you can check out Jamie Corkhill’s article on “[How To Get Started With Node: An Introduction To APIs, HTTP And ES6+ JavaScript](https://www.smashingmagazine.com/2019/02/node-api-http-es6-javascript/)”.

In the code above, we can also see some database operations like in the <em>register</em> route. We stored the email of a new user with `db.createa` and checked for the email in the login function with `db.findOne`. Now, before we can do all of it, we need to name a collection or table with the `db.collection` method. That's exactly what we'll be covering next.

**Note**: *To learn more about the database operations in MongoDB, check the [mongo Shell Methods](https://docs.mongodb.com/manual/reference/method/) documentation.*

## Building A Simple Blockchain Smart Contract With Solidity

Now we’re going to write a Blockchain contract in Solidity (that's the language that smart contracts are written in) to simply store our data and retrieve it when we need it. The data we want to store is the music file data, meaning that we have to upload the music to IPFS, then store the address of the buffer in a blockchain.

First, we create a new file in the contract folder and name it *Inbox.sol*. To write a smart contract, it's useful to have a good understanding of Solidity, but it’s not difficult as it’s similar to JavaScript.

**Note**: *If you’re interested in learning more about Solidity, I’ve added a few resources at the bottom of the article to get you started.*

<div class="break-out">

 <pre><code class="language-javascript">pragma solidity ^0.5.0;


contract Inbox{
    //Structure
    mapping (string=>string) public ipfsInbox;
    //Events
    event ipfsSent(string &#95;ipfsHash, string &#95;address);
    event inboxResponse(string response);
    //Modifiers
    modifier notFull (string memory &#95;string) {
    bytes memory stringTest = bytes(&#95;string);
    require(stringTest.length==0);
    &#95;;
    }
    // An empty constructor that creates an instance of the conteact
    constructor() public{}
    //takes in receiver's address and IPFS hash. Places the IPFSadress in the receiver's inbox
    function sendIPFS(string memory &#95;address, string memory &#95;ipfsHash) notFull(ipfsInbox[&#95;address]) public{
        ipfsInbox[&#95;address] = &#95;ipfsHash;
        emit ipfsSent(&#95;ipfsHash, &#95;address);
    }
    //retrieves hash
    function getHash(string memory &#95;address) public view returns(string memory) {
        string memory ipfs&#95;hash=ipfsInbox[&#95;address];
         //emit inboxResponse(ipfs&#95;hash);
        return ipfs&#95;hash;
    }
}
</code></pre>
</div>

In our contract, we have two main functions: the `sendIPFS` and the `getHash` functions. Before we talk about the functions, we can see that we had to define a contract first called `Inbox`. Inside this class, we have structures used in the `ipfsInbox` object (first events, then modifiers).

After defining the structures and events, we have to initialize the contract by calling the `constructor` function. Then we defined three functions. (The `checkInbox` function was used in the test for testing results.)

The `sendIPFS` is where the user inputs the identifier and hash address after which it is stored on the blockchain. The `getHash` function retrieves the hash address when it is given the identifier. Again, the logic behind this is that we ultimately want to store the music in IPFS. To test how it works, you can hop on to a [Remix IDE](https://remix.ethereum.org), copy, paste, and test your contract, as well as debug any errors and run again (hopefully it won't be needed!).

After testing that our code works correctly in the remix, let’s move on to compiling it locally with the Truffle suite. But first, we need to make some changes to our files and set up our emulator using `ganache-cli`:

First, let’s install `ganache-cli`. In the same directory, run the following command in your terminal:

<pre><code class="language-bash">$ npm install ganache-cli -g
</code></pre>

Then let's open another Terminal and run another command in the same folder:

<pre><code class="language-bash">$ ganache-cli
</code></pre>

This starts up the emulator for our blockchain contract to connect and work. Minimize the Terminal and continue with the other Terminal you’ve been using.

Now go to the *truffle.js* file if you’re using a Linux/Mac OS or *truffle-config.js* in Windows, and modify this file to look like this:

<pre><code class="language-javascript">const path = require("path");
module.exports = {
  // to customize your Truffle configuration!
  contracts_build_directory: path.join(__dirname, "/build"),
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*" //Match any network id
    }
  }
};
</code></pre>

Basically what we did is adding the path of the build folder where the smart contract is converted to JSON files. Then we also specified the network that Truffle should use for migration.

Then, also in the <em>migrations</em> folder, create a new file named *2_migrate_inbox.js* and add the following code inside the files:

<pre><code class="language-javascript">var IPFSInbox = artifacts.require("./Inbox.sol");
module.exports = function(deployer) {
    deployer.deploy(IPFSInbox);
};
</code></pre>

We did so to get the contract file and deploy it automatically to a JSON, using the `deployer` function during the Truffle migration.

After the above changes we run:

<pre><code class="language-bash">$ truffle compile
</code></pre>

We should see some messages at the end which show successful compilation, such as:

<pre><code class="language-bash">> Compiled successfully using:
	- solc: 0.5.16+commit.9c3226ce.Emscripten.clang
</code></pre>

Next, we migrate our contract by running:

<pre><code class="language-bash">$ truffle migrate
</code></pre>

Once we have successfully migrated our contracts, we should have something like this at the end:

<pre><code class="language-bash">Summary
=======
> Total deployments:   1
> Final cost:          0.00973432 ETH
</code></pre>

And we’re almost done! We have built our API with Node.js, and also set up and built our smart contract.

We should also write tests for our contract to test the behaviour of our contract and ensure it is the desired behaviour. The tests are usually written and placed in the `test` folder. An example test written in a file named *InboxTest.js* created in the test folder is:

<div class="break-out">

 <pre><code class="language-javascript">const IPFSInbox = artifacts.require("./Inbox.sol")
contract("IPFSInbox", accounts =>{
    it("emit event when you send a ipfs address", async()=>{
        //ait for the contract
        const ipfsInbox = await IPFSInbox.deployed()

        //set a variable to false and get event listener
        eventEmitted = false
        //var event = ()
        await ipfsInbox.ipfsSent((err,res)=>{
            eventEmitted=true
        })
        //call the contract function  which sends the ipfs address
        await ipfsInbox.sendIPFS(accounts[1], "sampleAddress", {from: accounts[0]})
        assert.equal(eventEmitted, true, "sending an IPFS request does not emit an event")
    })
})
</code></pre>
</div>

So we run our test by running the following:

<pre><code class="language-bash">$ truffle test
</code></pre>

It tests our contract with the files in the <em>test</em> folder and shows the number of passed and failed tests. For this tutorial, we should get:

<div class="break-out">

 <pre><code class="language-bash">$ truffle test
Using network 'development'.
Compiling your contracts...
===========================
> Compiling .\contracts\Inbox.sol
> Artifacts written to C:\Users\Ademola\AppData\Local\Temp\test--2508-n0vZ513BXz4N
> Compiled successfully using:
   &mdash; solc: 0.5.16+commit.9c3226ce.Emscripten.clang

  Contract: IPFSInbox
    √ emit event when you send an ipfs address (373ms)

  1 passing (612ms)
</code></pre>
</div>

## Integrating The Smart Contract To The Backend API Using Web3

Most times when you see tutorials, you see decentralized apps built to integrate the frontend directly to the blockchain. But there are times when the integration to the backend is needed as well, for example when using third-party backend APIs and services, or when using blockchain to build a CMS.

The use of Web3 is very important to this cause, as it helps us access remote or local Ethereum nodes and use them in our applications. Before we go on, we’ll discuss the local and remote Ethereum nodes. The local nodes are the nodes deployed on our system with emulators like `ganache-cli` but a remote node is one that is deployed on online faucets/platforms like <em>ropsten</em> or <em>rinkeby</em>. To dive in deeper, you can follow a tutorial on how to deploy on ropsten [5-minute guide to deploying smart contracts with Truffle and Ropsten](https://medium.com/coinmonks/5-minute-guide-to-deploying-smart-contracts-with-truffle-and-ropsten-b3e30d5ee1e) or you could use truffle wallet provider and deploy via [An Easier Way to Deploy Your Smart Contracts](https://www.trufflesuite.com/blog/an-easier-way-to-deploy-your-smart-contracts).

We are using `ganache-cli` in this tutorial, but if we were deploying on ropsten, we should have copied or stored our contract address somewhere like in our .env file, then move on to update the <em>server.js</em> file, import web3, import the migrated contract and set up a Web3 instance.

<div class="break-out">

 <pre><code class="language-javascript">require('dotenv').config();
const express= require('express')
const app =express()
const routes = require('./routes')
const Web3 = require('web3');
const mongodb = require('mongodb').MongoClient
const contract = require('truffle-contract');
const artifacts = require('./build/Inbox.json');
app.use(express.json())
if (typeof web3 !== 'undefined') {
    var web3 = new Web3(web3.currentProvider)
  } else {
    var web3 = new Web3(new Web3.providers.HttpProvider('https://localhost:8545'))
}
const LMS = contract(artifacts)
LMS.setProvider(web3.currentProvider)
mongodb.connect(process.env.DB,{ useUnifiedTopology: true }, async(err,client)=>{
    const db =client.db('Cluster0')
    const accounts = await web3.eth.getAccounts();
    const lms = await LMS.deployed();
    //const lms = LMS.at(contract_address) for remote nodes deployed on ropsten or rinkeby
    routes(app,db, lms, accounts)
    app.listen(process.env.PORT || 8082, () => {
       console.log('listening on port '+ (process.env.PORT || 8082));
     })
})
</code></pre>
</div>

In the *server.js* file, we check if the web3 instance is initialized already. If not, we initialize it on the network port which we defined earlier (`8545`). Then we build a contract based on the migrated JSON file and `truffle-contract` package, and set the contract provider to the Web3 instance provider which must have been initialized by now.

We then get accounts by `web3.eth.getAccounts`. For the development stage, we call the deployed function in our contract class that asks `ganache-cli` — which is still running — to give us a contract address to use. But if we’ve already deployed our contract to a remote node, we call a function inputting the address as an argument. The sample function is commented below the defined `lms` variable in our code above. Then we call the `routes` function inputting the app instance, database instance, contract instance (`lms`), and accounts data as arguments. Finally, we listen for requests on port `8082`.

Also, by now, we should have installed the MongoDB package, because we are using it in our API as our database. Once we have that, we move onto the routes page where we use the methods defined in the contract to accomplish tasks like saving and retrieving the music data.

In the end, our routes.js should look like this:

<div class="break-out">

 <pre><code class="language-javascript">const shortid = require('short-id')
const IPFS =require('ipfs-api');
const ipfs = IPFS({ host: 'ipfs.infura.io',
    port: 5001,protocol: 'https' });

function routes(app, dbe, lms, accounts){
    let db= dbe.collection('music-users')
    let music = dbe.collection('music-store')
    app.post('/register', (req,res)=>{
        let email = req.body.email
        let idd = shortid.generate()
        if(email){
            db.findOne({email}, (err, doc)=>{
                if(doc){
                    res.status(400).json({"status":"Failed", "reason":"Already registered"})
                }else{
                    db.insertOne({email})
                    res.json({"status":"success","id":idd})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })

    app.post('/login', (req,res)=>{
        let email = req.body.email
        if(email){
            db.findOne({email}, (err, doc)=>{
                if(doc){
                    res.json({"status":"success","id":doc.id})
                }else{
                    res.status(400).json({"status":"Failed", "reason":"Not recognised"})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.post('/upload', async (req,res)=>{
        let buffer = req.body.buffer
        let name = req.body.name
        let title = req.body.title
        let id = shortid.generate() + shortid.generate()
        if(buffer && title){
            let ipfsHash = await ipfs.add(buffer)
            let hash = ipfsHash[0].hash
            lms.sendIPFS(id, hash, {from: accounts[0]})
            .then((_hash, _address)=>{
                music.insertOne({id,hash, title,name})
                res.json({"status":"success", id})
            })
            .catch(err=>{
                res.status(500).json({"status":"Failed", "reason":"Upload error occured"})
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.get('/access/:email', (req,res)=>{
        if(req.params.email){
            db.findOne({email: req.body.email}, (err,doc)=>{
                if(doc){
                    let data = music.find().toArray()
                    res.json({"status":"success", data})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
    app.get('/access/:email/:id', (req,res)=>{
      let id = req.params.id
        if(req.params.id && req.params.email){
            db.findOne({email:req.body.email},(err,doc)=>{
                if(doc){
                    lms.getHash(id, {from: accounts[0]})
                    .then(async(hash)=>{
                        let data = await ipfs.files.get(hash)
                        res.json({"status":"success", data: data.content})
                    })
                }else{
                    res.status(400).json({"status":"Failed", "reason":"wrong input"})
                }
            })
        }else{
            res.status(400).json({"status":"Failed", "reason":"wrong input"})
        }
    })
}

module.exports = routes
</code></pre>
</div>

At the beginning of the *routes* file, we imported the `short-id` package and `ipfs-http-client` and then initialized IPFS with the HTTP client using the backend URL `ipfs.infura.io` and port `5001`. This allowed us to use the IPFS methods to upload and retrieve data from IPFS ([check out more here](https://github.com/ipfs/js-ipfs/tree/master/packages/ipfs-http-client)).

In the upload route, we save the audio buffer to IPFS which is better compared to just storing it on the blockchain for anyone registered or unregistered to use. Then we saved the address of the buffer in the blockchain by generating an ID and using it as an identifier in the `sendIFPS` function. Finally, then we save all the other data associated with the music file to our database. We should not forget to update our argument in the routes function since we changed it in the *server.js* file.

In the access route using <code>id</code>, we then retrieve our data by getting the <code>id</code> from the request, using the <code>id</code> to access the IPFS hash address, and then access the audio buffer using the address. But this requires authentication of a user by email which is done before anything else.

Phew, <strong>we’re done</strong>! Right now we have an API that can receive requests from users, access a database, and communicate to a node that has the software running on them. We shouldn’t forget that we have to export our function with `module.exports` though!

As we have noticed, our app is a <strong>decentralized app</strong>. However, it's not fully decentralized as we only stored our address data on the blockchain and every other piece of data was stored securely in a centralized database which is the basis for <em>semi-dApps</em>. So the consumption of data can be done directly via request or using a frontend application in JavaScript to send fetch requests.

Our music store backend app can now safely store music data and provide access to anyone who needs to access it, provided it is a registered user. Using blockchain for music sharing makes it cheaper to store music data while focusing on connecting artists directly with users, and perhaps it could help them generate revenue that way. This wouldn't require a middleman that uses royalty; instead, all of the revenue would go to the artist as users request their music to either download or stream. A good example of a music streaming application that uses blockchain just like this is Opus [OPUS: Decentralized music sharing platform](https://opus.audio/). However, there are also a few others like Musicoin, Audius, and Resonate.

## What Next?

The final thing after coding is to start our server by running `npm run start` or `npm run build` and test our backend endpoints on either the browser or with Postman. After running and testing our API we could add more features to our backend and blockchain smart contract. If you'd like to get more guidance on that, please check the further reading section for more articles.

It's worth mentioning that it is critical to write unit and integration tests for our API to ensure correct and desirable behaviors. Once we have all of that done, we can deploy our application on the cloud for public use. This can be done on its own with or without adding a frontend (microservices) on Heroku, GCP, or AWS for public use. <em>Happy coding!</em>

**Note**: *You can always [check my repo for reference](https://github.com/agbanusi/Music-share-platform-through-Blockchain). Also, please note that the .env file containing the MongoDB database URI is included for security reasons.*

### Further Reading And Related Resources

<ul>
<li>“<a title="Read 'How to Build Ethereum Dapp with React.js: Complete Step-By-Step Guide'" href="https://www.dappuniversity.com/articles/ethereum-dapp-react-tutorial" rel="bookmark">How to Build Ethereum Dapp with React.js: Complete Step-By-Step Guide</a>,” Gregory McCubbin</li>
<li>“<a title="Read 'Ethereum + IPFS + React DApp Tutorial Pt. 1'" href="https://blog.goodaudience.com/ethereum-ipfs-react-dapp-tutorial-pt-1-a9dfd5079491" rel="bookmark">Ethereum + IPFS + React DApp Tutorial Pt. 1</a>,” Alexander Ma</li>
<li>“<a title="Read 'Ethereum Development with Go'" href="https://goethereumbook.org/en/" rel="bookmark">Ethereum Development with Go</a>,” Miguel Mota</li>
<li>“<a title="Read 'Create your first Ethereum dAPP with Web3 and Vue.JS (Part 1)'" href="https://itnext.io/create-your-first-ethereum-dapp-with-web3-and-vue-js-c7221af1ed82" rel="bookmark">Create your first Ethereum dAPP with Web3 and Vue.JS (Part 1)</a>,” Nico Vergauwen</li>
<li>“<a title="Read 'Deploy a Smart Contract on Ethereum with Python, Truffle and web3py'" href="https://dev.to/gcrsaldanha/deploy-a-smart-contract-on-ethereum-with-python-truffle-and-web3py-5on" rel="bookmark">Deploy a Smart Contract on Ethereum with Python, Truffle and web3py</a>,” Gabriel Saldanha</li>
<li>“<a title="Why Use Blockchain Technology?" href="https://www.bernardmarr.com/default.asp?contentID=1786" rel="bookmark">Why Use Blockchain Technology?</a>,” Bernard Marr</li>
<li>“<a title="How To Build Your Own Blockchain Using Node.js" href="https://www.devteam.space/blog/how-to-build-your-own-blockchain-using-node-js/">How To Build Your Own Blockchain Using Node.js</a>,” DevTeam.Space</li>
<li>“<a title="How To Build A Blockchain App With Ethereum, Web3.js & Solidity Smart Contracts" href="https://www.dappuniversity.com/articles/how-to-build-a-blockchain-app">How To Build A Blockchain App With Ethereum, Web3.js & Solidity Smart Contracts</a>,” Gregory McCubbin</li>
<li>“<a title="How To Build A Simple Cryptocurrency Blockchain In Node.js" href="https://www.smashingmagazine.com/2020/02/cryptocurrency-blockchain-node-js/">How To Build A Simple Cryptocurrency Blockchain In Node.js</a>,” Alfrick Opidi</li>
<li>“<a title="How Blockchain Technology Is Going To Revolutionize Ecommerce" href="https://www.eteam.io/blog/blockchain-and-ecommerce">How Blockchain Technology Is Going To Revolutionize Ecommerce</a>,” Sergii Shanin</li>
<li>“<a title="" href="https://www.gartner.com/smarterwithgartner/4-ways-blockchain-will-transform-higher-education/">4 Ways Blockchain Will Transform Higher Education &mdash; Smarter With Gartner</a>,” Susan Moore</li>
<li>“<a title="How To Learn Solidity: The Ultimate Ethereum Coding Tutorial" href="https://blockgeeks.com/guides/solidity/">How To Learn Solidity: The Ultimate Ethereum Coding Tutorial</a>,” Ryan Molecke</li>
<li>“<a title="Developing Ethereum Smart Contracts for Beginners" href="https://coursetro.com/courses/20/Developing-Ethereum-Smart-Contracts-for-Beginners">Developing Ethereum Smart Contracts For Beginners</a>,” Coursetro</li>
<li>“<a title="Learn about Ethereum | ethereum.org" href="https://ethereum.org/en/learn/">Learn about Ethereum</a>,” Ethereum official site</li>
</ul>

{{< signature "vf, il" >}}
