# Joint limits

This repository contains the code for adding joint limits to the human body model.

The implementation consist of two AnyScript class templates. A low level class
generic template `KinLimitsDriver` which can add limits to any kinematic measures, and high
level class template `CreateJointLimitDrivers` which makes it easy to add
kinematic limits to all joints of Body model in the AnyBody Managed Model
Repository (AMMR).

## Usage: CreateJointLimitDrivers

Add `#include "../path/to/KinLimitsDriver_template.any"` in the beginning
of your main file. Then create the `KinLimitsDriver` class inside Main after 
the human model is included in the model:

```
#include "../path/to/KinLimitsDriver_template.any"

Main = {

  // It is important that the human model is include
  // before the JointLimit template. This is to ensure
  // that all BM statements are defined.
  #include "<ANYBODY_PATH_BODY>/HumanModel.any"


  CreateJointLimitDrivers JointLimits(
      ARM_RIGHT = BM_ARM_RIGHT,
      ARM_LEFT = BM_ARM_LEFT,
      LEG_RIGHT = BM_LEG_RIGHT,
      LEG_LEFT = BM_LEG_LEFT,
      TRUNK_NECK = BM_TRUNK_NECK
   ) = {
      // Example of changing af few of the limits
      Limits.Trunk.PelvisThoraxExtension = {-90, 90};
      Limits.Right.ElbowPronation = {-90, 90};
   }; 
      
```

If some joint should not have limits, the class accepts arguments for disabling individual joint limits. eq

```
  CreateJointLimitDrivers JointLimits(
    PELVIS_THORAX_LATERAL_BENDING = "Off"
    ... 
```

