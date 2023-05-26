---
title: An Introduction To Programming Type Systems
slug: introduction-to-programming-type-systems
image: null
date: 2013-04-18T08:30:57.000Z
author: zack-grossbart
description: >-
  Static typing is great because it keeps you out of trouble. Dynamic typing is
  great because it gets out of your way and lets you get your work done faster.
  The debate between strongly and dynamically typed languages rages on.
categories:
  - Coding
  - JavaScript
  - Optimization
  - Essentials
---
Static typing is great because it keeps you out of trouble. Dynamic typing is great because it gets out of your way and lets you get your work done faster. The debate between strongly and dynamically typed languages rages on, but <strong>understanding the issue starts with weak typing</strong> and languages such as <a href="https://en.wikipedia.org/wiki/C_(programming_language)">C</a>.

C treats everything like a number. A character like <code>a</code> or <code>7</code> or <code>%</code> is the number of the ASCII symbol representing it; “true” and “false” are just 1 and 0.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [Don’t Be Scared Of Functional Programming](https://www.smashingmagazine.com/2014/07/dont-be-scared-of-functional-programming/)
*   [An Introduction To Full-Stack JavaScript](https://www.smashingmagazine.com/2013/11/introduction-to-full-stack-javascript/)
*   [Declarative Programming And The Web](https://www.smashingmagazine.com/2014/07/declarative-programming/)

C defines variables with types such as <code>int</code> for integer and <code>char</code> for character, but that just defines how much memory to use. To access the variable and print it out, <strong>I need to know the type.</strong>

{{% feature-panel %}}

<pre><code class="language-javascript">
int a = 1;
printf("The number is %in", a);

char z = 'z';
printf("The character is %cn", z);
</code></pre>

When I run this program, it shows this:

<pre>The number is 1
The character is z
</pre>

The <code>printf</code> function needs a hint from us to know how to format the variable. If I give the wrong hint…

<pre><code class="language-javascript">
char z = 'z';
printf("The character is %in", z);
</code></pre>

… then I get this:

<pre>The character is 122
</pre>

C doesn’t know whether <code>z</code> is a character or an integer; it has a weak type.

<strong>Weak typing is fast because there’s no overhead of remembering the different types</strong>, but it leads to some nasty bugs. There’s no way to format the <code>z</code> if you don’t know its type ahead of time. Imagine accessing a variable and getting the number <code>1229799107</code>. The number could be the result of a mathematical calculation (1,229,799,107), the cost of a government program ($1.2 billion) or a date (Saturday, 20 December 2008). When all you have is the number, there’s no way to know that it’s really the code for the letters in my name: <code>zack</code>.

So far, we’ve just covered weak typing. “Weak versus strong” and “static versus dynamic” are often spoken of synonymously, but they each describe a different phase of the same problem. They’re also politicized, with the words carrying an implied value judgment. “Weak versus strong” makes one of them sound a lot better than the other, while “static vs. dynamic” makes one sound stodgy and the other exciting.

<img class="aligncenter size-full wp-image-121120" title="Jelly bean" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/de228c8f-2d24-4c97-a577-38eba35c63e8/jellybean.jpg" alt="" width="500" height="208" /><br>
<em>(Image: <a href="https://www.flickr.com/photos/c_r_i_s/77763830/">Cris</a>)</em>

These two terms are used interchangeably, but they describe the difference between the way a language defines types and how it figures them out when the program runs. For example:
<table class="table-overview"><br>
<tbody>
<tr>
<td style="width: 175px">Weak with no typing</td>
<td><a href="https://en.wikipedia.org/wiki/Assembly_language">Assembly languages</a> don’t provide any way of specifying or checking types at all. Everything is just a number.</td>
</tr>
<tr>
<td>Weak static typing</td>
<td>C lets you define object types as structures, but it doesn’t do much to enforce or remember them. C automatically convert between many types. <a href="https://en.wikipedia.org/wiki/C%2B%2B">C++</a> and <a href="https://en.wikipedia.org/wiki/Objective-C">Objective-C</a> go further with the definitions but still don’t enforce the resulting types.</td>
</tr>
<tr>
<td>Strong static typing</td>
<td><a href="https://en.wikipedia.org/wiki/Java_(programming_language)">Java</a> forces you to define all types and checks them with a virtual machine.</td>
</tr>
<tr>
<td>Strong dynamic typing</td>
<td><a href="https://en.wikipedia.org/wiki/Python_(programming_language)">Python</a>, <a href="https://en.wikipedia.org/wiki/Javascript">JavaScript</a> and <a href="https://en.wikipedia.org/wiki/Ruby_(programming_language)">Ruby</a> dynamically infer the types of objects, instead of forcing you to define them, and then enforce those types when the program runs in the interpreter. All dynamically typed languages need a strong typing system at runtime or else they won’t be able to resolve the object types.</td>
</tr>
<tr>
<td>Weak dynamic typing</td>
<td>Dynamically inferred types don’t work in a weakly typed language because there aren’t any types to infer.</td>
</tr>
</tbody>
</table>
<strong>No programming language fits any of these definitions 100%.</strong> Java is considered one of the most static languages, but it implemented a comprehensive <a href="https://en.wikipedia.org/wiki/Reflection_(computer_programming)">reflection</a> API that lets you change classes at runtime, thus resembling more dynamic languages. This feature allows the Java Virtual Machine to support very dynamic languages such as <a href="https://en.wikipedia.org/wiki/Groovy_(programming_language)">Groovy</a>.

<a href="https://en.wikipedia.org/wiki/Functional_programming">Functional programming languages</a> such as <a href="https://en.wikipedia.org/wiki/Lisp_(programming_language)">Lisp</a>, <a href="https://en.wikipedia.org/wiki/Erlang_(programming_language)">Erlang</a> and <a href="https://en.wikipedia.org/wiki/Haskell_(programming_language)">Haskell</a> blur the lines even more.

Usually when people argue about the merits of strong versus weak programming languages, they really mean the varying degrees of weak, strong, static and dynamic philosophies in every language.</p>

## Weak Static Languages: C, C++ And Objective-C

These next programming languages use a subset of C’s functionality and strict guidelines to improve the loose nature of the language. <a href="https://en.wikipedia.org/wiki/C%2B%2B">C++</a> and <a href="https://en.wikipedia.org/wiki/Objective-C">Objective-C</a> compile into the same bytes as C, but they use the compiler to restrict the code you can write.

In C++ and Objective-C, <strong>our number (1229799107) has a meaning</strong>. I can define it as a string of characters and make sure that no one uses it as a currency or a date. The compiler enforces its proper use.

Static typing supports objects with sets of functionality that always work in a well-defined way. Now I can create a <code>Person</code> object and make sure the <code>getName</code> function always returns the string of someone’s name.

<pre><code class="language-javascript">
class Person {
    public:
        string getName() {
            return "zack";
        }
};
</code></pre>

Now I can call my object like this:

<pre><code class="language-javascript">
Person p;
printf("The name is %sn", p.getName().c_str());
</code></pre>

Static typing goes a long way to avoid the bugs of weakly typed languages by <strong>adding more constraints in the compiler</strong>, but it can’t check anything when the program is running because a C++ or Objective-C program is just like C code when it runs. Both languages also leave the option of mixing weakly typed C code with static typed C++ or Objective-C to bypass all of the type checking.

Java goes a step beyond that, adding type checking when the code runs in a virtual machine.</p>

## Strong Static Languages: Java

C++ offers some stricter ways of using C; Java makes sure you use them. <strong>Java needs everything to be defined</strong> so that you know at all times what type of object you have, which functions that object has and whether you’re calling them properly.

Java also stopped supporting C code and other ways of getting out of static typing.

The <code>Person</code> object looks almost the same in Java:

<pre><code class="language-javascript">
public class Person {
    public String getName() {
        return "zack";
    }
}
</code></pre>

I get the name by creating a new object and calling the <code>getName</code> function, like this:

<pre><code class="language-javascript">
public class Main {
    public static void main (String args[]) {
        Person person = new Person();
        System.out.println("The name is " + person.getName());
    }
}
</code></pre>

This code creates a new <code>Person</code> object, assigns it to a variable named <code>person</code>, calls the <code>getName</code> function and prints out the value.

If I try to assign my <code>person</code> variable to a different type, such as a character or integer, then the Java compiler will show an error that these types are incompatible. If I was calling a separate API that had changed since I compiled, then the Java runtime would still find the type error.

<strong>Java doesn’t allow code outside of a class.</strong> It’s a major reason why people complain that Java forces you to write too much boilerplate.

The popularity of Java and its strong adherence to strong typing made a huge impact on the programming landscape. Strong typing advocates lauded Java for fixing the cracks in C++. But many programmers found Java overly prescriptive and rigid. They wanted a fast way to write code without all of the extra definition of Java.

## Strong Dynamic Languages: JavaScript, Python, Ruby And Many More

In JavaScript, I <strong>define a variable with the keyword</strong> <code>var</code>, instead of a type like <code>int</code> or <code>char</code>. I don’t know the type of this variable and I don’t need to until I actually want to access it.

I can define an object in JavaScript with the <code>getName</code> function.

<pre><code class="language-javascript">
var person = {
    getName: function() {
        return 'zack';
    }
};

alert('The name is ' + person.getName());
</code></pre>

Now I have an object named <code>person</code>, and it has a function named <code>getName</code>. If I call <code>person.getName()</code>, it will result in <code>zack</code>.

I declared <code>person</code> as a <code>var</code>, and I can reassign it to anything.

<pre><code class="language-javascript">
var person = {
    getName: function() {
        return 'zack';
    }
};

person = 5;

alert('The name is ' + person.getName());
</code></pre>

This code creates a variable named <code>person</code> and assigns it to an object with a <code>getPerson</code> function, but then it reassigns that variable to the number 5. When this code runs, the result is <code>TypeError: Object 5 has no method 'getName'</code>. JavaScript says that the object <code>5</code> doesn’t have a function named <code>getName</code>. In Java, this error would come up during compilation, but <strong>JavaScript makes you wait for runtime</strong>.

I can also change the type of the object based on the conditions of the program.

<pre><code class="language-javascript">
var person = {
    getName: function() {
        return 'zack';
    }
};

if (new Date().getMinutes() &gt; 29) {
    person = 5;
}

alert('The name is ' + person.getName());
</code></pre>

Now this code will work at 9:15 but will fail at 9:30. Java would call this a type error, but it’s fine in JavaScript.

The most popular form of dynamic typing is called “duck typing” because the code looks at the object during runtime to determine the type — and if it walks like a duck and quacks like a duck, then it must be a duck.

<strong>Duck typing enables you to redefine any object in the middle of the program.</strong> It can start as a duck and turn into a swan or goose.

<pre><code class="language-javascript">
var person = {
    getName: function() {
        return 'zack';
    }
};

person['getBirthday'] = function() {
    return 'July 18th';
};

alert('The name is ' + person.getName() + ' ' +
      'and the birthday is ' + person.getBirthday());
</code></pre>

At any point, I can change the nature of my <code>Person</code> object to add the new <code>getBirthday</code> function or to remove existing functionality. Java won’t allow that because you can’t check object types when they’re always changing. Dynamically redefining objects gives you a lot of power, for good and bad.

C shows errors when the program runs. C++, Objective-C and Java use the compiler to catch errors at compile time. JavaScript pushes those errors back to the runtime of the application. That’s why supporters of strong typing hate JavaScript so much: it seems like a big step backward. They’re always <a href="https://www.smashingmagazine.com/2012/12/14/which-javascript-recipe-is-right-for-you/">looking for JavaScript alternatives</a>.</p>

## Which Is Better?

I’m looking for a program to parse XML, find a particular element, make a change and save the file. On a team of Java programmers, I wrote the code in the dynamic language <a href="https://en.wikipedia.org/wiki/Python_(programming_language)">Python</a>.

<pre><code class="language-python">import sys
import string
from xml.dom.minidom import parse

dom = parse(sys.argv[1])

for node in dom.getElementsByTagName('property'):
    attr = node.attributes['name'];
    if attr.value == 'my value':
        node.childNodes[0] = dom.createTextNode('my new value');

file = open(sys.argv[1], 'w');
file.write(dom.toxml('UTF-8'));
file.close();
</code></pre>

This program finds every property node with the name <code>my value</code> and sets the contents to <code>my new value</code>. I define the variables <code>dom</code> for my XML document, <code>node</code> for each node of XML that I find, and <code>attr</code> for the attribute. Python doesn’t even require the keyword <code>var</code>, and it doesn’t know that <code>node</code> has <code>childNodes</code> or that <code>attr</code> has <code>value</code> until I call it.

To change an XML file in Java, I would write a new class, open an input stream, call the DOM parser, traverse the tree, call the right methods on the right elements, and write the file out to an output stream. I could simplify some of those calls with a library, but I’d still have the overhead of defining my static types. All of the extra definition of objects and variables could easily take a hundred lines. Python takes 14.

<strong>Dynamic code is generally shorter than static code</strong> because it needs less description of what the code is going to do. This program would be shorter in Python than in C++ and shorter in Ruby than in Objective-C.

So, which is better?
<table class="table-overview"><br>
<tbody>
<tr>
<th><strong>The static programmer says:</strong></th>
<th><strong>The dynamic programmer says:</strong></th>
</tr>
<tr>
<td>“Static typing catches bugs with the compiler and keeps you out of trouble.”</td>
<td>“Static typing only catches some bugs, and you can’t trust the compiler to do your testing.”</td>
</tr>
<tr>
<td>“Static languages are easier to read because they’re more explicit about what the code does.”</td>
<td>“Dynamic languages are easier to read because you write less code.”</td>
</tr>
<tr>
<td>“At least I know that the code compiles.”</td>
<td>“Just because the code compiles doesn’t mean it runs.”</td>
</tr>
<tr>
<td>“I trust the static typing to make sure my team writes good code.”</td>
<td>“The compiler doesn’t stop you from writing bad code.”</td>
</tr>
<tr>
<td>“Debugging an unknown object is impossible.”</td>
<td>“Debugging overly complex object hierarchies is unbearable.”</td>
</tr>
<tr>
<td>“Compiler bugs happen at midmorning in my office; runtime bugs happen at midnight for my customers.”</td>
<td>“There’s no replacement for testing, and unit tests find more issues than the compiler ever could.”</td>
</tr>
</tbody>
</table>

Static typing made our <code>Person</code> object easier to understand. We defined a <code>Person</code> with a name and agreed about which fields mattered ahead of time. Establishing everything clearly makes our <code>Person</code> easier to debug but harder to change.

What happens <strong>when someone in our application needs a second email address?</strong> In a static language, we’d need to redefine the object so that everyone has two email addresses, even though most people don’t. Add in a birthday, favorite color and a few more items and every <code>Person</code> will have twice as many fields as they need.

<strong>Dynamic languages make this problem much easier.</strong> We can add a second email field to one <code>Person</code> without adding it to everyone. Now, each object has only the fields it needs. A static language could handle this with a generic map of values, but then you’re fighting the static environment to write dynamic code. C programmers spent years tearing their hair out over errors in type conversions, corrupt values, and the terrible bugs that come from small typos. They’ve been burnt by weak typing, and dynamic typing looks weak.

Dynamic programmers spent years banging their heads over the rigidity of static languages, and they crave the freedom to make the languages do what they want.

I’ve seen static code get overly complex and become impossible to follow. Try debugging an <a href="https://en.wikipedia.org/wiki/Enterprise_JavaBeans">enterprise JavaBean</a> or understanding all of the details of <a href="https://en.wikipedia.org/wiki/Generics_in_Java">generics in Java</a>. I’ve seen dynamic code turn into a giant mound of unmaintainable spaghetti. Look at the myriad of terrible JavaScript programs before jQuery. <a href="https://en.wikipedia.org/wiki/Node.js">Node.js</a> does some amazing things, but I can’t look at it without traumatic flashbacks of horrible JavaScript that I’ve debugged.</p>

## Conclusion

There’s no clear conclusion. Dynamically typed languages are popular now. The pendulum will swing back and forth many times in the coming years. The only solution is flexibility. Learn to work in each environment and you’ll work well with any team.

<em>Image credits of image on front page: <a href="https://www.flickr.com/photos/73807667@N02/8021619893/sizes/c/">Alexflx54</a></em>

<em>(al) (ea)</em>

