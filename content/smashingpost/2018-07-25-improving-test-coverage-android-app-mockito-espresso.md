---
title: 'How To Improve Test Coverage For Your Android App Using Mockito And Espresso'
slug: improving-test-coverage-android-app-mockito-espresso
author: vivek-maskara
image: >-
  //archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a17ec68e-9d06-4ca5-abb5-4cd2f85f8f47/mockito-espresso-ide-green-play-button.png
date: 2018-07-25T14:00:04+02:00
summary: >-
  Frameworks such as Espresso and Mockito provide easy-to-use APIs that make writing tests for various scenarios easier. Let's cover the fundamentals of testing and frameworks which developers can use to write unit tests.
description: >-
  Frameworks such as Espresso and Mockito provide easy-to-use APIs that make writing tests for various scenarios easier. Let's cover the fundamentals of testing and frameworks which developers can use to write unit tests.
categories:
  - Android
  - Testing
  - Frameworks
  - Apps
---
In app development, a variety of use cases and interactions come up as one iterates the code. The app might need to fetch data from a server, interact with the device's sensors, access local storage or render complex user interfaces.

The important thing to consider while writing tests is the units of responsibility that emerge as you design the new feature. The unit test should cover all possible interactions with the unit, including standard interactions and exceptional scenarios.

In this article, we will cover the fundamentals of testing and frameworks such as Mockito and Espresso, which developers can use to write unit tests. I will also briefly discuss how to write testable code. I’ll also explain how to get started with local and instrumented tests in Android. 

<p><strong>Recommended reading</strong>: <em><a href="https://www.smashingmagazine.com/2017/04/automated-testing-system-android-phones/">How To Set Up An Automated Testing System Using Android Phones (A Case Study)</a></em></p>

## Fundamentals Of Testing

A typical unit test contains three phases.

1. First, the unit test initializes a small piece of an application it wants to test.
2. Then, it applies some stimulus to the system under test, usually by calling a method on it.
3. Finally, it observes the resulting behavior.

If the observed behavior is consistent with the expectations, the unit test passes; otherwise, it fails, indicating that there is a problem somewhere in the system under test. These three unit test phases are also known as **a****rrange**, **a****ct** and **a****ssert**, or simply AAA. The app should ideally include three categories of tests: small, medium and large.

- **Small tests** comprise unit tests that mock every major component and run quickly in isolation.
- **Medium tests** are integration tests that integrate several components and run on emulators or real devices.
- **Large tests** are integration and UI tests that run by completing a UI workflow and ensure that the key end-user tasks work as expected.

**Note:** *An instrumentation test is a type of integration test. These are tests that run on an Android device or emulator. These tests have access to instrumentation information, such as the context of the app under test. Use this approach to run unit tests that have Android dependencies that mock objects cannot easily satisfy.*

{{% feature-panel %}}

Writing small tests allows you to address failures quickly, but it’s difficult to gain confidence that a passing test will allow your app to work. It’s important to have tests from all categories in the app, although the proportion of each category can vary from app to app. A good unit test should be **easy to write**, **readable**, **reliable** and **fast**.  

Here’s a brief introduction to Mockito and Espresso, which make testing Android apps easier. 

### Mockito

There are various mocking frameworks, but the most popular of them all is [Mockito](https://site.mockito.org/):

<blockquote>Mockito is a mocking framework that tastes really good. It lets you write beautiful tests with a clean & simple API. Mockito doesn’t give you hangover because the tests are very readable and they produce clean verification errors.</blockquote>

Its fluent API separates pre-test preparation from post-test validation. Should the test fail, Mockito makes it clear to see where our expectations differ from reality! The library has everything you need to write complete tests.

### Espresso

Espresso helps you write concise, beautiful and reliable Android UI tests.

The code snippet below shows an example of an Espresso test. We will take up the same example later in this tutorial when we talk in detail about instrumentation tests. 

<div class="break-out">

<pre><code class="language-javascript">@Test
public void setUserName() {
    onView(withId(R.id.name_field)).perform(typeText("Vivek Maskara"));
    onView(withId(R.id.set_user_name)).perform(click());
    onView(withText("Hello Vivek Maskara!")).check(matches(isDisplayed()));
}
</code></pre></div>

Espresso tests state expectations, interactions and assertions clearly, without the distraction of boilerplate content, custom infrastructure or messy implementation details getting in the way. Whenever your test invokes `onView()`, Espresso waits to perform the corresponding UI action or assertion until the synchronization conditions are met, meaning:

- the message queue is empty,
- no instances of `AsyncTask` are currently executing a task,
- the idling resources are idle.

These checks ensure that the test results are reliable.

## Writing Testable Code

Unit testing Android apps is difficult and sometimes impossible. A good design, and only a good design, can make unit testing easier. Here are some of the concepts that are important for writing testable code. 

### Avoid Mixing Object Graph Construction With Application Logic

In a test, you want to instantiate the class under test and apply some stimulus to the class and assert that the expected behavior was observed. Make sure that the class under test doesn't instantiate other objects and that those objects do not instantiate more objects and so on. In order to have a testable code base, your application should have two kinds of classes:

- The factories, which are full of the "new" operators and which are responsible for building the object graph of your application;
- The application logic classes, which are devoid of the "new" operator and which are responsible for doing the work.

### Constructors Should Not Do Any Work

The most common operation you will do in tests is the instantiation of object graphs. So, make it easy on yourself, and make the constructors do no work other than assigning all of the dependencies into the fields. Doing work in the constructor not only will affect the direct tests of the class, but will also affect related tests that try to instantiate your class indirectly.

### Avoid Static Methods Wherever Possible

The key to testing is the presence of places where you can divert the normal execution flow. Seams are needed so that you can isolate the unit of test. If you build an application with nothing but static methods, you will have a procedural application. How much a static method will hurt from a testing point of view depends on where it is in your application call graph. A leaf method such as `Math.abs()` is not a problem because the execution call graph ends there. But if you pick a method in a core of your application logic, then everything behind the method will become hard to test, because there is no way to insert test doubles

### Avoid Mixing Of Concerns

A class should be responsible for dealing with just one entity. Inside a class, a method should be responsible for doing just one thing. For example, `BusinessService` should be responsible just for talking to a `Business` and not `BusinessReceipts`. Moreover, a method in `BusinessService` could be `getBusinessProfile`, but a method such as `createAndGetBusinessProfile` would not be ideal for testing. [S](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)?oldformat=true)[OLID](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)?oldformat=true) [design principles](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)?oldformat=true) must be followed for good design: 

- **S**: single-responsibility principle;
- **O**: open-closed principle;
- **L**: Liskov substitution principle;
- **I**: interface segregation principle;
- **D**: dependency inversion principle.

In the next few sections, we will be using examples from a really simple application that I built for this tutorial. The app has an `EditText` that takes a user name as input and displays the name in a `TextView` upon the click of a button. Feel free to take the complete [source code](https://github.com/maskaravivek/AndroidTestingExamples) for the project from GitHub. Here’s a screenshot of the app:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff53d66-273d-452a-88fe-7e434ba87ff9/mockito-espresso-testing-example.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff53d66-273d-452a-88fe-7e434ba87ff9/mockito-espresso-testing-example.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2ff53d66-273d-452a-88fe-7e434ba87ff9/mockito-espresso-testing-example.png'>Large preview</a>" alt="Testing example" >}}

## Writing Local Unit Tests

Unit tests can be run locally on your development machine without a device or an emulator. This testing approach is efficient because it avoids the overhead of having to load the target app and unit test code onto a physical device or emulator every time your test is run. In addition to Mockito, you will also need to configure the testing dependencies for your project to use the standard APIs provided by the JUnit 4 framework.

### Setting Up The Development Environment

Start by adding a dependency on JUnit4 in your project. The dependency is of the type `testImplementation`, which means that the dependencies are only required to compile the test source of the project.

<pre><code class="language-javascript">testImplementation 'junit:junit:4.12'
</code></pre>

We will also need the Mockito library to make interaction with Android dependencies easier.

<div class="break-out">

<pre><code class="language-javascript">testImplementation "org.mockito:mockito-core:$MOCKITO_VERSION"</code></pre></div>

Make sure to sync the project after adding the dependency. Android Studio should have created the folder structure for unit tests by default. If not, make sure the following directory structure exists:

<div class="break-out">

<pre><code class="language-html">&lt;Project Dir&gt;/app/src/test/java/com/maskaravivek/testingExamples
</code></pre></div>

{{% ad-panel-leaderboard %}}

### Creating Your First Unit Test

Suppose you want to test the `displayUserName` function in the `UserService`. For the sake of simplicity, the function simply formats the input and returns it back. In a real-world application, it could make a network call to fetch the user profile and return the user’s name. 

<div class="break-out">

<pre><code class="language-javascript">@Singleton
class UserService @Inject
constructor(private var context: Context) {

    fun displayUserName(name: String): String {
        val userNameFormat = context.getString(R.string.display_user_name)
        return String.format(Locale.ENGLISH, userNameFormat, name)
    }
}
</code></pre></div>

We will start by creating a `UserServiceTest` class in our test directory. The `UserService` class uses `Context`, which needs to be mocked for the purpose of testing. Mockito provides a `@Mock` notation for mocking objects, which can be used as follows:

<pre><code class="language-javascript">@Mock internal var context: Context? = null
</code></pre>

Similarly, you’ll need to mock all dependencies required to construct the instance of the `UserService` class. Before your test, you’ll need to initialize these mocks and inject them into the `UserService` class. 

- `@InjectMock` creates an instance of the class and injects the mocks that are marked with the annotations `@Mock` into it.
- `MockitoAnnotations.initMocks(this);` initializes those fields annotated with Mockito annotations.

Here's how it can be done:

<div class="break-out">

<pre><code class="language-javascript">class UserServiceTest {

    @Mock internal var context: Context? = null
    @InjectMocks internal var userService: UserService? = null

    @Before
    fun setup() {
        MockitoAnnotations.initMocks(this)
    }
}
</code></pre></div>

Now you are done setting up your test class. Let's add a test to this class that verifies the functionality of the `displayUserName` function. Here's what the test looks like:

<div class="break-out">

<pre><code class="language-javascript">@Test
fun displayUserName() {
    doReturn("Hello %s!").`when`(context)!!.getString(any(Int::class.java))
    val displayUserName = userService!!.displayUserName("Test")
    assertEquals(displayUserName, "Hello Test!")
}
</code></pre></div>

The test uses a `doReturn().when()` statement to provide a response when a `context.getString()` is invoked. For any input integer, it will return the same result, `"Hello %s!"`. We could have been more specific by making it return this response only for a particular string resource ID, but for the sake of simplicity, we are returning the same response to any input.
Finally, here's what the test class looks like:

<div class="break-out">

<pre><code class="language-javascript">class UserServiceTest {
    @Mock internal var context: Context? = null
    @InjectMocks internal var userService: UserService? = null
    @Before
    fun setup() {
        MockitoAnnotations.initMocks(this)
    }

    @Test
    fun displayUserName() {
        doReturn("Hello %s!").`when`(context)!!.getString(any(Int::class.java))
        val displayUserName = userService!!.displayUserName("Test")
        assertEquals(displayUserName, "Hello Test!")
    }
}
</code></pre></div>

### Running Your Unit Tests

In order to run the unit tests, you need to make sure that Gradle is synchronized. In order to run a test, click on the green play icon in the IDE. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/080d9ba0-59a0-4f88-b595-ae198005901c/mockito-espresso-ide-green-icon.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/080d9ba0-59a0-4f88-b595-ae198005901c/mockito-espresso-ide-green-icon.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/080d9ba0-59a0-4f88-b595-ae198005901c/mockito-espresso-ide-green-icon.png'>Large preview</a>" alt="making sure that Gradle is synchronized" >}}

When the unit tests are run, successfully or otherwise, you should see this in the “Run” menu at the bottom of the screen:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024460c9-cbdc-4b04-bddf-9d4bd5f53ed5/mockito-espresso-display-user-name-test.gif"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024460c9-cbdc-4b04-bddf-9d4bd5f53ed5/mockito-espresso-display-user-name-test.gif" width="288" height="512" alt="result after unit tests are run" /></a><figcaption><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/024460c9-cbdc-4b04-bddf-9d4bd5f53ed5/mockito-espresso-display-user-name-test.gif">Large preview</a></figcaption></figure>

You are done with your first unit test!

## Writing Instrumentation Tests

Instrumentation tests are most suited for checking values of UI components when an activity is run. For instance, in the example above, we want to make sure that the `TextView` shows the correct user name after the `Button` is clicked. They run on physical devices and emulators and can take advantage of the Android framework APIs and supporting APIs, such as the Android Testing Support Library. 
We'll use Espresso to take actions on the main thread, such as button clicks and text changes.

### Setting Up The Development Environment

Add a dependency on Espresso:

<div class="break-out">

<pre><code class="language-javascript">androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'
</code></pre></div>

Instrumentation tests are created in an `androidTest` folder.

<div class="break-out">

<pre><code class="language-javascript">&lt;Project Dir&gt;/app/src/androidTest/java/com/maskaravivek/testingExamples
</code></pre></div>

If you want to test a simple activity, create your test class in the same package as your activity.

### Creating Your First Instrumentation Test

Let’s start by creating a simple activity that takes a name as input and, on the click of a button, displays the user name. The code for the activity above is quite simple:

<div class="break-out">

<pre><code class="language-javascript">class MainActivity : AppCompatActivity() {

    var button: Button? = null
    var userNameField: EditText? = null
    var displayUserName: TextView? = null

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        AndroidInjection.inject(this)
        setContentView(R.layout.activity_main)
        initViews()
    }

    private fun initViews() {
        button = this.findViewById(R.id.set_user_name)
        userNameField = this.findViewById(R.id.name_field)
        displayUserName = this.findViewById(R.id.display_user_name)

        this.button!!.setOnClickListener({
            displayUserName!!.text = "Hello ${userNameField!!.text}!"
        })
    }
}
</code></pre></div>

To create a test for the `MainActivity`, we will start by creating a `MainActivityTest` class under the `androidTest` directory. Add the `AndroidJUnit4` annotation to the class to indicate that the tests in this class will use the default Android test runner class.

<pre><code class="language-javascript">@RunWith(AndroidJUnit4::class)
class MainActivityTest {}
</code></pre>

Next, add an `ActivityTestRule` to the class. This rule provides functional testing of a single activity. For the duration of the test, you will be able to manipulate your activity directly using the reference obtained from `getActivity()`.

<pre><code class="language-javascript">@Rule @JvmField var activityActivityTestRule = ActivityTestRule(MainActivity::class.java)
</code></pre>

Now that you are done setting up the test class, let’s add a test that verifies that the user name is displayed by clicking the “Set User Name” button.

<div class="break-out">

<pre><code class="language-javascript">@Test
fun setUserName() {
    onView(withId(R.id.name_field)).perform(typeText("Vivek Maskara"))
    onView(withId(R.id.set_user_name)).perform(click())
    onView(withText("Hello Vivek Maskara!")).check(matches(isDisplayed()))
}
</code></pre></div>

The test above is quite simple to follow. It first simulates some text being typed in the `EditText`, performs the click action on the button, and then checks whether the correct text is displayed in the `TextView`.

The final test class looks like this:

<div class="break-out">

<pre><code class="language-javascript">@RunWith(AndroidJUnit4::class)
class MainActivityTest {

    @Rule @JvmField var activityActivityTestRule = ActivityTestRule(MainActivity::class.java)

    @Test
    fun setUserName() {
        onView(withId(R.id.name_field)).perform(typeText("Vivek Maskara"))
        onView(withId(R.id.set_user_name)).perform(click())
        onView(withText("Hello Vivek Maskara!")).check(matches(isDisplayed()))
    }
}
</code></pre></div>

### Running Your Instrumentation Tests

Just like for unit tests, click on the green play button in the IDE to run the test. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a17ec68e-9d06-4ca5-abb5-4cd2f85f8f47/mockito-espresso-ide-green-play-button.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a17ec68e-9d06-4ca5-abb5-4cd2f85f8f47/mockito-espresso-ide-green-play-button.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a17ec68e-9d06-4ca5-abb5-4cd2f85f8f47/mockito-espresso-ide-green-play-button.png'>Large preview</a>" alt="clicking on the green play button in IDE to run the test" >}}

Upon a click of the play button, the test version of the app will be installed on the emulator or device, and the test will run automatically on it. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png'>Large preview</a>" alt="" >}}

## Intrumentation Testing Using Dagger, Mockito, And Espresso

Espresso is one of the most popular UI testing frameworks, with good documentation and community support. Mockito ensures that objects perform the actions that are expected of them. Mockito also works well with dependency-injection libraries such as Dagger. Mocking the dependencies allows us to test a scenario in isolation.
Until now, our `MainActivity` hasn't used any dependency injection, and, as a result, we were able to write our UI test very easily. To make things a bit more interesting, let’s inject `UserService` in the `MainActivity` and use it to get the text to be displayed.

<div class="break-out">

<pre><code class="language-javascript">class MainActivity : AppCompatActivity() {

    var button: Button? = null
    var userNameField: EditText? = null
    var displayUserName: TextView? = null

    @Inject lateinit var userService: UserService

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        AndroidInjection.inject(this)
        setContentView(R.layout.activity_main)
        initViews()
    }

    private fun initViews() {
        button = this.findViewById(R.id.set_user_name)
        userNameField = this.findViewById(R.id.name_field)
        displayUserName = this.findViewById(R.id.display_user_name)

        this.button!!.setOnClickListener({
            displayUserName!!.text = userService.displayUserName(userNameField!!.text.toString())
        })
    }
}
</code></pre></div>

With Dagger in the picture, we will have to set up a few things before we write instrumentation tests.
Imagine that the `displayUserName` function internally uses some API to fetch the details of the user. There should not be a situation in which a test does not pass due to a server fault. To avoid such a situation, we can use the dependency-injection framework Dagger and, for networking, Retrofit.

{{% ad-panel-leaderboard %}}

### Setting Up Dagger In The Application

We will quickly set up the basic modules and components required for Dagger. If you are not 
familiar with Dagger, check out [Google’s documentation](https://google.github.io/dagger/) on it.  We will start adding dependencies for using Dagger in the `build.gradle` file. 

<div class="break-out">

<pre><code class="language-javascript">implementation "com.google.dagger:dagger-android:$DAGGER_VERSION"
implementation "com.google.dagger:dagger-android-support:$DAGGER_VERSION"
implementation "com.google.dagger:dagger:$DAGGER_VERSION"
kapt "com.google.dagger:dagger-compiler:$DAGGER_VERSION"
kapt "com.google.dagger:dagger-android-processor:$DAGGER_VERSION"
</code></pre></div>

Create a component in the `Application` class, and add the necessary modules that will be used in our project. We need to inject dependencies in the `MainActivity` of our app. We will add a `@Module` for injecting in the activity. 

<div class="break-out">

<pre><code class="language-javascript">@Module
abstract class ActivityBuilder {
    @ContributesAndroidInjector
    internal abstract fun bindMainActivity(): MainActivity
}
</code></pre></div>

The `AppModule` class will provide the various dependencies required by the application. For our example, it will just provide an instance of `Context` and `UserService`. 

<div class="break-out">

<pre><code class="language-javascript">@Module
open class AppModule(val application: Application) {
    @Provides
    @Singleton
    internal open fun provideContext(): Context {
        return application
    }

    @Provides
    @Singleton
    internal open fun provideUserService(context: Context): UserService {
        return UserService(context)
    }
}
</code></pre></div>    

The `AppComponent` class lets you build the object graph for the application. 

<div class="break-out">

<pre><code class="language-javascript">@Singleton
@Component(modules = [(AndroidSupportInjectionModule::class), (AppModule::class), (ActivityBuilder::class)])
interface AppComponent {

    @Component.Builder
    interface Builder {
        fun appModule(appModule: AppModule): Builder
        fun build(): AppComponent
    }

    fun inject(application: ExamplesApplication)
}
</code></pre></div>

Create a method that returns the already built component, and then inject this component into `onCreate()`.

<div class="break-out">

<pre><code class="language-javascript">open class ExamplesApplication : Application(), HasActivityInjector {
    @Inject lateinit var dispatchingActivityInjector: DispatchingAndroidInjector&lt;Activity&gt;

    override fun onCreate() {
        super.onCreate()
        initAppComponent().inject(this)
    }

    open fun initAppComponent(): AppComponent {
        return DaggerAppComponent
            .builder()
            .appModule(AppModule(this))
            .build()
    }

    override fun activityInjector(): DispatchingAndroidInjector&lt;Activity&gt;? {
        return dispatchingActivityInjector
    }
}
</code></pre></div>

### Setting Up Dagger In The Test Application

In order to mock responses from the server, we need to create a new `Application` class that extends the class above.

<div class="break-out">

<pre><code class="language-javascript">class TestExamplesApplication : ExamplesApplication() {

    override fun initAppComponent(): AppComponent {
        return DaggerAppComponent.builder()
            .appModule(MockApplicationModule(this))
            .build()
    }

    @Module
    private inner class MockApplicationModule internal constructor(application: Application) : AppModule(application) {
        override fun provideUserService(context: Context): UserService {
            val mock = Mockito.mock(UserService::class.java)
            `when`(mock!!.displayUserName("Test")).thenReturn("Hello Test!")
            return mock
        }
    }
}
</code></pre></div>

As you can see in the example above, we’ve used Mockito to mock `UserService` and assume the results. We still need a new runner that will point to the new application class with the overwritten data.

<div class="break-out">

<pre><code class="language-javascript">class MockTestRunner : AndroidJUnitRunner() {

    override fun onCreate(arguments: Bundle) {
        StrictMode.setThreadPolicy(StrictMode.ThreadPolicy.Builder().permitAll().build())
        super.onCreate(arguments)
    }

    @Throws(InstantiationException::class, IllegalAccessException::class, ClassNotFoundException::class)
    override fun newApplication(cl: ClassLoader, className: String, context: Context): Application {
        return super.newApplication(cl, TestExamplesApplication::class.java.name, context)
    }
}
</code></pre></div>

Next, you need to update the `build.gradle` file to use the `MockTestRunner`.

<pre><code class="language-javascript">android {
    ...

    defaultConfig {
        ...
        testInstrumentationRunner ".MockTestRunner"
    }
}
</code></pre>

### Running The Test

All tests with the new `TestExamplesApplication` and `MockTestRunner` should be added at `androidTest` package. This implementation makes the tests fully independent from the server and gives us the ability to manipulate responses. 
With the setup above in place, our test class won't change at all. When the test is run, the app will use `TestExamplesApplication` instead of `ExamplesApplication`, and, thus, a mocked instance of `UserService` will be used.

<div class="break-out">

<pre><code class="language-javascript">@RunWith(AndroidJUnit4::class)
class MainActivityTest {
    @Rule @JvmField var activityActivityTestRule = ActivityTestRule(MainActivity::class.java)

    @Test
    fun setUserName() {
        onView(withId(R.id.name_field)).perform(typeText("Test"))
        onView(withId(R.id.set_user_name)).perform(click())
        onView(withText("Hello Test!")).check(matches(isDisplayed()))
    }
}
</code></pre></div>

The test will run successfully when you click on the green play button in the IDE. 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png" sizes="100vw" caption="<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/875a391d-47f2-49b3-88c7-824356d4bae2/mockito-espresso-successful-test-run-ide.png'>Large preview</a>" alt="successfully setting up Dagger and run tests using Espresso and Mockito" >}}

That’s it! You have successfully set up Dagger and run tests using Espresso and Mockito. 

## Conclusion

We’ve highlighted that the most important aspect of improving code coverage is to write testable code. Frameworks such as Espresso and Mockito provide easy-to-use APIs that make writing tests for various scenarios easier. Tests should be run in isolation, and mocking the dependencies gives us an opportunity to ensure that objects perform the actions that are expected of them. 

A variety of Android testing tools are available, and, as the ecosystem matures, the process of setting up a testable environment and writing tests will become easier.

Writing unit tests requires some discipline, concentration and extra effort. By creating and running unit tests against your code, you can easily verify that the logic of individual units is correct. Running unit tests after every build helps you to quickly catch and fix software regressions introduced by code changes to your app. Google’s testing blog discusses the [advantages of unit testing.](https://testing.googleblog.com/2009/07/by-shyam-seshadri-nowadays-when-i-talk.html) 
The complete [source code](https://github.com/maskaravivek/AndroidTestingExamples) for the examples used in this article is available on GitHub. Feel free to take a look at it. 

{{< signature "da, lf, ra, al, il" >}}
