---
title: 'Fluid Sizing Instead Of Multiple Media Queries?'
slug: fluid-sizing-multiple-media-queries
author: ruslan-yevych
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8325e378-54a4-435f-8867-8eedcbebbd04/1-fluid-typography-say-no-media-queries.png
date: 2022-08-01T10:30:00.000Z
summary: >-
  If you like math and CSS, you’ll love this one. We don’t need to use media queries to change the values of some CSS properties — *font-size*, *padding*, *margin* etc. — depending on the viewport width, with the CSS `clamp` function. But: we still need to use media queries for changing colors, borders, shadows and other CSS styles. This article is an enhanced release of the [tutorial](https://habr.com/ru/post/646089/) published earlier.
description: >-
  If you like math and CSS, you’ll love this one. We don’t need to use media queries to change the values of some CSS properties — *font-size*, *padding*, *margin* etc. — depending on the viewport width, with the CSS `clamp` function. But: we still need to use media queries for changing colors, borders, shadows and other CSS styles.
categories:
  - Typography
  - CSS
---

Media queries are a great concept. Building a complex structure in an HTML document and adapting it for various devices is not often possible without them (for the moment at least). Here we will talk about the fact that one of the drawbacks of **fluid typography**, namely the appearance of a large number of media queries, can be avoided. Or, at least, the number of records in *@media* rule can be reduced.

The advent of `vw` and `vh` relative units, the `calc` function, and later the `min`, `max`, `clamp` functions in CSS gave us a lot of power. An exhaustive [review of Modern Fluid Typography Using CSS Clamp](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/) has been recently published by Adrian Bece. I advise everyone to get acquainted with it.

The advantages of the **`clamp` function** are obvious. We can define a change, for example, of a font size in a certain range of viewport (screen size) and, at the same time, limit it by maximum and minimum values. In such a simple case, we automatically (thanks to clamp) do not need to use media queries for changing sizes on breakpoints.

So, the following block in the CSS:

<pre><code class="language-css">.block{
 font-size: 2rem;
}
@media (max-width: 1200px) {
 .block{
   font-size: calc(-1rem + 4vw);
 }
}
@media (max-width: 800px) {
 .block{
   font-size: 1rem;
 }
}</code></pre>

...can be easily replaced using `clamp` with a single line:

<pre><code class="language-css">.block{
 font-size: clamp(1rem, -1rem + 4vw, 2rem);
}</code></pre>

But what if we need to set a **more complex behavior** which is determined by variety of unique behavior on different ranges of the screen width? Look at the following modified code:

<pre><code class="language-css">.block{
 font-size: calc(-4rem + 8vw);
}
@media (max-width: 1200px) {
 .block{
   font-size: calc(-1rem + 4vw);
 }
}
@media (max-width: 800px) {
 .block{
   font-size: calc(0.5rem + 0.8vw);
 }
}</code></pre>

Can the `clamp` help us again? 

Let’s take a closer look: from simple to complex.

## Brief Digression Into Mathematics

As we all know, there is only one way to **draw a straight line** through two points. There are several ways to write equations to define the straight line. Below, it will be convenient for us to write the equation in the form:

$$(1)\;\;\; y=y_0 + k&#42;x$$

where _y<sub>0</sub>_ is a **point of intersection** of the line with the `Y`-axis (fig.1), `k` parameter defines the slope of the straight line to the `X`-axis and represents the growth/fall rate. Using the following canonical representation of the equation of a straight line:

$$\frac{y - y_1}{y_1 - y_2}=\frac{x - x_1}{x_1 - x_2}$$

It is easy to connect the _y<sub>0</sub>_ and `k` parameters with the coordinates of the two points that belong to this line:

$$(1a)\;\;\; k=\frac{y_2 - y_1}{x_2 - x_1} ,\;\;\; y_0=y_1 - k&#42;x_1$$

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229e59a2-7543-46b0-9df9-96c1ccfcb840/30-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229e59a2-7543-46b0-9df9-96c1ccfcb840/30-fluid-typography-say-no-media-queries.png" width="800" height="612" sizes="100vw" caption="A straight line drawn through two points with coordinates (x<sub>1</sub>, y<sub>1</sub>) and (x<sub>2</sub>, y<sub>2</sub>). (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/229e59a2-7543-46b0-9df9-96c1ccfcb840/30-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="A graph with a straight line" >}}

It should be noted that in such problems it is convenient to **define the input parameters** (point coordinates) in pixels. But at the output the relative unit `rem` is preferable. We should also remember the fact that viewport width is equal to `100vw` (this follows from the definition of `vw` unit). So, in equation (1) we must replace `x` variable by just `100vw`. Hence, we’ll have:

$$(1b)\;\;\; y=y_0 + k&#42;100vw$$

Now it becomes clear the origin of expressions like `1rem + 2.5vw` as one of the arguments of `clamp` or `calc` function. The first term (`1rem`) is the *y<sub>0</sub>* parameter expressed in relative units (`rem`), and the second one (`2.5vw`) is the parameter `k` multiplied by `100vw` since `x=100vw`. The choice of such units &mdash; relative unit (`rem`) for values of output variable and viewport unit (`vw`) for screen size &mdash; has been made due to **accessibility and responsiveness**, respectively.

So, now we know how to determine the parameters in the equation of the form (1) or (1b) of a straight line drawn through two points. This will be used in the next section.

{{% feature-panel %}}

## Main Formula Derivation For General Case

Now we’ll try to obtain an equation for `F(x)` function that will follow the behavior of property in general case (fig.2). Some information below may be omitted for readers who do not like pure math. You can look at the **final equation (3)** and **the simple example** for explanation how to use it. 

Let’s look at fig. 2a (below). As you can see from the figure, the behavior of the property is determined (tabulated) by `N` points with coordinates *(x<sub>i</sub>, y<sub>i</sub>)*. Let *f<sub>i</sub>(x)* be a function that defines the straight line drawn through *(x<sub>i</sub>, y<sub>i</sub>)* and *(x<sub>i+1</sub>, y<sub>i+1</sub>)* points. We have `(N-1)` such functions (fig2b). So, how to get a general `F(x)` function that will be exactly equal to *f<sub>i</sub>(x)* function on the corresponding *[x<sub>i</sub>, x<sub>i+1</sub>]* range, notably **completely repeat the behavior** of property from fig.2? 

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8325e378-54a4-435f-8867-8eedcbebbd04/1-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8325e378-54a4-435f-8867-8eedcbebbd04/1-fluid-typography-say-no-media-queries.png" width="800" height="307" sizes="100vw" caption="Fig.2. An example of behavior of the values for some CSS property. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8325e378-54a4-435f-8867-8eedcbebbd04/1-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="An example of behavior of the values for some CSS property" >}}

Let’s define the collection of functions *g<sub>i</sub>(x)* as:

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mrow>
      <mi mathcolor="#000000">g</mi>
    </mrow>
    <mrow>
      <mi mathcolor="#000000">i</mi>
    </mrow>
  </msub>
  <mo stretchy="false" mathcolor="#000000">(</mo>
  <mi mathcolor="#000000">x</mi>
  <mo stretchy="false" mathcolor="#000000">)</mo>
  <mo mathcolor="#000000">=</mo>
  <mi mathcolor="#000000">c</mi>
  <mi mathcolor="#000000">l</mi>
  <mi mathcolor="#000000">a</mi>
  <mi mathcolor="#000000">m</mi>
  <mi mathcolor="#000000">p</mi>
  <mfenced mathcolor="#000000" separators="|">
    <mrow>
      <msub>
        <mrow>
          <mi mathcolor="#000000">y</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">i</mi>
        </mrow>
      </msub>
      <mo mathcolor="#000000">,</mo>
      <msub>
        <mrow>
          <mi mathcolor="#000000">f</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">i</mi>
        </mrow>
      </msub>
      <mo stretchy="false" mathcolor="#000000">(</mo>
      <mi mathcolor="#000000">x</mi>
      <mo stretchy="false" mathcolor="#000000">)</mo>
      <mo mathcolor="#000000">,</mo>
      <msub>
        <mrow>
          <mi mathcolor="#000000">y</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">i</mi>
          <mo mathcolor="#000000">+</mo>
          <mn mathcolor="#000000">1</mn>
        </mrow>
      </msub>
    </mrow>
  </mfenced>
  <mo mathcolor="#000000">.</mo>
</math>

<br />
According to `clamp` function definition:
<br />

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mrow>
      <mi mathcolor="#000000">g</mi>
    </mrow>
    <mrow>
      <mi mathcolor="#000000">i</mi>
    </mrow>
  </msub>
  <mo stretchy="false" mathcolor="#000000">(</mo>
  <mi mathcolor="#000000">x</mi>
  <mo stretchy="false" mathcolor="#000000">)</mo>
  <mo mathcolor="#000000">=</mo>
  <mfenced mathcolor="#000000" open="{" close="" separators="|">
    <mrow>
      <mtable mathcolor="#000000">
        <mtr>
          <mtd>
            <msub>
              <mrow>
                <mi mathcolor="#000000">y</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
              </mrow>
            </msub>
            <mo mathcolor="#000000">,</mo>
            <mi mathcolor="#000000"> </mi>
            <mi mathcolor="#000000">x</mi>
            <mo mathcolor="#000000">&lt;</mo>
            <msub>
              <mrow>
                <mi mathcolor="#000000">x</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
              </mrow>
            </msub>
            <mo mathcolor="#000000">;</mo>
          </mtd>
        </mtr>
        <mtr>
          <mtd>
            <msub>
              <mrow>
                <mi mathcolor="#000000">f</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
              </mrow>
            </msub>
            <mo stretchy="false" mathcolor="#000000">(</mo>
            <mi mathcolor="#000000">x</mi>
            <mo stretchy="false" mathcolor="#000000">)</mo>
            <mo mathcolor="#000000">,</mo>
            <msub>
              <mrow>
                <mi mathcolor="#000000">x</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
              </mrow>
            </msub>
            <mo mathcolor="#000000">≤</mo>
            <mi mathcolor="#000000">x</mi>
            <mo mathcolor="#000000">&lt;</mo>
            <msub>
              <mrow>
                <mi mathcolor="#000000">x</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
                <mo mathcolor="#000000">+</mo>
                <mn mathcolor="#000000">1</mn>
                <mo mathcolor="#000000">;</mo>
              </mrow>
            </msub>
            <mi mathcolor="#000000"> </mi>
          </mtd>
        </mtr>
        <mtr>
          <mtd>
            <msub>
              <mrow>
                <mi mathcolor="#000000">y</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
                <mo mathcolor="#000000">+</mo>
                <mn mathcolor="#000000">1</mn>
              </mrow>
            </msub>
            <mo mathcolor="#000000">,</mo>
            <mi mathcolor="#000000">x</mi>
            <mo mathcolor="#000000">≥</mo>
            <msub>
              <mrow>
                <mi mathcolor="#000000">x</mi>
              </mrow>
              <mrow>
                <mi mathcolor="#000000">i</mi>
                <mo mathcolor="#000000">+</mo>
                <mn mathcolor="#000000">1</mn>
              </mrow>
            </msub>
            <mo mathcolor="#000000">.</mo>
          </mtd>
        </mtr>
      </mtable>
    </mrow>
  </mfenced>
</math>

<br />
Let’s sum the *g<sub>i</sub>(x)* functions, and denote the result as `G(x)` function, <math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">G</mi>
  <mfenced mathcolor="#000000" separators="|">
    <mrow>
      <mi mathcolor="#000000">x</mi>
    </mrow>
  </mfenced>
  <mo mathcolor="#000000">=</mo>
  <mrow>
    <msubsup>
      <mo mathcolor="#000000" stretchy="false">∑</mo>
      <mrow>
        <mi mathcolor="#000000">i</mi>
        <mo mathcolor="#000000">=</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
      <mrow>
        <mi mathcolor="#000000">N</mi>
        <mo mathcolor="#000000">-</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
    </msubsup>
    <mrow>
      <msub>
        <mrow>
          <mi mathcolor="#000000">g</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">i</mi>
        </mrow>
      </msub>
      <mfenced mathcolor="#000000" separators="|">
        <mrow>
          <mi mathcolor="#000000">x</mi>
        </mrow>
      </mfenced>
    </mrow>
  </mrow>
  <mo mathcolor="#000000">.</mo>
  <mi mathcolor="#000000"> </mi>
</math>

Now we can calculate the values of this function for different ranges of `x` variable:
<br />

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">G</mi>
  <mo stretchy="false" mathcolor="#000000">(</mo>
  <mi mathcolor="#000000">x</mi>
  <mo stretchy="false" mathcolor="#000000">)</mo>
  <mo mathcolor="#000000">=</mo>
  <mfenced mathcolor="#000000" open="{" close="" separators="|">
    <mrow>
      <mtable mathcolor="#000000">
        <mtr>
          <mtd>
            <mrow>
              <maligngroup/>
              <mtable mathcolor="#000000">
                <mtr>
                  <mtd>
                    <mrow>
                      <maligngroup/>
                      <mtable mathcolor="#000000">
                        <mtr>
                          <mtd>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">f</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">1</mn>
                              </mrow>
                            </msub>
                            <mo stretchy="false" mathcolor="#000000">(</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo stretchy="false" mathcolor="#000000">)</mo>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">3</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <mo mathcolor="#000000">…</mo>
                            <mo mathcolor="#000000">+</mo>
                            <mi mathcolor="#000000"> </mi>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">1</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">,</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">1</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">≤</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo mathcolor="#000000">&lt;</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">;</mo>
                          </mtd>
                        </mtr>
                        <mtr>
                          <mtd>
                            <msub>
                              <mrow>
                                <msub>
                                  <mrow>
                                    <mi mathcolor="#000000">y</mi>
                                  </mrow>
                                  <mrow>
                                    <mn mathcolor="#000000">2</mn>
                                  </mrow>
                                </msub>
                                <mo mathcolor="#000000">+</mo>
                                <mi mathcolor="#000000">f</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo stretchy="false" mathcolor="#000000">(</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo stretchy="false" mathcolor="#000000">)</mo>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">3</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <mo mathcolor="#000000">…</mo>
                            <mo mathcolor="#000000">+</mo>
                            <mi mathcolor="#000000"> </mi>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">1</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">,</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">≤</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo mathcolor="#000000">&lt;</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">3</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">;</mo>
                          </mtd>
                        </mtr>
                        <mtr>
                          <mtd>
                            <msub>
                              <mrow>
                                <msub>
                                  <mrow>
                                    <mi mathcolor="#000000">y</mi>
                                  </mrow>
                                  <mrow>
                                    <mn mathcolor="#000000">2</mn>
                                  </mrow>
                                </msub>
                                <mo mathcolor="#000000">+</mo>
                                <msub>
                                  <mrow>
                                    <mi mathcolor="#000000">y</mi>
                                  </mrow>
                                  <mrow>
                                    <mn mathcolor="#000000">3</mn>
                                  </mrow>
                                </msub>
                                <mo mathcolor="#000000">+</mo>
                                <mi mathcolor="#000000">f</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">3</mn>
                              </mrow>
                            </msub>
                            <mo stretchy="false" mathcolor="#000000">(</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo stretchy="false" mathcolor="#000000">)</mo>
                            <mo mathcolor="#000000">+</mo>
                            <mo mathcolor="#000000">…</mo>
                            <mo mathcolor="#000000">+</mo>
                            <mi mathcolor="#000000"> </mi>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">2</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">+</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">y</mi>
                              </mrow>
                              <mrow>
                                <mi mathcolor="#000000">N</mi>
                                <mo mathcolor="#000000">-</mo>
                                <mn mathcolor="#000000">1</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">,</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">3</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">≤</mo>
                            <mi mathcolor="#000000">x</mi>
                            <mo mathcolor="#000000">&lt;</mo>
                            <msub>
                              <mrow>
                                <mi mathcolor="#000000">x</mi>
                              </mrow>
                              <mrow>
                                <mn mathcolor="#000000">4</mn>
                              </mrow>
                            </msub>
                            <mo mathcolor="#000000">;</mo>
                          </mtd>
                        </mtr>
                      </mtable>
                    </mrow>
                  </mtd>
                </mtr>
                <mtr>
                  <mtd>
                    <mrow>
                      <maligngroup/>
                      <mo mathcolor="#000000">⋮</mo>
                    </mrow>
                  </mtd>
                </mtr>
              </mtable>
            </mrow>
          </mtd>
        </mtr>
        <mtr>
          <mtd>
            <mrow>
              <maligngroup/>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">y</mi>
                </mrow>
                <mrow>
                  <mn mathcolor="#000000">2</mn>
                </mrow>
              </msub>
              <mo mathcolor="#000000">+</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">y</mi>
                </mrow>
                <mrow>
                  <mn mathcolor="#000000">3</mn>
                </mrow>
              </msub>
              <mo mathcolor="#000000">+</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">y</mi>
                </mrow>
                <mrow>
                  <mn mathcolor="#000000">4</mn>
                </mrow>
              </msub>
              <mo mathcolor="#000000">+</mo>
              <mo mathcolor="#000000">…</mo>
              <mo mathcolor="#000000">+</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">y</mi>
                </mrow>
                <mrow>
                  <mi mathcolor="#000000">N</mi>
                  <mo mathcolor="#000000">-</mo>
                  <mn mathcolor="#000000">1</mn>
                </mrow>
              </msub>
              <mo mathcolor="#000000">+</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">f</mi>
                </mrow>
                <mrow>
                  <mi mathcolor="#000000">N</mi>
                  <mo mathcolor="#000000">-</mo>
                  <mn mathcolor="#000000">1</mn>
                </mrow>
              </msub>
              <mo stretchy="false" mathcolor="#000000">(</mo>
              <mi mathcolor="#000000">x</mi>
              <mo stretchy="false" mathcolor="#000000">)</mo>
              <mo mathcolor="#000000">,</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">x</mi>
                </mrow>
                <mrow>
                  <mi mathcolor="#000000">N</mi>
                  <mo mathcolor="#000000">-</mo>
                  <mn mathcolor="#000000">1</mn>
                </mrow>
              </msub>
              <mo mathcolor="#000000">≤</mo>
              <mi mathcolor="#000000">x</mi>
              <mo mathcolor="#000000">&lt;</mo>
              <msub>
                <mrow>
                  <mi mathcolor="#000000">x</mi>
                </mrow>
                <mrow>
                  <mi mathcolor="#000000">N</mi>
                </mrow>
              </msub>
              <mo mathcolor="#000000">;</mo>
            </mrow>
          </mtd>
        </mtr>
      </mtable>
    </mrow>
  </mfenced>
</math>

or 
<br />

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">G</mi>
  <mo stretchy="false" mathcolor="#000000">(</mo>
  <mi mathcolor="#000000">x</mi>
  <mo stretchy="false" mathcolor="#000000">)</mo>
  <mo mathcolor="#000000">=</mo>
  <msub>
    <mrow>
      <mi mathcolor="#000000">f</mi>
    </mrow>
    <mrow>
      <mi mathcolor="#000000">i</mi>
    </mrow>
  </msub>
  <mo stretchy="false" mathcolor="#000000">(</mo>
  <mi mathcolor="#000000">x</mi>
  <mo stretchy="false" mathcolor="#000000">)</mo>
  <mo mathcolor="#000000">+</mo>
  <mi mathcolor="#000000">C</mi>
  <mi mathcolor="#000000">o</mi>
  <mi mathcolor="#000000">n</mi>
  <mi mathcolor="#000000">s</mi>
  <mi mathcolor="#000000">t</mi>
  <mo mathcolor="#000000">,</mo>
</math>

<br />
for
<br />

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msub>
    <mrow>
      <mi mathcolor="#000000">x</mi>
    </mrow>
    <mrow>
      <mi mathcolor="#000000">i</mi>
    </mrow>
  </msub>
  <mo mathcolor="#000000">≤</mo>
  <mi mathcolor="#000000">x</mi>
  <mo mathcolor="#000000">&lt;</mo>
  <msub>
    <mrow>
      <mi mathcolor="#000000">x</mi>
    </mrow>
    <mrow>
      <mi mathcolor="#000000">i</mi>
      <mo mathcolor="#000000">+</mo>
      <mn mathcolor="#000000">1</mn>
    </mrow>
  </msub>
  <mo mathcolor="#000000">,</mo>
</math> 
<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">i</mi>
  <mo mathcolor="#000000">=</mo>
  <mn mathcolor="#000000">1,</mn>
  <mo mathcolor="#000000">…</mo>
  <mo mathcolor="#000000">,</mo>
  <mfenced mathcolor="#000000" separators="|">
    <mrow>
      <mi mathcolor="#000000">N</mi>
      <mo mathcolor="#000000">-</mo>
      <mn mathcolor="#000000">1</mn>
    </mrow>
  </mfenced>
  <mo mathcolor="#000000">,</mo>
</math>

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">C</mi>
  <mi mathcolor="#000000">o</mi>
  <mi mathcolor="#000000">n</mi>
  <mi mathcolor="#000000">s</mi>
  <mi mathcolor="#000000">t</mi>
  <mo mathcolor="#000000">=</mo>
  <mrow>
    <munderover>
      <mo mathcolor="#000000" stretchy="false">∑</mo>
      <mrow>
        <mi mathcolor="#000000">j</mi>
        <mo mathcolor="#000000">=</mo>
        <mn mathcolor="#000000">2</mn>
      </mrow>
      <mrow>
        <mi mathcolor="#000000">N</mi>
        <mo mathcolor="#000000">-</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
    </munderover>
    <mrow>
      <msub>
        <mrow>
          <mi mathcolor="#000000">y</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">j</mi>
        </mrow>
      </msub>
    </mrow>
  </mrow>
</math>

<br />
It follows that `G(x)` function is equal to corresponding *f<sub>i</sub>(x)* function for each [x<sub>i</sub>, x<sub>i+1</sub>] ranges, after deduction of `Const` constant term, or...
<br />

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <mi mathcolor="#000000">F</mi>
  <mfenced mathcolor="#000000" separators="|">
    <mrow>
      <mi mathcolor="#000000">x</mi>
    </mrow>
  </mfenced>
  <mo mathcolor="#000000">=</mo>
  <mi mathcolor="#000000">G</mi>
  <mfenced mathcolor="#000000" separators="|">
    <mrow>
      <mi mathcolor="#000000">x</mi>
    </mrow>
  </mfenced>
  <mo mathcolor="#000000">-</mo>
  <mi mathcolor="#000000">C</mi>
  <mi mathcolor="#000000">o</mi>
  <mi mathcolor="#000000">n</mi>
  <mi mathcolor="#000000">s</mi>
  <mi mathcolor="#000000">t</mi>
  <mo mathcolor="#000000">=</mo>
  <mrow>
    <munderover>
      <mo mathcolor="#000000" stretchy="false">∑</mo>
      <mrow>
        <mi mathcolor="#000000">i</mi>
        <mo mathcolor="#000000">=</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
      <mrow>
        <mi mathcolor="#000000">N</mi>
        <mo mathcolor="#000000">-</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
    </munderover>
    <mrow>
      <mi mathcolor="#000000">c</mi>
      <mi mathcolor="#000000">l</mi>
      <mi mathcolor="#000000">a</mi>
      <mi mathcolor="#000000">m</mi>
      <mi mathcolor="#000000">p</mi>
      <mfenced mathcolor="#000000" separators="|">
        <mrow>
          <msub>
            <mrow>
              <mi mathcolor="#000000">y</mi>
            </mrow>
            <mrow>
              <mi mathcolor="#000000">i</mi>
            </mrow>
          </msub>
          <mo mathcolor="#000000">,</mo>
          <msub>
            <mrow>
              <mi mathcolor="#000000">f</mi>
            </mrow>
            <mrow>
              <mi mathcolor="#000000">i</mi>
            </mrow>
          </msub>
          <mo stretchy="false" mathcolor="#000000">(</mo>
          <mi mathcolor="#000000">x</mi>
          <mo stretchy="false" mathcolor="#000000">)</mo>
          <mo mathcolor="#000000">,</mo>
          <msub>
            <mrow>
              <mi mathcolor="#000000">y</mi>
            </mrow>
            <mrow>
              <mi mathcolor="#000000">i</mi>
              <mo mathcolor="#000000">+</mo>
              <mn mathcolor="#000000">1</mn>
            </mrow>
          </msub>
        </mrow>
      </mfenced>
    </mrow>
  </mrow>
  <mo mathcolor="#000000">-</mo>
  <mrow>
    <munderover>
      <mo mathcolor="#000000" stretchy="false">∑</mo>
      <mrow>
        <mi mathcolor="#000000">i</mi>
        <mo mathcolor="#000000">=</mo>
        <mn mathcolor="#000000">2</mn>
      </mrow>
      <mrow>
        <mi mathcolor="#000000">N</mi>
        <mo mathcolor="#000000">-</mo>
        <mn mathcolor="#000000">1</mn>
      </mrow>
    </munderover>
    <mrow>
      <msub>
        <mrow>
          <mi mathcolor="#000000">y</mi>
        </mrow>
        <mrow>
          <mi mathcolor="#000000">i</mi>
        </mrow>
      </msub>
    </mrow>
  </mrow>
</math>

Equation (3) represents the final result and is the solution to the problem.

**Several remarks** should be made here:

- If we have the range with *y<sub>i</sub>= y<sub>i+1</sub>* then *f<sub>i</sub>(x)= y<sub>i</sub>*, and *clamp(y<sub>i</sub>, y<sub>i</sub>, y<sub>i</sub>) = y<sub>i</sub>* properly. This fact will give us some simplification in the final expression for `F(x)` function.
- If we have the range where the *y<sub>i</sub>&#62;y<sub>i+1</sub>* inequality is satisfied, then we should write the corresponding *g<sub>i</sub>(x)* function in the following form:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff9eb1b-3ea4-4d90-8a33-df25f3014508/31-fluid-typography-say-no-media-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff9eb1b-3ea4-4d90-8a33-df25f3014508/31-fluid-typography-say-no-media-queries.jpg" width="800" height="85" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/cff9eb1b-3ea4-4d90-8a33-df25f3014508/31-fluid-typography-say-no-media-queries.jpg'>Large preview</a>)" alt="function" >}}

... because of `clamp` function definition.

- Let’s consider the ranges where *х&#60;х<sub>1</sub>* and *х&#62;х<sub>N</sub>*. From equation (3) it follows that the values of property inside these ranges will be constant and equal to *y<sub>1</sub>* and *y<sub>N</sub>*, correspondingly. We can do nothing and leave it like that. But in these intervals, I prefer that the **values continue to change** according to the same laws as in the *[x<sub>1</sub>, x<sub>2</sub>]* and *[x<sub>N-1</sub>, x<sub>N</sub>]* ranges. Therefore, *g<sub>1</sub>(x)* and *g<sub>N-1</sub>(x)* functions should be written not by `clamp` function but through `min` or `max` functions depending on the increasing or decreasing of the values in the given ranges. If we take the behavior of the property from fig.2 as an example, then we will have the following two redefinitions:

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8a9a7e2-70fa-4649-a716-f8e50660e42b/32-fluid-typography-say-no-media-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8a9a7e2-70fa-4649-a716-f8e50660e42b/32-fluid-typography-say-no-media-queries.jpg" width="802" height="87" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8a9a7e2-70fa-4649-a716-f8e50660e42b/32-fluid-typography-say-no-media-queries.jpg'>Large preview</a>)" alt="function" >}}

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/219e096d-c91e-4d90-acea-844a7499ac37/33-fluid-typography-say-no-media-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/219e096d-c91e-4d90-acea-844a7499ac37/33-fluid-typography-say-no-media-queries.jpg" width="800" height="80" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/219e096d-c91e-4d90-acea-844a7499ac37/33-fluid-typography-say-no-media-queries.jpg'>Large preview</a>)" alt="function" >}}

- It is possible to set an **abrupt change** in the property. In this case, the maximum difference between *х<sub>i</sub>* and *х<sub>i+1</sub>* is set to `1px` (fig.3) or, which is even more convenient in practice, even less than 1px.
- Obviously, the more complex (more ranges) the behavior of the property is, the longer the resulting function will be and vice versa.
- Because of the possible complex structure of the function by equation (3), it must be used as an argument of the CSS `calc` function in the CSS stylesheet.

{{< rimg href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110b5e9-1842-4bf1-8661-5eba1ce06fc7/34-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110b5e9-1842-4bf1-8661-5eba1ce06fc7/34-fluid-typography-say-no-media-queries.png" width="800" height="612" sizes="100vw" caption="Fig. 3. Abrupt change of values of some property. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0110b5e9-1842-4bf1-8661-5eba1ce06fc7/34-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="Abrupt change of values of some property" >}}

{{% ad-panel-leaderboard %}}

### Simple Example

Let’s simulate the following simple case. We have a header with a logo and menu items on some page. For mobile devices we need to create a **hamburger menu**. In this case, the font size of menu items, for example, is equal to `18px` at `1920px` of screen size and decreases to `12px` at the viewport width of `768px`. In the range from `320px` to `767.98px` of viewport width, the font-size is fixed at `20px` (fig 4a.). This behavior of font size can be described by equation (3). Let’s start.

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e26ec17-d4d4-41c1-b4a5-3375c89e63d1/35-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e26ec17-d4d4-41c1-b4a5-3375c89e63d1/35-fluid-typography-say-no-media-queries.png" width="800" height="328" sizes="100vw" caption="Fig.4. The example of a font size (a) and a margin (b) values dependence on viewport width. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9e26ec17-d4d4-41c1-b4a5-3375c89e63d1/35-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="The example of a font size (a) and a margin (b) values dependence on viewport width" >}}

1\. We need to calculate the parameters for *f<sub>1</sub>*, *f<sub>2</sub>* and *f<sub>3</sub>* lines according to equation (1a) for its representation in the (1b) form. For *f<sub>1</sub>* function we have (using the coordination of 1 and 2 points):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4959e479-97c3-4e6e-b2bb-2ccc83c8d5b1/36-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4959e479-97c3-4e6e-b2bb-2ccc83c8d5b1/36-fluid-typography-say-no-media-queries.png" width="800" height="48" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4959e479-97c3-4e6e-b2bb-2ccc83c8d5b1/36-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

So, using equation (1b):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4530949-0078-4037-8410-0104f9166bbc/37-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4530949-0078-4037-8410-0104f9166bbc/37-fluid-typography-say-no-media-queries.png" width="800" height="56" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b4530949-0078-4037-8410-0104f9166bbc/37-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}	

The same procedure for another two lines gives us:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c785887-c3d3-47b2-84b5-5802342d5352/38-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c785887-c3d3-47b2-84b5-5802342d5352/38-fluid-typography-say-no-media-queries.png" width="800" height="87" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/2c785887-c3d3-47b2-84b5-5802342d5352/38-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

and

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d5ee0d8-42e0-41e0-a925-658226a8c9a7/39-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d5ee0d8-42e0-41e0-a925-658226a8c9a7/39-fluid-typography-say-no-media-queries.png" width="800" height="142" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1d5ee0d8-42e0-41e0-a925-658226a8c9a7/39-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

and

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddcf22d6-804f-439b-a901-9392570151ad/40-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddcf22d6-804f-439b-a901-9392570151ad/40-fluid-typography-say-no-media-queries.png" width="800" height="40" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ddcf22d6-804f-439b-a901-9392570151ad/40-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

2\. Now we can construct the *g<sub>i</sub>* functions using equation (2):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d08842-9686-4d89-9cfa-72e5890a6fda/41-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d08842-9686-4d89-9cfa-72e5890a6fda/41-fluid-typography-say-no-media-queries.png" width="800" height="64" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/53d08842-9686-4d89-9cfa-72e5890a6fda/41-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="functions" >}}

3\. The last term (constant) in equation (3) can be determined:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8953fddc-5785-4793-a5a1-4a709ee929b2/43-fluid-typography-say-no-media-queries.jpg" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8953fddc-5785-4793-a5a1-4a709ee929b2/43-fluid-typography-say-no-media-queries.jpg" width="800" height="117" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/8953fddc-5785-4793-a5a1-4a709ee929b2/43-fluid-typography-say-no-media-queries.jpg'>Large preview</a>)" alt="function" >}}

4\. Desired form of equation (3) is...

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7a0a3ac-a7b6-4b8c-959b-9f9bc17ee04f/44-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7a0a3ac-a7b6-4b8c-959b-9f9bc17ee04f/44-fluid-typography-say-no-media-queries.png" width="800" height="44" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c7a0a3ac-a7b6-4b8c-959b-9f9bc17ee04f/44-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

or, in the final form:

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21d323b9-2740-41fa-9890-86d7ee6c666a/45-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21d323b9-2740-41fa-9890-86d7ee6c666a/45-fluid-typography-say-no-media-queries.png" width="800" height="55" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/21d323b9-2740-41fa-9890-86d7ee6c666a/45-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

5\. Final record in CSS file will be (by remark 6):

<div class="break-out">

<pre><code class="language-css">.block{
 font-size: calc(clamp(0.75rem, 19200.75rem – 40000vw, 1.25rem) + max(0.75rem, 0.5rem + 0.5208333vw) – 0.75rem); 
}</code></pre>
</div>

... and is fully equivalent to:

<pre><code class="language-css">.block{
 font-size: calc(0.5rem + 0.5208333333vw);
}
@media (max-width: 767px) {
 .block {
  font-size: 1.25rem;
 }
}</code></pre>

Evaluations for modeling right margin behavior (see fig. 4b) give the following equation (everyone can verify this):

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/198ec156-aa2c-4a45-8ecb-96b795922fa2/46-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/198ec156-aa2c-4a45-8ecb-96b795922fa2/46-fluid-typography-say-no-media-queries.png" width="800" height="47" sizes="100vw" caption="(<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/198ec156-aa2c-4a45-8ecb-96b795922fa2/46-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="function" >}}

You can check this example here:

{{< codepen height="480" theme_id="light" slug_hash="qBxdpqx" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Header [forked]](https://codepen.io/smashingmag/pen/qBxdpqx) by <a href="https://codepen.io/ryevych">Ruslan</a>.{{< /codepen >}}  

### Another Example

The following dependence of `padding`:

<pre><code class="language-css">.block {
 padding: 3rem;
}

@media (max-width: 1199px) {
 .block {
  padding: 2.5rem;
 }
}
@media (max-width: 991px) {
 .block {
  padding: 2rem;
 }
}
@media (max-width: 767px) {
 .block {
  padding: 1.5rem;
 }
}
@media (max-width: 575px) {
 .block {
  padding: 1rem;
 }
}</code></pre>

... can be also easily replaced by:

<div class="break-out">

<pre><code class="language-css">.block {
 padding: calc(clamp(1rem, -14398.5rem + 40000vw, 1.5rem) + clamp(1.5rem, -19198rem + 40000vw, 2rem) + clamp(2rem, -24797.5rem + 40000vw, 2.5rem) + clamp(2.5rem, -29997rem + 40000vw, 3rem) - 6rem);
}</code></pre>
</div>

So, equation (3) gives us the possibility to **describe any arbitrary behavior** of the property depending on the viewport width. And it should be pointed out, we achieved this by completely eliminating the use of media queries.

Obviously, formula (3) can be used to describe **not only the `font size`**, but also every other property whose dimension is a unit of length. This limitation is due to a limitation in CSS itself, namely the lack of support for mathematical operations on values that have dimensions. For example, we cannot calculate something like `(2px*6px)/4px` in CSS at the date. I hope that such restrictions will disappear in future, and the equation (3) will be applied to properties specified as a percentage or dimensionless.

Also, it should be noted that it makes sense to apply the equation (3) only when the dependence is more complex than in **primitive cases** shown below:

1. **Continuous unlimited change**, the behavior is determined by two points only, `k` parameter of `f` function can be positive, negative or even zero (see fig.5a, `k>0`, for example). Instead of the equation(3) we use a function of the form `calc(f(x))`. A font size of some text that monotonically changes with viewport width can be as an example.
2. **Behavior is determined by three points**, for `k` parameters of *f<sub>1</sub>* and *f<sub>2</sub>* functions the inequality *k<sub>1</sub>&#62;k<sub>2</sub>* is satisfied (see fig.5b, *k<sub>1</sub>&#62;0* and *k<sub>2</sub>&#60;0*, for example). In such case, *min(f<sub>1</sub>,f<sub>2</sub>)* function should be used instead of equation (3). A font size of some text that monotonically changes with viewport width to a certain value and then keeps a constant value can be used as an example.
3. The same as the second case, but the inequality *k<sub>1</sub>&#60;k<sub>2</sub>* is satisfied (see fig.5c, *k<sub>1</sub>&#60;0* and *k<sub>2</sub>&#62;0*, for example). In such case, *max(f<sub>1</sub>,f<sub>2</sub>)* function should be used instead of equation (3).

{{< rimg breakout="true" href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c2f42d-5955-4c58-b8c9-c593d0d1acaf/47-fluid-typography-say-no-media-queries.png" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c2f42d-5955-4c58-b8c9-c593d0d1acaf/47-fluid-typography-say-no-media-queries.png" width="800" height="223" sizes="100vw" caption="Fig.5. The elemental behaviors of the values of some CSS property. (<a href='https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d8c2f42d-5955-4c58-b8c9-c593d0d1acaf/47-fluid-typography-say-no-media-queries.png'>Large preview</a>)" alt="The elemental behaviors of the values of some CSS property" >}}

{{< codepen height="480" theme_id="light" slug_hash="qBxdpKy" default_tab="result" breakout="true" user="smashingmag" editable="true" data-editable="true" >}}See the Pen [Quick CSS example [forked]](https://codepen.io/smashingmag/pen/qBxdpKy) by <a href="https://codepen.io/ryevych">Ruslan</a>.{{< /codepen >}}  

Everyone can write their own mixin or function based on the equation (3) or use [my implementation as CSS functions](https://github.com/ryevych/adaptiveValueFunction) that take into account the above **remarks** and **primitive cases**.

You can also find a **simple example** with the flex structure [here](https://ryevych.github.io/adaptiveValueFunction/). In this example, the width of flex elements is calculated using the equation (3). This is an attempt to avoid media queries with such a **commonly used transformation** &mdash; initially the width of each of the four flex items is set to 25% (convert to px units, of course), and then, as the viewport width decreases, it changes to 50%, and then to 100%. It even seems possible to take into account the value of gap, and make it also responsive.

But the example will break as soon as there is a **vertical scroll**. To avoid example breaking and to compensate for scrollbar, we can replace `vw` units by `%` in expressions for width of flex elements. But while CSS restrictions do not allow us to use the equation (3) directly for values given in percentages, it is better to abandon such idea. 

{{% ad-panel-leaderboard %}}

## Summary

I’d like to mention that the idea was just to proving the **possibility of such an approach**, and the suitability of its application is your own choice. Of the obvious disadvantage of this approach, I have to highlight that the resulting code becomes less readable. The advantage is that media queries remain solely for describing the logic of changes while adaptive, structural changes and are not clogged with technical lines of changing font sizes, paddings, margins etc.

*Editor’s note*: It would be fantastic to build up a little tool that would allow developers to define changes and construct these complex queries in no time. Still, the maintainance would become quite a hassle — unless we use a Sass-mixing for it, maybe? We kindly thank Ruslan for taking the time to work on this, and oh my, what a journey it was!

### Acknowledgements

*Thanks to [Evgeniy Andrikanich](https://fls.guru/) and his YouTube channel “[FreelancerStyle](https://www.youtube.com/channel/UCedskVwIKiZJsO8XdJdLKnA)” for creation of free high-quality educational content (HTML, CSS, JS).*

### Sources

- “[Responsible Property By One Line](https://habr.com/ru/post/646089/)” (in Russian)
- “[Modern Fluid Typography Using CSS Clamp](https://www.smashingmagazine.com/2022/01/modern-fluid-typography-css-clamp/),” Adrian Bece

{{< signature "vf, yk, il" >}}

<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
<style type="text/css">
@media (prefers-color-scheme: dark) {
  mjx-mi, mjx-mo, mjx-c {
    color: white !important;
  }
}
</style>
