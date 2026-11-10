# Bipod Mod Guide

> Source: https://mod.io/g/pavlov/r/mod-bipod-guide
> Author: DarkAtツ | Added: 2024-05-26 | Updated: 2024-06-01 | Views: 770 | Comments: 2 | Tags: Bipods, Gun
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 2 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: A guide on how to use the Bipod Mod and how to add Bipod-Support to your custom weapons. WIP

---
### WIP

A guide on how to use the Bipod Mod and how to add Bipod-Support to your custom weapons.

### Spawn Mounted Weapons

#### (World) BP_MountedWeaponSpawner

#### (Actor) CMP_MountedWeaponSpawner

#### (Code) FL_MountedWeaponSpawner/Spawn Mounted Weapon

### Add Bipod Support to Custom Weapons

#### Read/Create RecoilCurves

                1. Place or spawn the BP_ReadRecoil in a map.

                2. Disable Virtual Stock ingame if you have that checked in the Game Settings.

                3. Ingame press B to open the ReadRecoil UI. Note: Opening/Closing the UI fast can possibly freeze your game. If that happens you need to restart your game.

                4. Make sure that you have a high FPS value. (displayed at the top right)

                    If the FPS are 9 or 10 or just low in general, close the UI , wait a moment, press B to open the UI again. This should fix it.

                5. Set the SampleFrequency to a value that your pc can handle. You can orient the value on the FPS.

                    If you leave the SampleFrequency at 0.005 you need to have at least 200 FPS at ALL times.

                    Going lower than 0.005 is not really needed & gives no real benefit.

                    If you have less than 200 FPS you can calculate the value by using your min FPS value that you have by all times: 1/MinFPS

                    0.01 would be a good value if you have at least 100 FPS at all times.

                    Realistically speaking if you have less FPS than 100 something is wrong.

                6. Enter the WeaponID of your gun. You can uncheck TwoHanded if you want to read the recoil when the gun is not gripped by two hands, this is pretty much never needed.

                    Optionally adjust the Samples value to create the recoil curve from more samples. Having a value of 1 is fine. More will even out the curve more but might not give an as accurate result.

                7. Click on Start and wait until the Log on the right side says Finished.

                8. Select and Copy the Rotational Recoil Curve displayed in the bottom middle right.

                9. In Unreal Engine create a CurveVector. *Miscellaneous/Curve/CurveVector*

                10. Open the CurveVector and select X,Y and Z on the left. Now paste the data copied before in there. Make Sure that it pasted all 3 curves correctly to XYZ and save the CurveVector.

                Note: Make sure to close the ReadRecoil UI before leaving the Map/Server. If you dont you need to restart the game if you want to continue doing anything in Pavlov in that session.

#### Setup Bipod Component

                Also look at the Examples from the Source Plugin.

                1. Add the BipodComponent to your gun bp.

                2. Add following code to the gun:

                  
![image](images/mod-bipod-guide/8b1567fa38.jpg) <!-- src: https://image.modcdn.io/members/7c1e/5313379/profile/screenshot2024-05-30164038.jpg -->

                3. Click on the BipodComponent and check the BipodComponent/Setup/Mounted/Mounted Setup variable.

                4. Look below and set the rest of the variables. Setup/Self in the BipodComponent can be ignored, dont change anything there.

##### Default

                    Bipod Bone:

                            Enter the name of the Bipod Bone, which should be used as the pivot point when the gun is deployed/mounted.

                            If your gun has no Bipod Bone that can be used for this leave this untouched.

                    Gun Rotation Limit (Yaw):

                            How far can the gun horizontally rotate? Values in degrees.  X = Min Value, Y = Max Value

                    Gun Rotation Limit (Pitch):

                            How far can the gun vertically rotate? Values in degrees. X = Min Value, Y = Max Value

                    Bipod Length:

                            How long is the distance from the bipods pivot point to the floor when deployed? The value would be the *Adjacent* and the length of the bipod leg itself the *Hypotenuse*.

                    Bipod Offset:

                            Manually set the pivot point for when the gun is deployed/mounted here. If a value is set it will always use this value instead of calculating the offset itself using the Bipod Bone.

                    Max Distance to Grip:

                            How far can the actual controller of the player be measured from the grip to either undeploy the bipod or ungrib the mounted weapon. Unit= UnrealUnits/cm

                    Useable by Driver:

                            Can a driver of the vehicle use this Mounted weapon? Should be mainly checked/used for testing.

                    Hide Bipod Bone:

                            Should the Bipod Bone if set be hidden? Note: It works by scaling the Bipod Bone to 0. Attached objects will also be 0 here.

                    Static Bipod:

                            Is the bipod of the gun from a static type? (Bipod (legs) have no movement/are fixed) If yes check this.

##### Gun

                    Override ABP:

                            Optionally override the guns ABP class on runtime.

                   * *Firerate:

                            Enter the Fire Rate of your Gun here. (copy paste it from your gun bp) Value needs to be the time of how long one shot needs to be fired. 60 divided by RoundsPerMinute(RPM)

                    Never Destroy for Inactivity:

                            Match this to the Nerver Destroy for Inactivity value of your gun. If its checked in your gun check it here too. If its not checked in your gun dont check it here.

##### Recoil

                    Rotational Recoil Curve:

                            Select the Rotational Recoil Curve here which you created before.

                    Rotational Recoil Scale:

                            Scale the Rotaitonal Recoil Curve here. 1 = 100%/full recoil and 0 = 0%/no recoil

                            X should be 0 as the roll is currently not being used.

                            Y is the Vertical recoil and is by default at 25% (0.25) -> 75% vertical recoil reduction

                            Z is the Horizontal recoil and is by default at 10% (0.1) -> 90% horizontal recoil reduction

##### BulletSpray - No clue how works exactly right now lol, cant remember

                    Spray Curve:

                    Default Bullet Spray:

                    Bullet Spray Scale:

##### Manual

                    Allow Manual Deployment:

                            Should the gun be manually deployable?

                    Bipod Max Ground Angle:

                            How high can the angle of the surface to which the bipod wants to attach to be? If the angle is greater than the given value it wont attach to that surface.

                    Bipod Trace Channels:

                            Which Trace Channels should the BipodComponent use to trace for surfaces when deploying? This setting can be leaved as it is pretty much always.

##### Mounted

                    Mounted Setup:

                            Has the gun the code to support mounting? Check this when adding the code required to support mounting.

                    Allow Mounting:

                            Should the gun be able to be mounted?

                    Mounted Reset Speed:

                            How fast the gun reset to its given default rotation when ungrabbed. Value in DegreesPerSecond, 0 = no reset

#### Setup Interaction for Bipod Component

                Add ways to interact with the Bipod. You can use the ActivateBipod, DeactivateBipod and ToggleBipod functions of the BipodComponent for that.

                One way to have interaction with the Bipod would be the BipodInteractionComponent.

##### BipodInteractionComponent

                        Also look at the Examples from the Source Plugin.

                        1. Add VRHandles to the guns bipod legs

                        2. On Begin Play of the BipodInteractionComponent run the Setup VRHandles function with your VRHandles as the input.

                          
![image](images/mod-bipod-guide/1488100e83.jpg) <!-- src: https://image.modcdn.io/members/7c1e/5313379/profile/screenshot2024-05-30170146.jpg -->

#### Add Bipod Animation


---

## Comments (mod.io API, 2)

- **evanboi96** (2024-07-17): how do i place the bipods
- **evanboi96** (2024-07-17): i Don rally get how to use the bipod guns
