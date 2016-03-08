# Normal Mapping Tutorial

This program demonstrates the implementation of normal maps to produce finer lighting details.

# About

Normal maps are also textures, but instead of using the RGB value at a pixel to select the color, we use the RGB values X, Y and Z values of the normal at that point. This allows us to define different normal at for each pixel. We use this normal to do the lighting calculations. This makes the object look like it has finer details than the base geometry. One complication which arises, is that the normal in the normal map are in tangent space. The vertices we send to the GPU now also have a 3rd parameter, tangent. This should be same for all the vertices in the object. Otherwise the lighting calculation will look out of the ordinary.

In this example, we render a plane and map a texture on it and light it using the normal obtained from the normal map. Instead of passing just one texture to the GPU, we send two: the texture itself and its normal map. Inside the vertexShader, we compute a matrix using the normal, tangent and binormal to convert the point from model space to tangent space. This matrix is passed to the fragment shader. In fragment shader the normal is extracted from the normal map texture and multiplied with the toTangentSpace matrix. This gives us the normal in world space coordinate system.

Using this normal, we do the lighting calculations and display the color.
In this example, we do not pass any lighting data to the GPU. The light is a constant point at (3,3,3)
and it is created in the GPU itself.

For more on lighting consider looking at other examples such as: [Directional Light](https://github.com/igme-rit/directional-light-tutorial), [Point Lights](https://github.com/igme-rit/point-light-tutorial),
[Spot Lights](https://github.com/igme-rit/spot-light-tutorial), etc.

Use "W,A,S and D" to turn the plane vertically or horizontally.

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

Sample references the [OpenGL 4 Shading Language Cookbook](https://www.packtpub.com/game-development/opengl-4-shading-language-cookbook-second-edition), Second edition by David Wolff.
