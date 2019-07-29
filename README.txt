Documentation Author: Niko Procopi 2019

This tutorial was designed for Visual Studio 2017 / 2019
If the solution does not compile, retarget the solution
to a different version of the Windows SDK. If you do not
have any version of the Windows SDK, it can be installed
from the Visual Studio Installer Tool

Welcome to the Multiple OBJs Tutorial!
Prerequesites: Object Loading

When we load multiple different OBJs, each one should have
their own seperate VAO, VBO, and array of vertices, array
of indices, etc. In ResourceManager::Init, we call LoadOBJ 
for each object.

Inside LoadOBJ, each object loaded is given its own Mesh
class (or struct in this case). The Mesh structure
is created inside ResourceManager.h, and each Mesh has 
everything that an object would need:

struct Mesh
{
	GLuint vao;
	GLuint vbo;
	GLfloat* vertexBuffer;
	GLint vertexBufferSize;
	GLuint ebo;
	GLint* elementBuffer;
	GLint count;
};

In main.cpp's InitScene, the position and scale can be
set for every object in the scene.

RenderManager::Draw draws all of the objects. This
tutorial uses renderlists to handle how each object
is drawn. Truthfully we need to redo this tutorial to 
make it more like all the other tutorials, we'll do that
soon.
