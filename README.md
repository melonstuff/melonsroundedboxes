# Melon's Rounded Boxes
A way of rounding polygons with proper UV mapping

![this](https://i.imgur.com/HpZoXGj.png)  

# Installation
1. Download the file
2. Put it in your project
3. Modify the file to declare the local as global or use the return

# Usage
### Rounded Boxes
The primary use of this library is for creating Rounded Box polygons, you can do this very simply with `boxes.RoundedBox`

```lua
--- Expensive operation
--- Create a rounded box with a rounding of 10
--- Position of 0, 0
--- And size of 100, 100
local box = boxes.RoundedBox(10, 0, 0, 100, 100)

--- Set the draw color to red
--- And material to Material("vgui/gradient-l")
--- Then call surface.DrawPoly with the box polygon
--- Done!
surface.SetDrawColor(255, 0, 0)
surface.SetMaterial(mat_vgui_gradient_l)
surface.DrawPoly(box)
```

### Per-Vertex Rounding
This library also supports per-vertex rounding, which means, you can have a polygon which looks like the header image above.  

This is done very simply with arguments on `boxes.RoundedBox`
```lua
--- Create a rounded box with the same parameters as above
--- But also round each corner differently
--- Note: I do not recommend mixing arg#1 with the individual corner arguments, it seems to have issues I have not diagnosed
local box = boxes.RoundedBox(
  nil, 0, 0, 100, 100, --- rnd, x, y, w, h,
  10, --- Bottom left
  20, --- Top left
  30, --- Top right
  40, --- Bottom right
)

--- Now you can surface.DrawPoly here
```

### Rounded Polygons
At the core of `boxes.RoundedBox`, is a function called `boxes.RoundedPolygonUV`, this function simply rounds the vertices of a polygon individually  
This function reads a new polygon vertexdata parameter called `radius`, as seen below
```lua
--- Define a polygon
--- Notice the radius parameter on [2], this determines a vertex-specific radii
local poly = {
  {x = 0, y = 0},
  {x = 100, y = 0, radius = 15},
  {x = 0, y = 150}
}

--- Copy and round that polygon with the default radius being 10
--- And provide the bounds of the polygon, for UV purposes
local rounded = boxes.RoundedPolygonUV(poly, 10, 0, 0, 100, 150) --- Furthest right is 100, furthest down is 150

--- And now you can draw it the same as above here
```
