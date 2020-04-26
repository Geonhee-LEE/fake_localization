# fake_localization
A ROS node that simply forwards odometry information.

#### Description
The fake_localization package provides a single node, fake_localization, which substitutes for a localization system, providing a subset of the ROS API used by amcl.
This node is most frequently used during simulation as a method to provide perfect localization in a computationally inexpensive manner.
Specifically, fake_localization converts odometry data into pose, particle cloud, and transform data of the form published by amcl.


####  Nodes

fake_localization substitutes for a localization system, providing a subset of the ROS API used by amcl.

##### Subscribed Topics
- base_pose_ground_truth (nav_msgs/Odometry)
    - The position of the robot as published by a simulator.
- initialpose (geometry_msgs/PoseWithCovarianceStamped)
    - Allows for setting the pose of fake_localization using tools like rviz or nav_view to give a custom offset from the ground truth source being published. New in 1.1.3

##### Published Topics
- amcl_pose (geometry_msgs/PoseWithCovarianceStamped)
    - Just passes through the pose reported by a simulator.
- particlecloud (geometry_msgs/PoseArray)
    - A particle cloud used to visualize the robot's pose in rviz and nav_view.


#### Parameters
- ~odom_frame_id (string, default: "odom")
    - The name of the odometric frame of the robot.
- ~delta_x (double, default: 0.0)
    - The x offset between the origin of the simulator coordinate frame and the map coordinate frame published by fake_localization.
- ~delta_y (double, default: 0.0)
    - The y offset between the origin of the simulator coordinate frame and the map coordinate frame published by fake_localization.
- ~delta_yaw (double, default: 0.0)
    - The yaw offset between the origin of the simulator coordinate frame and the map coordinate frame published by fake_localization.
- ~global_frame_id (string, default: /map)
    - The frame in which to publish the global_frame_id→odom_frame_id transform over tf. New in 1.1.3
- ~base_frame_id (string, default: base_link)
    - The base frame of the robot. New in 1.1.3


#### Provided tf Transforms
/map → <value of odom_frame_id parameter>
    Passed on from the simulator over tf.
    
# Reference
- [ROS fake localiation package](http://wiki.ros.org/fake_localization)
