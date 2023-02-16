**How to build the projects like o3de-physics-test-scene**
1. Change o3de and o3de-extras to the latest version: o3de(`f829a0687ae271966ad063c1278df9928f2c7b2b`), o3de-extra(3aba9ad206c9acee4d9f6ee19f4c23360a899f79)
2. Follow exactly the [ROS2 Project Template](https://github.com/o3de/o3de-extras/tree/development/Templates/Ros2ProjectTemplate) step 1 and step 2. Remember to synchronize the o3de-extra folders( (${O3DE_HOME}/Projects/o3de-extras)) as the (3aba9ad206c9acee4d9f6ee19f4c23360a899f79), as referred in [this reply](https://github.com/o3de/o3de-extras/issues/121#issuecomment-1428064276)

3. Clone the project
```
git clone https://github.com/o3de/o3de-physics-test-scene.git
```
3. Register the project to o3de
```
export PROJECT_NAME=o3de-physics-test-scene
export PROJECT_PATH=/home/<user>/${PROJECT_NAME} ## or wherever your project is 
${O3DE_ENGINE}/scripts/o3de.sh register -pp $PROJECT_PATH
```
5. Enable the gems to project
```
${O3DE_ENGINE}/scripts/o3de.sh enable-gem --gem-name ROS2 --project-path $PROJECT_PATH
${O3DE_ENGINE}/scripts/o3de.sh enable-gem --gem-name WarehouseSample --project-path $PROJECT_PATH
${O3DE_ENGINE}/scripts/o3de.sh enable-gem --gem-name RosRobotSample --project-path $PROJECT_PATH
```
6. Build the project
```
cd $PROJECT_PATH
source /opt/ros/humble/setup.bash
cmake -B build/linux -G "Ninja Multi-Config" -DLY_UNITY_BUILD=OFF -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -DLY_PARALLEL_LINK_JOBS=16 -DLY_STRIP_DEBUG_SYMBOLS=OFF
cmake --build build/linux --config profile --target $PROJECT_NAME.GameLauncher Editor
```

