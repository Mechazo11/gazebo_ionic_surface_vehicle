# gazebo_maritime surface vehicle generation

TODO


# Commands

* Install and source ```workspace``` from [Source Install on Ubuntu](https://github.com/gazebosim/docs/blob/master/ionic/install_ubuntu_src.md) tutorial.

* Source that workspace ```source ~/workspace/install/setup.bash``` and test. Run this command ```gz sim --version``` and the following output should come out

```bash
Gazebo Sim, version 9.0.0~pre1
Copyright (C) 2018 Open Source Robotics Foundation.
Released under the Apache 2.0 License.
```

* Downloand and unzip the ```gz_maritime_ws```
```bash
wget https://raw.githubusercontent.com/gazebosim/gz-sim/gz-sim8/tutorials/files/surface_vehicles/gz_maritime_ws.zip -O ~/gz_maritime_ws.zip

unzip ~/gz_maritime_ws.zip
```

* Build and source ```gz_maritime_ws```
```bash
cd ~/gazebo_maritime_ws
colcon build --merge-install
```

* Export some variables