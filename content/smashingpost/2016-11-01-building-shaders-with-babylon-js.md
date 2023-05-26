---
title: Building Shaders With Babylon.js
slug: building-shaders-with-babylon-js
image: >-
  https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c517b5f8-63bb-4e88-b85e-5276b0445080/babylon-1-preview-opt.png
date: 2016-11-01T21:46:44.000Z
author: davidcatuhe
description: >-
  Shaders are a key concept if you want to unleash the raw power of your GPU. I
  will help you understand how they work and even experiment with their inner
  power in an easy way, thanks to _Babylon.js_.

  Before experimenting, we must see how things work internally. When dealing
  with hardware-accelerated 3D, you will have to deal with two CPUs: the main
  CPU and the GPU. The GPU is a kind of extremely specialized CPU.
categories:
  - Coding
  - Tools
  - JavaScript
  - Techniques
---
Shaders are a key concept if you want to unleash the raw power of your GPU. I will help you understand how they work and even experiment with their inner power in an easy way, thanks to <a href="https://www.babylonjs.com/">Babylon.js</a>.</p>

## How Does It Work?

Before experimenting, we must see how things work internally.

When dealing with hardware-accelerated 3D, you will have to deal with two CPUs: the main CPU and the GPU. The GPU is a kind of extremely specialized CPU.</p>

## <span class="rh">Further Reading</span> on SmashingMag:

*   [<span class="headline">Building A Cross-Platform WebGL Game With Babylon.js</span>](https://www.smashingmagazine.com/2016/07/babylon-js-building-sponza-a-cross-platform-webgl-game/)
*   [Using The Gamepad API In Web Games](https://www.smashingmagazine.com/2015/11/gamepad-api-in-web-games/)
*   [Introduction To Polygonal Modeling And Three.js](https://www.smashingmagazine.com/2013/09/introduction-to-polygonal-modeling-and-three-js/)
*   [<span class="headline">How To Create A Responsive 8-Bit Drum Machine</span>](https://www.smashingmagazine.com/2016/08/how-to-create-a-responsive-8-bit-drum-machine-using-web-audio-svg-and-multitouch/)

{{% feature-panel %}}

The GPU is a state machine that you set up using the CPU. For instance, the CPU will configure the GPU to render lines instead of triangles; it will define whether transparency is on; and so on.

Once all of the states are set, the CPU can define what to render: the geometry.

The geometry is composed of:

*   a list of points that are called vertices and stored in an array called vertex buffer,
*   a list of indexes that define the faces (or triangles) stored in an array named index buffer.

The final step for the CPU is to define how to render the geometry; for this task, the CPU will define shaders in the GPU. Shaders are pieces of code that the GPU will execute for each of the vertices and pixels it has to render. (A vertex — or vertices when there are several of them — is a "point" in 3D).

There are two kinds of shaders: vertex shaders and pixel (or fragment) shaders.</p>

### Graphics Pipeline

Before digging into shaders, let’s step back. To render pixels, the GPU will take the geometry defined by the CPU and will do the following:

*   Using the index buffer, three vertices are gathered to define a triangle.
*   Index buffer contains a list of vertex indexes. This means that each entry in the index buffer is the number of a vertex in the vertex buffer.
*   This is really useful to avoid duplicating vertices.

For instance, the following index buffer is a list of two faces: [1 2 3 1 3 4]. The first face contains vertex 1, vertex 2 and vertex 3. The second face contains vertex 1, vertex 3 and vertex 4. So, there are four vertices in this geometry:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca137714-04de-4ce0-a1f0-e6c052fe24b6/babylon-1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/c517b5f8-63bb-4e88-b85e-5276b0445080/babylon-1-preview-opt.png" alt="" width="500" height="305" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ca137714-04de-4ce0-a1f0-e6c052fe24b6/babylon-1-large-opt.png">View large version</a>)</figcaption></figure>

The vertex shader is applied to each vertex of the triangle. The primary goal of the vertex shader is to produce a pixel for each vertex (the projection on the 2D screen of the 3D vertex):

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef802b90-741d-4f08-a616-691690457590/babylon-2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/1f127934-ab24-4af2-a16b-ab7036b5d39c/babylon-2-preview-opt.png" alt="" width="500" height="367" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ef802b90-741d-4f08-a616-691690457590/babylon-2-large-opt.png">View large version</a>)</figcaption></figure>

Using these three pixels (which define a 2D triangle on the screen), the GPU will interpolate all values attached to the pixel (at least their positions), and the pixel shader will be applied to every pixel included in the 2D triangle in order to generate a color for every pixel:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde13b3d-ad93-4106-b741-79cd960e54d4/babylon-3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a3978d88-0536-4d8d-ac50-365dd22d592b/babylon-3-preview-opt.png" alt="" width="500" height="368" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/bde13b3d-ad93-4106-b741-79cd960e54d4/babylon-3-large-opt.png">View large version</a>)</figcaption></figure>

This process is done for every face defined by the index buffer.

Obviously, due to its parallel nature, the GPU is able to process this step for a lot of faces simultaneously and achieve really good performance.</p>

### GLSL

We have just seen that to render triangles, the GPU needs two shaders: the vertex shader and the pixel shader. These shaders are written in a language named Graphics Library Shader Language (GLSL). It looks like C.

Here is a sample of a common vertex shader:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec2 uv;

// Uniforms
uniform mat4 worldViewProjection;

// Varying
varying vec2 vUV;

void main(void) {
    gl_Position = worldViewProjection * vec4(position, 1.0);

    vUV = uv;
}
</code></pre>

### Vertex Shader Structure

A vertex shader contains the following:

*   **Attributes**.  An attribute defines a portion of a vertex. By default, a vertex should at least contain a position (a `vector3:x, y, z`). However, as a developer, you can decide to add more information. For instance, in the former shader, there is a `vector2` named `uv` (i.e. texture coordinates that allow you to apply a 2D texture to a 3D object).
*   **Uniforms**.  A uniform is a variable used by the shader and defined by the CPU. The only uniform we have here is a matrix used to project the position of the vertex (x, y, z) to the screen (x, y).
*   **Varying**.  Varying variables are values created by the vertex shader and transmitted to the pixel shader. Here, the vertex shader will transmit a `vUV` (a simple copy of `uv`) value to the pixel shader. This means that a pixel is defined here with a position and texture coordinates. These values will be interpolated by the GPU and used by the pixel shader.
*   **Main**.  The function named `main` is the code executed by the GPU for each vertex and must at least produce a value for `gl_position` (the position of the current vertex on the screen).

We can see in our sample that the vertex shader is pretty simple. It generates a system variable (starting with <code>gl_</code>) named <code>gl_position</code> to define the position of the associated pixel, and it sets a varying variable called <code>vUV</code>.</p>

### The Voodoo Behind Matrices

The thing about our shader is that we have a matrix named <code>worldViewProjection</code>, and we use this matrix to project the vertex position to the <code>gl_position</code> variable. That is cool, but how do we get the value of this matrix? It is a uniform, so we have to define it on the CPU side (using JavaScript).

This is one of the complex parts of doing 3D. You must understand complex math (or you will have to use a 3D engine such as Babylon.js, which we will see later).

The <code>worldViewProjection</code> matrix is the combination of three different matrices:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c52d92-5327-4990-a19a-0aceb796808b/babylon-4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/d998f48f-1161-4711-9a83-94b32e6e7b18/babylon-4-preview-opt.png" alt="" width="500" height="251" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/17c52d92-5327-4990-a19a-0aceb796808b/babylon-4-large-opt.png">View large version</a>)</figcaption></figure>

Using the resulting matrix enables us to transform 3D vertices to 2D pixels, while taking into account the point of view and everything related to the position, scale and rotation of the current object.

This is your responsibility as a 3D developer: to create and keep this matrix up to date.</p>

### Back to the Shaders

Once the vertex shader is executed on every vertex (three times, then), we will have three pixels with the correct <code>gl_position</code> and a <code>vUV</code> value. The GPU is going to interpolate these values on every pixel contained in the triangle produced with these pixels.

Then, for each pixel, it will execute the pixel shader:

<pre><code class="language-javascript">
precision highp float;
varying vec2 vUV;
uniform sampler2D textureSampler;

void main(void) {
    gl_FragColor = texture2D(textureSampler, vUV);
}
</code></pre>

### Pixel (or Fragment) Shader Structure

The structure of a pixel shader is similar to that of a vertex shader:

*   **Varying**.  Varying variables are value created by the vertex shader and transmitted to the pixel shader. Here, the pixel shader will receive a `vUV` value from the vertex shader.
*   **Uniforms**.  A uniform is a variable used by the shader and defined by the CPU. The only uniform we have here is a sampler, which is a tool used to read texture colors.
*   **Main**.  The function named `main` is the code executed by the GPU for each pixel and that must at least produce a value for `gl_FragColor` (i.e. the color of the current pixel).

This pixel shader is fairly simple: It reads the color from the texture using texture coordinates from the vertex shader (which, in turn, gets it from the vertex).

The problem is that when shaders are developed, you are only halfway there, because you then have to deal with a <em>lot</em> of WebGL code. Indeed, WebGL is really powerful but also really low-level, and you have to do everything yourself, from creating the buffers to defining vertex structures. You also have to do all of the math, set all of the states, handle texture-loading, and so on.</p>

## Too Hard? BABYLON.ShaderMaterial To The Rescue

I know what you’re thinking: "Shaders are really cool, but I do not want to bother with WebGL’s internal plumbing or even with the math."

And you are right! This is a perfectly legitimate question, and that is exactly why I created Babylon.js!

To use Babylon.js, you first need a simple web page:

<pre><code class="language-javascript">
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;Babylon.js&lt;/title&gt;
    &lt;script src="Babylon.js"&gt;&lt;/script&gt;

    &lt;script type="application/vertexShader" id="vertexShaderCode"&gt;
        precision highp float;

        // Attributes
        attribute vec3 position;
        attribute vec2 uv;

        // Uniforms
        uniform mat4 worldViewProjection;

        // Normal
        varying vec2 vUV;

        void main(void) {
        gl_Position = worldViewProjection * vec4(position, 1.0);

        vUV = uv;
        }
    &lt;/script&gt;

    &lt;script type="application/fragmentShader" id="fragmentShaderCode"&gt;
        precision highp float;
        varying vec2 vUV;

        uniform sampler2D textureSampler;

        void main(void) {
        gl_FragColor = texture2D(textureSampler, vUV);
        }
    &lt;/script&gt;

    &lt;script src="index.js"&gt;&lt;/script&gt;
    &lt;style&gt;
        html, body {
            width: 100%;
            height: 100%;
            padding: 0;
            margin: 0;
            overflow: hidden;
            margin: 0px;
            overflow: hidden;
        }

        #renderCanvas {
            width: 100%;
            height: 100%;
            touch-action: none;
            -ms-touch-action: none;
        }
    &lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;canvas id="renderCanvas"&gt;&lt;/canvas&gt;
&lt;/body&gt;
&lt;/html&gt;
</code></pre>

You’ll notice that shaders are defined by <code>&lt;script&gt;</code> tags. With Babylon.js, you can also define them in separate files (<code>.fx</code> files).

*   [Babylon.js source](https://www.babylonjs.com/babylon.js)
*   [GitHub repository](https://github.com/BabylonJS/Babylon.js)

Finally, the main JavaScript code is this:

<pre><code class="language-javascript">
"use strict";
document.addEventListener("DOMContentLoaded", startGame, false);

function startGame() {
    if (BABYLON.Engine.isSupported()) {
        var canvas = document.getElementById("renderCanvas");
        var engine = new BABYLON.Engine(canvas, false);
        var scene = new BABYLON.Scene(engine);
        var camera = new BABYLON.ArcRotateCamera("Camera", 0, Math.PI / 2, 10, BABYLON.Vector3.Zero(), scene);

        camera.attachControl(canvas);

        // Creating sphere
        var sphere = BABYLON.Mesh.CreateSphere("Sphere", 16, 5, scene);

        var amigaMaterial = new BABYLON.ShaderMaterial("amiga", scene, {
            vertexElement: "vertexShaderCode",
            fragmentElement: "fragmentShaderCode",
        },
        {
            attributes: ["position", "uv"],
            uniforms: ["worldViewProjection"]
        });
        amigaMaterial.setTexture("textureSampler", new BABYLON.Texture("amiga.jpg", scene));

        sphere.material = amigaMaterial;

        engine.runRenderLoop(function () {
            sphere.rotation.y += 0.05;
            scene.render();
        });
    }
};
</code></pre>

You can see that I use <code>BABYLON.ShaderMaterial</code> to get rid of the burden of compiling, linking and handling shaders.

When you create <code>BABYLON.ShaderMaterial</code>, you have to specify the DOM element used to store the shaders or the base name of the files where the shaders are. If you choose to use files, you must create a file for each shader and use the following pattern: <code>basename.vertex.fx</code> and <code>basename.fragment.fx</code>. Then, you will have to create the material like this:

<pre><code class="language-markup">
var cloudMaterial = new BABYLON.ShaderMaterial("cloud", scene, "./myShader",
        {
            attributes: ["position", "uv"],
            uniforms: ["worldViewProjection"]
        });

</code></pre>

You must also specify the names of attributes and uniforms that you use.

Then, you can directly set the values of your uniforms and samplers using <code>setTexture</code>, <code>setFloat</code>, <code>setFloats</code>, <code>setColor3</code>, <code>setColor4</code>, <code>setVector2</code>, <code>setVector3</code>, <code>setVector4</code>, <code>setMatrix</code> functions.

Pretty simple, right?

And do you remember the previous <code>worldViewProjection</code> matrix, using Babylon.js and <code>BABYLON.ShaderMaterial</code>. You just don’t have to worry about it! <code>BABYLON.ShaderMaterial</code> will automatically compute it for you because you’ll declare it in the list of uniforms.</p>

<code>BABYLON.ShaderMaterial</code> can also handle the following matrices for you:

*   `world`,
*   `view`,
*   `projection`,
*   `worldView`,
*   `worldViewProjection`.

No need for math anymore. For instance, each time you execute <code>sphere.rotation.y += 0.05</code>, the <code>world</code> matrix of the sphere will be generated for you and transmitted to the GPU.

See the <a href="https://www.catuhe.com/msdn/babylonjs/CYOS/step1/index.html">live result</a> for yourself.</p>

## Create Your Own Shader (CYOS)

Now, let’s go bigger and create a page where you can dynamically create your own shaders and see the result immediately. This page is going to use the same code that we discussed previously and is going to use the <code>BABYLON.ShaderMaterial</code> object to compile and execute shaders that you will create.

I used the ACE code editor for <a href="https://www.babylonjs.com/CYOS">Create Your Own Shader</a> (CYOS). It is an incredible code editor, with syntax highlighting. Feel free to <a href="https://ace.c9.io/#nav=about">have a look at it</a>.

Using the first combo box, you will be able to select predefined shaders. We will see each of them right after.

You can also change the mesh (i.e. the 3D object) used to preview your shaders using the second combo box.

The compile button is used to create a new <code>BABYLON.ShaderMaterial</code> from your shaders. The code used by this button is as follows:

<pre><code class="language-javascript">
// Compile
shaderMaterial = new BABYLON.ShaderMaterial("shader", scene, {
    vertexElement: "vertexShaderCode",
    fragmentElement: "fragmentShaderCode",
},
    {
        attributes: ["position", "normal", "uv"],
        uniforms: ["world", "worldView", "worldViewProjection"]
    });

var refTexture = new BABYLON.Texture("ref.jpg", scene);
refTexture.wrapU = BABYLON.Texture.CLAMP_ADDRESSMODE;
refTexture.wrapV = BABYLON.Texture.CLAMP_ADDRESSMODE;

var amigaTexture = new BABYLON.Texture("amiga.jpg", scene);

shaderMaterial.setTexture("textureSampler", amigaTexture);
shaderMaterial.setTexture("refSampler", refTexture);
shaderMaterial.setFloat("time", 0);
shaderMaterial.setVector3("cameraPosition", BABYLON.Vector3.Zero());
shaderMaterial.backFaceCulling = false;

mesh.material = shaderMaterial;
</code></pre>

Incredibly simple, right? The material is ready to send you three pre-computed matrices (<code>world</code>, <code>worldView</code> and <code>worldViewProjection</code>). Vertices will come with position, normal and texture coordinates. Two textures are also already loaded for you:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cf1e2c-205a-46b1-98bd-a6a859cb8466/babylon-5-amiga-large-opt.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/519e329d-7897-4e99-bb36-4b8dea083e27/babylon-5-amiga-preview-opt.jpg" alt="" width="500" height="500" /></a><figcaption><code>amiga.jpg</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/69cf1e2c-205a-46b1-98bd-a6a859cb8466/babylon-5-amiga-large-opt.jpg">View large version</a>)</figcaption></figure>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/14d47f08-2871-4367-b00f-394ad2c49cc5/babylon-5-amiga-preview-opt-84x84.jpg"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3ceb8c-8e8d-4125-95eb-bc01b48e3270/babylon-6-ref-preview-opt.jpg" alt="" width="500" height="500" /></a><figcaption><code>ref.jpg</code> (<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fd3ceb8c-8e8d-4125-95eb-bc01b48e3270/babylon-6-ref-preview-opt.jpg">View large version</a>)</figcaption></figure>

Finally, the <code>renderLoop</code> is where I update two convenient uniforms:

*   One is called `time` and gets some funny animations.
*   The other is called `cameraPosition`, which gets the position of the camera into your shaders (useful for lighting equations).</p>

<pre><code class="language-javascript">
engine.runRenderLoop(function () {
    mesh.rotation.y += 0.001;

    if (shaderMaterial) {
        shaderMaterial.setFloat("time", time);
        time += 0.02;

        shaderMaterial.setVector3("cameraPosition", camera.position);
    }

    scene.render();
});
</code></pre>

### Basic Shader

Let’s start with the very first shader defined in CYOS: the basic shader.

We already know this shader. It computes the <code>gl_position</code> and uses texture coordinates to fetch a color for every pixel.

To compute the pixel position, we just need the <code>worldViewProjection</code> matrix and the vertex’s position:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec2 uv;

// Uniforms
uniform mat4 worldViewProjection;

// Varying
varying vec2 vUV;

void main(void) {
    gl_Position = worldViewProjection * vec4(position, 1.0);

    vUV = uv;
}
</code></pre>

Texture coordinates (<code>uv</code>) are transmitted unmodified to the pixel shader.

Please note that we need to add <code>precision mediump float</code> on the first line for both the vertex and pixel shaders because Chrome requires it. It specifies that, for better performance, we do not use full precision floating values.

The pixel shader is even simpler, because we just need to use texture coordinates and fetch a texture color:

<pre><code class="language-javascript">

precision highp float;

varying vec2 vUV;

uniform sampler2D textureSampler;

void main(void) {
    gl_FragColor = texture2D(textureSampler, vUV);
}

</code></pre>

We previously saw that the <code>textureSampler</code> uniform is filled with the <code>amiga</code> texture. So, the result is the following:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dc01fa6-a933-4db9-97ab-1e4aa95c3ed2/babylon-7-capture1-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/15a81eb4-62cf-4bdf-b233-302055ccc61d/babylon-7-capture1-preview-opt.png" alt="" width="500" height="369" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/3dc01fa6-a933-4db9-97ab-1e4aa95c3ed2/babylon-7-capture1-large-opt.png">View large version</a>)</figcaption></figure>

### Black and White Shader

Let’s continue with a new shader: the black and white shader. The goal of this shader is to use the previous one but with a black and white-only rendering mode.

To do so, we can keep the same vertex shader. The pixel shader will be slightly modified.

The first option we have is to take only one component, such as the green one:

<pre><code class="language-javascript">
precision highp float;

varying vec2 vUV;

uniform sampler2D textureSampler;

void main(void) {
    gl_FragColor = vec4(texture2D(textureSampler, vUV).ggg, 1.0);
}
</code></pre>

As you can see, instead of using <code>.rgb</code> (this operation is called a swizzle), we’ve used <code>.ggg</code>.

But if we want a really accurate black and white effect, then computing the luminance (which takes into account all components) would be better:

<pre><code class="language-javascript">
precision highp float;

varying vec2 vUV;

uniform sampler2D textureSampler;

void main(void) {
    float luminance = dot(texture2D(textureSampler, vUV).rgb, vec3(0.3, 0.59, 0.11));
    gl_FragColor = vec4(luminance, luminance, luminance, 1.0);
}
</code></pre>

The <code>dot</code> operation (or <code>dot</code> product) is computed like this: <code>result = v0.x * v1.x + v0.y * v1.y + v0.z * v1.z</code>.

So, in our case, <code>luminance = r * 0.3 + g * 0.59 + b * 0.11</code>. (These values are based on the fact that the human eye is more sensitive to green.)

Sounds cool, doesn’t it?

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba8f7aa7-11ac-4ba7-bbbd-d1027e8416ee/babylon-8-capture2-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9223d8a7-7d74-4ee9-a883-5a6dfd290e04/babylon-8-capture2-preview-opt.png" alt="" width="500" height="368" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/ba8f7aa7-11ac-4ba7-bbbd-d1027e8416ee/babylon-8-capture2-large-opt.png">View large version</a>)</figcaption></figure>

### Cell-Shading Shader

Let’s move to a more complex shader: the cell-shading shader.

This one will require us to get the vertex’s normal and the vertex’s position into the pixel shader. So, the vertex shader will look like this:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec3 normal;
attribute vec2 uv;

// Uniforms
uniform mat4 world;
uniform mat4 worldViewProjection;

// Varying
varying vec3 vPositionW;
varying vec3 vNormalW;
varying vec2 vUV;

void main(void) {
    vec4 outPosition = worldViewProjection * vec4(position, 1.0);
    gl_Position = outPosition;

    vPositionW = vec3(world * vec4(position, 1.0));
    vNormalW = normalize(vec3(world * vec4(normal, 0.0)));

    vUV = uv;
}
</code></pre>

Please note that we also use the world matrix because position and normal are stored without any transformation, and we must apply the world matrix to take into account the object’s rotation.

The pixel shader is as follows:

<pre><code class="language-javascript">
precision highp float;

// Lights
varying vec3 vPositionW;
varying vec3 vNormalW;
varying vec2 vUV;

// Refs
uniform sampler2D textureSampler;

void main(void) {
    float ToonThresholds[4];
    ToonThresholds[0] = 0.95;
    ToonThresholds[1] = 0.5;
    ToonThresholds[2] = 0.2;
    ToonThresholds[3] = 0.03;

    float ToonBrightnessLevels[5];
    ToonBrightnessLevels[0] = 1.0;
    ToonBrightnessLevels[1] = 0.8;
    ToonBrightnessLevels[2] = 0.6;
    ToonBrightnessLevels[3] = 0.35;
    ToonBrightnessLevels[4] = 0.2;

    vec3 vLightPosition = vec3(0, 20, 10);

    // Light
    vec3 lightVectorW = normalize(vLightPosition - vPositionW);

    // diffuse
    float ndl = max(0., dot(vNormalW, lightVectorW));

    vec3 color = texture2D(textureSampler, vUV).rgb;

    if (ndl &gt; ToonThresholds[0])
    {
        color *= ToonBrightnessLevels[0];
    }
    else if (ndl &gt; ToonThresholds[1])
    {
        color *= ToonBrightnessLevels[1];
    }
    else if (ndl &gt; ToonThresholds[2])
    {
        color *= ToonBrightnessLevels[2];
    }
    else if (ndl &gt; ToonThresholds[3])
    {
        color *= ToonBrightnessLevels[3];
    }
    else
    {
        color *= ToonBrightnessLevels[4];
    }

    gl_FragColor = vec4(color, 1.);
}
</code></pre>

The goal of this shader is to simulate light, and instead of computing smooth shading, we will apply the light according to specific brightness thresholds. For instance, if the light intensity is between 1 (maximum) and 0.95, the color of the object (fetched from the texture) would be applied directly. If the intensity is between 0.95 and 0.5, the color would be attenuated by a factor of 0.8. And so on.

There are mainly four steps in this shader.

First, we declare thresholds and levels constants.

Then, we compute the lighting using the Phong equation (we’ll consider that the light is not moving):

<pre><code class="language-javascript">
vec3 vLightPosition = vec3(0, 20, 10);

// Light
vec3 lightVectorW = normalize(vLightPosition - vPositionW);

// diffuse
float ndl = max(0., dot(vNormalW, lightVectorW));
</code></pre>

The intensity of light per pixel depends on the angle between the normal and light direction.

Then, we get the texture color for the pixel.

Finally, we check the threshold and apply the level to the color.

The result looks like a cartoon object:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b87f06a8-cdb8-42b3-90f0-5aa8102d41cc/babylon-9-capture3-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/94f968b9-7f5f-4e6c-9e96-68b4963a554f/babylon-9-capture3-preview-opt.png" alt="" width="500" height="367" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b87f06a8-cdb8-42b3-90f0-5aa8102d41cc/babylon-9-capture3-large-opt.png">View large version</a>)</figcaption></figure>

### Phong Shader

We used a portion of the Phong equation in the previous shader. Let’s use it completely now.

The vertex shader is clearly simple here because everything will be done in the pixel shader:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec3 normal;
attribute vec2 uv;

// Uniforms
uniform mat4 worldViewProjection;

// Varying
varying vec3 vPosition;
varying vec3 vNormal;
varying vec2 vUV;

void main(void) {
    vec4 outPosition = worldViewProjection * vec4(position, 1.0);
    gl_Position = outPosition;

    vUV = uv;
    vPosition = position;
    vNormal = normal;
}
</code></pre>

According to the equation, we must compute the "diffuse" and "specular" parts using light direction and vertex’s normal:

<pre><code class="language-javascript">
precision highp float;

// Varying
varying vec3 vPosition;
varying vec3 vNormal;
varying vec2 vUV;

// Uniforms
uniform mat4 world;

// Refs
uniform vec3 cameraPosition;
uniform sampler2D textureSampler;

void main(void) {
    vec3 vLightPosition = vec3(0, 20, 10);

    // World values
    vec3 vPositionW = vec3(world * vec4(vPosition, 1.0));
    vec3 vNormalW = normalize(vec3(world * vec4(vNormal, 0.0)));
    vec3 viewDirectionW = normalize(cameraPosition - vPositionW);

    // Light
    vec3 lightVectorW = normalize(vLightPosition - vPositionW);
    vec3 color = texture2D(textureSampler, vUV).rgb;

    // diffuse
    float ndl = max(0., dot(vNormalW, lightVectorW));

    // Specular
    vec3 angleW = normalize(viewDirectionW + lightVectorW);
    float specComp = max(0., dot(vNormalW, angleW));
    specComp = pow(specComp, max(1., 64.)) * 2.;

    gl_FragColor = vec4(color * ndl + vec3(specComp), 1.);
}
</code></pre>

We already used the diffuse part in the previous shader, so here we just need to add the specular part. You can find more information about <a href="https://en.wikipedia.org/wiki/Phong_reflection_model">Phong shading on Wikipedia</a>.

The result of our sphere:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fecb1d1b-f320-4c34-8783-3173cc0d13a3/babylon-10-capture4-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/5c0a3f44-f0e9-4d62-b04e-ebcdec432dc3/babylon-10-capture4-preview-opt.png" alt="" width="" height="" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/fecb1d1b-f320-4c34-8783-3173cc0d13a3/babylon-10-capture4-large-opt.png">View large version</a>)</figcaption></figure>

### Discard Shader

For the discard shader, I would like to introduce a new concept: the <code>discard</code> keyword.

This shader discards every non-red pixel and creates the illusion of a dug object.

The vertex shader is the same used by the basic shader:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec3 normal;
attribute vec2 uv;

// Uniforms
uniform mat4 worldViewProjection;

// Varying
varying vec2 vUV;

void main(void) {
    gl_Position = worldViewProjection * vec4(position, 1.0);

    vUV = uv;
}
</code></pre>

The pixel shader on its side will have to test the color and use discard when, for instance, the green component is too high:

<pre><code class="language-javascript">
precision highp float;

varying vec2 vUV;

// Refs
uniform sampler2D textureSampler;

void main(void) {
    vec3 color = texture2D(textureSampler, vUV).rgb;

    if (color.g &gt; 0.5) {
        discard;
    }

    gl_FragColor = vec4(color, 1.);
}
</code></pre>

The result is a little funny:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4884b406-b151-4802-a648-914b4d34e0d9/babylon-11-capture5-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/e32c0085-f5d3-457c-ac84-859c1b835c95/babylon-11-capture5-preview-opt.png" alt="" width="500" height="365" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/4884b406-b151-4802-a648-914b4d34e0d9/babylon-11-capture5-large-opt.png">View large version</a>)</figcaption></figure>

### Wave Shader

We’ve played a lot with pixel shader, but I also want to let you know that we can do a lot of thing with vertex shaders.

For the wave shader, we will reuse the Phong pixel shader.

The vertex shader will use the uniform named <code>time</code> to get some animated values. Using this uniform, the shader will generate a wave with the vertices’ positions:

<pre><code class="language-javascript">
precision highp float;

// Attributes
attribute vec3 position;
attribute vec3 normal;
attribute vec2 uv;

// Uniforms
uniform mat4 worldViewProjection;
uniform float time;

// Varying
varying vec3 vPosition;
varying vec3 vNormal;
varying vec2 vUV;

void main(void) {
    vec3 v = position;
    v.x += sin(2.0 * position.y + (time)) * 0.5;

    gl_Position = worldViewProjection * vec4(v, 1.0);

    vPosition = position;
    vNormal = normal;
    vUV = uv;
}
</code></pre>

A sinus is applied to <code>position.y</code>, and the result is as follows:

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a339aa4d-068e-4b10-92b2-79b7360c5ae0/babylon-12-capture6-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/b5157299-bd4a-436f-b880-61d67b141c03/babylon-12-capture6-preview-opt.png" alt="" width="500" height="366" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a339aa4d-068e-4b10-92b2-79b7360c5ae0/babylon-12-capture6-large-opt.png">View large version</a>)</figcaption></figure>

### Spherical Environment Mapping

This one was <em>largely</em> inspired by the article "<a href="https://www.clicktorelease.com/blog/creating-spherical-environment-mapping-shader">Creating a Spherical Reflection/Environment Mapping Shader</a>." I’ll let you read that excellent article and play with the associated shader.</p>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dc00e00-3f0f-4370-a851-5af825d2a313/babylon-13-capture7-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/31f92893-6c90-4c50-81f5-a448e597c491/babylon-13-capture7-preview-opt.png" alt="" width="500" height="366" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/9dc00e00-3f0f-4370-a851-5af825d2a313/babylon-13-capture7-large-opt.png">View large version</a>)</figcaption></figure>

### Fresnel Shader

I would like to conclude this article with my favorite: the Fresnel shader.

This shader is used to apply a different intensity according to the angle between the view direction and the vertex’s normal.

The vertex shader is the same one used by the cell-shading shader, and we can easily compute the Fresnel term in our pixel shader (because we have the normal and the camera’s position, which can be used to evaluate the view direction):

<pre><code class="language-javascript">
precision highp float;

// Lights
varying vec3 vPositionW;
varying vec3 vNormalW;

// Refs
uniform vec3 cameraPosition;
uniform sampler2D textureSampler;

void main(void) {
    vec3 color = vec3(1., 1., 1.);
    vec3 viewDirectionW = normalize(cameraPosition - vPositionW);

    // Fresnel
    float fresnelTerm = dot(viewDirectionW, vNormalW);
    fresnelTerm = clamp(1.0 - fresnelTerm, 0., 1.);

    gl_FragColor = vec4(color * fresnelTerm, 1.);
}
</code></pre>

<figure><a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f6cf9a-ce08-4512-aa2f-3849c29e0f43/babylon-14-capture8-large-opt.png"><img loading="lazy" decoding="async" src="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/0b206972-bc0c-4596-859d-a2515580134f/babylon-14-capture8-preview-opt.png" alt="" width="500" height="365" /></a><figcaption>(<a href="https://archive.smashing.media/assets/344dbf88-fdf9-42bb-adb4-46f01eedd629/a5f6cf9a-ce08-4512-aa2f-3849c29e0f43/babylon-14-capture8-large-opt.png">View large version</a>)</figcaption></figure>

### Your Shader?

You are now more prepared to create your own shader. Feel free to post to the Babylon.js forum to share your experiments!

If you want to go further, here are some useful links:

*   [Babylon.js](https://www.babylonjs.com/), official website
*   [Babylon.js](https://github.com/BabylonJS/Babylon.js), GitHub repository
*   [Babylon.js forum](https://www.html5gamedevs.com/forum/16-babylonjs/), HTML5 Game Devs
*   [Create Your Own Shader (CYOS)](https://www.babylonjs.com/CYOS), Babylon.js
*   [OpenGL Shading Language](https://en.wikipedia.org/wiki/OpenGL_Shading_Language)," Wikipedia
*   [OpenGL Shading Language](https://www.opengl.org/documentation/glsl/), documentation

{{< signature "rb, al" >}}

