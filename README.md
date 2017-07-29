# imu_filter

This is a project that uses IMU filter algorithm in ROS(Robot Operating System). The IMU I use is ICM 20602, consisting of a tri-axis gyroscope and a tri-axis accelerometer.

# ROS API  
# Subscribed Topics
imu0(sensor_msgs/Imu) 

    Message containing raw IMU data, including angular velocities and linear accelerations.   
# Published Topics
quaternion(geometry_msg/QuaternionStamped)</br>
ypr(geometry_msgs/Vector3Stamped)  

    The fused pose representation.
# Parameters
Dynamically Reconfigurable Parameters</br>
(Mahony_filter)  twoKp, twoKi</br>
(Madgwick_filter) beta  

    After run the node, you can input "rosrun rqt_configure rqt_reconfigure" to tune the dynamic parameters.
    According to Madgwick's thesis, the suggested beta = sqrt(3.0f / 4.0f) * gyroMeasError. 
    ICM20602's gyroscope sensitivity erroris ±1%. Thus the default beta is setting to 0.1088.
    As the specific application, the value can be tuned accoring to response and requriments.
Not Dynamically Reconfigurable Parameters </br>
sampleFreq(float, default: 400.0)</br>
Such as: rosrun filter Madgwick_filter _sampleFreq:=200
# provied tf Transforms
odom -> imu  
![Alt Text](git@github.com:marooncn/imu_filter.git.Screenshot from 2017-07-29 10-49-16.png)
    So you can open rviz and set the fixed frame "odom", add TF then you can use it to verify the effect directly.
# Result
The Madgwick_filter node's effect is acceptable, but the Mahony_filter is disappointing.

