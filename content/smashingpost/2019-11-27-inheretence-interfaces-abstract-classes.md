---
title: 'Mastering OOP: A Practical Guide To Inheritance, Interfaces, And Abstract Classes'
slug: guide-oop-inheritance-interfaces-abstract-classes
author: ryan-kay
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e655273f-ba34-4f69-8b10-7655e20de084/guide-oop-inheritance-interfaces-abstract-classes.png
date: 2019-11-27T11:00:00.000Z
summary: >-
  Arguably the worst way to teach the fundamentals of programming, is to describe what something is, without mention of how or when to use it. In this article, Ryan M. Kay discusses three core concepts in OOP in the least ambiguous terms so that you may never again wonder when to use inheritance, interfaces, or abstract classes. Code examples provided are in Java with some references to Android, but only basic knowledge of Java is required to follow along.
description: >-
  Arguably the worst way to teach the fundamentals of programming, is to describe what something is, without mention of how or when to use it. In this article, Ryan M. Kay discusses three core concepts in OOP.
categories:
  - Techniques
  - Coding
---
So far as I can tell, it is uncommon to come across educational content in the field of software development which provides an appropriate mixture of theoretical and practical information. If I was to guess why, I assume it is because individuals who focus on theory tend to get into teaching, and individuals who focus on practical information tend to get paid to solve specific problems, using specific languages and tools.

This is, of course, a broad generalization, but if we accept it briefly for arguments sake, it follows that many people (by no means all people) who take on the role of teacher, tend to be either poor at, or utterly incapable of explaining the practical knowledge relevant to a particular concept. 

In this article, I will do my best to discuss three core mechanisms which you will find in most Object Oriented Programming (OOP) languages: *Inheritance*, *interfaces* (a.k.a. *protocols*), and *abstract classes*. Rather than giving you technical and complex verbal explanations of what each mechanism **is**, I will do my best to focus on what they **do**, and **when** to use them. 

However, before addressing them individually, I would like to briefly discuss what it means to give a theoretically sound, yet practically useless explanation. My hope is that you can use this information to help you sift through different educational resources and to avoid blaming yourself when things do not make sense.

{{% feature-panel %}}

## Different Degrees Of Knowing

### Knowing Names

Knowing the name of something is arguably the most shallow form of knowing. In fact, a name is only generally useful to the extent that it either is commonly used by many people to refer to the same thing and/or it helps to describe the thing. Unfortunately, as anyone who has spent time in this field has discovered, many people use different names for the same thing (e.g. *interfaces* and *protocols*), the same names for different things (e.g. *modules* and *components*), or names which are esoteric to the point of being absurd (e.g. *Either Monad*). Ultimately, names are just pointers (or references) to mental models, and they can be of varying degrees of usefulness. 

To make this field even more difficult to study, I would hazard a guess that for most individuals, writing code is (or at least was) a very unique experience. Even more complicated is understanding how that code is ultimately compiled into machine language, and represented in physical reality as a series of electrical impulses changing over time. Even if one can recall the names of the processes, concepts, and mechanisms that are employed in a program, there is no guarantee that the mental models which one creates for such things are consistent with the models another individual; let alone whether they are objectively accurate.

It is for these reasons, alongside the fact that I do not have a naturally good memory for jargon, that I consider names to be the least important aspect of knowing something. That is not to say that names are useless, but I have in the past learned and employed many design patterns in my projects, only to learn of the commonly used name months, or even years later. 

### Knowing Verbal Definitions And Analogies

Verbal definitions are the natural starting point for describing a new concept. However, as with names, they can be of varying degrees of usefulness and relevance; much of that depending on what the end goals of the learner are. The most common problem I see in verbal definitions is assumed knowledge typically in the form of jargon. 

Suppose for example, that I was to explain that a *thread* is very much like a *process*, except that *threads* occupy the same *address space* of a given *process*. To someone who is already familiar with *processes* and *address spaces*, I have essentially stated that *threads* can be associated with their understanding of a *process* (i.e. they possess many of the same characteristics), but they can be differentiated based on a distinct characteristic. 

To someone who does not possess that knowledge, I have at best not made any sense, and at worst caused the learner to feel inadequate in some way for not knowing the things **I have assumed** they should know. In fairness, this is acceptable if your learners really ought to possess such knowledge (such as teaching graduate students or experienced developers), but I consider it to be a monumental failure to do so in any introductory level material.

Often it is very difficult to provide a good verbal definition of a concept when it is unlike anything else the learner has seen before. In this case, it is very important for the teacher to select an analogy which is likely to be familiar to the average person, and also relevant insofar as it conveys many of the same qualities of the concept.

For example, it is critically important for a software developer to understand what it means when software entities (different parts of a program) are _tightly-coupled_ or _loosely-coupled_. When building a garden shed, a junior carpenter may think that it is _faster_ and _easier_ to put it together using nails instead of screws. This is true up until the point at which a mistake is made, or a change in the design of the garden shed necessitates rebuilding part of the shed. 

At this point, the decision to use nails to _tightly-couple_ the parts of the garden shed together, has made the construction process as a whole more difficult, likely slower, and extracting nails with a hammer runs the risk of damaging the structure. Conversely, screws can take a bit of extra time to assemble, but they are easy to remove and pose little risk of damaging nearby parts of the shed. This is what I mean by _loosely-coupled_. Naturally, there are cases where you really just need a nail, but that decision ought to be guided by critical thinking and experience.

As I will discuss in detail later on, there are different mechanisms for connecting parts of a program together which provide varying degrees of _coupling_; just like *nails* and *screws*. While my analogy may have helped you understand what this critically important term means, I have not given you any idea of how to apply it outside of the context of building a garden shed. This leads me to the most important kind of knowing, and the key to deeply understanding vague and difficult concepts in any field of inquiry; although we will stick to writing code in this article.

{{% ad-panel-leaderboard %}}

### Knowing In Code

In my opinion, strictly regarding software development, the most import form of knowing a concept comes from being able to use it in the working application code. This form of knowing can be attained simply by writing lots of code and solving many different problems; jargon names and verbal definitions need not be included.

In my own experience, I recall solving the problem of communicating with a remote database, and a local database through a single *interface* (you will know what that means soon if you do not already); rather than the client (whatever class which talks to the _interface_) needing to call the remote and local (or even a test database) explicitly. In fact, the client had no idea what was behind the interface, so I did not need to change it regardless of if it was running in a production app or a test environment. About a year after I solved this problem, I came across the term “Facade Pattern”, and not long after the term “Repository Pattern”, which are both names that people use for the solution described prior.

All of this preamble is to hopefully illuminate some of the flaws which are most often made in explaining topics such as *inheritance*, *interfaces*, and *abstract classes*. Of the three, *inheritance* is likely the simplest one to both use and understand. In my experience both as a student of programming, and a teacher, the other two are almost invariably an issue to learners unless very special attention is paid to avoiding the mistakes discussed earlier. From this point on, I will do my best to make these topics as simple as they should be, but no simpler.

### A Note On The Examples

Being most fluent in Android mobile application development myself, I will use examples taken from that platform so that I may teach you about building GUI applications at the same time as introducing language features of Java. However, I will not be going into so much detail that the examples ought to be unintelligible by someone with a cursory understanding of Java EE, Swing or JavaFX. My ultimate goal in discussing these topics is to help you to understand what they mean in the context of solving a problem in just about any sort of application. 

I would also like to warn you, dear reader, that at times it may seem like I am being needlessly philosophical and pedantic about specific words and their definitions. The reason for this is that there truly is a deep philosophical underpinning required to understand the difference between something which is *concrete* (real), and something which is *abstract* (less detailed than a real thing). This understanding applies to many things outside of the field of computing, but it is of particularly high importance for any software developer to grasp the nature of *abstractions*. In any case, if my words fail you, the examples in code will hopefully not.

{{% ad-panel-leaderboard %}}

## Inheritance And Implementation

When it comes to building applications with a graphical user interface (GUI), _inheritance_ is arguably the most important mechanism for making it possible to quickly build an application. 

Although there is a lesser understood benefit to using _inheritance_ to be discussed later, **the primary benefit is to share implementation between classes**. This word “implementation”, at least for the purposes of this article, has a distinct meaning. To give a general definition of the word in English, I might say that to *implement* something, is to *make it real*. 

To give a technical definition specific to software development, I might say that to *implement* a piece of software, is to write *concrete* lines of code which satisfy the requirements of said piece of software. For example, suppose I am writing a *sum method*:
`private double sum(double first, double second){`

<pre><code class="language-javascript">private double sum(double first, double second){
        //TODO: implement
}
</code></pre>

The snippet above, even though I have made it as far as writing a return type (`double`) and a _method declaration_ which specifies the arguments (`first, second`) and the name which can be used to call said _method_ (`sum`), it has **not been _implemented_**. In order to _implement_ it, we must complete the _method body_ like so:

<pre><code class="language-javascript">private double sum(double first, double second){
        return first + second;
}
</code></pre>

Naturally, the first example would not compile, but we will see momentarily that _interfaces_ are a way in which we can write these sorts of **unimplemented** functions without errors.

### Inheritance In Java

Presumably, if you are reading this article, you have used the `extends` Java keyword at least once. The mechanics of this keyword are simple and most often described using examples to do with different kinds of animals or geometric shapes; `Dog `and `Cat `extend `Animal`, and so forth. I will assume that I do not need to explain rudimentary type theory to you, so let us get right into the primary benefit of _inheritance_ in Java, via the `extends `keyword.

Building a console-based “Hello World” application in Java is very simple. Assuming you possess a Java Compiler (_javac_) and runtime environment (_jre_), you can write a class which contains a _main_ function like so:

<pre><code class="language-javascript">public class JavaApp{
     public static void main(String []args){
        System.out.println("Hello World");
     }
}
</code></pre>

Building a GUI application in Java on almost any of its main platforms (Android, Enterprise/Web, Desktop), with a bit of help from an IDE to generate the skeleton/boilerplate code of a new app, is also relatively easy thanks to the `extends `keyword. 

Suppose that we have an XML Layout called `activity_main.xml` (we typically build user interfaces declaratively in Android, via Layout files) containing a `TextView `(like a text label) called `tvDisplay`:

<pre><code class="language-javascript">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;FrameLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent"&gt;

    &lt;TextView
        android:id="@+id/tvDisplay"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        /&gt;


&lt;/FrameLayout&gt;
</code></pre>

Also, suppose that we would like `tvDisplay `to say “Hello World!” To do so, we simply need to write a class which uses the `extends `keyword to inherit from the `Activity `class:

<pre><code class="language-javascript">import android.app.Activity;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


        ((TextView)findViewById(R.id.tvDisplay)).setText("Hello World");
    }
</code></pre>

The effect of inheriting the implementation of the `Activity `class can be best appreciated by taking a quick look at its [source code](https://android.googlesource.com/platform/frameworks/base/+/master/core/java/android/app/Activity.java). I highly doubt that Android would have become the dominant mobile platform if one needed to *implement* even a small portion of the 8000+ lines necessary to interact with the system, just to generate a simple window with some text. _Inheritance_ is what allows us to not have to rebuild the _Android framework_, or whatever platform you happen to be working with, from scratch. 

### Inheritance Can Be Used For Abstraction

Insofar as it can be used to share implementation across classes, _inheritance_ is relatively simple to understand. However, there is another important way in which _inheritance_ can be used, which is conceptually related to the _interfaces_ and _abstract classes_ which we will be discussing soon. 

If you please, suppose for the next little while that an abstraction, used in the most general sense, is _a less detailed representation of a thing_. Instead of qualifying that with a lengthy philosophical definition, I will try to point out how _abstractions_ work in daily life, and shortly thereafter discuss them expressly in terms of software development. 

Suppose you are traveling to Australia, and you are aware that the region you are visiting is host to a particularly high density of inland taipan snakes (they are apparently quite poisonous). You decide to consult Wikipedia to learn more about them by looking at images and other information. By doing so, you are now acutely aware of a particular kind of snake which you have never seen before.

Abstractions, ideas, models, or whatever else you want to call them, are less detailed representations of a thing. It is important that they are less detailed than the real thing because a real snake can bite you; images on Wikipedia pages typically do not. _Abstractions_ are also important because both computers and human brains have a limited capacity to store, communicate, and process information. Having enough detail to use this information in a practical way, without taking up too much space in memory, is what makes it possible for computers and human brains alike to solve problems.


To tie this back into _inheritance_, all of the three main topics I am discussing here can be used as _abstractions_, or mechanisms of _abstraction_. Suppose that in our “Hello World” app’s layout file, we decide to add an `ImageView`,  `Button`, and `ImageButton`:

<div class="break-out">

 <pre><code class="language-javascript">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;LinearLayout xmlns:android="https://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent"&gt;
    &lt;Button
       android:id="@+id/btnDisplay"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"/&gt;

    &lt;ImageButton
        android:id="@+id/imbDisplay"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/&gt;

    &lt;ImageView
        android:id="@+id/imvDisplay"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/&gt;
&lt;/LinearLayout&gt;
</code></pre>
</div>

Also suppose that our Activity has implemented `View.OnClickListener` to handle clicks:

<div class="break-out">

 <pre><code class="language-javascript">public class MainActivity extends Activity implements View.OnClickListener {
    private Button b;
    private ImageButton ib;
    private ImageView iv;    


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //...
        b = findViewById(R.id.imvDisplay).setOnClickListener(this);
        ib = findViewById(R.id.btnDisplay).setOnClickListener(this);
        iv = findViewById(R.id.imbDisplay).setOnClickListener(this);
    }

    @Override
    public void onClick(View view) {
        final int id = view.getId();
        //handle click based on id...
    }
}
</code></pre>
</div>

The key principle here is that `Button`, `ImageButton`, and `ImageView `inherit from the `View `class. The result is that this function `onClick `can receive click events from disparate (though hierarchically related) UI elements by referencing them as their less detailed parent class. This is far more convenient than having to write a distinct _method_ for handling every kind of widget on the _Android platform_ (not to mention custom widgets).

## Interfaces And Abstraction

You may have found the previous code example to be a bit uninspiring, even if you understood why I chose it. Being able to share _implementation_ across a hierarchy of classes is incredibly useful, and I would argue that to be the primary utility of _inheritance_. As for allowing us to treat a set of classes that have a common _parent class_ as equal in _type_ (i.e. as the _parent class_), that feature of _inheritance_ has limited use. 

By limited, I am speaking of the requirement of child classes to be within the same class hierarchy in order to be referenced via, or known as the parent class. In other words, _inheritance_ is a very restrictive mechanism for _abstraction_. In fact, if I suppose that _abstraction_ is a spectrum that moves between different levels of detail (or information), I might say that _inheritance_ is **the least abstract** mechanism for _abstraction_ in Java.

Before I proceed to discussing _interfaces_, I would like to mention that as of _Java 8_, two features called _Default Methods_ and _Static Methods_ have been added to _interfaces_. I will discuss them eventually, but for the moment I would like us to pretend that they do not exist. This is in order for me to make it easier to explain the primary purpose of using an _interface_, which was initially, and arguably still is, **the most abstract mechanism for abstraction in Java**.


### Less Detail Means More Freedom

In the section on _inheritance_, I gave a definition of the word _implementation_, which was meant to contrast with another term we will now go into. To be clear, I do not care about the words themselves, or whether you agree with their usage; only that you understand what they conceptually point to. 

Whereas _inheritance_ is primarily a tool to share _implementation_ across a set of classes, we might say that _interfaces_ are primarily a mechanism to share _behavior_ across a set of classes. _Behavior_ used in this sense is truly just a non-technical word for _abstract methods_. An _abstract method_ is a _method_ which does not, in fact cannot, contain a _method body_:

<pre><code class="language-javascript">public interface OnClickListener {
        void onClick(View v);
}
</code></pre>

The natural reaction for me, and a number of individuals whom I have tutored, after first looking at an _interface_, was to wonder what the utility of sharing only a _return type_, _method name_, and _parameter list_ might be. On the surface, it looks like a great way to create extra work for yourself, or whoever else might be writing the class which `implements `the _interface_. The answer, is that _interfaces_ are perfect for situations where you want a set of classes to _behave_ in the same manner (i.e. they possess the same public _abstract methods_), but you expect them to _implement_ that _behavior_ in different ways. 

To take a simple but relevant example, the Android platform possesses two classes which are primarily in the business of creating and managing part of the user interface: `Activity` and `Fragment`. It follows that these classes will very often have the requirement of listening to events which pop up when a widget is clicked (or otherwise interacted with by a user). For argument’s sake, let us take a moment to appreciate why _inheritance_ will almost never solve such a problem:

<pre><code class="language-javascript">public class OnClickManager {
    public void onClick(View view){
        //Wait a minute... Activities and Fragments almost never 
        //handle click events exactly the same way...
    }
}
</code></pre>

Not only would making our _Activities_ and _Fragments_ inherit from `OnClickManager `make it impossible to handle events in a different manner, but the kicker is that we could not even do that if we wanted to. Both _Activity_ and _Fragment_ already extend a _parent class_, and Java does not allow multiple _parent classes_. So our problem is that we want a set of classes to _behave_ the same way, but **we must** have flexibility on how the class _implements_ that _behavior_. This brings us back to the earlier example of the `View.OnClickListener`:

<pre><code class="language-javascript">public interface OnClickListener {
        void onClick(View v);
}
</code></pre>

This is the actual source code (which is nested in the `View `class), and these few lines allow us to ensure consistent _behavior_ across different widgets (_Views_) and UI controllers (_Activities, Fragments, etc._).

### Abstraction Promotes Loose-Coupling

I have hopefully answered the general question about why interfaces exist in Java; among many other languages. From one perspective, they are just a means of sharing code between classes, but they are deliberately less detailed in order to allow for different _implementations_. But just as _inheritance_ can be used both as a mechanism for sharing code and _abstraction_ (albeit with restrictions on class hierarchy), it follows that _interfaces_ provide a more flexible mechanism for _abstraction_.

In an earlier section of this article, I introduced the topic of _loose/tight-coupling_ by analogy of the difference between using _nails_ and _screws_ to build some kind of structure. To recap, the basic idea is that you will want to use _screws_ in situations where changing the existing structure (which can be a result of fixing mistakes, design changes, and so forth) is likely to happen. _Nails_ are fine to use when you just need to fasten parts of the structure together and are not particularly worried about taking them apart in the near future. 

_Nails_ and _screws_ are meant to be analogous to _concrete_ and _abstract references_ (the term _dependencies_ also applies) between classes. Just so there is no confusion, the following sample will demonstrate what I mean:

<pre><code class="language-javascript">class Client {
    private Validator validator;
    private INetworkAdapter networkAdapter;

    void sendNetworkRequest(String input){
        if (validator.validateInput(input)) {
            try {
                networkAdapter.sendRequest(input);
            } catch (IOException e){
                //handle exception
            }
        }
    }
}

class Validator {
    //...validation logic
    boolean validateInput(String input){
        boolean isValid = true;
        //...change isValid to false based on validation logic
        return isValid;
    }
}

interface INetworkAdapter {
    //...
    void sendRequest(String input) throws IOException;
}
</code></pre>

Here, we have a class called `Client ` which possesses two kinds of _references_. Notice that, assuming `Client `does not have anything to do with creating its _references_ (it really should not), it is decoupled from the implementation details of any particular network adapter. 

There are a few important implications of this _loose coupling_. For starters, I can build `Client `in absolute isolation of any _implementation_ of `INetworkAdapter`. Imagine for a moment that you are working in a team of two developers; one to build the front end, one to build the back end. As long as both developers are kept aware of the _interfaces_ which couple their respective classes together, they can carry on with the work virtually independently of one another.

Secondly, what if I were to tell you that both developers could verify that their respective _implementations_ functioned properly, also independently of each other’s progress? This is very easy with interfaces; just build a _Test Double_ which `implements `the appropriate _interface_:


<pre><code class="language-javascript">class FakeNetworkAdapter implements INetworkAdapter {
    public boolean throwError = false;


    @Override
    public void sendRequest(String input) throws IOException {
        if (throwError) throw new IOException("Test Exception");
    }
}
</code></pre>

In principle, what can be observed is that working with _abstract references_ opens the door to increased modularity, testability, and some very powerful design patterns such as the *Facade Pattern*, *Observer Pattern*, and more. They can also allow developers to find a happy balance of designing different parts of a system based on _behavior_ (_Program To An Interface_), without getting bogged down in _implementation_ details.

### A Final Point On Abstractions

_Abstractions_ do not exist in the same way as a _concrete_ thing. This is reflected in the Java Programming language by the fact that _abstract classes_ and _interfaces_ may not be instantiated.

For example, this would definitely not compile:

<pre><code class="language-javascript">public class Main extends Application {
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
      //ERROR x2:
        Foo f = new Foo();
        Bar b = new Bar()

    }


    private abstract class Foo{}
    private interface Bar{}


}
</code></pre>

In fact, the idea of expecting an unimplemented _interface_ or _abstract class_ to function at runtime makes as much sense as expecting a UPS uniform to float around delivering packages. Something concrete must be behind the _abstraction_ for it to be of utility; even if the calling class does not need to know what is actually behind _abstract references_.

## Abstract Classes: Putting It All Together

If you have made it this far, then I am happy to tell you that I have no more philosophical tangents or jargon phrases to translate. Simply put, _abstract classes_ are a mechanism for sharing _implementation_ and _behavior_ across a set of classes. Now, I will admit straight away that I do not find myself using _abstract classes_ all that often. Even so, my hope is that by the end of this section you will know exactly when they are called for.

### Workout Log Case Study

Roughly a year into building Android apps in Java, I was rebuilding my first Android app from scratch. The first version was the kind of horrendous mass of code that you would expect from a self-taught developer with little guidance. By the time I wanted to add new functionality, it became clear that the _tightly coupled_ structure I had built exclusively with _nails_, was so impossible to maintain that I must rebuild it entirely.

The app was a workout log that was designed to allow easy recording of your workouts, and the ability to output the data of a past workout as a text or image file. Without getting into too much detail, I structured the data models of the app such that there was a `Workout `object, which comprised of a collection of `Exercise `objects (among other fields which are irrelevant to this discussion).

As I was implementing the feature for outputting workout data to some kind of visual medium, I realized that I had to deal with a problem: Different kinds of exercises would require different kinds of text outputs.

To give you a rough idea, I wanted to change the outputs depending on the type of exercise like so:

*   Barbell: 10 REPS @ 100 LBS
*   Dumbbell: 10 REPS @ 50 LBS x2
*   Bodyweight: 10 REPS @ Bodyweight
*   Bodyweight +: 10 REPS @ Bodyweight + 45 LBS
*   Timed: 60 SEC @ 100 LBS

Before I proceed, note that there were other types (working out can become complicated) and that the code I will be showing has been trimmed down and changed to fit nicely into an article.

In keeping with my definition from before, the goal of writing an _abstract class_, is to _implement_ everything (even _state_ such as _variables_ and _constants_) which is shared across all _child classes_ in the _abstract class_. Then, for anything which changes across said _child classes_, create an _abstract method_:

<div class="break-out">

 <pre><code class="language-javascript">abstract class Exercise {
    private final String type;
    protected final String name;
    protected final int[] repetitionsOrTime;
    protected final double[] weight;

    protected static final String POUNDS = "LBS";
    protected static final String SECONDS = "SEC ";
    protected static final String REPETITIONS = "REPS ";

    public Exercise(String type, String name, int[] repetitionsOrTime, double[] weight) {
        this.type = type;
        this.name = name;
        this.repetitionsOrTime = repetitionsOrTime;
        this.weight = weight;
    }

    public String getFormattedOutput(){
        StringBuilder sb = new StringBuilder();
        sb.append(name);
        sb.append("\n");
        getSetData(sb);
        sb.append("\n");
        return sb.toString();
    }

    /**
     * Append data appropriately based on Exercise type
     * @param sb - StringBuilder to Append data to
     */
    protected abstract void getSetData(StringBuilder sb);
    
    //...Getters
}

</code></pre>
</div>

I may be stating the obvious, but if you have any questions about what should or should not be _implemented_ in the _abstract class_, the key is to look at any part of the _implementation_ which has been repeated in all child classes. 

Now that we have established what is common amongst all exercises, we can begin to create child classes with specializations for each kind of String output:


#### Barbell Exercise:

<div class="break-out">

 <pre><code class="language-javascript">class BarbellExercise extends Exercise {
    public BarbellExercise(String type, String name, int[] repetitionsOrTime, double[] weight) {
        super(type, name, repetitionsOrTime, weight);
    }

    @Override
    protected void getSetData(StringBuilder sb) {
        for (int i = 0; i < repetitionsOrTime.length; i++) {
            sb.append(repetitionsOrTime[i]);
            sb.append(" ");
            sb.append(REPETITIONS);
            sb.append(" @ ");
            sb.append(weight[i]);
            sb.append(POUNDS);
            sb.append("\n");
        }
    }
}
</code></pre>
</div>

#### Dumbbell Exercise:

<div class="break-out">

 <pre><code class="language-javascript">class DumbbellExercise extends Exercise {
    private static final String TIMES_TWO = "x2";

    public DumbbellExercise(String type, String name, int[] repetitionsOrTime, double[] weight) {
        super(type, name, repetitionsOrTime, weight);
    }

    @Override
    protected void getSetData(StringBuilder sb) {

        for (int i = 0; i < repetitionsOrTime.length; i++) {
            sb.append(repetitionsOrTime[i]);
            sb.append(" ");
            sb.append(REPETITIONS);
            sb.append(" @ ");
            sb.append(weight[i]);
            sb.append(POUNDS);
            sb.append(TIMES_TWO);
            sb.append("\n");
        }
    }
}
</code></pre>
</div>

#### Bodyweight Exercise:

<div class="break-out">

 <pre><code class="language-javascript">class BodyweightExercise extends Exercise {
    private static final String BODYWEIGHT = "Bodyweight";

    public BodyweightExercise(String type, String name, int[] repetitionsOrTime, double[] weight) {
        super(type, name, repetitionsOrTime, weight);
    }

    @Override
    protected void getSetData(StringBuilder sb) {

        for (int i = 0; i < repetitionsOrTime.length; i++) {
            sb.append(repetitionsOrTime[i]);
            sb.append(" ");
            sb.append(REPETITIONS);
            sb.append(" @ ");
            sb.append(BODYWEIGHT);
            sb.append("\n");
        }
    }
}
</code></pre>
</div>

I am certain that some astute readers will find things which could have been _abstracted out_ in a more efficient manner, but the purpose of this example (which has been simplified from the original source) is to demonstrate the general approach. Of course, no programming article would be complete without something which can be executed. There are several online Java compilers which you may use to run this code if you want to test it out (unless you already have an IDE):

<pre><code class="language-javascript">public class Main {
    public static void main(String[] args) {
        //Note: I actually used another nested class called a "Set" instead of an Array
        //to represent each Set of an Exercise.
        int[] reps = {10, 10, 8};
        double[] weight = {70.0, 70.0, 70.0};

        Exercise e1 = new BarbellExercise(
                "Barbell",
                "Barbell Bench Press",
                reps,
                weight
        );

        Exercise e2 = new DumbbellExercise(
                "Dumbbell",
                "Dumbbell Bench Press",
                reps,
                weight
        );

        Exercise e3 = new BodyweightExercise(
                "Bodyweight",
                "Push Up",
                reps,
                weight
        );

        System.out.println(
                e1.getFormattedOutput()
                + e2.getFormattedOutput()
                + e3.getFormattedOutput()
        );
    }
}
</code></pre>

Executing this toy application yields the following output:
`Barbell Bench Press`

<pre><code class="language-javascript">10 REPS  @ 70.0LBS
10 REPS  @ 70.0LBS
8 REPS  @ 70.0LBS

Dumbbell Bench Press
10 REPS  @ 70.0LBSx2
10 REPS  @ 70.0LBSx2
8 REPS  @ 70.0LBSx2

Push Up
10 REPS  @ Bodyweight
10 REPS  @ Bodyweight
8 REPS  @ Bodyweight
</code></pre>

### Further Considerations

Earlier, I mentioned that there are two features of Java _interfaces_ (as of Java 8) which are decidedly geared towards sharing _implementation_, as opposed to _behavior_. These features are known as _Default Methods_ and _Static Methods_. 

I have decided not to go into detail on these features for the reason that they are most typically used in mature and/or large code bases where a given _interface_ has many _inheritors._ Despite the fact that this is meant to be an introductory article, and I still encourage you to take a look at these features eventually, even though I am confident that you will not need to worry about them just yet. 

I would also like to mention that there are other ways to share _implementation_ across a set of classes (or even _static methods_) in a Java application that does not require _inheritance_ or _abstraction_ at all. For example, suppose you have some _implementation_ which you expect to use in a variety of different classes, but does not necessarily make sense to share via _inheritance_. A common pattern in Java is to write what is known as a _Utility_ class, which is a simple `class `containing the requisite _implementation_ in a _static method_:


<div class="break-out">

 <pre><code class="language-javascript">public class TimeConverterUtil {

    /**
     * Accepts an hour (0-23) and minute (0-59), then attempts to format them into an appropriate
     * format such as 12, 30 -> 12:30 pm
     */    
    public static String convertTime (int hour, int minute){
        String unformattedTime = Integer.toString(hour) + ":" + Integer.toString(minute);
        DateFormat f1 = new SimpleDateFormat("HH:mm");

        Date d = null;
        try { d = f1.parse(unformattedTime); } 
        catch (ParseException e) { e.printStackTrace(); }
        DateFormat f2 = new SimpleDateFormat("h:mm a");
        return f2.format(d).toLowerCase();
    }
}
</code></pre>
</div>


Using this _static method_ in an external class (or another _static method_) looks like this:

<pre><code class="language-javascript">
public class Main {
    public static void main(String[] args){
        //...
        String time = TimeConverterUtil.convertTime(12, 30);
        //...
    }
}
</code></pre>

## Cheat Sheet

We have covered a lot of ground in this article, so I would like to spend a moment summarizing the three main mechanisms based on what problems they solve. Since you should possess a sufficient understanding of the terms and ideas I have either introduced or redefined for the purposes of this article, I will keep the summaries brief.

#### I Want A Set Of Child Classes To Share Implementation

Classic _inheritance_, which requires a _child class_ to _inherit_ from a _parent class_, is a very simple mechanism for sharing _implementation_ across a set of classes. An easy way to decide if some _implementation_ should be pulled into a _parent class_, is to see whether it is repeated in a number of different classes line for line. The acronym **DRY** (_Don’t Repeat Yourself_) is a good mnemonic device to watch out for this situation.

While coupling _child classes_ together with a common _parent class_ can present some limitations, a side benefit is that they can all be referenced as the _parent class_, which provides a limited degree of _abstraction_.

#### I Want A Set Of Classes To Share Behavior

Sometimes, you want a set of classes to be capable of possessing certain _abstract methods_ (referred to as _behavior_), but you do not expect the _implementation_ of that _behavior_ to be repeated across inheritors. 

By definition, Java interfaces may not contain any implementation (except for _Default_ and _Static Methods_), but any class which implements an _interface_, must supply an _implementation_ for all abstract methods, otherwise, the code will not compile. This provides a healthy measure of flexibility and restriction on what is actually shared and does not require the inheritors to be of the same _class hierarchy_.

#### I Want A Set Of Child Classes To Share Behavior And Implementation

Although I do not find myself using _abstract classes_ all over the place, they are perfect for situations when you require a mechanism for sharing both _behavior_ and _implementation_ across a set of classes. Anything which will be repeated across _inheritors_ may be _implemented_ directly in the `abstract class`, and anything which requires flexibility may be specified as an _abstract method_.

{{< signature "dm, il" >}}
