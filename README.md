# Topic_basied_communacation
一、流程简介
1.编写发布方实现
2.编写订阅方实现
3.编辑配置文件
4.编译
5.执行

从终端进入ws01_plumbing文件夹下的src：cd src
在src下建立c++功能包：ros2 pkg create cpp01_topic --build-type ament_cmake --dependencies rclcpp std_msgs base_interfaces_demo --node-name dem01_taker_str
在src下建立python功能包：ros2 pkg create py01_topic --build-type ament_python --dependencies rclpy std_msgs base_interfaces_demo --node-name dem01_taker_str_py

C++
1.发布方实现：编辑dem01_taker_str.cpp文件
2.订阅方实现：在cpp01_topic的src目录下新建dem02_listener_str.cpp文件
3.编辑配置文件:
编写完dem02_listener_str文件后修改CMakeLists.txt文件修改内容如下：
（1）复制add_executable(dem01_taker_str src/dem01_taker_str.cpp)，并将复制的内容修改为add_executable(dem02_listener_str src/dem02_listener_str.cpp)，再重新粘贴回原add_executable(dem01_taker_str src/dem01_taker_str.cpp)下面
（2）复制ament_target_dependencies(
  dem01_taker_str
  "rclcpp"
  "std_msgs"
  "base_interfaces_demo"
)
并将复制内容修改为
ament_target_dependencies(
  dem02_listener_str
  "rclcpp"
  "std_msgs"
  "base_interfaces_demo"
)
，再重新粘贴回原文下面
（3）在install(TARGETS dem01_taker_str
  DESTINATION lib/${PROJECT_NAME})中的
  dem01_taker_str后面空格加入dem02_listener_strinstall
  即修改完后的内容为
  install(TARGETS dem01_taker_str dem02_listener_str
  DESTINATION lib/${PROJECT_NAME})
  保存
4.编译colcon build --packages-select cpp01_topic
配置环境变量：. install/setup.bash
5.执行：
先执行发布方，再执行订阅方

python 
1.发布方实现：编辑dem01_taker_str_py.py文件
2.订阅方实现：在py01_topic的src目录下新建ddem02_listener_str_py.py文件
3.编辑配置文件
把setup.py文件夹下的'dem01_taker_str_py = py01_topic.dem01_taker_str_py:main'，复制一行，修改为'dem02_listener_str_py = py01_topic.dem02_listener_str_py:main'再粘贴到原文的下方，即改后为
entry_points={
        'console_scripts': [
            'dem01_taker_str_py = py01_topic.dem01_taker_str_py:main',
            'dem02_listener_str_py = py01_topic.dem02_listener_str_py:main'
        ],


