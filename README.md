<h1>About Three.js</h1>
Three.js is an Javascript library for 3D graphics. It's an open sourced project initially created by Ricardo Cabello (or "mr.doob"), and many programmers have made contributions to it.
Three.js uses the common concepts of 3D modelling, such as geometric objects, transformations, lights, materials, textures, and cameras. But it also has additional features that build on the power and flexibility of WegGL.

<h1>Libraries and Downloads</h1>
You can download the full three.js libraries and find their documentations at the main web site: <link href="http://threejs.org/">http://threejs.org 

However the full download is extremely large and contains many libraries and example files not commonly used. 
The core features of three.js are defined in a single large JavaScript file named "three.js". There is also a smaller "minified" version, three.min.js, that contains the same definitions in a format that is not meant to be human-readable.

To use three.js on a web page, you need to include one of the two scripts in a <script> element on the page. For example, assuming that three.min.js is in the same folder as the web page, then the script element would be:

<code> <script src="three.min.js"></script> </code>

<h1> Object Oriented Programming and Scene Graphs </h1>
In order to more intuitive program with Three.js, it is helpful to take a quick look at the data structure of the objects being rendered, and how it affects how we code.
<img src="http://math.hws.edu/graphicsbook/c2/scene-graph.png" width="494" height="535" alt="">
Scene Graph: 
A data structure that represents the objects in a scene, together with attributes of the objects and the modeling transformations that are applied to the objects. An image of the scene is created by traversing the scene graph data structure. A scene graph might exist only conceptually, or it might be an actual data structure in a program.


<div style="background: #272822; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #66d9ef">const</span> <span style="color: #a6e22e">WIDTH</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">400</span><span style="color: #f8f8f2">;</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">HEIGHT</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">300</span><span style="color: #f8f8f2">;</span>

<span style="color: #75715e">// Set some camera attributes.</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">VIEW_ANGLE</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">45</span><span style="color: #f8f8f2">;</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">ASPECT</span> <span style="color: #f92672">=</span> <span style="color: #a6e22e">WIDTH</span> <span style="color: #f92672">/</span> <span style="color: #a6e22e">HEIGHT</span><span style="color: #f8f8f2">;</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">NEAR</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">0.1</span><span style="color: #f8f8f2">;</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">FAR</span> <span style="color: #f92672">=</span> <span style="color: #ae81ff">10000</span><span style="color: #f8f8f2">;</span>

<span style="color: #75715e">// Get the DOM element to attach to</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">container</span> <span style="color: #f92672">=</span>
    <span style="color: #f8f8f2">document.</span><span style="color: #a6e22e">querySelector</span><span style="color: #f8f8f2">(</span><span style="color: #e6db74">&#39;#container&#39;</span><span style="color: #f8f8f2">);</span>

<span style="color: #75715e">// Create a WebGL renderer, camera</span>
<span style="color: #75715e">// and a scene</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">renderer</span> <span style="color: #f92672">=</span> <span style="color: #66d9ef">new</span> <span style="color: #a6e22e">THREE</span><span style="color: #f8f8f2">.</span><span style="color: #a6e22e">WebGLRenderer</span><span style="color: #f8f8f2">();</span>
<span style="color: #66d9ef">const</span> <span style="color: #a6e22e">camera</span> <span style="color: #f92672">=</span>
    <span style="color: #66d9ef">new</span> <span style="color: #a6e22e">THREE</span><span style="color: #f8f8f2">.</span><span style="color: #a6e22e">PerspectiveCamera</span><span style="color: #f8f8f2">(</span>
        <span style="color: #a6e22e">VIEW_ANGLE</span><span style="color: #f8f8f2">,</span>
        <span style="color: #a6e22e">ASPECT</span><span style="color: #f8f8f2">,</span>
        <span style="color: #a6e22e">NEAR</span><span style="color: #f8f8f2">,</span>
        <span style="color: #a6e22e">FAR</span>
    <span style="color: #f8f8f2">);</span>
</pre></div>
