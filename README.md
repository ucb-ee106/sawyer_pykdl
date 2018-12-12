# sawyer_pykdl
Clone this repository into the `src` folder of your ROS workspace. After runing `catkin_make`, you will be able to import and use `sawyer_kinematics` in your code.

## Example
This example assumes you have completed the Rethink Robotics ![Workstation Setup](http://sdk.rethinkrobotics.com/intera/Workstation_Setup) exactly as written. Also, your Sawyer needs to be connected and turned on.

### Clone and make the repository
```
$ cd ~/ros_ws/src/
$ git clone https://github.com/rupumped/sawyer_pykdl.git
$ cd ~/ros_ws
$ catkin_make
```

### Start Intera
```
$ ./intera.sh
```

### Run Example Scripts
```
$ cd ~/ros_ws/src/sawyer_pykdl/scripts
$ python display_urdf.py
```

Output should be a parsed list of everything in the URDF XML file, something like:
```
joints:
- axis: None
  calibration: None
  child: torso
  dynamics: None
  limit: None
  mimic: None
  name: torso_t0
  origin:
    rpy: [0.0, 0.0, 0.0]
    xyz: [0.0, 0.0, 0.0]
  parent: base
  safety_controller: None
  type: fixed
- axis: None
  calibration: None
  child: pedestal
  dynamics: None
  limit: None
  mimic: None
  name: pedestal_fixed
  origin:
    rpy: [0.0, 0.0, 0.0]
    xyz: [0.0, 0.0, 0.0]
  parent: base
  safety_controller: None
  type: fixed
- axis: None
  calibration: None
  child: right_arm_base_link
  dynamics: None
  limit: None
  mimic: None
  name: right_arm_mount
  origin:
    rpy: [0.0, 0.0, 0.0]
    xyz: [0.0, 0.0, 0.0]
  parent: base
  safety_controller: None
  type: fixed
- axis: [0.0, 0.0, 1.0]
  calibration: None
  child: right_l0
  dynamics: None
  limit: {effort: 80.0, lower: -3.0503, upper: 3.0503, velocity: 1.74}
  mimic: None
...
```

The second example script illustrates how to access important kinematic characteristics, like the Jacobian of the Sawyer arem in its current state:
```
$ cd ~/ros_ws/src/sawyer_pykdl/scripts
$ python sawyer_kinematics.py
```

The output should be an illustration of the various functions of `sawyer_kinematics`, something like:
```
*** Sawyer PyKDL Kinematics ***

Material has neither a color nor texture
*** Sawyer Description ***

URDF non-fixed joints: 8;
URDF total joints: 23
URDF links: 24
KDL joints: 8
KDL segments: 23

*** Sawyer KDL Chain ***

* right_arm_base_link
* right_l0
* right_l1
* right_l2
* right_l3
* right_l4
* right_l5
* right_l6
* right_hand

*** Sawyer Position FK ***

[ 0.49672357 -0.25167693  0.45103778 -0.52594021 -0.50428066 -0.18977582
  0.65808286]

*** Sawyer Position IK ***

[-0.54770192 -0.36004664 -0.03120962  1.612114    0.1012133   3.45750696
 -3.88903798]

*** Sawyer Pose IK ***

[-0.92583868 -1.042773    0.46862263  1.96199766 -0.09023808  0.60272804
 -4.92797995]

*** Sawyer Jacobian ***

[[  2.52060619e-01   1.12292741e-01   2.21879462e-01  -1.57227095e-01
    9.64052001e-02  -6.78902811e-03   9.97465999e-18]
 [  4.96485145e-01  -7.49497058e-02   1.62357126e-01   9.34306516e-02
   -2.67175428e-02   6.15768724e-03   4.22838847e-18]
 [ -9.10614599e-04  -4.73462289e-01  -8.90834003e-02  -2.24016994e-01
    1.19180385e-01   1.34314877e-01  -1.38777878e-17]
 [  2.76282427e-03   5.49656703e-01   5.66521763e-01   7.52428180e-01
    4.15134230e-01   8.83985859e-01  -4.64095440e-01]
 [  4.31456700e-04   8.35388519e-01  -3.70292319e-01   5.96525201e-01
   -7.56470879e-01   4.66933911e-01   8.83625030e-01]
 [  9.99996090e-01  -1.87906422e-03   7.36163494e-01  -2.79301842e-01
   -5.05386367e-01   2.32749486e-02  -6.18241786e-02]]
...
```

That's it! You can now use `sawyer_kinematics` similarly to how it is used in `sawyer_kinematics.py` by including the following in your own scripts:
```
from sawyer_pykdl import sawyer_kinematics
```
