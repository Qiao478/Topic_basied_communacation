# Topic_basied_communacation
一、流程简介
1.编写发布方实现
2.编写订阅方实现
3.编辑配置文件
4.编译
5.执行

从终端进入ws01_plumbing文件夹下的src：cd src
在src下建立功能包：ros2 pkg create cpp01_topic --build-type ament_cmake --dependencies rclcpp std_msgs base_interfaces_demo --node-name dem01_taker_str
