---
title: 'Smashing Podcast Episode 27 With Stefan Baumgartner: What Is TypeScript?'
slug: smashing-podcast-episode-27
author: drew-mclellan
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/76ab8c17-bf02-4275-9705-173fc6953e77/smashing-podcast-episode-27.png
date: 2020-10-20T05:00:00.000Z
summary: >-
  We’re talking about TypeScript. What is it, and how can it help us write better JavaScript? Drew McLellan talks to expert Stefan Baumgartner to find out.
description: >-
  We’re talking about TypeScript. What is it, and how can it help us write better JavaScript? Drew McLellan talks to expert Stefan Baumgartner to find out.
categories:
  - Smashing Podcast
  - TypeScript
disable_ads: true
disable_panels: true
disable_newsletterbox: true
---

We’re talking about TypeScript. What is it, and how can it help us write better JavaScript? I spoke to expert Stefan Baumgartner to find out.

<iframe src="https://share.transistor.fm/e/2b6b7871/dark" width="100%" height="180" frameborder="0" scrolling="no" seamless="true" style="width:100%; height:180px;"></iframe>

## Show Notes

- Stefan’s book [TypeScript in 50 Lessons](https://typescript-book.com) is available now
- Official site for [TypeScript](https://www.typescriptlang.org)
- Stefan [on Twitter](https://twitter.com/ddprrt)
- Stefan’s [personal website](https://fettblog.eu)

### Weekly Update

- “[React Form Validation With Formik And Yup](https://www.smashingmagazine.com/2020/10/react-validation-formik-yup/)”  
*written by Nefe Emadamerho-Atori*
- “[Design Shopping: Get A Faster Client Buy-In Through A Guided Design Showcase](https://www.smashingmagazine.com/2020/10/design-shopping-workflow-showcase/)”  
*written by Kelly Schummer*
- “[Build And Deploy An Angular Form With Netlify Forms And Edge](https://www.smashingmagazine.com/2020/10/angular-feedback-netlify-forms-edge/)”  
*written by Zara Cooper*
- “[Managing Long-Running Tasks In A React App With Web Workers](https://www.smashingmagazine.com/2020/10/tasks-react-app-web-workers/)”  
*written by Chidi Orji*
- “[Supercharge Testing React Applications With Wallaby.js](https://www.smashingmagazine.com/2020/10/supercharge-testing-react-applications-wallabyjs/)”  
*written by Kelvin Omereshone*

## Transcript

<p><a href="https://twitter.com/ddprrt"><img style="float: right; padding: 1em;border-radius: 110px;max-width: 50%;height:auto" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/84699d25-42cb-4995-a5b7-05c3b207e733/stefan-baumgartner-200x200-opt.jpg" width="200" height="200" alt="Photo of Stefan Baumgartner" /></a><span class="smashing-tv-host">Drew McLellan:</span> He’s a web developer and web lover based in Linz, Austria. Currently working at web performance company Dynatrace, he writes, speaks and organizes events all about software development and web technologies. Lately he’s the author of the book TypeScript in 50 Lessons, published this autumn by Smashing. So we know he’s an expert in TypeScript, but did you know he can juggle up to eight fiery weasels whilst blindfolded on a unicycle? My Smashing friends, please welcome Stefan Baumgartner. Hi, Stefan. How are you?</p>

<span class="smashing-tv-speaker">Stefan Baumgartner:</span> Hi. I’m smashing. I didn’t that about me, so that’s very interesting.

<span class="smashing-tv-host">Drew:</span> It’s amazing what people find out about themselves on this podcast.

<span class="smashing-tv-speaker">Stefan:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> So, I wanted to talk to you today about TypeScript.

<span class="smashing-tv-speaker">Stefan:</span> Yes.

<span class="smashing-tv-host">Drew:</span> It’s the subject of your new book, so clearly it’s something you’ve spent a lot of time getting to really know in depth.

<span class="smashing-tv-speaker">Stefan:</span> Yes, absolutely.

<span class="smashing-tv-host">Drew:</span> For those who have not used TypeScript before, so might not be familiar with what it is, how would you describe TypeScript, and what problem is it actually solving for us?

<span class="smashing-tv-speaker">Stefan:</span> It’s a very good question. So, there are many ways of approaching TypeScript and one way that I like most, and also the way that I like to describe in my book, is as a tooling layer on top of JavaScript. JavaScript is a wonderful language, but it has its quirks. There’s some parts that can have multiple meanings. You have dynamic typing, which means that while you can have different types like number or string or an object based on the position where they are in your code, and there’s lots of implicit knowledge when you work, especially with the technologies or with Node.js, That you have to know about some interfaces that you use from APIs, function signatures, etc.

<span class="smashing-tv-speaker">Stefan:</span> And TypeScript tries to give you a type system around all that, to give you this information. So, it tries to figure out which types you set when assigning variable. It tells you which function signatures expect which well use at which position, and which return objects that you get that you can then access and modify and work with.

<span class="smashing-tv-speaker">Stefan:</span> And this was, back in the day when TypeScript was created, that’s now about 80 years ago, the prime goal of the TypeScript team to create this tooling layer, in form of an additional language. So, to take all the risk from JavaScript and then on top they create their own kind of meta language that allows you to define types for your functions, your objects, whatever there is. And this also means that every JavaScript code is TypeScript code, which also means that you can get started right away. If you know JavaScript, you’re basically a TypeScript developer as well. And you just take what you need to get more and more information about your code.

<span class="smashing-tv-host">Drew:</span> So, TypeScript is almost like imposing a sort of bunch of more strict rules about how we write JavaScript in order to make code more reliable? Is that...

<span class="smashing-tv-speaker">Stefan:</span> Yes, yes, this is exactly what it is. So, the strictness is totally up to you. So you can tell TypeScript how strict you want to have it. But their goal is to catch as much errors, or as much possible errors, that there can be. Like oh well this value could be null, so better do a check if this value you exists or it can be undefined. Or, at this position I don’t exactly know if it’s a string or a number so check if it’s type of string, check if it’s type of number.

<span class="smashing-tv-speaker">Stefan:</span> So TypeScript knows more, or can give you more information about the class of failures that you’re dealing with. And right now, the main goals of TypeScript are to catch as many errors as there are. So they spent a lot of time in providing more tools for you to declare your types and to declare the strict rules for you to figure out if there’s any error in your code that you might have a problem with in the long run.

<span class="smashing-tv-host">Drew:</span> So, I mean, really to get back to basics when we talk about types in a programing language, which obviously TypeScript is all about types, we have strictly type languages and weakly type languages and JavaScript is weakly typed, isn’t it? What do we actually mean when we say something is weakly typed?

<span class="smashing-tv-speaker">Stefan:</span> There’s weakly typed, and another word for that is also dynamically typed, which means that you don’t always have to know which type your variables or your constants have. So, the moment you assign a variable, let’s say var fu or let fu with a number once you forget something, the cross-credentials say fu is now of type number, it’s a number and I can’t do number operations on top of it, like addition, multiplication, subtractions and all those kinds of things. If you assign it a string then it’s a string.

<span class="smashing-tv-speaker">Stefan:</span> And, in JavaScript, you have the possibility to override it with the value of an entirely different class, entirely different type. So, you can, say at one point in time it’s 1, 2, 3, 4, at another point in time it’s a string like, "Hello world, Stefan," or "fussy cat" or something like that. And this can cause for couple of errors because what if you expect your variable fu at some point in time to be a string and then you do string operation on top of it like two uppercase, two lowercase. Or if you expect a number and you want to edit to something, then you could do result, which you don’t expect.

<span class="smashing-tv-speaker">Stefan:</span> And, with TypeScript, you can explicitly set the types or you can tell TypeScript to infer a type from an assignment. So the moment you assign one to free, TypeScript knows, Hey, this is number, and throughout your whole code, throughout every user through, it will think it’s a number and it will tell you if you do something that is not allowed with numbers. So, yeah. And this is the difference between a statically or strongly typed language, where you say, okay, once it has the type it has to be of the type and the type can’t change afterwards. In the weakly or dynamically typed language where the type just depends on where you are in your code and it can change, especially at run times or during the execution of the code, which can cause a ton of problems if you don’t pay attention.

<span class="smashing-tv-host">Drew:</span> So, yes, there’s that whole class of error, isn’t there, where you, as a developer, think that a variable contains a certain type of value and actually when it comes to that point in the code and that’s executed, for whatever reason it’s something different. And TypeScript is adding that enforcement of types on top of JavaScript to sort of give us that extra level of checks and reliability to it, to get rid of that type of bug.

<span class="smashing-tv-speaker">Stefan:</span> Exactly. The best example is for, for example, at the string two, with the number two, and you get 22 as a string, at the number two vice-versa and you get the number four. So, it’s apparently the same operation, but just if you swap the number in the string you get two totally different results. And TypeScript pays attention that it don’t have errors like that. And the one biggest rule that it sets like, so once you do an assignment, it has to be of that type, and the type can’t change.

<span class="smashing-tv-host">Drew:</span> So, TypeScript doesn’t actually get run by the browser, does it? Or by node or whatever run time you’re using, it presumably gets compiled down somehow to JavaScript?

<span class="smashing-tv-speaker">Stefan:</span> Yes. So you, there are two ways of working with TypeScript. One way is just exactly what you said, you write the TypeScript code, especially with this typing meta language that you use, and then you have a compile step where TypeScript erases all the types and spits out regular JavaScript code. And TypeScript is also transpiled so you can, say if you write more than the JavaScript, you can compile it down to something that I-11, if you have to support it, can work with. That’s one way.

<span class="smashing-tv-speaker">Stefan:</span> The other way is, and this is an interesting way which I like a lot and which people are using actually, you write regular JavaScript and then you add type declarations in a separate file, and refer to it by adding JSDoc comments in your code. And TypeScript can read this comment information, this documentation information, maps it to the types you created in separate file, and can give you the same tooling, the same information that you would get if you write in this transpiled, compiled way.

<span class="smashing-tv-host">Drew:</span> Okay, so then, that way you just keep your standard JavaScript, but the tooling that you’re using around it knows to reference the sort of side car file that has all the definitions of what the types are.

<span class="smashing-tv-speaker">Stefan:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> Type checking is one thing, but surely that’s the sort of thing we can, we don’t need a new language to do. That sort of analysis we could just have running in a code editor in a VS Code or whatever for example. Does TypeScript add things that take us beyond just what you could do in a code editor?

<span class="smashing-tv-speaker">Stefan:</span> The biggest advantage that you get is actually from code editors. One funny thing is that if you work with Virtual Studio Code and you write regular JavaScript, what you’re really doing is writing TypeScript because Virtual Studio Code has built in TypeScript a checker and analyser that gives you, that tries to figure out as much information as possible and gives this information back to the editor and has a close relationship to the editor into TypeScript. In particular, especially since you mentioned VS Code. VS code was their first project to work with TypeScript. Back in the day, where it was called Strada or Project Strada, where all the developers figured out how to actually create a language like that.

<span class="smashing-tv-speaker">Stefan:</span> So, editors and language are very, very much connected and you get the best benefit if you’re working with modern day editor. And thanks to the TypeScript team this doesn’t have to be VS Code. It can be basically any editor. So the proactive blankets for almost any editor out there that supports a so-called language protocol. There also getting it for all the other programming language, feedback and editor feedback, and analyzing information.

<span class="smashing-tv-speaker">Stefan:</span> So, yeah. This is actually the main use-case for that. And, of course, if you have bigger projects and you used to compile stepped version of TypeScript, having some sort of continuous integration, continuous delivery, where you constantly check if your project makes sense, you’re creating bundles that you should begin, this is also a part of TypeScript plays a huge role because with every commit to a GitHub repo or something you can do type checks and see if there might be an error slipped in that should be taken care of.

<span class="smashing-tv-host">Drew:</span> So, I guess there’s a level that your code editor can do automatically. Like you said that Visual Studio Code does by just analyzing it as your writing JavaScript, but then when you’re using these, when you’re declaring types specifically or adding these JSDoc comments that’s what takes it a step beyond that. That’s where you’re actually, it’s defined as more of a language on top of JavaScript.

<span class="smashing-tv-speaker">Stefan:</span> Yep. The cool thing is TypeScript is, in the way it’s designed, that it tries to get as much information out of your JavaScript as possible without you doing anything. So, if it sees a number in the wild it knows that this type is going to be number. Or if you have a function signature and you say you have a default value like the way you add a tax to a price and you see it as standard way you add a tax is 0.2. So if you add this in the function signature TypeScript already knows at this point I expect you to pass number and not something else.

<span class="smashing-tv-speaker">Stefan:</span> Also, if you return an object or if you write a JavaScript class, TypeScript can figure out what the well use are, what the types of your fields should be. And this works for actually quite a lot of use cases. So you have lots of scenarios where this is totally sufficient and you don’t need anything else. But when you do, this is now your part to strengthen TypeScript with additional type information that you provide. So, let’s say you want to create a type article which should have a number, a description, a price. You have different types for that. And then you create a compound or object type and once you declare this type and you know that your object should be of this type, TypeScript knows which values and which fields to expect.

<span class="smashing-tv-speaker">Stefan:</span> And one thing that’s particularly interesting here is that TypeScript is one of the few and certainly the most popular type system that works with structural typing, which means that as long as the shape properties and types of those properties is the same as the object that you pass along or the object that you get from somebody else, it will say it’s okay. You don’t have to have the exact name, it just needs to have the exact structure. So if you have a type called book which happens to have name, description, and price and you have a type called video which happens to have name, description, and price, those types are compatible with each other.

<span class="smashing-tv-host">Drew:</span> Okay, so that means we can sort of define customer types that make sense in terms of the project and the objects that our project is trying to model and then use TypeScript to enforce the shape of those.

<span class="smashing-tv-speaker">Stefan:</span> Yep.

<span class="smashing-tv-host">Drew:</span> So if we’ve got a product that has a price property that’s an integer in sense or what have you, then TypeScript will enforce that for us and if we pass in something that’s not a product or doesn’t have a price or whatever, that’s when we start getting our errors. Can you then go sort of step beyond that if you had like a cart type that had an array of products inside it? Can you enforce all the way that level?

<span class="smashing-tv-speaker">Stefan:</span> Yep. Yeah, exactly. You can enforce that as well. There you enter also a class of types which is already goes into very advanced topics which is generic types. So, the array type is a generic type. It tells you an array has certain interest so you can index them. It has a certain properties like length or map or for each, but the well use inside this array are defined by a so called generic. So you can say you have an array of number, you have an array of string, you have an array of articles.

<span class="smashing-tv-speaker">Stefan:</span> And then if you do array.map then you get, inside this map function, you get the type again like a string, number, article, whatever you pass along. And with generics you can do a lot of things. So this is where the type system really tries to make sense out of all the possible cases people encounter in JavaScript frameworks. So you have, especially in JavaScript you have so many functions that can mean so much. Like, okay the first argument is now a string, the second argument has to be an object, or if the first argument is a number, the second argument has to be a string. You’ve seen that in the wild in countless, countless libraries that you use.

<span class="smashing-tv-speaker">Stefan:</span> And, for this kind of scenario TypeScript also has structures in generic types and conditional types where you can have checks if this is one class of types do this, if this is another class of types do that, which really tries to figure out most of the scenarios that you find in day to day JavaScript code.

<span class="smashing-tv-speaker">Stefan:</span> So, and this is actually where the fun starts. The thing like creating object types, creating regular types like number, string, etc., or creating function types that’s one thing. But if you try to model a very complex behavior just within the type system, this can get very, how do I say it, mind boggling. Yeah, I guess mind boggling is the right word. This can be very mind boggling, but also a lot of fun.

<span class="smashing-tv-speaker">Stefan:</span> And this is where I kind of got my, found my call to work more with TypeScript because I just found out that I could do so many that I see in, not only in my code but in the code for my colleagues and code that I find online, to make more sense out of it and to be prepared for future scenarios. So, I mostly write types in TypeScript because I know that at some point in time I have to revisit code and I want to know what I’ve been thinking back when I originally wrote it.

<span class="smashing-tv-host">Drew:</span> Where is in your project that you would define these types? Because presumably you want them to be reusable all around your project. Where do you define them?

<span class="smashing-tv-speaker">Stefan:</span> So, I usually define them very close to the code that I actually write. So, when I write TypeScript I write in TypeScript first. So I transpile, I usually have a compile slip anyway of, maybe because I’m doing React and I need to transpile JSX, or because the project is so big that I want to do extra checks. So there’s a built chain anyway. Either I need to bundle or I need to transpile, so I’m writing regular TypeScript, not JavaScript with this JSDoc extensions. And there I try to keep the types very close to the objects that I declare.

<span class="smashing-tv-speaker">Stefan:</span> If there’s a type that is used throughout the whole project, I’m not only expecting the type, but also the objects or the functions for that objects. So this is some way of splitting and moving files and types around. There’s a very rare case where I also have one of those global type finishing files next to me, which is if my app has to deal with something that’s in the environment where I run it, be it either node or browser or whatever, where some global ideas or global concepts are that I want to carry in my program and hold. And this is actually a pretty standard set up.

<span class="smashing-tv-speaker">Stefan:</span> So you have your TypeScript files on one side, you have couple of type definition files on the other side, and then TypeScript tries to figure out everything, if it makes sense and if it’s possible to do and hopefully that’s the case.

<span class="smashing-tv-host">Drew:</span> Yes, I think we’re all very sort of used to having a build step, combilation step, in our work flows these days, aren’t we? With whether it’s running Babble or dealing with JSX and React or Web Pack and what have you so...

<span class="smashing-tv-speaker">Stefan:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> I guess adding TypeScript into there is just another small step in the process and quite easy to do.

<span class="smashing-tv-speaker">Stefan:</span> Yeah. So it’s, on one side TypeScript is a great extension, especially if you have a Babble set up running. So they provide an interface where you can do TypeScript type checks, even though your whole application is transpiled with Babble. TypeScript also has a lot of tools so it can be the only transpiler that you need. So it can transpile JSX, it can transpile down to Equiscript 5, Equiscript 3. The only thing that it doesn’t do anymore is bundling. So if you want to have bundled up application you need to take another tool like Roll Up or Web Pack or whatnot.

<span class="smashing-tv-host">Drew:</span> One of the features that I liked in newer versions of PHP, back when I was writing a lot of PHP, they brought in the ability to declare the types of each argument that a function was expecting. TypeScript does the same thing, right? You can say the first argument should be a number, the second argument should be a string-

<span class="smashing-tv-speaker">Stefan:</span> Yes.

<span class="smashing-tv-host">Drew:</span> ... and then the tool sets going to catch that if you try and pass the wrong thing in.

<span class="smashing-tv-speaker">Stefan:</span> Exactly.

<span class="smashing-tv-host">Drew:</span> In a lot of sort of real world cases I find that I have function arguments or variables that would be of a given type, but there might also be null. Is that something that TypeScript allows for?

<span class="smashing-tv-speaker">Stefan:</span> Yep, yep. So, this is where you enter the wonderful world of Union types and this is the big chapter in my book in the middle where we go from beginner concepts to advanced concepts. Where we realize that you don’t, not only have different classed of types like numbers, string, or several object types, but you can combine them. So you can say, this argument can be of type of string, of type number, or of type null or of type undefined, or for some object type. And with that your arguments, especially function arguments become much, much more varied.

<span class="smashing-tv-speaker">Stefan:</span> So if you can for one thing say, if this function argument does not have null in its unit type, then you’re not allowed to pass null. And you can make sure that inside this function, this way you is never null. If it can happen that it’s null, you add pipe to pipe operator null to it, and suddenly you have to check if it’s null or if it isn’t. Which makes it very, very interesting. So, especially the case of null checks and having undefined values. This is something that you happened to have in TypeScript all the time, or in JavaScript all the time.

<span class="smashing-tv-speaker">Stefan:</span> And with this one little addition, like make sure you check for your null-ish values and if you don’t allow null-ish values they can’t be null. This erases a whole clause of errors that you would otherwise encounter. And this is also one lesson in my book where I just talk about this one compile of next trick null checks and what it means for your work and what you suddenly have to do. And at some point you realize, okay it’s much more tedious to add pipe null to every possible case where it could be null, instead of just for one time in one place of your code, check if it’s actually null and then just continue with what you did. So, that’s a very nice way of working with null and undefined values.

<span class="smashing-tv-host">Drew:</span> A lot of sort of more formal languages, OO type languages, have classes and give you the ability to define a class interface to be able to say if it’s a class that uses this interface it needs to have these methods, it needs to behave like this. Is that something that TypeScript gives us?

<span class="smashing-tv-speaker">Stefan:</span> Yeah, absolutely. So this is very much related to the history of TypeScript. TypeScript, when it got first released, you know it was eight years ago we weren’t talking about Equiscript 6 there, we weren’t talking about native Equiscript classes, we spoke mostly about objects and functions. There was no modern system so it was a very different type of JavaScript eight years ago than we have today. And eight years ago, the TypeScript team introduced lot of features from other program languages like Java, C#, like classes, interfaces, extra classes, name spaces, to create some sort of structural or structured programming tools that make it possible for you to lay out your code entirely different than you’re used to.

<span class="smashing-tv-speaker">Stefan:</span> But over the years, lots of those concepts found there way into JavaScript, especially classes. So, they had to revisit lots of that concepts again and made it much, much more aligned to the way JavaScript is right now. So you still have classes, you still have interfaces, but TypeScript classes are just the same JavaScript classes. And TypeScript interfaces are like compound type or composite types where you have just list of properties. They can be function properties or string properties or mass object properties, and interfaces and type declarations are, in the most parts, just the same.

<span class="smashing-tv-speaker">Stefan:</span> You also can implement, you know the implements keep it exist, you can implement an interface, you can implement a type. There are, just in some rare cases, effective to some rare cases there are totally the same. So, yes they exist, but they mean something different than your used to from other programming languages. And this is also something where I’d say people who come from other programming languages have to look out for things like that because they can be false friends. Where you, they think, Okay, oh this just works just like in Java or this works just like NC Sharp, where in turn it’s just borrowed language or it’s just the same names for concepts that are nuanced and somewhat different than to what you would expect.

<span class="smashing-tv-host">Drew:</span> It can be a real sort of mental hurdle to jump over, isn’t it?

<span class="smashing-tv-speaker">Stefan:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> If you’re familiar with a name meaning one sort of thing and now it means something else.

<span class="smashing-tv-speaker">Stefan:</span> Yep.

<span class="smashing-tv-host">Drew:</span> It can be quite difficult to reset how you think about those things. So, it sounds like TypeScript has some sort of really advanced features that help us who are working really hard in JavaScript all day. Is it just for us super nerds or can people who less familiar with JavaScript, is it useful for the more, the beginner or the intermediate as well?

<span class="smashing-tv-speaker">Stefan:</span> Yeah, I’d say both. So one of the nice things about TypeScript is it’s creditable. So you just use as much of TypeScript as you want to use. So if you learn JavaScript, you get some additional tooling that gently tells you, Hey, there might be some properties that you want to select. Like if you call document .queries elect it already tells you, no queries elect exists and it gives you some hint on what to expect as an argument without throwing a single error and without you needing to do anything with those red streak lines that you get in your editor.

<span class="smashing-tv-speaker">Stefan:</span> And for that already TypeScript can do a lot of things. So this basic tool aspect of it can help beginners just as much as people who are more familiar with JavaScript and then have been in JavaScript for a very, very long time. But as you progress you can buy into more and more and more concepts as long as it’s reasonable for you to do. So I’m always a strong proponent of not having to use every feature a programing language gives you, but just the features that you actually need and TypeScript is perfect for that because it has a ton of features from the history that we spoke about where it tried to introduce concepts that haven’t been in JavaScript. And now from all those concepts that try to make the most sense out of all the JavaScript code that there is outside, you can take whatever you need and whatever you like from that.

<span class="smashing-tv-speaker">Stefan:</span> And this is, I guess, what makes TypeScript so special. When I started working with TypeScript, like seriously working working with TypeScript, the things that it most was like having a react component and being super happy that if I press control space that I get all the name of the properties my function component would expect. So this alone helped me a lot and it did nothing else but using this feature for a very, very, very long time. And then I started, in some sort of library code that I created for my colleagues or for people who I work with, creating a type core set around my function so people who use my code know better what I meant when I wrote those particular functions. And there I go all in. I’m very deep, deep down the type system rabbit hole.

<span class="smashing-tv-host">Drew:</span> Yeah, I mean that’s interesting. In the last episode of this podcast I talked to Natalia from Vue JS all about Vue 3 and one of the big changes they’d made in Vue 3 was that it was rewritten using TypeScript. How important is it for libraries and frameworks to adopt TypeScript? What benefit is that actually providing those who are working with the library and not on the library code itself?

<span class="smashing-tv-speaker">Stefan:</span> So, I think for one part you get a lot of implicit documentation. Especially if you import Vue or React, React is kind of a mixed bag, but if you import Vue or Preact for that matter, Preact is also written in TypeScript. People who use your framework immediately have some information about all the functions and all the objects that they get without you needing to look up anything and you get some extra checks if what you’re doing is the right thing to do.

<span class="smashing-tv-speaker">Stefan:</span> So that’s a lot of implicit documentation for all the users of those libraries that you get, basically for free, if you start writing in TypeScript anyway. So every project that is written in TypeScript gets, produces all this extra information for free. I guess as a team, as a library author, it makes contributions a lot, lot easier for the same documenting reasons. It also makes checks a lot easier because there’s a whole class of errors that you can catch in the type system that you, that would take ages to catch in tests. That’s why nobody writes test for that, especially if this is of a certain type, kind of tests.

<span class="smashing-tv-speaker">Stefan:</span> And yeah, and then you of course get all the benefits that you would get if you used TypeScript in any other project are catching errors before they happen. And one thing that I have to mention here is, especially Preact because Preact tries to do the kind of thing that write JavaScript code, and add additional types on the side, which gives them a low barrier of entry for people who want to contribute because they don’t have to figure out how the type system works or how type script works because they’re just like JavaScript code. But they, as library authors, get the additional benefits of having type checks, of seeing if this works the way it is intended, and I think this is for lots of projects. Especially Open Source projects really the best way to go.So, I strongly advocate for the idea of having JavaScript types on the sides because it can help people so, so much for basically not a lot of investment on your part.

<span class="smashing-tv-host">Drew:</span> Increasingly, we’re seeing sort of whole organizations moving to JavaScript as their sort of language of choice, both in the front end where it’s an obvious choice, but in the back end of their products and systems. Would you consider TypeScript something that sort of larger teams and larger organizations would really benefit from? More than individuals?

<span class="smashing-tv-speaker">Stefan:</span> So, I’m currently in the same transition. So we have lots of Java NC Plus developers who are going to write a lot of JavaScript in the future and you know what, TypeScript can be some sort of guide for those carry areas of new program languages. JavaScript has a lot of quirks, a lot of history and a lot of prejudices if you come from a different programing language. So TypeScript can be a guide because there’s some concepts that you’re familiar with it in the type system.

<span class="smashing-tv-speaker">Stefan:</span> But also, I think, especially when you have lots of people working in the same hole base or lots of people who need to work with each other, this can be an additional layer of guidance in your project where you don’t have any bad surprises in the end. So, of course technology doesn’t solve any communication problems. This is not what TypeScript is intended for, but it can lower, it can make lot more room for the right discussion then, if you don’t have to talk about what do you expect from me in your code, but rather what should your code do or what should your library do.

<span class="smashing-tv-speaker">Stefan:</span> And, I always say that if you ever write code for other people or if you write code with lots of people or if you just write code for yourself, you have to revisit the next day, consider TypeScript because it might help you in the long run. And this is not just an investment for the next project of next week, but more for one who say, Okay, especially if long lasting projects for month, two, or years. Definitely offer that. You’re never going to know what you’ve been thinking of when you wrote the little piece of code one year ago, but types can give you a hint of what you meant.

<span class="smashing-tv-host">Drew:</span> One thing I think that stopped me looking too closely at TypeScript in the past is I sort of remember things like Coffee Script that were a sort of new Syntacs that sort of transpired down and I kind of thought that TypeScript was another one of those, but it’s really not, is it? It’s plain JavaScript with some extra things layered on top.

<span class="smashing-tv-speaker">Stefan:</span> Yeah, so this is something that the team also strengths a lot. It’s fundamentally not a new language. So, it could look like that if you look at examples from 80 years ago, this was also part, just like you too. I was avoiding for such long time, firstly because of Coffee Script, second because of tons of JavaScript developers telling me that this is Java 4 or this is JavaScript for child developers, like and now finally get all those tools that I know from years and years of writing Java and I don’t want to change the ways I write, I just want to have the same tools but drawing in a different environment and this scared me and I didn’t want to have to do anything with it. And it took me, I guess about six years or so until I tried it again.

<span class="smashing-tv-speaker">Stefan:</span> Especially after watching some videos of TypeScript’s creator Anders Hejlsberg who spoke exclusively about the tooling aspects and about this is JavaScript. So, I met him twice in Seattle and when he went into interview sessions where we all were, he said from himself that he was writing JavaScript for the better part of the last decade. And if the creator of TypeScript has this idea that he’s writing JavaScript, perhaps you know with this extra type annotations, this takes the whole language and the whole tool into totally different light.

<span class="smashing-tv-speaker">Stefan:</span> And that’s why they’re stretching the fact so much that everything that you have, especially if it’s a new language feature, this is JavaScript. So they are very closely aligned to the ECMAScript standard. They are also championing a couple of proposals in the ECMAScript standard. They are involved, they know what’s happening, and if there’s a new feature that reaches a certain stage, they’re adopting it in TypeScript, but they’re not creating any new language features on their own.

<span class="smashing-tv-speaker">Stefan:</span> Where they innovate is in the type system. And you can really separate the type system from the actual JavaScript code. Of course there’s some mingling of JavaScript code and types group, especially when you do type annotations, but other than that it’s JavaScript with benefits. And those benefits are what makes it worth in my opinion.

<span class="smashing-tv-host">Drew:</span> And I guess we could go through all sorts of those benefits, all sorts of features that are in TypeScript, we could go through them blow by blow, but it doesn’t necessarily make sense to do that in a podcast. It’s difficult to describe code, isn’t it?

<span class="smashing-tv-speaker">Stefan:</span> Oh, you an write an entire book about that.

<span class="smashing-tv-host">Drew:</span> Are there any particular features of TypeScript that you’re most excited about or think provide the most value to users?

<span class="smashing-tv-speaker">Stefan:</span> I guess one of the features from the type system that I like most, which is again advanced but not super advanced so that it’s easily graspable, are union and section types. Where you can say, Okay, this argument or this variable can be not only of this type, but also of another type. Or it needs to have features from this type and this other type. And if you, once you realize that you can make use of that, you suddenly can model your application a lot, lot better.

<span class="smashing-tv-speaker">Stefan:</span> So, I adopted a work for where I tried to think about the object and the functions that I have, like what do they expect, what is the data, how are the properties designed. And then I tried to work with them as much within functions and if you use an intersection types you can, you have so many tools of modeling your data that if you spend a little time doing that you catch a ton of errors and a ton of problems up front without spending too much time into, in TypeScript land.

<span class="smashing-tv-speaker">Stefan:</span> And that’s why I guess they would be my most favorite feature. And also the fact that TypeScript transpires everything. I don’t need any Babble or any other transpile and I’m pretty tired of having too many tools that I need to use. So if I just can rely on one tool and maybe another one for bundling, that takes a lot of noise off my mind. So, that’s what I’m also very thankful for. It can just do a lot.

<span class="smashing-tv-host">Drew:</span> You’ve written about what it can do in a new book for Smashing. Loads of great information for people who are wanting to learn TypeScript. So, what sort of developer is the book aimed at?

<span class="smashing-tv-speaker">Stefan:</span> Yeah, so if you read TypeScript in 50 Lessons, we assume that you are already a JavaScript developer. You don’t have to be a seasoned JavaScript developer, so just enough that you, you’ve written application with it, you know some quirks, you know what an object is, you know what an error is, you know what a function is, you know what an assignment is. So stuff like that.

<span class="smashing-tv-speaker">Stefan:</span> And we take you from there, from just enough JavaScript that you know how to be dangerous, and guide you through the TypeScript layer. So, you could write books about TypeScript that you just speak about every feature that there is and explain just a little and let the reader figure out whatever to do with it, and we take a total different approach. We focus on one particular part, which is the type system, we leave out a lot of other things that, they are, neither the team nor seasoned TypeScript developers would recommend that you do, and focus just on the part that is long lasting.

<span class="smashing-tv-speaker">Stefan:</span> So, this was one thing that I really cared about when writing this book that once it’s out it should have some relevance in years to come. Especially with TypeScript getting four releases a year, you never know all the features and you can’t express all the features. But you can express, or explain, how the type system works. And from that on you figure out the things on your own. And this is what we do, so we give a very in depth introduction into the type system.

<span class="smashing-tv-speaker">Stefan:</span> First, in the first four chapters we guide you to the point where Okay, yeah, you know how to assign types, now you know how to work with types. Then there’s this water sheds chapter where we go into unit intersection types and from then on you learn about type modeling and about moving into types system. And after you read the last few chapters, we had seven chapters in total, you should know everything, to be prepared for every single TypeScript that there is. And for every new class of types they introduce and for every new class of errors they try to solve.

<span class="smashing-tv-speaker">Stefan:</span> And it took me quite a while to write this book to be honest, so me knowing that it didn’t have to change the table of contents and it didn’t have to introduce any new concepts over the last 1 1/2 years to me is proof enough that we succeeded in that. So, maybe we snuck in one or two features from TypeScript 4.0 but not all. So all the learnings that you have are still well it even though we, I designed them 1 1/2 years ago. So, yeah this is the main goal of the book. And it’s kind of what we see in the tag line. We want to take you from a beginner to an expert. And I hope we succeed with that. Yeah.

<span class="smashing-tv-host">Drew:</span> I certainly found reading the book though because it is broken down in, you know it’s 50 lessons so it’s all in sort of fairly bite size chunks, and I found that I was able to start using all of that straight away. You’d read about something and then you could start using it. It’s not one of those books where you have to make it all the way through to the end before you can start being productive.

<span class="smashing-tv-speaker">Stefan:</span> Yeah. Yep. Absolutely.

<span class="smashing-tv-host">Drew:</span> Very easy to just sort of drop in and drop out of which with many of us being so busy and under so much pressure in our jobs and things at the moment, it’s great just to be able to read a little bit and then forget about it for a while and then come back and read a bit more.

<span class="smashing-tv-speaker">Stefan:</span> Yep. This is also something that we take a lot of care, that we really cared about to achieve. It can be really overwhelming to learn a new language. Especially a new programming language. And so those bite sized chunks, you know you just spend about five or maybe ten minutes with one of those lessons. And you can immediately apply the learnings of those lessons to some actual code and we provide you with all the code examples online. So if you go to TypeScript-Book.com you see a list of all the code examples that there are.

<span class="smashing-tv-speaker">Stefan:</span> And this helps you just getting in as much as you need and as much as you like and it gives you also a lot of room to breathe and to take a break and to get your mind off of it and then revisit back later. This is also by the edit some interludes in between chapters which are mostly non-technical. They give you little bit of TypeScript culture, little bit of ideas how the TypeScript team thinks, how the community thinks, and how writing good TypeScript code because you without actually focusing on the coding aspect. And we also added those to give you a little break, a little room to breathe, to digest what you just learned because we know that this can be a lot of stuff. And, yeah, so if you just take one lesson a day, you are through with it in 50 days and are an expert in TypeScript, so.

<span class="smashing-tv-host">Drew:</span> I often find that when I’m writing about something I’ve been putting together a presentation or an article or something like that, I find that I learn new things that I didn’t appreciate before because having to explain something, you have to make sure you really understand all the details. Was there anything that you found about TypeScript in writing the book that you realized you were learning for the first time?

<span class="smashing-tv-speaker">Stefan:</span> Yes. There were two kind of things that I learned while writing the book that really surprised me. And one thing is how the type definitions TypeScript brings along are structured and created and declared. So they have written a parcel that goes over all the web standards on top of your 3C and there’s this web interface definition language which is it’s own language created by W3C to declare JavaScript interfaces and to take this code slip, it’s refracted them into TypeScript types. And then have some way of structuring them to be ready from ECMAScript 5 standards up to ECMAScript 2020, 2021 standards and if you browse through those alter generated file and read how good they are and how well documented they are and how the structure types that you can learn a lot.

<span class="smashing-tv-speaker">Stefan:</span> So this was one thing there. I kind of lost track at some point while writing it because it was just spending two or three days within, in those lib.d.ts files and soaking up everything that they created. I even have one lesson dedicated to lib.d.ts because it was so, so surprising. And the other thing is, I guess, realizing how generics and conditional types really work under the hood.

<span class="smashing-tv-speaker">Stefan:</span> Because when you apply them and you work with them you just use them as much so you get the right results, but you never question what’s actually making them work and by explaining them in chapters five and six in my book I really found out there are very delicate mechanics underneath and if you understand those mechanics it gets a lot, lot easier creating conditional types, creating generic types, than it would be without just by trying to figure out things. That’s why I also have some flows of code in my book where we start with the conditional type that you write and then we go step by step evaluating what it means until we get to the result type.

<span class="smashing-tv-speaker">Stefan:</span> And this is something where I found some joy in it because it really made me understand what my book should be actually about. That I spend a lot of time and cared a lot about getting those examples right, so. I hope readers will find the same joy out of it because it can be very, very interesting. And, yeah, it gets a little bit nerdy, but that’s part of the fun.

<span class="smashing-tv-host">Drew:</span> For anyone wanting to actually get started with JavaScript it sounds like your book is a really great place to begin. Are there any other resources that you’d recommend?

<span class="smashing-tv-speaker">Stefan:</span> So, one thing that I also mention very early in the book is the TypeScript Playground. So, TypeScript offers an interactive editor online with lots and lots and lots of examples to give you good feeling of how it is to work with TypeScript, how TypeScript in the JavaScript only scenario looks like and works like or which language features there and what they mean for your types and especially in the recent year, the TypeScript team hired a person, Orta, just to work on documentation and Playground and website and all those learning resources. And you can see that the process immensely.

<span class="smashing-tv-speaker">Stefan:</span> So, he spend so much time into refactoring every bit and piece of the whole website that it’s now a great learning resource and Otta also, has also written the forward to my book and were chatting about how a book on TypeScript can or should be different compared to what they provide as a learning resource. And I think they work really well together. The book gives you a very tailored and opinionated view and the learning resource that guides you step by step whereas the handbook is this big knowledge base where you get all the additional information and can dig deep into one specific scenario that wouldn’t have enough room in a book.

<span class="smashing-tv-host">Drew:</span> Stefan’s book TypeScript in 50 Lessons is available digitally from Smashing right now and it’ll be available in print from November 2020. You can find it at TypeScript-Book.com. So, I’ve been learning all about TypeScript. What have you been learning about lately Stefan?

<span class="smashing-tv-speaker">Stefan:</span> I’m digging into different programing languages again. I’ve been learning a little bit of Go and a little bit of Thrust and what scenarios there are for using them and it’s fun learning something entirely new. It gives you a new perspective on what you already learned so far. So, this is what I enjoy a lot at the moment.

<span class="smashing-tv-host">Drew:</span> It’s always exciting, isn’t it? Learning a new language and getting a new perspective on how other languages are structured.

<span class="smashing-tv-speaker">Stefan:</span> Absolutely.

<span class="smashing-tv-host">Drew:</span> If you, dear listener, would like to hear more from Stefan, you can follow him on Twitter where he’s DDPRRT and you can find his personal site at fetblog.edu. TypeScript in 50 Lessons is available now from Smashing and you can read all about it at TypeScript-Book.com. Thanks for joining us today, Stefan. Do you have any parting words?

<span class="smashing-tv-speaker">Stefan:</span> Thank you very much. No, well, DDPRRT is the worst Twitter handle in the entire world and if you say it very fast it’s dead parrot, and if you know Monty Python, you might know about the dead parrot. So, that’s all I can say about the worst twitter handle that there is.

<span class="smashing-tv-host">Drew:</span> He’s pining for the fjords.

<span class="smashing-tv-speaker">Stefan:</span> Yeah. But, seriously, I hope people enjoy working with TypeScript. I hope they enjoy my book. I’m really, really excited about feedback, so if you have any feedback hit me up on Twitter. I’m here to chat with you about all that stuff. And I’m also very happy to work with you on type programs. If you have something that you can’t quite make sense out of it just drop me a line or a Twitter direct message. I really take the time to see if we can solve the problem.

{{< signature "il" >}}
