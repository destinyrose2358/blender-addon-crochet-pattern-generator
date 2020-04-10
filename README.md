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

  * Calculate planes (assign splitting_planes) that bisect neighboring axes
  * Calculate the intersection of the model and splitting_planes (assign seams)
  * Section out the part of the model between every 2 neighboring seams, and store them in an object that uses the first seam as the index (assign sections)
  * Iterating over sections (assign section):
   * Assign the first seam to current_row_edges
   * Assign the splitting_plane that touches the first point of this sections axis to prev_row_edges
   * While current_row_edges has content:
    * Calculate a new model
     * Assign possible_stitch_spaces
     * It uses the union of
      * Half cylinders with each edge as a center line
      * Half spheres centered on each vertex
      * None of these half-shapes being in between the prev_row_edges and current_row_edges
   * Push prev_row_edges onto all_row_edges
   * Calculate the intersection of possible_stitch_spaces and section then:
      * Assign to new_row_edges
      * Assign prev_row_edges, current_row_edges = current_row_edges, new_row_edges
