# Rasterization

## Pixel Coordinate System

> The pixel coordinate system in Direct3D 10 defines the origin of a render target at the upper-left corner. as shown in the following diagram. Pixel centers are offset by (0.5f,0.5f) from integer locations.

https://docs.microsoft.com/en-us/windows/win32/direct3d10/d3d10-graphics-programming-guide-resources-coordinates

## Some Mathematics

[Barycentric coordinate system](https://en.wikipedia.org/wiki/Barycentric_coordinate_system)


## Line Rasterization

- Bresenham's line algorithm
- diamond-exit rasterization rule

## Triangle Rasterization

- How to draw a flat-bottom or flat-top triangle?
- How to divide an arbitrary triangle into a flat-bottom triangle and a flat-top triangle?
- top-left rasterization rule
- How to check if 3 vertices are colinear, clockwise or counter-clockwise
    - https://www.geeksforgeeks.org/orientation-3-ordered-points/
- **edge function** vs **line scanning**

## Depth Testing

## References

### Articles

https://docs.microsoft.com/en-us/windows/win32/direct3d11/d3d10-graphics-programming-guide-rasterizer-stage-rules

https://docs.microsoft.com/en-us/windows/win32/direct3d10/d3d10-graphics-programming-guide-resources-coordinates

https://fgiesen.wordpress.com/2013/02/08/triangle-rasterization-in-practice/

https://www.scratchapixel.com/lessons/3d-basic-rendering/rasterization-practical-implementation/rasterization-stage

https://github.com/ssloy/tinyrenderer/wiki/Lesson-2:-Triangle-rasterization-and-back-face-culling

### Videos

https://www.youtube.com/watch?v=9A5TVh6kPLA&list=PLqCJpWy5Fohe8ucwhksiv9hTF5sfid8lA&index=6