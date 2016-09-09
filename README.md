# Obj Loading Tutorial

This program demonstrates loading of obj model files to render them in a scene

# About

This example rebuilds a lot of the code the has been established through the teapot examples. There are two main points to this example. The first is obj file loading. While obj files are fairly simple in their format, making them into actual meshes that you can render is a bit of a chore. The second point is the use of uniform buffer objects. Up to this point we have been using uniform variables for passing data to the shader from the main code. While this technically works, it is still poor coding standards to do so as it is less flexible and less efficient than packaging uniform values pertaining to a particualar source into their own buffer. One important property of these uniform buffers is that a single buffer can be accessed by multiple shaders referencing the same binding point.

There are 5 static component classes that make up the base functionality for this example:

1. RenderManager
  - This class maintains the display list for the scene being rendered and thus handles the processes of updating and drawing all of the RenderObjects that have been instantiated in the scene.
2. CameraManager
  - This class maintains data relating to the view and projection matrices used in the rendering pipeline. It also handles updating this data based on user input.
3. InputManager
  - This class maintains data for the current state of user input for the mouse and keyboard.
4. LightingManager
  - This class maintains data for an array of eight lights, each posessing a trasform, color and power, handles the updating thereof and maintains gpu-side buffers reflecting this data for use in the shaders.
5. ResourceManager
  - This class maintains all the data from external sources necessessary to run the program. In this instance, this includes obj loading, parsing, and storage, vao, vbo, and ebo generation and storage, shader loading, compiling and linking, and uniform buffer object generation, binding and storage.

RenderObject
  - Tracks the instance of an object that can be drawn to the screen. Contains data for transforms, a mesh, a shader, drawing mode (eg triangles, lines), and a layer. The layer is a value that can be used to mask certain objects from a draw call. The object has a layer which is some power of 2 and then there is a mask for the draw call which is a 32 bit number. A bit-wise & between these numbers decides whether or not the object in question is drawn.

SHADERS
  - Now use uniform buffer objects for receiving uniform data.

- vShader.glsl
  - Through shader, nothing fancy
- fShader.glsl
  - Applies a phong lighting model based on the data sent from the lighting manager, functions the same as the phong shader from the geometric lighting improved example.

# Setup

In order to setup, run the following in a shell, then open the project in your preferred editor. Windows setup has been configured for use with Visual Studio.

Windows:
```
cd path/to/folder
setup.cmd
```
Linux:
```
cd path/to/folder
./setup
```

# Credits

More information on uniform buffer objects can be found here: https://www.opengl.org/wiki/Uniform_Buffer_Object
