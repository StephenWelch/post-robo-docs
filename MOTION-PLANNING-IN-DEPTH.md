# Motion Planning

This document will go in-depth into how to drive a robot in a specific, repeatable trajectory and explain the concepts and algorithms needed to do so. It will roughly follow the same arc that my own self-learning did over the course of roughly 7 months from June 2018 to December 2018.

## Trajectories vs. Paths
A path is a sequence of waypoints for the robot to follow, while a trajectory is a sequence of time-indexed waypoints. In other words, in addition to position and any other information each waypoint has a time assigned to it. The robot is expected to be at each waypoint at this time in addition to meeting any other constraint the waypoint imposes (linear velocity, centripetal acceleration, etc.).

## Comparison of Techniques

## Basic Trajectory Following

### Velocity Control and Feedforwards

## Kinematics

## Odometry

## Simulation

## Advanced Trajectory Following

## Advanced Feedforwards

