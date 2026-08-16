When we're designing simple levels in Godot, we should take advantage of materials so we can help flavour our levels. This serves a few purposes:
- Plain, no colours, is boring!
- Some basic styles can help establish a general feeling and vibe for the scene; very basic storytelling
- We can use colour to our advantage, to help point our players in the right direction.

So how does Godot handle materials?
Godot's main Material type is **BaseMaterial3D**, and utilises **Physically Based Rendering**, which is a common technique across most game dev, modelling, and 3D animation engines. You can even import Blender materials into Godot!

## Material Properties
### Albedo - Base Colour
- It's the colour of the object! 
- We're going to use the rest of the settings to change how light interacts with the object, but at a fundamental level, this is **the colour**
- Use the Albedo > Color setting to change the base colour. Don't worry about the transparency setting, there's a different setting for that!

### Metallic
- This defines how metallic an object is!
- It's a property with a slider range from 0 - 1
	- **`0.0` (Non-Metal):** Plastic, painted wood, stone, skin, glass. Non-metals reflect white/neutral specular highlights regardless of the surface colour.
    
	- **`1.0` (Pure Metal):** Gold, iron, chrome, copper. Metals reflect light that is tinted by the material's **Albedo** colour.
- You can make interesting materials with settings in between the 0 - 1 values, but real world objects are rarely in between.

### Roughness
- Controls how smooth or coarse the surface is, which changes how sharp or blurry reflections appear
- Again, we have a slider range from 0 - 1
	-  **`0.0` (Smooth / Glossy):** Creates sharp, clear reflections (e.g., a polished mirror, glossy car paint, or wet ice).
    
	- **`1.0` (Rough / Matte):** Scatters light evenly in all directions, creating soft or invisible reflections (e.g., chalk, dry cloth, or unpolished stone).
- This is a really useful setting for changing material appearance, it can make a huge difference so have some fun with it.

### Emission (Emits Light)
- This setting makes the object glow.
- Enable the emission setting, change the emission colour, and adjust the Energy Multiplier.
- Mildly counterintuitiviely, this doesn't REALLY make it a light source, so it won't cast shadows, but it will show up as "bright"
	- This is mostly for making the surface look bright on a screen. (think about a TV in your scene)
	- There are settings to make it create shadows etc., but they're a bit more computationally intensive, so I'm not going to go into them here. Have a googs if you're curious!

### Transparency and Refraction (Glass and Liquid!)
- This will control how light passes through the material
- First, go back to your Albedo setting, and adjust the Alpha setting on the colour there.
- Then go to the Transparency setting and set it to "Alpha"
	- You can of course play with the other settings here, for example "Alpha Hash" gives a bit of a "Minecraft Leaves" style of transparency!
Check out my glass wall! The settings are:

|**Setting**|**Value**|
|---|---|
|**Transparency**|Alpha|
|**Albedo**|`#ffffff4a`|
|**Metallic**|`1.0`|
|**Roughness**|`0.5`|

![[GlassExample.png]]

## Handy Basic Material Reference
| Preset Material | Albedo (Hex) | Metallic | Roughness |
| :--- | :--- | :--- | :--- |
| **Polished Chrome** | `#e6e6e6` | `1.0` | `0.05` |
| **Gold** | `#ffe266` | `1.0` | `0.15` |
| **Rusted Metal** | `#5c2a18` | `0.1` | `0.85` |
| **Glossy Plastic** | `#3b82f6` | `0.0` | `0.10` |
| **Matte Chalkboard** | `#26392f` | `0.0` | `0.90` |
| **Wet Rubber** | `#1a1a1a` | `0.0` | `0.25` |