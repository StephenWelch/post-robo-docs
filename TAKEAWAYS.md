# Takeaways
Takeaways from my time on the programming team.

## Logging and Graphing
It's super-valuable and a huge timesaver to be able to easily log and graph values from the robot code. This is helpful for tuning PIDs and even for debugging mechanical issues. I did this by using `ReflectingCSVWriter` to write data to a local CSV file on the RoboRIO, which I would then SCP to my computer and graph with GNUPlot. While this gives you a bit more flexibility in what is graphed (what the axes are, scale, etc.) the graphs don't update live and it takes a bit of legwork to get the CSV files from the robot to your computer. I'd recommend using [FRCGrapher](https://github.com/SumiGovindaraju/FRC-Grapher) for most applications instead.

## Constants
Tuning things both pre and during competition is a lot easier if you can update robot constants on-the-fly, rather than editing them manually and re-deploying robot code each time. Our 2019 robot code has this functionality through `NetworkTablesConstantsBase`, which allows you to read/write constants values through NetworkTables. Constants can be updated either through a tool such as Shuffleboard or through our own constants edting GUI (Which has some connection problems that need to be fixed)

## Git and Commits
You will regret every single time you cut corners with Git. Commit atomically (in as small chunks as possible) and you'll find it much easier to isolate changes that introduced a bug, see the content of pull requests at a glance, and keep your development organized.

## Feedforwards
When controlling a mechanical system on the robot, make every effort (with sacrificing simplicity) to model the behavior of the system *before* applying PID. This will make the PID easier to tune, cutting down the time it takes to integrate mechanical changes with the robot.
