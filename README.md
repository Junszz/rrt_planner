# rrt_planner
This repository contains two packages. 

## Installation

Fristly, clone this repository in a catkin workspace and run the following command to build the packages:

```
catkin build

```
## Loading the map

There are a total of 4 maps avaialible in the maps library. To select the map, set the map_file arg to the corresponding file name. If no map is selected, an empty canvas will be launched.

```
roslaunch planner rrt_planner.launch map_title:=<directory of the package>/rrt_planner/mapping/maps/map1.png
```

## Mapping

The mapping package provides a minimalistic GUI to draw obstacles in a 2D environment and choose starting position and goal. Similarly, user can choose to load any of the maps otherwise an empty canvas will be provided instead.

![Map](images/map.png)


To run the mapping node:
```
roslaunch mapping mapping_node.launch map_title:=<directory of the package>/rrt_planner/mapping/maps/map1.png
```

The following parameters can be set in the launch file:

 - `map_topic (default: "/map")`: Topic where the map should be published (type: *nav_msgs/OccupancyGrid*)
 - `goal_topic (default: "/goal")`: Topic where goal should be published (type: *geometry_msgs/Pose2D*)
 - `pose_topic (default: "/pose")`: Topic where starting position should be published (type: *geometry_msgs/Pose2D*)
 - `height (default: 500)`: Height of map
 - `width (default: 500)`: Width of map
 - `resolution (default: 0.05)`: Resolution of map
 - `save_map (default: "none")`: If this parameter is set, the created map will be stored to this path 
 - `load_map (default: "none")`: If this parameter is set, map will be loaded from an image file at this path

When running the mapping node:
 - Press 'q' to quit
 - Press 's' to save and move on
 - Press numbers to the keyboard to change width of paint brush
 - Right-click to toggle between eraser and paint brush
 

## Planner

The planner package provides an implementation of the RRT algorithm.

![Path](images/path.gif)


To run the rrt planner node:
```
roslaunch planner rrt_planner_node.launch
```

The following parameters can be set in the launch file:

 - `map_topic (default: "/map")`: Topic where the map is published (type: *nav_msgs/OccupancyGrid*)
 - `goal_topic (default: "/goal")`: Topic where goal is published (type: *geometry_msgs/Pose2D*)
 - `pose_topic (default: "/pose")`: Topic where starting position is published (type: *geometry_msgs/Pose2D*)
 - `max_vertices (default: 1500)`: Maximum vertices to be added to graph after which goal search should be stopped
 - `step_size (default: 20)`: Size of steps. Bigger steps means smaller graphs but more time and vice versa
