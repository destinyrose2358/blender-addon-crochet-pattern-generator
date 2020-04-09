# Crochet Pattern Generator
This is a Blender addon that generates a in-the-round crochet pattern from a model.

## Algorithm Outline

### Variables Given

* Axes - a group of edges that describes the axes of a crochet project (the line that the project rotates on)
* Starting Stitch Plane - a plane that shares an edge with one of the axes and represents the line of starting stitches
* Minimun Stitch Width - the minimum width that a stitch can be
* Maximum Stitch Width - the maximum width that a stitch can be
* Stitch Heights - the heights that a stitch can be
  *  The widths and heights can be calculated by creating a sampling of the yarn intended to be used

### Steps

  * Calculate planes (assigned splitting_planes) that bisect neighboring axes
  * Calculate the intersection of the model and splitting_planes (assigned seams)
  * Sweeping smoothly from seam to seam (assign plane as current_ring):
    * Calculate the intersection of the model, current_ring, and the set of points stitch heights can reach from prev_ring (assigned at the end of each iteration)
  
