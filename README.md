# deimos_trials
Code for problem statements for deimos trials

First unzip all the files. (I am very sorry I included the gazebo models into my source file so I ended up with this).

Only dependencies are the turtlebot3, turtlebot3_simulations and gazebo packages(along with the usual dependencies on rosdep and roscpp).

For mapping

First run the launch file for hospital.world
Run:

export TURTLEBOT3_MODEL=burger(or any other bot)

roslaunch turtlebot3_gazebo hospital.launch

#This launches the world in gazebo with the turtlebot.

#Open a new terminal

export TURTLEBOT3_MODEL=burger(keep the same model)

roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping(runs the slam node)

#This opens rviz for us to do the mapping

#Open a new terminal

export TURTLEBOT3_MODEL=burger(same as above)

roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch(runs teleop node)

#Now you can use teleop to make the map in rviz

#When you are done

rosrun map_server map_saver -f ~/map_name(uses map server to save in home directory)

#Replace map name with any name you want. You can also save it in a different directory by including the path you want to save it at.

#My partial map is named map4


For navigation

export TURTLEBOT3_MODEL=burger(keep the same model with which you created the map)

roslaunch turtlebot3_gazebo hospital.launch

#This launches the file in gazebo

#open new terminal

export TURTLEBOT3_MODEL=burger

roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map_name.yaml(runs navigation node using the saved map)

#relace with the map name and the path the file is saved on. In case you want to use the premade partial map replace with map4.

#rviz opens. Click initial pose estimation then click and drag on the map in rviz the location and orientation(the pose) of the bot in gazebo.

#open new terminal to launch teleop node

export TURTLEBOT3_MODEL=burger

roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch(runs teleop node)

#now use teleop to align the green map being created in rviz with the premade map.

#once done terminate teleop node with ctrl+c

#now you can do autonomous navigation by pressing 2D nav goal and setting the fial pose we want the robot to achive. It will automatically navigate to the required position. It will also avoid any new obstacles created in the map such as cylinders added in the gazebo world.
