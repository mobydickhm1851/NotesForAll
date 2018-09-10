# ROS NOTE     
###### Sep 2018 LiuYC at SOLab
## ROS Launch Files
### __Using of namespace__
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
