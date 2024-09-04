# Gazebo Ionic Test and Tutorial Party 2024: gz-sim: Create a surface vehicle #1287 

This repo contains a modified version of ```gazebo_maritime_ws``` where I have updated the Cmake dependencies to conform to Gazebo Ionic packages. 

## Dependencies

* Install ```workspace``` from [Source Install on Ubuntu](https://github.com/gazebosim/docs/blob/master/ionic/install_ubuntu_src.md) tutorial.

* I have used a copy of the ```sydney_regatta.sdf``` to test this tutorial.

## Steps to reproduce the error

* Source ```workspace``` workspace that brings in all Gazebo Ionic packages.

```bash
cd ~/gazebo_maritime_ws
source ~/workspace/install/setup.bash
colcon build --merge-install
source ./install/setup.bash
```

* Export these variables
```bash
export GZ_SIM_RESOURCE_PATH=$GZ_SIM_RESOURCE_PATH:~/gazebo_maritime_ws/install/share/gazebo_maritime/models
export GZ_SIM_SYSTEM_PLUGIN_PATH=$GZ_SIM_SYSTEM_PLUGIN_PATH:~/gazebo_maritime_ws/install/lib
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/gazebo_maritime_ws/install/lib
```

* Launch simulator: ```gz sim -r src/gazebo_maritime/worlds/sydney_regatta_wamv.sdf```

* Error message

```shell
gz sim server: symbol lookup error: /home/az-ubuntu-2204/gazebo_maritime_ws/install/lib/libSurface.so: undefined symbol: _ZN8maritime9Wavefield18ComputeDepthSimplyERKN2gz4math2v87Vector3IdEEdd
libEGL warning: egl: failed to create dri2 screen
libEGL warning: egl: failed to create dri2 screen
libEGL warning: egl: failed to create dri2 screen
Escalating to SIGKILL on [Gazebo Sim GUI]
```

---

