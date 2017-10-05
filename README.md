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

Scene Graph: 
A data structure that represents the objects in a scene, together with attributes of the objects and the modeling transformations that are applied to the objects. An image of the scene is created by traversing the scene graph data structure. A scene graph might exist only conceptually, or it might be an actual data structure in a program.

<img src="http://math.hws.edu/graphicsbook/c2/scene-graph.png" width="444" height="481" alt="">

Three.js follows this kind of hierarchical structure, and the 3D object being rendered and the properties of it, such as shape, material and color, rely on this kind of "Parent-child" relationship.

<h1>Scene, Renderer, Camera</h1>

Scene:

The three.js library is made up of a large number of classes. Three of the most basic are <i>THREE.Scene</i>, <i>THREE.Camera</i>, and <i>THREE.WebGLRenderer</i>. A three.js program will need at least one object of each type. Those objects are often stored in global variables, declared at the top of the program:

    var scene, renderer, camera;

A Scene object is a holder for all the objects that make up a 3D world, including lights, graphical objects, and possibly cameras. It acts as a root node for the scene graph. A Camera is a special kind of object that represents a viewpoint from which an image of a 3D world can be made. It represents a combination of a viewing transformation and a projection. A renderer is an object that can create an image from a scene graph.

A scene can be created as an object of type THREE.Scene using a constructor with no parameters:

    scene = new THREE.Scene();

Camera:

There are two kinds of camera, one using orthographic projection and one using perspective projection. They are represented by classes THREE.OrthographicCamera and THREE.PerspectiveCamera, which are subclasses of THREE.Camera. The constructors must specify the projection with corresponding parameters:

Orthographic Camera: 
    
    camera = new THREE.OrthographicCamera( left, right, top, bottom, near, far );
   
Perspective Camera: 
    
    camera = new THREE.PerspectiveCamera( fieldOfViewAngle, aspect, near, far );
    
The parameters for the orthographic camera specify the x, y, and z limits of the view volume, in eye coordinates—that is, in a coordinate system in which the camera is at (0,0,0) looking in the direction of the negative z-axis, with the y-axis pointing up in the view. The near and far parameters give the z-limits in terms of distance from the camera. 

<img src="http://learnwebgl.brown37.net/_images/side_view_frustum.png" width="444" height="481" alt="">

Perspective cameras are more common. The first parameter determines the vertical extent of the view volume, given as an angle measured in degrees. The aspect is the ratio between the horizontal and vertical extents; it should usually be set to the width of the canvas divided by its height. And near and far give the z-limits on the view volume as distances from the camera. For a perspective projection, both must be positive, with near less than far. Typical code for creating a perspective camera would be:

    camera = new THREE.PerspectiveCamera( 45, canvas.width/canvas.height, 1, 100 );

In this case, "canvas" holds a reference to the <canvas> element where the image will be rendered. The near and far values mean that only things between 1 and 100 units in front of the camera are included in the image. While the camera can be added to a scene, it does not have to be part of the scene graph to be used. In other words, it doesn't have to be the "children" of a particular object. However, in either case, you must define its position and orientation in 3D space.
    
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
