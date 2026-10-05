# ECE6397 - LLM WEB APPLICATION

Kaden Helmka; 9/20/2026

Google Gemini was used to port `demonstrations.wolfram.com/ProbabilisticRoadmapMethodIn3D/` to a standalone web application for the `Programming Assignment 2 of 2 — LLM Conversion and Critical Evaluation` assignment.

## Table of contents
1. [Failures](#falures)
2. [Successes](#successes)
3. [Revision History](#revision-history)

## Failures

The Google Gemini LLM failed in converting convert the following items after 5 revisions. 

1. The coordinate frame of the points is not displayed as a box with x, y, and z becoming ($\theta_1$), ($\theta_2$), ($\theta_3$), respectively.

2. The uniformly randomly generated points are not disbursed evenly throughout the [0,2($\pi$)] coordinate frame. Rather they seems to be randomly placed on the surface of a sphere of unknown size.

2. There are no coordinate axes present to indicate size, scale, or orientation.

3. There are no controls for moving the origin and orientation (transform) of the robot within the world.

3. The solution path "arm" object does not follow the solution path. Rather, it has a "sweeping" arc motion between the pairs of solution points, with minimal bending in the arm.

4. Only one solution arm is present rather than two.

5. There is a slider for the connection radius, which seems to be incorrectly tied to the number of points being generated. It does, however, correctly fail attemps when no valid solutions are present with the given connection radius.

6. Only one viewport is present, which is used for both the robot workspace and visualizing the randomly placed points.

## Successes

The Google Gemini LLM succeeded in converting the following after 5 revisions:

1. The application contains viewport gizmo controls for very easily and quickly manipulating the two obstacle spheres.

2. The coordinate frame (as visible from the above gizmo controls) is right handed.

2. The two obstacle spheres are about the same relative size as they were in the original Mathematica demo.

2. The algorithm correctly avoids the obstacles and ensures that a new path is found (if possible) whenever the obstacles are moved.

3. The "add 100 vertices" button is present and works as expected.

4. The "restart" button is present and works as intended.

5. The "New Random Goal" button works as expected, without resetting the initially randomly generated nodes.

6. The path solving algorithm is rerun and new solution is automatically found whenever any of the above controls are used.

7. The performance, both graphical and computational, far exceed that of the Mathematica demo. (eg. viewport movement is realtime)

8. A control is presnt to hide/unhide the nodes and final solution path.

9. A message is present that details the world statistics and current path length (node count).

## Revision History

1. [Revision 1](#revision-1)
2. [Revision 2](#revision-2)
3. [Revision 3](#revision-3)
4. [Revision 4](#revision-4)
5. [Revision 5](#revision-5)

### Revision 1
Prompt
> please convert the mathematic project https://demonstrations.wolfram.com/ProbabilisticRoadmapMethodIn3D/ to a lightweight web application

Response
> Key Features Implemented:Interactive 3D Kinematics: A 3-DOF articulated robot arm rendered in real time inside a 3D WebGL viewport powered by Three.js.Workspace Obstacles: Sphere obstacles placed in 3D space with continuous segment-to-sphere collision checking.Probabilistic Roadmap (PRM):Sampling: Generates configuration nodes ($\theta_1, \theta_2, \theta_3$) and verifies safety.Local Planner: Evaluates straight line paths between free configurations within a user-configurable connection radius ($\Delta\theta$).A Search:* Calculates the shortest valid graph trajectory connecting the start configuration to the goal.Traversal Slider: Interactively animate the robot arm stepping through the generated solution trajectory.

### Revision 2

Prompt:
> 1. edit the file such that the user may edit the positions of the obstacles.
> 2. the positioning of the nodes should be random within a box, not a sphere

Response:
> Here is the updated full-featured web application.Key Updates:Interactive Box Obstacles & Position Controls:The obstacles have been updated to 3D Boxes / Rectangular Prisms instead of spheres.Slider controls added in the UI allow adjusting the X, Y, and Z positions of both the Blue and Yellow obstacles dynamically in real time.Box-Based Random Node Sampling:Sampled configurations ($\theta_1, \theta_2, \theta_3$) are generated uniformly within a 3D configuration-space box domain ($\theta_1 \in [-\pi, \pi]$, $\theta_2 \in [0, \pi]$, $\theta_3 \in [-\pi/2, \pi/2]$).Collision detection uses exact Oriented Bounding Box (OBB) vs. Line Segment intersections to ensure accuracy against the rectangular obstacles.Save the code below as an .html file and open it in any browser:

### Revision 3

Prompt
> 1. pressing new goal should not delete all the points, rather it should just create a new point and run the algorithm again
> 2. make the nodes in space within a bounding box not a sphere
> 3. make the nodes in space better visible

Response
> Here is the updated single-file web application incorporating all three requirements:Preserve Existing Vertices on "New Goal": Clicking New Goal now only generates and appends a new target configuration (and updates index 1 / goal node) without wiping or resetting the sampled vertices. It then instantly re-runs the local planner and A* graph solver.Bounding Box Sampled Nodes in Space: The random sampling generates vertices uniformly within a configuration-space box domain $(\theta_1 \in [-\pi, \pi]$, $\theta_2 \in [0, \pi]$, $\theta_3 \in [-\pi/2, \pi/2])$.Enhanced Node Visibility:Every graph node (free and obstacle-collision states) is explicitly rendered as a 3D sphere object at the end-effector position in workspace.Green spheres represent valid/collision-free configurations, red spheres represent invalid/obstacle configurations, blue sphere marks the start state, and gold sphere marks the target goal state.Distinctive thick graph edge connections and path lines ensure high visibility and clarity against dark or bright backgrounds.

### Revision 4

Prompt
> 1. the nodes should be randomly placed within a box, not on the surface of a sphere

Response
> Here is the updated code.What was changed:Workspace Point Placement (Box Bounding Box vs Sphere Surface):Previously, the sampled configuration parameters ($\theta_1, \theta_2, \theta_3$) caused end-effector workspace coordinates to form spherical arcs.Now, nodes are directly generated randomly inside a 3D rectangular box domain in workspace coordinates ($X, Y, Z \in [-2.2, 2.2] \times [0.2, 3.2] \times [-2.2, 2.2]$).Inverse Kinematics (IK) calculates valid configuration angles $(\theta_1, \theta_2, \theta_3)$ for each sampled workspace point inside the box, ensuring that nodes are uniformly distributed throughout a 3D spatial box region rather than clustered on spherical surfaces.

### Revision 5

Prompt
> 1. make the two box obstacles into two sphere obstacles
> 2. add gizmos to the two sphere obstacles so that the user can more easily move the obstacles around
> 3. the nodes are still randomly placed on the surface of a sphere. make the nodes be randomly distributed within a box

Response
> Here is the updated single-file web application incorporating all three requirements:Sphere Obstacles: Reverted the obstacles back to spheres.Interactive 3D Gizmos (TransformControls): Added interactive 3D translation gizmos directly attached to each obstacle sphere in the 3D scene. You can drag the X, Y, Z arrows directly in the viewport to move obstacles (the sidebar sliders sync automatically in real time).Box Domain Node Sampling: Sampled PRM vertices are generated strictly uniformly within a 3D rectangular box volume in configuration space ($\theta_1 \in [-\pi, \pi]$, $\theta_2 \in [0, \pi]$, $\theta_3 \in [-\pi/2, \pi/2]$) rather than being placed on spherical surfaces.
