This Daz Studio script can be used to bake poses to the timeline

It can be easily changed to bake eCTRL (Face Poses), pCTRL (Body Poses), or several others

The following instructions will walk you through:

Transferring a base character mesh into Unreal Engine

1. Opening the Daz Script IDE Window
2. Baking poses to the timeline
3. Transferring the animations to Unreal Engine via the Daz to Unreal Bridge
4. Creating Pose Assets from the Animations
5. Setting up the Animation Blueprint

Export Base Character:

In Daz Studio load a base character into the scene.

Send the character mesh to Unreal by going to:

File -> Send To -> Daz To Unreal

![Imgur](https://i.imgur.com/CbymIUP.png)

Set the Asset Type to Skeletal Mesh

Uncheck Enable Morphs

Uncheck Enable Subdivisions

and click Accept

![Imgur](https://i.imgur.com/gOJ61MM.png)

Enable The Script IDE Pane(tab):

Go up to Window -> Panes (Tabs) -> Click on Script IDE

![Imgur](https://i.imgur.com/snKZJVi.png)

Open or paste the script in the Script IDE Window

Click Execute to add all the eCTRL poses (Face Poses) at the maximum (+) value to the timeline

![Imgur](https://i.imgur.com/sx2xeQl.png)

Once completed this will generate a list of poses that were added to the timeline

Select all the pose names

Right click and select copy

![Imgur](https://i.imgur.com/812t5Cm.png)

Export the animation by once again going to File -> Send To -> Daz To Unreal

Change the Asset Name to something like eCTRL_Max

Set the Asset Type to Animation

Uncheck Enable Morphs

Uncheck Enable Subdivisions

![Imgur](https://i.imgur.com/7cMV7Ev.png)

Click Accept

Once imported right click on the animation

Go up to Create and click Create PoseAsset

![Imgur](https://i.imgur.com/Ad09wKK.png)

Paste the names of the max value poses into the dialog box and click Accept

![Imgur](https://i.imgur.com/IgT8xwH.png)

Back in Daz Studio Script IDE window change var bMax from true to false

![Imgur](https://i.imgur.com/f3WnOU6.png)

Click Execute again to add all the eCTRL poses (Face Poses) at the minimum (-) value to the timeline

Select all the pose names

Right click and copy the list of the minimum value poses

![Imgur](https://i.imgur.com/BzGj8Qn.png)

Once again export the animation by going to File -> Send To -> Daz To Unreal

Change the Asset Name to something like eCTRL_Min

Set the Asset Type to Animation

Uncheck Enable Morphs

Uncheck Enable Subdivisions

![Imgur](https://i.imgur.com/iLOZwPC.png)

Click Accept

Once imported right click on the animation

Go up to Create and click Create PoseAsset

![Imgur](https://i.imgur.com/s9byKdt.png)

Paste the names of the min value poses into the dialog box and click Accept

![Imgur](https://i.imgur.com/YE0moyf.png)

Setting Up The Animation Blueprint:

Right click in the Content Browser

Mouse over Animation and select Animation Blueprint

![Imgur](https://i.imgur.com/k1Mtn55.png)

Choose the skeleton that matches your character

![Imgur](https://i.imgur.com/Mr859GJ.png)

In the Animation Blueprint AnimGraph right click and create a Modify Curve node

![Imgur](https://i.imgur.com/D2DABFx.png)

Pull off of the output pin and create a Node to Evaluate Pose eCTRL_MaxPoseAsset

![Imgur](https://i.imgur.com/88KGCXl.png)

Pull off of the output pin and create a Node to Evaluate Pose eCTRL_MinPoseAsset

![Imgur](https://i.imgur.com/fmLVTOp.png)

Connect it to the Output Pose

Setting up Pose Inputs:

Right click on the Modify Curve Node and select one of the eCTRL poses you want to control

For this example I'm using the BrowInnerUp-Down Pose

![Imgur](https://i.imgur.com/M4pCp8o.png)

Pull off from the input pin and Promote to Variable

![Imgur](https://i.imgur.com/ejVK3qI.png)

Compile the Blueprint

Name the Variable something like BrowInner

Set the Slider Range Minimum to -1 and maximum to 1

Set the Value Range Minimum to -1 and maximum to 1

![Imgur](https://i.imgur.com/kZHUXEt.png)

In order for the eCTRL_MinPoseAsset poses to work in the 0 to -1 range we have to set up a custom curve

Back in the Content Browser right click, go up to Miscellanaous, and select Curve

![Imgur](https://i.imgur.com/zpP5vOt.png)

Make it a CurveFloat and click Select

![Imgur](https://i.imgur.com/BGRejS5.png)

Name the Curve something like CTRL_Min_Curve

Open the curve

Put your mouse over the 0,0 center of the grid and scroll wheel click to create a pin

Move you mouse to the right and create another pin and Time:1 Value:0

Drag that pin down until the value equals -1

It should look like this:

![Imgur](https://i.imgur.com/ON9NNAs.png)

Right click on the graph line and set the Pre-Extrap to Linear

![Imgur](https://i.imgur.com/2Uc6nvY.png)

Back in the Animation Blueprint

Click on the eCtrl_Min_PoseAsset Node

In the details panel change the Blend Option to Custom

Change the Custom Curve from None to the Curve you just created

![Imgur](https://i.imgur.com/IXpg6FM.png)

You should now be able to change the value of the BrowInner variable and see the brows go up a down from -1 to 1

Using the pose assets and animation blueprint for multiple characters:

Open the eCTRL_Max_PoseAsset

In the Asset Details Panel under Additive

Check Additive and change the base pose to pose_eCTRL_Reference_Pose

Click on Convert to Additive Pose

![Imgur](https://i.imgur.com/BCdMz3g.png)

Do the same for the eCTRL_Min_PoseAsset

Back in the Animation Blueprint Preview Scene Setting Tab you can change the Preview Mesh

![Imgur](https://i.imgur.com/lP7I6sh.png)
