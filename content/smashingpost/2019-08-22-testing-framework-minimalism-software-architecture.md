---
title: 'Testing Made Easier Via Framework Minimalism And Software Architecture'
slug: testing-framework-minimalism-software-architecture
author: ryan-kay
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1c1bd138-3d7f-41b0-929c-d93ce2b2f13d/testing-framework-minimalism-software-architecture.png
date: 2019-08-22T13:00:59+02:00
summary: >-
  As with many other topics in software development, testing and test driven development are often made needlessly complex in theory and implementation by placing too much emphasis on learning a wide array of testing frameworks. In this article, we will revisit what testing means by a simple analogy, explore concepts in software architecture which will directly result in a reduced need for testing frameworks, and some arguments as to why you might benefit from an attitude of minimalism for your testing process.
description: >-
   In this article, we will revisit what testing means by a simple analogy, explore concepts in software architecture, and some arguments as to why you might benefit from an attitude of minimalism for your testing process.
categories:
  - Android
  - Testing
  - Frameworks
---
Like many other Android developers, my initial foray into testing on the platform lead me to be immediately confronted with a demoralizing degree of jargon. Further, what few examples I came across at the time (circa 2015) did not present practical use cases which may have inclined me to think that the cost to benefit ratio of learning a tool like *Espresso* in order to verify that a *TextView.setText(...)* was working properly, was a reasonable investment.

To make matters even worse, I did not have a working understanding of software architecture in theory or practice, which meant that even if I bothered to learn these frameworks, I would have been writing tests for *monolithic* applications comprised of a few `god` classes, written in *spaghetti code*. The punchline is that building, testing, and maintaining such applications is an exercise in self-sabotage quite regardless of your framework expertise; yet this realization only becomes clear after one has built a *modular*, *loosely-coupled*, and *highly-cohesive* application.

From here we arrive at one of the main points of discussion in this article, which I will summarize in plain language here: Among the primary benefits of applying the golden principles of software architecture (do not worry, I will discuss them with simple examples and language), is that your code can become easier to test. There are other benefits to applying such principles, but the relationship between software architecture and testing is the focus of this article.

However, for the sake of those who wish to understand why and how we test our code, we will first explore the concept of testing by analogy; without requiring you to memorize any jargon. Before getting deeper into the primary topic, we will also look at the question of why so many testing frameworks exist, for in examining this we may begin to see their benefits, limitations, and perhaps even an alternative solution.

{{% feature-panel %}}

## Testing: Why And How

This section will not be new information for any seasoned tester, but perhaps you may enjoy this analogy nonetheless. Of course I am a software engineer, not a rocket engineer, but for a moment I will borrow an analogy which relates to designing and building objects both in physical space, and in the memory space of a computer. It turns out that while the medium changes, the process is in principle quite the same.

<p class="c-pre-sidenote--left">Suppose for a moment that we are rocket engineers, and our job is to build the first stage* rocket booster of a space shuttle. Suppose as well, that we have come up with a serviceable design for the first stage to begin building and testing in various conditions.</p><p class="c-sidenote c-sidenote--right">“First stage” refers to boosters which are fired when the rocket is first launched</p>

Before we get to the process, I would like to point out why I prefer this analogy: You should not have any difficulty answering the question of *why* we are bothering to test our design before putting it in situations where human lives are at stake. While I will not try to convince you that testing your applications before *launch* could save lives (although it is possible depending on the nature of the application), it could save ratings, reviews, and your job. In the broadest sense, testing is the way in which we make sure that single parts, several components, and whole systems work before we employ them in situations where it is critically important for them to not fail.

Returning to the how aspect of this analogy, I will introduce the process by which engineers go about testing a particular design: *redundancy*. Redundancy is simple in principle: Build copies of the component to be tested to the same design specification as what you wish to use at launch time. Test these copies in an isolated environment which strictly controls for preconditions and variables. While this does not guarantee that the *rocket booster* will work properly when integrated in the whole shuttle, one can be certain that if it does not work in a controlled environment, it will be very unlikely to work at all.

Suppose that of the hundreds, or perhaps thousands of variables which the *copies* of the rocket design have been tested against, it comes down to ambient temperatures in which the *rocket booster* will be test fired. Upon testing at 35° Celsius, we see that everything functions without error. Again, the rocket is tested at roughly room temperature without failure. The final test will be at the lowest recorded temperature for the launch site, at -5° Celcius. During this final test, the rocket fires, but after a short period, the rocket flares up and shortly thereafter explodes violently; but fortunately in a controlled and safe environment.

At this point, we know that changes in temperature appear to be at least involved in the failed test, which leads us to consider what parts of the *rocket booster* may be adversely effected by cold temperatures. Over time, it is discovered that one key component, a rubber *O-ring* which serves to staunch the flow of fuel from one compartment to another, becomes rigid and ineffectual when exposed to temperatures approaching or below freezing.

It is possible that you have noticed that his analogy is loosely based on the tragic events of the *Challenger* space shuttle disaster. For those unfamiliar, the sad truth (insofar as investigations concluded) is that there were plenty of failed tests and warnings from the engineers, and yet administrative and political concerns spurred the launch to proceed regardless. In any case, whether or not you have memorized the term *redundancy*, my hope is that you have grasped the fundamental process for testing parts of any kind of system.

{{% ad-panel-leaderboard %}}

### Concerning Software

Whereas the prior analogy explained the fundamental process for testing rockets (while taking plenty of liberty with the finer details), I will now summarize in a manner which is likely more relevant to you and I. While it is possible to test software by only launching it to devices once it is in any sort of deployable state, I suppose instead that we can apply the principle of *redundancy* to the individual parts of the application first.

This means that we create copies of the smaller parts of the whole application (commonly referred to as *Units* of software), set up an isolated test environment, and see how they behave based on whatever variables, arguments, events, and responses which may occur at runtime. Testing is truly as simple as that in theory, but the key to even getting to this process lies in building applications which are feasibly testable. This comes down to two concerns which we will look at in the next two sections. The first concern has to do with the *test environment*, and the second concern has to do with the way in which we structure applications.

## Why Do We Need Frameworks?

In order to test a piece of software (henceforth referred to as a *Unit*, although this definition is deliberately an over-simplification), it is necessary to have some kind of testing environment which allows you to interact with your software at runtime. For those building applications to be executed purely on a *JVM* (_Java Virtual Machine_) environment, all that is required to write tests is a *JRE* (_Java Runtime Environment_). Take for example this very simple *Calculator* class:

<pre><code class="language-java">class Calculator {
    private int add(int a, int b){
        return a + b;
    }

    private int subtract(int a, int b){
        return a - b;
    }
}
</code></pre>

In absence of any frameworks, as long as we have a test class which contains a `main`function to actually execute our code, we can test it. As you may recall, the `main` function denotes the starting point of execution for a simple Java program. As for what we are testing for, we simply feed some test data into the Calculator’s functions and verify that it is performing basic arithmetic properly:

<div class="break-out">

 <pre><code class="language-java">public class Main {

    public static void main(String[] args){
	//create a copy of the Unit to be tested
        Calculator calc = new Calculator();
	//create test conditions to verify behaviour
        int addTest = calc.add(2, 2);
        int subtractTest = calc.subtract(2, 2);

	//verify behaviour by assertion
        if (addTest == 4) System.out.println("addTest has passed.");
        else System.out.println("addTest has failed.");

        if (subtractTest == 0) System.out.println("subtractTest has passed.");
        else System.out.println("subtractTest has failed.");
    }
}
</code></pre>
</div>

Testing an Android application is of course, a completely different procedure. Although there is a `main` function buried deep within the source of the *ZygoteInit.java* file (the finer details of which are not important here), which is invoked prior to an Android application being launched on the *JVM*, even a junior Android developer ought to know that the system itself is responsible for calling this function; *not the developer*. Instead, the entry points for Android applications happen to be the `Application` class, and any `Activity` classes which the system can be pointed to via the *AndroidManifest.xml* file.

All of this is just a lead up to the fact that testing *Units* in an Android application presents a greater level of complexity, strictly because our testing environment must now account for the Android platform.

{{% ad-panel-leaderboard %}}

### Taming The Problem Of Tight Coupling

*Tight coupling* is a term which describes a function, class, or application module which is *dependent* on particular platforms, frameworks, languages, and libraries. It is a relative term, meaning that our *Calculator.java* example is tightly coupled to the Java programming language and standard library, but that is the extent of its coupling. Along the same lines, the *problem* of testing classes which are tightly coupled to the Android platform, is that you must find a way to work with or around the platform.

For classes tightly coupled to the Android platform, you have two options. The first, is to simply deploy your classes to an Android device (physical or virtual). While I do suggest that you test deploy your application code before shipping it to production, this is a highly inefficient approach during the early and middle stages of the development process with respect to time.

A *Unit*, however technical a definition you prefer, is generally thought of as a single function in a class (although some expand the definition to include subsequent helper functions which are called internally by the initial single function call). Either way, *Units* are meant to be small; building, compiling, and deploying an entire application to test a single *Unit* is to miss the point of testing in isolation **entirely**.

Another solution to the problem of tight coupling, is to use testing frameworks to interact with, or *mock* (simulate) platform dependencies. Frameworks such as *Espresso* and *Robolectric* give developers far more effective means for testing *Units* than the previous approach; the former being useful for tests run on a device (known as “instrumented tests” because apparently calling them device tests was not ambiguous enough) and the latter being capable of mocking the Android framework locally on a JVM.

Before I proceed to railing against such frameworks instead of the alternative I will discuss shortly, I want to be clear that I do not mean to imply that you should never use these options. The process which a developer uses to build and test their applications should be born of a combination of personal preference and an eye for efficiency.

For those who are not fond of building modular and loosely coupled applications, you will have no choice but to become familiar with these frameworks if you wish to have an adequate level of test coverage. Many wonderful applications have been built this way, and I am not infrequently accused of making my applications too modular and abstract. Whether you take my approach or decide to lean heavily on frameworks, I salute you for putting in the time and effort to test your applications.

### Keep Your Frameworks At Arms Length

For the final preamble to the core lesson of this article, it is worth discussing why you might want to have an attitude of minimalism when it comes to using frameworks (and this applies to more than just testing frameworks). The subtitle above is a paraphrase from the magnanimous teacher of software best practices: Robert “Uncle Bob” C. Martin. Of the many gems he has given me since I first studied his works, this one took several years of direct experience to grasp.

Insofar As I understand what this statement is about, the cost of using frameworks is in the time investment required to learn and maintain them. Some of them change quite frequently and some of them do not change frequently enough. Functions become deprecated, frameworks cease to be maintained, and every 6-24 months a new framework arrives to supplant the last. Therefore, if you can find a solution which can be implemented as a platform or language feature (which tend to last much longer), it will tend to be more resistant to changes of the various types mentioned above.

On a more technical note, frameworks such as *Espresso* and to a lesser degree *Robolectric*, can never run as efficiently as simple *JUnit* tests, or even the framework free test from earlier on. While *JUnit* is indeed a framework, it is tightly coupled to the *JVM*, which tends to change at a much slower rate than the Android platform proper. Fewer frameworks *almost* invariably means code which is more efficient in terms of the time it takes to execute and write one or more tests.

From this, you can probably gather that we will now be discussing an approach which will leverage some techniques which allows us to keep the Android platform at arms length; all the while allowing us plenty of code coverage, test efficiency, and the opportunity to still use a framework here or there when the need arises.

## The Art Of Architecture

To use a silly analogy, one might think of frameworks and platforms as being like overbearing colleagues who will take over your development process unless you set appropriate boundaries with them. The golden principles of software architecture can give you the general concepts and specific techniques necessary to both create and enforce these boundaries. As we will see in a moment, if you have ever wondered what the benefits of applying software architecture principles in your code truly are, some directly, and many indirectly make your code easier to test.

### Separation Of Concerns

*Separation Of Concerns* is by my estimation the most universally applicable and useful concept in software architecture as a whole (without meaning to say that others should be neglected). Separation of concerns (SOC) can be applied, or completely ignored, across every perspective of software development I am aware of. To briefly summarize the concept, we will look at SOC when applied to classes, but be aware that SOC can be applied to functions through extensive usage of *helper functions*, and it can be extrapolated to entire *modules* of an application (“modules” used in the context of Android/Gradle).

If you have spent much time at all researching software architectural patterns for GUI applications, you will likely have come across at least one of: Model-View-Controller (MVC), Model-View-Presenter (MVP), or Model-View-ViewModel (MVVM). Having built applications in every style, I will say upfront that I do not consider any of them to be the single best option for all projects (or even features within a single project). Ironically, the pattern which the Android team presented some years ago as their recommended approach, MVVM, appears to be the least testable in absence of Android specific testing frameworks (assuming you wish to use the Android platform’s ViewModel classes, which I am admittedly a fan of).

In any case, the specifics of these patterns are less important than their generalities. All of these patterns are just different flavours of SOC which emphasize a fundamental separation of three kinds of code which I refer to as: *Data*, *User Interface*, *Logic*.

So, how exactly does separating *Data*, *User Interface*, and *Logic* help you to test your applications? The answer is that by pulling logic out of classes which must deal with platform/framework dependencies into classes which possess little or no platform/framework dependencies, testing becomes easy and *framework minimal*. To be clear, I am generally talking about classes which must render the user interface, store data in a SQL table, or connect to a remote server. To demonstrate how this works, let us look at a simplified three layer architecture of a hypothetical Android application.

The first class will manage our user interface. To keep things simple, I have used an *Activity* for this purpose, but I typically opt for *Fragments* instead as user interface classes. In either case, both classes present similar tight coupling to the *Android* platform:

<div class="break-out">

 <pre><code class="language-java">public class CalculatorUserInterface extends Activity implements CalculatorContract.IUserInterface {

    private TextView display;
    private CalculatorContract.IControlLogic controlLogic;
    private final String INVALID_MESSAGE = "Invalid Expression.";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        controlLogic = new DependencyProvider().provideControlLogic(this);

        display = findViewById(R.id.textViewDisplay);
        Button evaluate = findViewById(R.id.buttonEvaluate);
        evaluate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                controlLogic.handleInput('=');
            }
        });
        //..bindings for the rest of the calculator buttons
    }

    @Override
    public void updateDisplay(String displayText) {
        display.setText(displayText);
    }

    @Override
    public String getDisplay() {
        return display.getText().toString();
    }

    @Override
    public void showError() {
        Toast.makeText(this, INVALID_MESSAGE, Toast.LENGTH_LONG).show();
    }
}
</code></pre>
</div>

As you can see, the *Activity* has two jobs: First, since it is the entry point of a given feature of an *Android* application, it acts as a sort of *container* for the other components of the feature. In simple terms, a *container* can be thought of as a sort of root class which the other components are ultimately tethered to via references (or private member fields in this case). It also inflates, binds references, and adds listeners to the XML layout (the user interface).

### Testing Control Logic

Rather than having the *Activity* possess a reference to a concrete class in the back end, we have it talk to an interface of type `CalculatorContract.IControlLogic.` We will discuss why this is an interface in the next section. For now, just understand that whatever is on the other side of that interface is supposed to be something like a *Presenter* or *Controller*. Since this class will be controlling interactions between the *front-end Activity* and the *back-end Calculator*, I have chosen to call it `CalculatorControlLogic`:

<div class="break-out">

 <pre><code class="language-java">public class CalculatorControlLogic implements CalculatorContract.IControlLogic {

    private CalculatorContract.IUserInterface ui;
    private CalculatorContract.IComputationLogic comp;

    public CalculatorControlLogic(CalculatorContract.IUserInterface ui, CalculatorContract.IComputationLogic comp) {
        this.ui = ui;
        this.comp = comp;
    }

    @Override
    public void handleInput(char inputChar) {
        switch (inputChar){
            case '=':
                evaluateExpression();
                break;
            //...handle other input events
        }
    }
    private void evaluateExpression() {
        Optional<String> result = comp.computeResult(ui.getDisplay());

        if (result.isPresent()) ui.updateDisplay(result.get());
        else ui.showError();
    }
}
</code></pre>
</div>

There are many subtle things about the way in which this class is designed that make it easier to test. Firstly, all of its references are either from the Java standard library, or interfaces which are defined within the application. This means that testing this class without any frameworks is an absolute breeze, and it could be done locally on a *JVM*. Another small but useful tip is that all of the different interactions of this class can be called via a single generic `handleInput(...)` function. This provides a **single entry point** to test every behaviour of this class.

Also note that in the `evaluateExpression()` function, I am returning a class of type `Optional<String>` from the back end. Normally I would use what functional programmers call an *Either Monad*, or as I prefer to call it, a *Result Wrapper*. Whatever stupid name you use, it is an object which is capable of representing multiple different states through a single function call. `Optional` is a simpler construct which can represent either a *null*, or some value of the supplied generic type. In any case, since the back end might be given an invalid expression, we want to give the `ControlLogic `class some means of determining the result of the backend operation; accounting for both success and failure. In this case, *null* will represent a failure.

Below is an example test class which has been written using *JUnit*, and a class which in testing jargon is called a *Fake*:

<div class="break-out">

 <pre><code class="language-java">public class CalculatorControlLogicTest {

    @Test
    public void validExpressionTest() {

        CalculatorContract.IComputationLogic comp = new FakeComputationLogic();
        CalculatorContract.IUserInterface ui = new FakeUserInterface();
        CalculatorControlLogic controller = new CalculatorControlLogic(ui, comp);

        controller.handleInput('=');

        assertTrue(((FakeUserInterface) ui).displayUpdateCalled);
        assertTrue(((FakeUserInterface) ui).displayValueFinal.equals("10.0"));
        assertTrue(((FakeComputationLogic) comp).computeResultCalled);

    }

    @Test
    public void invalidExpressionTest() {

        CalculatorContract.IComputationLogic comp = new FakeComputationLogic();
        ((FakeComputationLogic) comp).returnEmpty = true;
        CalculatorContract.IUserInterface ui = new FakeUserInterface();
        ((FakeUserInterface) ui).displayValueInitial = "+7+7";
        CalculatorControlLogic controller = new CalculatorControlLogic(ui, comp);

        controller.handleInput('=');

        assertTrue(((FakeUserInterface) ui).showErrorCalled);
        assertTrue(((FakeComputationLogic) comp).computeResultCalled);

    }

    private class FakeUserInterface implements CalculatorContract.IUserInterface{
        boolean displayUpdateCalled = false;
        boolean showErrorCalled = false;
        String displayValueInitial = "5+5";
        String displayValueFinal = "";

        @Override
        public void updateDisplay(String displayText) {
            displayUpdateCalled = true;
            displayValueFinal = displayText;
        }

        @Override
        public String getDisplay() {
            return displayValueInitial;
        }

        @Override
        public void showError() {
            showErrorCalled = true;
        }
    }

    private class FakeComputationLogic implements CalculatorContract.IComputationLogic{
        boolean computeResultCalled = false;
        boolean returnEmpty = false;

        @Override
        public Optional<String> computeResult(String expression) {
            computeResultCalled = true;
            if (returnEmpty) return Optional.empty();
            else return Optional.of("10.0");
        }
    }
}
</code></pre>
</div>

As you can see, not only can this test suite be executed very rapidly, but it did not take very much time at all to write. In any case, we will now look at some more subtle things which made writing this test class very easy.

### The Power Of Abstraction And Dependency Inversion

There are two other important concepts which have been applied to `CalculatorControlLogic` which have made it trivially easy to test. Firstly, if you have ever wondered what the benefits of using *Interfaces* and *Abstract Classes* (collectively referred to as *abstractions*) in Java are, the code above is a direct demonstration. Since the class to be tested references *abstractions* instead of *concrete* classes, we were able to create *Fake* test doubles for the *user interface* and *back end* from within our test class. As long as these test doubles implement the appropriate interfaces, `CalculatorControlLogic `could not care less that they are not the real thing.

Secondly, `CalculatorControlLogic `has been given its dependencies via the constructor (yes, that is a form of *Dependency Injection*), instead of creating its own dependencies. Therefore, it does not need to be re-written when used in a production or testing environment, which is a bonus for efficiency.

*Dependency Injection* is a form of *Inversion Of Control*, which is a tricky concept to define in plain language. Whether you use *Dependency Injection* or a *Service Locator Pattern*, they both achieve what Martin Fowler (my favourite teacher on such topics) describes as “the principle of separating configuration from use.” This results in classes which are easier to test, and easier to build in isolation from one another.

### Testing Computation Logic

Finally, we come to the `ComputationLogic` class, which is supposed to approximate an *IO device* such as an adapter to a remote server, or a local database. Since we need neither of those for a simple calculator, it will just be responsible for encapsulating the logic required to validate and evaluate the expressions we give it:

<div class="break-out">

 <pre><code class="language-java">public class CalculatorComputationLogic implements CalculatorContract.IComputationLogic {

    private final char ADD = '+';
    private final char SUBTRACT = '-';
    private final char MULTIPLY = '*';
    private final char DIVIDE = '/';

    @Override
    public Optional<String> computeResult(String expression) {
        if (hasOperator(expression)) return attemptEvaluation(expression);
        else return Optional.empty();

    }

    private Optional<String> attemptEvaluation(String expression) {
        String delimiter = getOperator(expression);
        Binomial b = buildBinomial(expression, delimiter);
        return evaluateBinomial(b);
    }

    private Optional<String> evaluateBinomial(Binomial b) {
        String result;
        switch (b.getOperatorChar()) {
            case ADD:
                result = Double.toString(b.firstTerm + b.secondTerm);
                break;
            case SUBTRACT:
                result = Double.toString(b.firstTerm - b.secondTerm);
                break;
            case MULTIPLY:
                result = Double.toString(b.firstTerm * b.secondTerm);
                break;
            case DIVIDE:
                result = Double.toString(b.firstTerm / b.secondTerm);
                break;
            default:
                return Optional.empty();
        }
        return Optional.of(result);
    }

    private Binomial buildBinomial(String expression, String delimiter) {
        String[] operands = expression.split(delimiter);
        return new Binomial(
                delimiter,
                Double.parseDouble(operands[0]),
                Double.parseDouble(operands[1])
        );
    }

    private String getOperator(String expression) {
        for (char c : expression.toCharArray()) {
            if (c == ADD || c == SUBTRACT || c == MULTIPLY || c == DIVIDE)
                return "\\" + c;
        }

        //default
        return "+";
    }

    private boolean hasOperator(String expression) {
        for (char c : expression.toCharArray()) {
            if (c == ADD || c == SUBTRACT || c == MULTIPLY || c == DIVIDE) return true;
        }
        return false;
    }

    private class Binomial {
        String operator;
        double firstTerm;
        double secondTerm;

        Binomial(String operator, double firstTerm, double secondTerm) {
            this.operator = operator;
            this.firstTerm = firstTerm;
            this.secondTerm = secondTerm;
        }

        char getOperatorChar(){
            return operator.charAt(operator.length() - 1);
        }
    }

    }
</code></pre>
</div>

There is not too much to say about this class since typically there would be some tight coupling to a particular back-end library which would present similar problems as a class tightly coupled to Android. In a moment we will discuss what to do about such classes, but this one is so easy to test that we may as well have a try:

<div class="break-out">

 <pre><code class="language-java">public class CalculatorComputationLogicTest {

    private CalculatorComputationLogic comp = new CalculatorComputationLogic();

    @Test
    public void additionTest() {
        String EXPRESSION = "5+5";
        String ANSWER = "10.0";

        Optional<String> result = comp.computeResult(EXPRESSION);

        assertTrue(result.isPresent());
        assertEquals(result.get(), ANSWER);
    }

    @Test
    public void subtractTest() {
        String EXPRESSION = "5-5";
        String ANSWER = "0.0";

        Optional<String> result = comp.computeResult(EXPRESSION);

        assertTrue(result.isPresent());
        assertEquals(result.get(), ANSWER);
    }

    @Test
    public void multiplyTest() {
        String EXPRESSION = "5*5";
        String ANSWER = "25.0";

        Optional<String> result = comp.computeResult(EXPRESSION);

        assertTrue(result.isPresent());
        assertEquals(result.get(), ANSWER);
    }

    @Test
    public void divideTest() {
        String EXPRESSION = "5/5";
        String ANSWER = "1.0";

        Optional<String> result = comp.computeResult(EXPRESSION);

        assertTrue(result.isPresent());
        assertEquals(result.get(), ANSWER);
    }

    @Test
    public void invalidTest() {
        String EXPRESSION = "Potato";

        Optional<String> result = comp.computeResult(EXPRESSION);

        assertTrue(!result.isPresent());
    }
}
</code></pre>
</div>

The easiest classes to test, are those which are simply given some value or object, and are expected to return a result without the necessity of calling some external dependencies. In any case, there comes a point where no matter how much software architecture wizardry you apply, you will still need to worry about classes which cannot be decoupled from platforms and frameworks. Fortunately, there is still a way we can employ software architecture to: At worst make these classes easier to test, and at best, so trivially simple that testing can be done *at a glance*.

### Humble Objects And Passive Views

The above two names refer to a pattern in which an object that must talk to low-level dependencies, is simplified so much that it *arguably* does not need to be tested. I was first introduced to this pattern via Martin Fowler’s blog on variations of Model-View-Presenter. Later on, through Robert C. Martin’s works, I was introduced to the idea of treating certain classes as *Humble Objects*, which implies that this pattern does not need to be limited to user interface classes (although I do not mean to say that Fowler ever implied such a limitation).

Whatever you choose to call this pattern, it is delightfully simple to understand, and in some sense I believe it is actually just the result of rigorously applying SOC to your classes. While this pattern applies also to back end classes, we will use our *user interface* class to demonstrate this principle in action. The separation is very simple: Classes which interact with platform and framework dependencies, do not think for themselves (hence the monikers *Humble* and *Passive*). When an event occurs, the only thing they do is forward the details of this event to whatever *logic* class happens to be listening:

<pre><code class="language-java">//from CalculatorActivity's onCreate() function:
evaluate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                controlLogic.handleInput('=');
            }
        });
</code></pre>

The logic class, which should be trivially easy to test, is then responsible for controlling the *user interface* in a very fine-grained manner. Rather than calling a single generic `updateUserInterface(...)` function on the `user interface` class and leaving it to do the work of a bulk update, the `user interface` (or other such class) will possess small and specific functions which should be easy to name and implement:

<div class="break-out">

 <pre><code class="language-java">//Interface functions of CalculatorActivity:
        @Override
    public void updateDisplay(String displayText) {
        display.setText(displayText);
    }

    @Override
    public String getDisplay() {
        return display.getText().toString();
    }

    @Override
    public void showError() {
        Toast.makeText(this, INVALID_MESSAGE, Toast.LENGTH_LONG).show();
    }
//…
</code></pre>
</div>

In principal, these two examples ought to give you enough to understand how to go about implementing this pattern. The object which possesses the logic is loosely coupled, and the object which is tightly coupled to pesky dependencies becomes almost devoid of logic.

Now, at the start of this subsection, I made the statement that these classes become *arguably* unnecessary to test, and it is important we look at both sides of this argument. In an absolute sense, it is impossible to achieve 100% test coverage by employing this pattern, unless you still write tests for such *humble*/*passive* classes. It is also worth noting that my decision to use a Calculator as an example App, means that I cannot escape having a gigantic mass of `findViewById(...)` calls present in the Activity. Giant masses of repetitive code are a common cause of typing errors, and in the absence of some Android UI testing frameworks, my only recourse for testing would be via deploying the feature to a device and manually testing each interaction. Ouch.

It is at this point that I will *humbly* say that I do not know if 100% code coverage is absolutely necessary. I do not know many developers who strive for absolute test coverage in production code, and I have never done so myself. One day I might, but I will reserve my opinions on this matter until I have the reference experiences to back them up. In any case, I would argue that applying this pattern will still ultimately make it simpler and easier to test tightly coupled classes; if for no reason other than they become simpler to write.

Another objection to this approach, was raised by a fellow programmer when I described this approach in another context. The objection was that the `logic` class (whether it be a `Controller`, `Presenter`, or even a `ViewModel` depending on how you use it), becomes a `God` class.

While I do not agree with that sentiment, I do agree that the end result of applying this pattern is that your *Logic* classes become larger than if you left more decisions up to your *user interface* class.

This has never been an issue for me as I treat each feature of my applications as self-contained components, as opposed to having one giant *controller* for managing multiple *user interface* screens. In any case, I think this argument holds reasonably true if you fail to apply SOC to your front end or back end components. Therefore, my advice is to apply SOC to your front end and back end components quite rigorously.

## Further Considerations

After all of this discussion on applying the principles of software architecture to reduce the necessity of using a wide-array of testing frameworks, improve the testability of classes in general, and a pattern which allows classes to be tested indirectly (at least to some degree), I am not actually here to tell you to stop using your preferred frameworks.

For those curious, I often use a library to generate *mock classes* for my *Unit* tests (for Java I prefer *Mockito*, but these days I mostly write Kotlin and prefer *Mockk* in that language), and *JUnit* is a framework which I use quite invariably. Since all of these options are coupled to languages as opposed to the Android platform, I can use them quite interchangeably across mobile and web application development. From time to time (if project requirements demand it), I will even use tools like *Robolectric*, *MockWebServer*, and in my five years of studying Android, I did begrudgingly use *Espresso* once.

My hope is that in reading this article, anyone who has experienced a similar degree of aversion to testing due to *paralysis by jargon analysis*, will come to see that getting started with testing really can be simple and *framework minimal*.

### <span class="rh">Further Reading</span> on SmashingMag:

<ul>
  <li><a title="Read 'Sliding In And Out Of Vue.js'" href="https://www.smashingmagazine.com/2019/02/vue-framework-third-party-javascript/" rel="bookmark">Sliding In And Out Of Vue.js</a></li>
  <li><a title="Read 'Designing And Building A Progressive Web Application Without A Framework'" href="https://www.smashingmagazine.com/2019/07/progressive-web-application-pwa-framework-part-1/" rel="bookmark">Designing And Building A Progressive Web Application Without A Framework</a></li>
  <li><a title="Read 'CSS Frameworks Or CSS Grid: What Should I Use For My Project?'" href="https://www.smashingmagazine.com/2018/11/css-frameworks-css-grid/" rel="bookmark">CSS Frameworks Or CSS Grid: What Should I Use For My Project?</a></li>
<li><a title="Read 'Using Google’s Flutter For Truly Cross-Platform Mobile Development'" href="https://www.smashingmagazine.com/2018/06/google-flutter-mobile-development/" rel="bookmark">Using Google’s Flutter For Truly Cross-Platform Mobile Development</a></li>
</ul>

{{< signature "dm, il" >}}
