# ROS NOTE     
###### Sep 2018 LiuYC at SOLab

## ROS Package 
### ROS Package Installation
 - If after installation (sudo apt-get install-<distro>-package-name or from source) but the package can't be found:
   - make sure to source `/path/to/catkin_ws/devel/setup.bash` again (you'll have to do this after every package addition / removal)
   - run `__rospack profile__` to force an update of the package cache that roscd uses

## ROS Launch Files
### __Use of namespace__
  The following launch node is in __move_base__ navigation package.
  ```
  <node pkg="move_base" type="move_base" name="move_base" machine="c2">
    <remap from="odom" to="pr2_base_odometry/odom" />
    <param name="controller_frequency" value="10.0" />
    <param name="footprint_padding" value="0.015" />
    <param name="controller_patience" value="15.0" />
    <param name="clearing_radius" value="0.59" />
    <rosparam file="$(find 2dnav_pr2)/config/costmap_common_params.yaml" command="load" ns="global_costmap" />
    <rosparam file="$(find 2dnav_pr2)/config/costmap_common_params.yaml" command="load" ns="local_costmap" />
    <rosparam file="$(find 2dnav_pr2)/move_base/local_costmap_params.yaml" command="load" />
    <rosparam file="$(find 2dnav_pr2)/move_base/global_costmap_params.yaml" command="load" />
    <rosparam file="$(find 2dnav_pr2)/move_base/navfn_params.yaml" command="load" />
    <rosparam file="$(find 2dnav_pr2)/move_base/base_local_planner_params.yaml" command="load" />
  </node>

  ```
  Note the line `<rosparam file="$(find 2dnav_pr2)/config/costmap_common_params.yaml" command="load" ns="global_costmap" />`
  , with the `ns="global_costmap"`, parameter in _costmap_common_params.yaml_ will have the name of __move_base/global_costmap/parameter_name__ .
  <br/>See [ros wiki page for more info][1].
  
  
  
  
  
  
  [1]:http://wiki.ros.org/ROS/Tutorials/Roslaunch%20tips%20for%20larger%20projects
