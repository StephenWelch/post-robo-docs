# Motion Planning

As you probably already know, I spent the greater part of my last year on 1885 working on integrating and understanding Team 254's trajectory generation and trajectory following code. I'm writing this document in order to give you an idea of the process I went through to do that, starting with literally zero knowledge of the topics at hand.

## Why?
I originally started working on this for two reasons:
- I thought it would make our robot more competitive in autonomous, where our performance seemed unreliable at best.
- I thought it was crazy cool.

## 2018

### Early 2018
I started in early 2018 working on generating and following pre-generated motion profiles using the [Pathfinder library](https://github.com/JacisNonsense/Pathfinder). It worked okay, but wasn't tested enough by stop build day to use during competition. Still, I learned a lot about the fundamentals of high-frequency control, velocity control with PID, and got experience integrating trajectory following with our robot code.

### Late 2018
After the performance of teams such as 1731, 846, and 1806 during the 2018 season (all of whom based their auto code off of 254) as well as 254 themselves, I started working on understanding why 254's robot performed so well in autonomous that season. I started off by looking at [this](https://www.dis.uniroma1.it/~labrob/pub/papers/Ramsete01.pdf) paper, which 254 had based their trajectory following code on. 

This paper, known for short as Ramsete, lays out a set of four equations which take as input the robot's position and a desired trajectory, then output angular and linear velocity commands which steer the robot along the trajectory. I realized that the first thing I had to do was understand how to determine the robot's (x, y) position, which I did by reverse-engineering 254's `RobotStateEstimator`, `Kinematics`, and `Twist2d` classes. These classes manage tracking a robot's position in 2d space and allow us to convert from a linear and angular velocity to the left and right velocity of the wheels. 

I ended up replicating (and sometimes outright stealing) this code and adapting it to determine the position of the robot on the field using log data. I did this by parsing the left and right position readings from our 2018 DCMP logs and feeding it through the previously mentioned code, generating a set of (x, y) points that clearly corresponded to our robot's path on the field during autonomous.

I then moved on to implementing the actual Ramsete equations. Since I didn't have an actual robot to work with, I built a simulation of a robot following a trajectory. The trajectory for the robot to follow was generated using the Pathfinder library, then fed through Ramsete, which took in information about the desired trajectory point we wanted to be at (x, y, angle, velocity) as well as the robot's current (x, y) position. The resulting linear and angular velocities from Ramsete were converted to left and right wheel velocities, which were then integrated to find wheel displacement, which was then used to find the robot's (x, y) position. This position was then fed back into Ramsete and so on and so forth.

After school started, I started working with an actual robot. In order to follow commanded left/right velocities, I had to rewrite our drivebase code so that it would support the special kind of velocity commands that our trajectory-following code would output. The trajectory following code itself was just 254's code modified for readability and structural reasons. I decided against re-writing this code for a couple of reasons:
- I knew their code was competition-tested already - I wouldn't have to spend time to debug it
- I felt that I had a decent understanding of how their code worked
- It was already integrated with their crazy-fast trajectory generation library - writing the trajectory follower from scratch meant I would either have to interface with it or just use pre-generated trajectories from Pathfinder.
It took me a really, really long time to get everything to work correctly - far past my target date of October 26th and into December. The challenge was determining where the root of problems were, working out bugs, and especially isolating errors in motor controller configuration. To do that, I logged data to CSV files on the RIO which I would `scp` to my laptop and plot with GNUPlot.

I finally got to a working version by the beginning of January, in time for competition season. We didn't end up using it during competition - but that's a whole different story.


