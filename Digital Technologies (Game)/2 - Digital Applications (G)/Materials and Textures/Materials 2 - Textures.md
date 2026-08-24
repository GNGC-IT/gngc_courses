# Materials 2 - Textures
Textures are image files that we can apply within materials, and they can greatly enhance the way objects in our scenes look.
There are plenty of different Texture Assets that we can use together in order to build a sophisticated and realistic material. I'm going to be using this [Metal Plate](https://polyhaven.com/a/metal_plate) texture from Poly Haven as an example throughout all of this guide.
![[MetalPlateBall.png|400x400]]![[MetalPlateFlat.png]]

When downloading the asset from Poly Haven, it includes 5 files by default, but there are extras that you can download as well. I'm going to stick to these five:
- _diff_ > Diffuse
- _nor_gl_ > Normal Map
- _disp_ >Displacement / Height Map
- _metal_ > Metallic
- _rough_ > Roughness

Let's take a look at their roles, and how we implement them into Godot:
## Diffuse (Albedo)
- Defines the base colour and pattern of the surface under neutral lighting
- Albedo textures are just a plain pattern, with no lighting, shadows, specular highlights, etc. These are all provided by adding in the other texture files!
- Take anything that says "Diffuse" or similar, and throw that in the Texture field for your Albedo settings
![[metal_plate_diff_4k.jpg|400x400]]]

## Normal Map
Here's where we start having fun.
- Normal maps **simulate geometry** and turns our flat texture into a fake 3D texture.
- The Normal Map image file is encoded with RGB colour values which map to our X, Y and Z direction vectors 
	- Red is X, Green is Y, Blue is Z
	- Anything showing up as Green with catch light shone from above
- They allow the light in our scene to interact realistically with our surface, without the need to actually render a 3D object!
- Add the Normal Map texture in under the "Normal Map"> Texture property
	- You can play with the Scale here too, to try and catch the light more or less depending on the asset and style you're going for!
![[metal_plate_nor_gl_4k.jpg|400x400]]]

## Displacement / Height Map
- Height Maps store geometric depth data (in greyscale) which allows us to give flat surfaces physical depth!
- In Godot, the engine uses "Parallax Occlusion Mapping" to shift texture coordinates to create the illusion of depth, again without modifying and rendering actual geometry
	- QUICK NOTE - The main trick that I am about to show below (UV1 > Triplanar) to make Textures appear neatly on any surface DISABLES HEIGHT MAPS
![[metal_plate_disp_4k.png|400x400]]]

## Metallic
- This one is fairly intuitive, it gives the material more information about which parts of the material should be more, and less metallic!
- Here, you can see this texture shows that the "sticky outtie" parts of the material should be more metallic than the flat sections beneath it!
- Add the file to the Metallic > Texture, and then adjust the Metallic 0-1 value to your liking. Maybe keep adjusting it while we implement the...
![[metal_plate_metal_4k.jpg|400x400]]]

## Roughness
- Similar rules to Metallic! Changes the roughness of specific parts of the image
- Add the file to the Roughness > Texture, and then adjust the Roughness 0-1 value to your liking. 
![[metal_plate_rough_4k.jpg|400x400]]]


### Finished Result
![[MetalPlateImplemented.png]]]


## Adjusting the texture to appear neatly
Sometimes the scale of the texture will be WAY off, and sometimes it'll just not be quite right.
In these cases, we're going to go down to the **UV1** settings and adjust the scaling!


