# ECE6397 - LLM WEB APPLICATION

Kaden Helmka; 10/04/2026

Google Gemini was used to port `demonstrations.wolfram.com/ProbabilisticRoadmapMethodIn3D/` to a standalone web application for the `Programming Assignment 1 of 2 — LLM Conversion and Critical Evaluation` assignment.

## Table of contents
1. [Failures](#falures)
2. [Successes](#successes)
3. [Revision History](#revision-history)

## Failures

The Google Gemini LLM failed in converting the following items after 1 revisions.

1. Only one viewport is present, which is used for both the robot workspace and visualizing the randomly placed points.

1. The coordinate frame of the only viewport of the points is not displayed as a box with x, y, and z becoming ($\theta_1$), ($\theta_2$), ($\theta_3$), respectively.

2. The uniformly randomly generated points are not disbursed evenly throughout the [0,2($\pi$)] coordinate frame. Rather they seems to be randomly placed on the surface of a sphere of unknown size.

2. There are no coordinate axes present to indicate size, scale, or orientation.

3. Pressing the New Random Goal destroys all previously generated nodes instead of picking new points within the current node set.

3. There are no controls for moving the origin and orientation (transform) of the robot within the world.

3. The random goal does not seem to be correctly tied to the generated nodes, rather it seems that the random goal is first generated, and then the nodes are added in later with no effect on the outcome of the demo.

3. Using the Connection Radius slider makes nodes disappear from the viewport.

3. There are no controls for moving the two obstacle spheres.

3. The solution path "arm" object does not follow the solution path. Rather, it has a "sweeping" arc motion between the pairs of solution points, with minimal bending in the arm.

4. Only one solution arm is present rather than two.

## Successes

The Google Gemini LLM succeeded in converting the following after 1 revisions:

1. The side panel does not scale corerctly with the browser window size.

2. The two obstacle spheres are about the same relative size as they were in the original Mathematica demo.

2. The colors of the two obstacles spheres are unique.

3. The "add 100 vertices" button is present and works as expected.

4. The "restart" button is present and works as expected.

7. The performance, both graphical and computational, far exceed that of the Mathematica demo. (eg. viewport movement is realtime)

8. A slider is present that allows the user to move an arm along the connecting solution path.

8. A checkbox is present to toggle the visibility of the nodes and their connections.

9. A message is present that details the world statistics and current path length (node count).

## Revision History

1. [Revision 1](#revision-1)

### Revision 1
Prompt
> please convert the mathematic project https://demonstrations.wolfram.com/ProbabilisticRoadmapMethodIn3D/ to a lightweight web application

Response
> Key Features Implemented:Interactive 3D Kinematics: A 3-DOF articulated robot arm rendered in real time inside a 3D WebGL viewport powered by Three.js.Workspace Obstacles: Sphere obstacles placed in 3D space with continuous segment-to-sphere collision checking.Probabilistic Roadmap (PRM):Sampling: Generates configuration nodes ($\theta_1, \theta_2, \theta_3$) and verifies safety.Local Planner: Evaluates straight line paths between free configurations within a user-configurable connection radius ($\Delta\theta$).A Search:* Calculates the shortest valid graph trajectory connecting the start configuration to the goal.Traversal Slider: Interactively animate the robot arm stepping through the generated solution trajectory.
