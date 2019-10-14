# Motion Planning

This document will go in-depth into how to drive a robot in a specific, repeatable trajectory and explain the concepts and algorithms needed to do so. It will roughly follow the same arc that my own self-learning did over the course of roughly 7 months from June 2018 to December 2018.

## Trajectories vs. Paths
A path is a sequence of waypoints for the robot to follow, while a trajectory is a sequence of time-indexed waypoints. In other words, in addition to position and any other information each waypoint has a time assigned to it. The robot is expected to be at each waypoint at this time in addition to meeting any other constraint the waypoint imposes (linear velocity, centripetal acceleration, etc.).

## Comparison of Techniques
Ordered from least difficult to most difficult to implement.
Keep in mind that any method that accounts for X and Y error requires tracking the robot's position, which adds complexity.

### Pure Trajectory Following
- Converts a trajectory into a set of velocities for each side of the drivetrain to follow using PIDVA
- Successfully used by Team 195 (2018)
#### Pros
- Easiest to implement
- Onboard motor controller PIDVA running at 1000Hz makes this a feasible option
- Controls robot's velocity throughout trajectory
- Guarantees a specific heading at end of trajectory

#### Cons
- Doesn't account for X-Y error accumulated if velocity PIDVA has small errors
- Velocity PIDVA may need to be re-tuned throughout season as robot deteriorates

### X-Y PID
- PID loops use X and Y error as feedback and output throttle and turn commands
- Successfully used by Team 1114 (2018), Team 1678 (2018)

#### Pros
- Easy to implement
- Accounts for X and Y error

#### Cons
- Following waypoints, not a trajectory or path, so there's no way to predict when the robot will finish the path besides testing or simulation.
- Needs heavy tuning
- Doesn't guarantee a specific heading at end of waypoints
- How the robot moves from waypoint-to-waypoint is determined by how the PIDs are tuned, not a pre-defined trajectory

### Pure Pursuit
- Uses the Pure Pursuit algorithm to follow a pre-defined path
- Widely used outside of FRC, many resources and examples to follow
- Used successfully by Team 1806 (2018), Team 254 (2016, 2017, 2019)

#### Pros
- Easy to implement
- Accounts for X and Y error
- Easier to tune than X-Y PID, behavior is easier to understand
- Doesn't require velocity control (but you should use it)

#### Cons 
- Wonky behavior when nearing end of path
- Doesn't guarantee a specific heading at end of path

### Ramsete
- Uses the Ramsete algorithm to follow a pre-defined trajectory
- Used by Team 254 (2018) and Team 5190 (2019)

#### Pros
- Accounts for X and Y error
- Controls robot's velocity throughout trajectory
- Guarantees a specific heading at end of trajectory

#### Cons
- Hard to implement
- Complexity makes it harder to debug

## Basic Trajectory Following

### Velocity Control and Feedforwards

## Kinematics

## Odometry

## Simulation

## Advanced Trajectory Following

## Advanced Feedforwards


