# Hiding the base Pavlov Scorebard

> Source: https://mod.io/g/pavlov/r/hiding-the-base-pavlov-scorebard
> Author: DaRealUnc | Added: 2025-03-23 | Updated: 2025-03-23 | Views: 457 | Comments: 0 | Tags: none
> Saved 2026-11-10 from the **mod.io API** (full HTML converted to markdown; 2 image link(s) kept inline as `![image](url)`, **images not downloaded**).
> Summary: this is a quick overview of how to hide the base scoreboard in pavlov shack using pavlov modkit.

---
First you need to open up your pavlov modkit. Once inside go to the UGC of the map where you wish to hide the scoreboard.

Now, you are going to want to add a function library.
you can do this by right clicking in your content browser, and selecting Blueprint Function Library

and you can name it whatever you want.

 

Inside you will see a function node

and name it accordingly

 

after that, you want to make two local variables.

the first one is a Soft Class Object Reference

 

*the pink one*

and the second one is a Class Object Reference

*the purple one*

 

After that you want to add an input to the function as I have 

 

Then you want to copy and paste this into your unreal editor

```
Begin Object Class=/Script/BlueprintGraph.K2Node_CallFunction Name="K2Node_CallFunction_7"
   bIsPureFunc=True
   FunctionReference=(MemberParent=/Script/CoreUObject.Class'"/Script/Engine.KismetSystemLibrary"',MemberName="Conv_SoftClassPathToSoftClassRef")
   NodePosX=-32
   NodePosY=64
   NodeGuid=F32BB0E64022B22E3AC791AF5058A1D1
   CustomProperties Pin (PinId=0957C8BD4DCCB664F18CD2B6FA3F8CC2,PinName="self",PinFriendlyName=NSLOCTEXT("K2Node", "Target", "Target"),PinToolTip="Target\nKismet System Library Object Reference",PinType.PinCategory="object",PinType.PinSubCategory="",PinType.PinSubCategoryObject=/Script/CoreUObject.Class'"/Script/Engine.KismetSystemLibrary"',PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,DefaultObject="/Script/Engine.Default__KismetSystemLibrary",PersistentGuid=00000000000000000000000000000000,bHidden=True,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,)
   CustomProperties Pin (PinId=25E87DD5493A04AAC802389A2F904525,PinName="SoftClassPath",PinToolTip="Soft Class Path\nSoft Class Path Structure (by ref)",PinType.PinCategory="struct",PinType.PinSubCategory="",PinType.PinSubCategoryObject=/Script/CoreUObject.ScriptStruct'"/Script/CoreUObject.SoftClassPath"',PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=True,PinType.bIsConst=True,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,SubPins=(K2Node_CallFunction_7 44FC1FF8409C4F3BC61136817ECCACEA,),PersistentGuid=00000000000000000000000000000000,bHidden=True,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=True,bAdvancedView=False,bOrphanedPin=False,)
   CustomProperties Pin (PinId=44FC1FF8409C4F3BC61136817ECCACEA,PinName="SoftClassPath_PathString",PinFriendlyName=LOCGEN_FORMAT_NAMED(NSLOCTEXT("KismetSchema", "SplitPinFriendlyNameFormat", "{PinDisplayName} {ProtoPinDisplayName}"), "PinDisplayName", "Soft Class Path", "ProtoPinDisplayName", "Path String"),PinToolTip="Soft Class Path Path String\nString",PinType.PinCategory="string",PinType.PinSubCategory="",PinType.PinSubCategoryObject=None,PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=False,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node_FunctionEntry_0 EF33E5134967C020EB377CBE387D3DF0,),ParentPin=K2Node_CallFunction_7 25E87DD5493A04AAC802389A2F904525,PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,)
   CustomProperties Pin (PinId=FADED6C24487440543155D8712F993C7,PinName="ReturnValue",PinToolTip="Return Value\nObject Soft Class Reference\n\nConverts a Soft Class Path into a base Soft Class Reference, this is not guaranteed to be resolvable",Direction="EGPD_Output",PinType.PinCategory="softclass",PinType.PinSubCategory="",PinType.PinSubCategoryObject=/Script/CoreUObject.Class'"/Script/CoreUObject.Object"',PinType.PinSubCategoryMemberReference=(),PinType.PinValueType=(),PinType.ContainerType=None,PinType.bIsReference=False,PinType.bIsConst=False,PinType.bIsWeakPointer=False,PinType.bIsUObjectWrapper=True,PinType.bSerializeAsSinglePrecisionFloat=False,LinkedTo=(K2Node_VariableSet_2 84F2E0CD438F7EAA7AC881AA8B92471B,),PersistentGuid=00000000000000000000000000000000,bHidden=False,bNotConnectable=False,bDefaultValueIsReadOnly=False,bDefaultValueIsIgnored=False,bAdvancedView=False,bOrphanedPin=False,)
End Object
```

 

You should get this node

connect it like this 

 

after that you want to setup the function like this

![image](https://image.modcdn.io/members/bca4/29218205/profile/screenshot2025-03-22231634.png)

 

next you want to go to your player info and grab the event begin play node

and set it up like this

![image](https://image.modcdn.io/members/bca4/29218205/profile/screenshot2025-03-22232218.png)

 

-

 
/Game/UI/ScoreBoard/Scoreboard_Base.Scoreboard_Base_C
 
paste this into the get soft class actor node
