# Custom vehicle guide

> Source: https://mod.io/g/pavlov/r/custom-vehicle-guide
> Author: Brav_Soldat | Added: 2024-08-08 | Updated: 2024-08-09 | Views: 926 | Comments: 4 | Tags: CustomVehicle, Vehicle
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 83 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: Follow this guide to create your own custom vehicle blueprint.

---
Before creating a custom vehicle, some assets need importing. Once this is done, we can move on to creating the blueprints. This guide should help with both processes.

This guide will probably need updating in the future, if any bits of info was missed/ overlooked.

 

**Copying some assets**

To make things easier, copy these 2 assets from the Willys example folder (PavExamples/Vehicles/Willys) to your custom vehicles folder:

![image](images/custom-vehicle-guide/f5c8e5eb5c.png) <!-- src: https://i.imgur.com/BaEk4tj.png -->

 

**Importing the assets**

It is important that your vehicle skeleton and mesh is oriented a certain way. A good rule of thumb to to keep everything x-facing. This guide will not teach you how to use various modeling softwares, such as blender, but there are plenty of tutorials online:

![image](images/custom-vehicle-guide/0a937aa34b.png) <!-- src: https://i.imgur.com/N7jbnA6.png -->

Note that the front right wheel is rigged x-facing. For your first custom vehicle, it would be easiest to copy the skeleton from a mesh included with the modkit (willys in this example) to the mesh of your custom vehicle. Then setup the vertex groups for each bone. 

 

As for the steering wheel, the axis of rotation should be the x-axis:

![image](images/custom-vehicle-guide/b2ca258209.png) <!-- src: https://i.imgur.com/XPntHI1.png -->

After ensuring the bones are oriented correctly, import the mesh to the editor.

 

**Editing the assets**

Open the physics asset:

![image](images/custom-vehicle-guide/e8736df951.png) <!-- src: https://i.imgur.com/IPGMKb6.png -->

Over on the left, we need to fix whats visible since by default, important things are hidden:

![image](images/custom-vehicle-guide/38c64034be.png) <!-- src: https://i.imgur.com/yn85dSZ.png -->

Click the gear icon, and select "Show All Bones" and also make sure Show Constraints/ Show Primitives is checked. This will let you see the whole bone tree for the skeleton.

![image](images/custom-vehicle-guide/4734917d8c.png) <!-- src: https://i.imgur.com/g68v3cF.png -->

Some primitives and constraints probably auto generated, we want to DELETE them. You can either select them under the skeleton tree or do ctrl+a and then press the delete key.

 

**Adding the collision**

Right click the root bone, then Add Shape, then Add box:

![image](images/custom-vehicle-guide/608846be67.png) <!-- src: https://i.imgur.com/Br559yC.png -->

![image](images/custom-vehicle-guide/e3a74d06c3.png) <!-- src: https://i.imgur.com/wymJSha.png -->

You can move/scale the box to match the body of the vehicle. Add however many boxes needed to achieve a general shape for the vehicle. Using primitives is best, but it's still possible to go overboard with them. Refer to the willys mesh to see how its collision was setup.

 

For the wheels, we need to add a sphere per each wheel bone:

![image](images/custom-vehicle-guide/35b6afd5d1.png) <!-- src: https://i.imgur.com/C3862np.png -->

 

The wheels need some special settings, such as kinematic and collision disabled over on the right:

![image](images/custom-vehicle-guide/e8c792ad4e.png) <!-- src: https://i.imgur.com/Y15LPFZ.png -->

 

**Adding sockets**

The last step before moving on to blueprints, is adding the skeletons sockets. Open the skeleton asset:

![image](images/custom-vehicle-guide/d0a4dae32c.png) <!-- src: https://i.imgur.com/6uFf3eM.png -->

Once open, you might have to click Show All Bones again:

![image](images/custom-vehicle-guide/889d6f1818.png) <!-- src: https://i.imgur.com/8O7sMOc.png -->

Right click on the steering wheel bone and select "Add Socket"

![image](images/custom-vehicle-guide/bb3c7efe83.png) <!-- src: https://i.imgur.com/LyXweUT.png -->

Name it "WheelSocketL" and move/rotate it to the left center of the steering wheel. Notice the direction each axis is facing, it is very important!

![image](images/custom-vehicle-guide/5992004705.png) <!-- src: https://i.imgur.com/wxpEesV.png -->

Do the same thing for the right side: "WheelSocketR" (WheelSocketL and WheelSocketR should have the same orientation)

Add two more sockets (CenterWheelL and CenterWheelR) about half way down the steering column:

![image](images/custom-vehicle-guide/dcc73ca640.png) <!-- src: https://i.imgur.com/EFhGFHC.png -->

![image](images/custom-vehicle-guide/4603d9f37b.png) <!-- src: https://i.imgur.com/EXGIjVm.png -->

Notice that these two sockets do NOT have the same orientation! SO make sure yours are correct.

Lastly, add an Engine socket where the engine would be:

![image](images/custom-vehicle-guide/4623a707aa.png) <!-- src: https://i.imgur.com/U1nEDfP.png -->

That should be all the pre-setup before we move on to blueprints. Remember, if you get stuck at any point, look at the included example vehicles in the modkit.

 

**Creating the vehicle blueprint**

Navigate to your vehicle folder, right click and select "Blueprint Class" then choose PavlovVehicle_4w:

![image](images/custom-vehicle-guide/ac433d1b9b.png) <!-- src: https://i.imgur.com/PbQR5uj.png -->

Give it a name and then open it.

In the bottom left, add a Wheels variable with the type **ChaosVehicleWheel:**

![image](images/custom-vehicle-guide/eee95eacb5.png) <!-- src: https://i.imgur.com/EgvXtsF.png -->

Make sure its an array, set this at the top right:

![image](images/custom-vehicle-guide/db2dbf74b8.png) <!-- src: https://i.imgur.com/sI2zb50.png -->

We will move on the the animation blueprint for now, but we will come back to this later.

 

**Creating the animation blueprint**

Right click the vehicle mesh, or skeleton, goto Create then Anim Blueprint:

![image](images/custom-vehicle-guide/81306dfea2.png) <!-- src: https://i.imgur.com/wih1DeO.png -->

Name it "ABP_CustomVehicle" and open it

At the top middle, click "Class Settings"

![image](images/custom-vehicle-guide/cf2e7c45fe.png) <!-- src: https://i.imgur.com/2Ay3P3S.png -->

Over on the right, set the Parent Class to: **PavlovVehicleAnimInstance**

![image](images/custom-vehicle-guide/e56498ea87.png) <!-- src: https://i.imgur.com/Bj0n8yR.png -->

Compile and Save the animation blueprint to apply the parent change.

In the bottom left, add a **Rotation** variable with the type rotator:

![image](images/custom-vehicle-guide/38556f3cc6.png) <!-- src: https://i.imgur.com/0hjOGXU.png -->

In the animation blueprint **event graph**, add this:

![image](images/custom-vehicle-guide/bc3ef863cf.png) <!-- src: https://i.imgur.com/hju09Ok.png -->

The cast node should be for your custom vehicle, the Willys cast is just an example. Make sure wheel index 0 and 1 are used like above.

Next, add the SetSteeringRotation event to set the Rotation variable:

![image](images/custom-vehicle-guide/93600a7e3b.png) <!-- src: https://i.imgur.com/96nC6Zd.png -->

![image](images/custom-vehicle-guide/f6caf183e8.png) <!-- src: https://i.imgur.com/0UYSDZY.png -->

In the animation blueprint **anim graph**, add this:

![image](images/custom-vehicle-guide/2ecb7468bc.png) <!-- src: https://i.imgur.com/gUubexF.png -->

For the Transform Modify Bone node, select it and make sure the bone to modify is  steeringWheel, and that the Rotation Mode is **Add to Existing** and Rotation Space is **Bone Space**:

![image](images/custom-vehicle-guide/3fcc740c3c.png) <!-- src: https://i.imgur.com/0wLSRZ5.png -->

That should be it for the animation blueprint. Remember, if you get stuck at any point, look at the included example vehicles in the modkit.

 

**Creating the occupant components**

Navigate to your vehicle folder, right click and select "Blueprint Class" then choose **VehicleOccupant**:

![image](images/custom-vehicle-guide/6c6a4baa1b.png) <!-- src: https://i.imgur.com/foB7Ww4.png -->

Name it "CMP_Occupant_Pass" then open it.

Select the settings you want and save it: (If you hover over each variable, there are tooltips if you are unsure what they do)

![image](images/custom-vehicle-guide/d44f9d5b02.png) <!-- src: https://i.imgur.com/TjdWAHC.png -->

Navigate to your vehicle folder, right click and select "Blueprint Class" then choose **VehicleOccupantPrototyping**:

![image](images/custom-vehicle-guide/fc4f2e5ae3.png) <!-- src: https://i.imgur.com/oqzDV8K.png -->

Name it "CMP_Occupant_Driver" then open it.

Select the settings you want and save it: (If you hover over each variable, there are tooltips if you are unsure what they do)

![image](images/custom-vehicle-guide/123e70f304.png) <!-- src: https://i.imgur.com/1OOe895.png -->

Make sure Start with Tick is **enabled**!

Over on the left, add these 3 variables:

![image](images/custom-vehicle-guide/aa0c2ab098.png) <!-- src: https://i.imgur.com/ZxhkXpf.png -->

WheelRot uses the struct we copied from the Willys folder as its type:

![image](images/custom-vehicle-guide/f5c8e5eb5c.png) <!-- src: https://i.imgur.com/BaEk4tj.png -->

Above the variables, add the SetSteeringInput function, add a **Steering** input for it:

![image](images/custom-vehicle-guide/879ab5794d.png) <!-- src: https://i.imgur.com/RD4ZLuN.png -->

![image](images/custom-vehicle-guide/8107e20b98.png) <!-- src: https://i.imgur.com/QQ0EfDx.png -->

In the SetSteeringInput function, add this:

![image](images/custom-vehicle-guide/ad57e8ac34.png) <!-- src: https://i.imgur.com/Dj1hQ1q.png -->

The cast node should be for your custom vehicle animation blueprint, the Willys cast is just an example.

In the driver occupants event graph, add this:

![image](images/custom-vehicle-guide/539d3c6304.png) <!-- src: https://i.imgur.com/19ix0Hk.png -->

This handles the throttle and brake input, we also need to add this:

![image](images/custom-vehicle-guide/242d52069e.png) <!-- src: https://i.imgur.com/2cVSSEf.png -->

This handles the steering input. That should be it for the vehicle occupant components, now we can create the wheel assets.

 

**Creating the wheel assets**

Navigate to your vehicle folder, right click and select "Blueprint Class" then choose **ChaosVehicleWheel**:

![image](images/custom-vehicle-guide/97f37be851.png) <!-- src: https://i.imgur.com/z2lMVHJ.png -->

Name it "Wheel_Custom_Back" then open it.

Select the settings you want and save it: (If you hover over each variable, there are tooltips if you are unsure what they do)

![image](images/custom-vehicle-guide/3a5ac1aaff.png) <!-- src: https://i.imgur.com/JFGlbdg.png -->

Look at the included Willys rear wheel, you can copy all the settings but the **Wheel Radius** will probably need to be different for your vehicle. (the radius is in unreal units)

Create another wheel asset and save it as "Wheel_Custom_Front" and open it, use the same settings as the Willys front wheel and change the **Wheel Radius** to match your rear wheel:

![image](images/custom-vehicle-guide/a43fa3d8af.png) <!-- src: https://i.imgur.com/Nan1ji8.png -->

That's it for the wheel assets, now we can resume the custom vehicle blueprint.

 

**Resuming the vehicle blueprint**

Open the vehicle blueprint again. Select the mesh component on the left, then set its mesh on the right:

![image](images/custom-vehicle-guide/5b18513f38.png) <!-- src: https://i.imgur.com/rbW4e5O.png -->

Make sure the mesh has simulate physics set to true, and these collisions:

![image](images/custom-vehicle-guide/5619e72859.png) <!-- src: https://i.imgur.com/FSFzuv0.png -->

Make sure to set the meshes anim class:

![image](images/custom-vehicle-guide/44c3768099.png) <!-- src: https://i.imgur.com/Ip5s0i3.png -->

Select class defaults at the top middle:

![image](images/custom-vehicle-guide/2013870182.png) <!-- src: https://i.imgur.com/1ECs68P.png -->

Over on the right, setup your amount of seats and the occupant classes to go with them (0 should always be the driver)

![image](images/custom-vehicle-guide/20785b9d8e.png) <!-- src: https://i.imgur.com/RMd7dU8.png -->

The passenger occupant component can be used on multiple seats if needed. This guide will only show the setup of 2 seats though (driver and passenger)

Most of these variables should have tooltips if you hover over them, to see what they do. If not, most are self explanatory or look at the included vehicle examples and see what they use.

![image](images/custom-vehicle-guide/e59dd8cc41.png) <!-- src: https://i.imgur.com/VW4NHZJ.png -->

There are sound settings, health, fx, and exit properties. I'm sure I'm forgetting a few settings, but you can always compare to the included Willys example to see its setup.

Over on the left, select the **Vehicle Movement Component**:

![image](images/custom-vehicle-guide/dbda70e42f.png) <!-- src: https://i.imgur.com/xr9rIRm.png -->

On the right, make sure the Wheel Setup is correct:

![image](images/custom-vehicle-guide/a3c949a700.png) <!-- src: https://i.imgur.com/boPFP5T.png -->

The **Wheel Class** should be the wheel assets we created earlier, and the **Bone Name** needs to match your skeleton. The rest of the Chaos Movement Component variables are up to you. Compare to the included Willys or ATV example to see what values to use. It is very difficult to tune a vehicle exact, its best to copy from the examples as a base and then modify that.

Now we can move on to adding components to the vehicle, such as the handles to enter/exit and the seats.

 

Select the vehicle mesh on the left, then click the green **Add** button. Search for "vrhandle" and select it.

Name it "DriverHandle"

![image](images/custom-vehicle-guide/7b91fbc536.png) <!-- src: https://i.imgur.com/Z6we6XU.png -->

![image](images/custom-vehicle-guide/d80093cb06.png) <!-- src: https://i.imgur.com/ThSE5cX.png -->

Position and scale it to the area you want the driver to enter, and make sure it has these settings:

![image](images/custom-vehicle-guide/9be4ce503a.png) <!-- src: https://i.imgur.com/eGJvBKM.png -->

Its collision settings need to be:

![image](images/custom-vehicle-guide/c186313f0d.png) <!-- src: https://i.imgur.com/hMhRJiO.png -->

Do this again for the passenger handle:

![image](images/custom-vehicle-guide/f4470c6d0f.png) <!-- src: https://i.imgur.com/lJ5ba4X.png -->

 

Select the vehicle mesh on the left, then click the green **Add** button. Search for "vrhandle" and select it.

Name it "HandleRight"

![image](images/custom-vehicle-guide/7b91fbc536.png) <!-- src: https://i.imgur.com/Z6we6XU.png -->

![image](images/custom-vehicle-guide/4526e4ab3d.png) <!-- src: https://i.imgur.com/u1hQE2e.png -->

Position and scale it near the steering wheel, and make sure it has these settings:

![image](images/custom-vehicle-guide/860e3044c7.png) <!-- src: https://i.imgur.com/V10mJvX.png -->

Make sure the **Parent Socket** is set to "WheelSocketR" we added in the skeleton earlier. Also notice the **Sequence Ref Comp Name** and the S**equence Ref Bone** match the skeleton.

Its collision settings needs to be:

![image](images/custom-vehicle-guide/ae97d6f5fd.png) <!-- src: https://i.imgur.com/U5uGxJe.png -->

Do this again for the left handle:

![image](images/custom-vehicle-guide/dd292d6355.png) <!-- src: https://i.imgur.com/H6rSpAZ.png -->

![image](images/custom-vehicle-guide/3622c4da3d.png) <!-- src: https://i.imgur.com/PdIDMs1.png -->

They should snap to the wheel when you select the Parent Socket.

 

Select the vehicle mesh on the left, then click the green **Add** button. Search for "audio" and select it.

Name it "EngineAudio"

![image](images/custom-vehicle-guide/ff4ef94f46.png) <!-- src: https://i.imgur.com/0rPHIm8.png -->

![image](images/custom-vehicle-guide/48180755d9.png) <!-- src: https://i.imgur.com/tmwGIR5.png -->

On the right, set the Sound to be used:

![image](images/custom-vehicle-guide/52917d3933.png) <!-- src: https://i.imgur.com/iwJash1.png -->

 

Select the vehicle mesh on the left, then click the green **Add** button. Search for "seat" and select it.

Name it "Seat0"

![image](images/custom-vehicle-guide/c1378a14c3.png) <!-- src: https://i.imgur.com/tgisZu8.png -->

![image](images/custom-vehicle-guide/77e3d4ed6b.png) <!-- src: https://i.imgur.com/4eQOYho.png -->

Move it to the area you want the driver to sit, and make sure it has the settings above on the right.

Add another seat, the only different is the seat index should be 1. The seat index corresponds to the occupant component setup in the vehicles class defaults:

![image](images/custom-vehicle-guide/5e8d053003.png) <!-- src: https://i.imgur.com/nygTW9F.png -->

![image](images/custom-vehicle-guide/6ccc0bafc6.png) <!-- src: https://i.imgur.com/zaCyNe9.png -->

 

Select the vehicle mesh on the left, then click the green **Add** button. Search for "bumper" and select it.

Name it "BumperFront"

![image](images/custom-vehicle-guide/0cbe0d9588.png) <!-- src: https://i.imgur.com/FB7XjBB.png -->

![image](images/custom-vehicle-guide/6c3ffd3ee1.png) <!-- src: https://i.imgur.com/ZTbyGhh.png -->

Move and scale it to the area you want, and make sure it has the settings above on the right. Make sure **Front Bumper** is checked.

Add another bumper for the rear, but leave **Front Bumper** unchecked. The **Truck Bed** option is pretty much a vertical death barrier to prevent players from getting stuck.

Now that all the components are added, we can move on to the blueprint logic:

 

In the event graph, add this to begin play:

![image](images/custom-vehicle-guide/970664d0c2.png) <!-- src: https://i.imgur.com/aRJlWwh.png -->

This saves the wheels for the animation blueprint to use.

 

Select the **DriverHandle** on the left, then in the bottom right, select the **OnHandleGrab** event:

![image](images/custom-vehicle-guide/dff4be79e0.png) <!-- src: https://i.imgur.com/LkgNde0.png -->

![image](images/custom-vehicle-guide/1b93a54661.png) <!-- src: https://i.imgur.com/q51JeY9.png -->

Add this to the event:

![image](images/custom-vehicle-guide/fe0974976e.png) <!-- src: https://i.imgur.com/jknCf5D.png -->

![image](images/custom-vehicle-guide/8c52de8945.png) <!-- src: https://i.imgur.com/NkwpLB5.png -->

Add this to the end, that way it forces the player to release the steering wheel when they get out. Add an **OnHandleGrab** event for the **PassengerHandle** and add the same exit logic minus the steering wheel ungrab nodes above. (make sure EnterVehicle uses Seat 1 for the passenger)

 

Select **HandleRight** on the left, then in the bottom right, select the **OnHandleGrab** event and add this logic:

![image](images/custom-vehicle-guide/8002741497.png) <!-- src: https://i.imgur.com/wSWgHim.png -->

Do this for **HandleLeft** as well. This prevents non drivers from grabbing the steering wheel.

 

Select **HandleRight** on the left, then in the bottom right, select the **OnHandleUngrab** event. Do this for **HandleLeft** as well:

![image](images/custom-vehicle-guide/0e8ece266b.png) <!-- src: https://i.imgur.com/8qBeJYU.png -->

This sets the steering wheel input back to 0 for whichever hand ungrabs.

 

Select **HandleRight** on the left, then in the bottom right, select the **OnHandleRotation** event. Do this for **HandleLeft** as well:

![image](images/custom-vehicle-guide/e4ba714e8f.png) <!-- src: https://i.imgur.com/2MheFau.png -->

Left and Right are slightly different, so refer to the Willys example to not get confused.

 

On the left, in the functions tab, select override:

![image](images/custom-vehicle-guide/7179433149.png) <!-- src: https://i.imgur.com/V7rb1d6.png -->

Select both **GetVehicleAudioComponents** and **GetVehicleEngineAudioComponents:**

![image](images/custom-vehicle-guide/487e06cd0b.png) <!-- src: https://i.imgur.com/GLHxh8C.png -->

In both function overrides, hook up the EngineAudio component we created earlier:

![image](images/custom-vehicle-guide/d0b85b8d56.png) <!-- src: https://i.imgur.com/gK6g5ck.png -->

 

To add the vehicle to the game, use the add vehicle to list node:

![image](images/custom-vehicle-guide/6a56704a07.png) <!-- src: https://i.imgur.com/pI2eMBG.png -->

 

That should be it. If you get lost at any point, refer to the included vehicle examples to see if something is missing or setup wrong. It's easiest to copy the Willys example and components, then use that as a base. If you do this, make sure all of the cast nodes are updated or any other references. If something doesn't work, its not setup right :jared:


---

## Comments (mod.io API, 4)

- **rmetellus79** (2024-08-12): Please can we have a tutorial video
- **GOOSEboy2** (2024-08-11): i need help pls ad me on discord my name is marius880
- **mezzmerize** (2024-08-09): is there a way i can make a seat without being able to drive or move in any way???
- **MaxweIl** (2024-08-09): -A small comment, the part about adding a vehicle to the game isn't the clearest, lemme say it my self, Go into the Plugins folder and then go into the custom map tools content then go into the Pav examples folder. -When in this folder locate the "Mod_Initializer_Example" BP and copy and paste that into your UGC folder that holds your custom car. -Open your new mod initializer file and delete all that is in the EventGraph and add a few nodes, add a "Event On Mod Initialized" drag the Global Info out and look for a "Add Vehicle to List" node (don't forget to connect the white arrow from the "Event On Mod Initialized" to the "Add Vehicle to List"), then drag the Vehicle out and look for a "Make VehicleList" node, the ID hold the identification that goes into the array for vehicle IDs on the Vehicle Spawner Proxy on a map. -Drag the Vehicle Soft Object Path back and look for a "Vehicle Class to Soft Path" node, this is where your vehicle blueprint goes, look for its name and select it to put into the node. -When done compile and save it. when done with that, go find your Definition file and add your initializer file under the Mod Initializer. save that and the upload it to the workshop! -Hope this helps! (if you cant find one or more of the nodes previously mentioned, try turning the "Context Sensitive" box on or off that shows up when adding a node)
