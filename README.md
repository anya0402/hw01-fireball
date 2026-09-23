# HW 1: WebGL Fireball

## Result

<p align="center">
  <img width="800" src="fireball-img.png">
</p>
<p align="center">Live demo: https://anya0402.github.io/hw01-fireball/</p>

<p align="center">
  <img src="fireball-gif.gif" width="230"/> <img src="fireball-transition2.gif" width="230"/> <img src="blue-fireball-gif.gif" width="230"/> 
</p>

This fireball was created by displacing vertices on an icosphere using various noise functions. In the vertex shader, I first create a low-frequency, high-amplitude displacement using various sine functions, which depend on the 3D coordinates and time. Then, I add a few layers of higher-frequency, lower-amplitude noise with fractal Brownian motion (fBm). I have two layers of fBm, one to add small detailed noise to the fire, and one to add curls to the fire. For all of my displacements, I scale it relative to how "up" the normal is pointing, so that the noise only gets applied toward the top of the fireball, creating the effect of rising flames.

The color of the fireball was defined in the fragment shader. I have two colors interpolated together based on the depth of the sphere. The interpolation value also incorporates the noise values that were calculated in the vertex shader. I also have a third color that is based on the height of the fireball, so that I could tune the bottom color of the fireball. These three colors are then mixed together. On top of that, I added a small Fresnel effect to attempt a small glow. I also used an impulse function that uses cosine and time to loop, which adds some flare. 

<p align="center">
  <img src="fireball-controls2.gif">
</p>

I have three interactive variables exposed to the GUI. The first one controls the height of the flame itself. The second one controls the amount of curl the flames have. The third one is a temperature control. As the temperature increases, the flame gets whiter, and then turns blue. I implemented this by having set color values at the lowest, middle, and highest temperature values, and then interpolating between the values. 

Finally, I render the background as a quad with some fBm noise to act as smoke moving upward.

Toolbox functions used: sine, cosine, smoothstep, and impulse


## Objective
Get comfortable with using WebGL and its shaders to generate an interesting 3D, continuous surface using a multi-octave noise algorithm.


## Getting Started
- __Fork__ this repository
- Run `npm install` and `npm run dev` to set up the dependencies for this project
- Under the Github repo settings, navigate to "Build and deployment" -> "Source", and select **GitHub Actions**
- Push (or re-push) to `master`. The workflow will build your project and deploy it automatically. The project should be visible at http://username.github.io/repo-name.

## Assignment Details
- You will alter the vertex and fragment shaders used to render the Icosphere so that it looks like a fireball.
- Your vertex shader should apply a low-frequency, high-amplitude displacement of your sphere so as to make it less uniformly sphere-like. You might consider using a combination of sinusoidal functions for this purpose. We recommend a function of the form `f(x, y, z) = h` to displace your vertices along a vector, such as their surface normals.
- Your vertex shader should also apply a higher-frequency, lower-amplitude layer of fractal Brownian motion to apply a finer level of distortion on top of the high-amplitude displacement.
- Your fragment shader should apply a gradient of colors to your fireball's surface, where the fragment color is correlated in some way to the vertex shader's displacement.
- Both the vertex and fragment shaders should alter their output based on a uniform time variable (i.e. they should be animated). You might consider making a constant animation that causes the fireball's surface to roil, or you could make an animation loop in which the fireball repeatedly explodes.
- Across both shaders, you should make use of at least four of the functions discussed in the Toolbox Functions slides.

## Noise Application
View your noise in action by applying it as a displacement on the surface of your icosahedron, giving your icosahedron a bumpy, cloud-like appearance. Simply take the noise value as a height, and offset the vertices along the icosahedron's surface normals. You are, of course, free to alter the way your noise perturbs your icosahedron's surface as you see fit; we are simply recommending an easy way to visualize your noise. You could even apply a couple of different noise functions to perturb your surface to make it even less spherical.

In order to animate the vertex displacement, use time as the third dimension or as some offset to the (x, y, z) input to the noise function. Pass the current time since start of program as a uniform to the shaders.

For both visual impact and debugging help, also apply color to your geometry using the noise value at each point. There are several ways to do this. For example, you might use the noise value to create UV coordinates to read from a texture (say, a simple gradient image), or just compute the color by hand by lerping between values.

## Interactivity
Using dat.GUI, make at least THREE aspects of your demo interactive variables. For example, you could add a slider to adjust the strength or scale of the noise, change the number of noise octaves, etc.

Add a button that will restore your fireball to some nice-looking (courtesy of your art direction) defaults.

## Extra Spice
Choose one of the following options:

- Background (easy-hard depending on how fancy you get): Add an interesting background or a more complex scene to place your fireball in so it's not floating in a black void
- Custom mesh (easy): Figure out how to import a custom mesh rather than using an icosahedron for a fancy-shaped cloud.
- Mouse interactivity (medium): Find out how to get the current mouse position in your scene and use it to deform your cloud, such that users can deform the cloud with their cursor.
- Music (hard): Figure out a way to use music to drive your noise animation in some way, such that your noise cloud appears to dance.

## Submission
1. Create a pull request to this repository with your completed code.
2. Update README.md to contain a solid description of your project with a screenshot of some visuals, and a link to your live demo.
3. Submit the link to your pull request on Gradescope, and add a comment to your submission with a hyperlink to your live demo.
4. Include a link to your live site.

## Resources
- Javascript modules https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import
- Typescript https://www.typescriptlang.org/docs/home.html
- dat.gui https://workshop.chromeexperiments.com/examples/gui/
- glMatrix http://glmatrix.net/docs/
- WebGL
  - Interfaces https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API
  - Types https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Types
  - Constants https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Constants
