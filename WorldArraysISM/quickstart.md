
World Arrays (ISM)
==================

Instanced Static Mesh Array Plugin Documentation
================================================

World Arrays (ISM) is an enhanced Instanced Static Mesh Component for Unreal Engine that allows creators to easily generate 1D, 2D, and 3D arrays of instances with automatic spacing, per-instance custom data, and powerful extensibility through Blueprints and C++.

The plugin provides the component UInstancedStaticMeshArrayComponent, which acts as a drop-in replacement for UInstancedStaticMeshComponent—but with array construction, indexing, and updates built in.

* * *

📌 Features Overview
====================

*   Automatically generate instance arrays in X, Y, Z, XY, XZ, YZ, or full 3D  
    
*   Auto-spacing using the mesh bounds or manual spacing per axis
*   Construct arrays at design time or runtime  
    
*   Per-instance activation toggling (for meters, progress bars, UI-style widgets)
*   Per-instance custom data updates for material-driven effects
*   Blueprint-extendable transform generation (MakeInstanceTransform)  
    
*   Blueprint-extendable per-instance custom data logic (OnInstanceCustomDataUpdated)  
    
*   Supports thousands of ISM instances with maximum performance

* * *

🚀 Quickstart Tutorial
======================

World Arrays (ISM)  Unreal Engine Plugin

Welcome to World Arrays (ISM)! This quickstart guide will walk you through creating your first array, customizing its layout, and driving per-instance material effects.

By the end, you will have:

✔ A working 1D, 2D, or 3D instanced mesh array  
✔ Custom spacing and scaling  
✔ Blueprint-controlled activation (progress bar, sci-fi panel, etc.)  
✔ Custom per-instance data driving a material

* * *

1\. Add the Component
=====================

1.  Create a new Actor Blueprint  
     Example: BP\_IsmArrayExample  
    
2.  Open the Blueprint  
    
3.  In the Components panel, click Add Component ➜ Instanced Static Mesh Array  
    
4.  Assign a Static Mesh (important!)

You will now see the array preview in the Blueprint viewport.

![](images/image10.png)

* * *

2\. Choose the Array Type
=========================

Inside the Details panel under Array Settings:

Select Array Type, for example:

*   ArrayX → A 1D line
*   ArrayXY → 2D grid
*   Array3D → Full 3D cube

When you select a type:

*   Only relevant axis options appear  
    
*   Axis counts & spacing auto-adjust

![](images/image2.png)  

* * *

3\. Set the Array Size
======================

Example for a 2D grid (ArrayXY):

*   TotalInstancesX = 10  
    
*   TotalInstancesY = 10  
    

You now have 100 instances.

Try a 3D cube:

*   ArrayType: Array3D  
    
*   X = 10  
    
*   Y = 10  
    
*   Z = 5  
    

Total = 500 instances

* * *

4\. Spacing Options
===================

### Option A — Auto Spacing

Toggle:

bAutoSpacing = true

Your mesh’s bounding box automatically determines spacing.  
Perfect for tiles, blocks, or voxels.

* * *

### Option B — Manual Spacing

Set:

SpacingX = 150

SpacingY = 150

SpacingZ = 150

Useful for:

*   Sci-fi light panels  
    
*   Pipes  
    
*   Grids with custom gaps  
    
*   Decorative patterns  
    

* * *

5\. Construct the Array
=======================

Click the button:

Construct Array

Or call ConstructArray in Blueprint or C++ at runtime.

![](images/image6.png)

If bAutoInitialize is enabled, construction happens automatically at:

*   Construction Script  
    
*   BeginPlay

  

* * *

6\. Driving Activation (Progress Bars & Panels)
===============================================

Every instance can be set active (1) or inactive (0) using custom data.

### Option A — Activate N instances

UpdateActiveInstances(AmountActive, CustomDataIndex)

Example:  
Activate the first 30 of the grid for a progress bar:

UpdateActiveInstances(30)

![](images/image7.png)

* * *

### Option B — Activate by percent

UpdateActivePercent(Percent)

![](images/image5.png)

Examples:

*   0.0 → All off  
    
*   0.5 → Half active  
    
*   1.0 → All active  
    

Useful for:

*   Health bars  
    
*   Loading indicators  
    
*   Heat meters  
    
*   Energy cells  
    
*   Sci-fi UI walls  
    

* * *

7\. Setting Up The Material
===========================

To visualize activation:

1.  Open your static mesh material  
    
2.  Add a PerInstanceCustomData node
3.  Use CustomData\[0\]  
    
4.  Drive brightness, color, mask, emissive, etc.  
    

Example:  
Multiply emissive color by CustomData\[0\] to toggle each instance independently.

![](images/image1.png)

* * *

8\. Adding Custom Per-Instance Data (Advanced)
==============================================

Call:

UpdateArrayCustomData(CustomDataIndex)

This calls your override of:

### Blueprint Event

OnInstanceCustomDataUpdated(InstanceIndex)

![](images/image3.png)

![](images/image8.png)

Example Blueprint use cases:

*   Gradient from center  
    
*   Height-based value  
    
*   Pulsing animation  
    
*   Random 0-1 values  
    
*   LOD-like distance fade  
    

* * *

9\. Customizing Instance Transforms (Advanced Pattern Control)
==============================================================

You can override:

MakeInstanceTransform(LinearIndex, X, Y, Z)

![](images/image4.png)

Use this to:

*   Add noise (jitter)  
    
*   Offset rows/columns  
    
*   Rotate 90° patterns  
    
*   Create spirals  
    
*   Make organic grids or pseudo-random clusters  
    

Example Blueprint logic:

![](images/image9.png)

This event fires for every instance during ConstructArray.

* * *

10\. Limiting Instances (Optional)
==================================

### MaxInstances

If you want to cap the total regardless of X/Y/Z values:

MaxInstances = 50

or automatically compute the max:

SetMaxInstancesToArray()

Useful for:

*   Previewing  
    
*   Performance tuning  
    
*   Procedural generation step-by-step  
    

* * *

11\. Simple Blueprint Examples
==============================

For Component Examples see:

/All/Plugins/WorldArraysISM/Examples/Components

*   BP\_ISMArray\_BrickLayout
*   BP\_ISMArray\_BrickRandomRotation
*   BP\_ISMArray\_ProgressMeter
*   BP\_ISMArray\_RandomLights
*   BP\_ISMArray\_WithAddedJitter

Actor Usage Examples:

/All/Plugins/WorldArraysISM/Examples/Actors

📌 API
======

* * *

ENUM: EArrayType
================

Defines the shape of the array generated.

UENUM(BlueprintType)

enum class EArrayType : uint8

{

        ArrayX,   // 1D in X

        ArrayY,   // 1D in Y

        ArrayZ,   // 1D in Z

        ArrayXY,  // 2D in XY

        ArrayXZ,  // 2D in XZ

        ArrayYZ,  // 2D in YZ

        Array3D   // 3D (XYZ)

};

* * *

Class: UInstancedStaticMeshArrayComponent
=========================================

“An Instanced Static Mesh component with useful built-in functions for creating world arrays.”

Attach this to any Actor to generate large grids of ISM geometry.

* * *

Component Properties
====================

### Array Settings

#### ArrayType (EArrayType)

Select the dimension type of the generated array.  
Controls which axes are used and displayed.

#### bAutoSpacing (bool)

*   When enabled, spacing values (X/Y/Z) are computed from the mesh bounds.  
    
*   Perfect for voxel grids, brick walls, tiles, etc.  
    

#### SpacingX / SpacingY / SpacingZ (float)

Manual spacing for each axis, hidden/enabled based on the chosen ArrayType.

#### TotalInstancesX / Y / Z (int32)

Number of instances along each axis.  
Must be ≥ 1.  
Only exposed for axes used by the selected ArrayType.

#### MaxInstances (int32)

Limits the total number of generated instances.  
Useful when randomizing or previewing.  
\-1 = unlimited.

#### MeshScale (FVector)

Uniform or axis-based scale applied to every instance transform.

#### bAutoInitialize (bool)

If enabled, the array constructs itself at construction and BeginPlay.

* * *

Runtime & Editor Functions
==========================

ConstructArray()
----------------

UFUNCTION(BlueprintCallable, CallInEditor)

void ConstructArray();

Generates (or regenerates) the array.  
Clears existing instances, builds new ones, and applies transform logic via MakeInstanceTransform.

* * *

SetNewMax(int32 NewMax)
-----------------------

Limits the total generated instances, and reconstructs the array.

* * *

SetMaxInstancesToArray()
------------------------

Automatically sets MaxInstances = GetMaxPossibleInstances().

Useful if you want rigid caps without manually calculating total count.

* * *

GetMaxPossibleInstances()
-------------------------

Returns the total number of instances given the current X/Y/Z sizes and ArrayType.

* * *

UpdateInstancesPercent(float Percent)
-------------------------------------

Rebuilds the array using only a percentage of the possible instances.  
Useful for efficiency or progressive reveals.

* * *

Per-Instance Activation
=======================

These functions update a per-instance custom data channel where:

*   1 = active
*   0 = inactive

Used for progress bars, health bars, loading widgets, indicator arrays, etc.

### UpdateActiveInstances(int32 AmountActive, int32 CustomDataIndex)

Sets first N instances active.

### UpdateActivePercent(float Percent, int32 CustomDataIndex)

Activates a percentage of all possible instances.

* * *

Per-Instance Custom Data System
===============================

UpdateArrayCustomData(int32 CustomDataIndex)
--------------------------------------------

Loops through all instances and updates a single custom data channel.

It calls:

### OnInstanceCustomDataUpdated(int32 InstanceIndex)

BlueprintNativeEvent  
Override to compute a custom value for each instance.

Examples:

*   gradients  
    
*   random jitter  
    
*   animated fill amounts  
    
*   heatmaps  
    
*   color banding  
    
*   audio visualizers  
    
*   material-driven effects  
    

* * *

Transform Customization
=======================

MakeInstanceTransform(int32 LinearIndex, int32 IndexX, int32 IndexY, int32 IndexZ)
----------------------------------------------------------------------------------

BlueprintNativeEvent—override this to freely control how instances are placed.

Examples:

*   grid offsets  
    
*   procedural jitter  
    
*   spiral patterns  
    
*   noise deformation  
    
*   offsets based on height or distance  
    
*   L-shapes or custom patterns  
    

This function is used inside ConstructArray() for every instance added.

* * *

Utility Functions
=================

### UpdateAxisUsageFromEnum()

Internal—syncs boolean flags (bUsesX/Y/Z) & editor visibility from the ArrayType.

* * *

### GetRandomSquareRotation()

Returns a random 0°, 90°, 180°, or 270° rotation.  
Useful for tile randomization.

* * *

Editor Support
==============

The plugin supports editor-time regeneration, property refresh, and live updates through:

virtual void PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) override;

When adjusting spacing, mesh, or counts, the array automatically updates when editing in the editor.

* * *

Internal Generation Flow
========================

### ConstructArray → GetArrayTransforms → MakeInstanceTransform → AddInstance

Each generated instance goes through:

1.  Axis usage determined from ArrayType  
    
2.  LinearIndex → (X,Y,Z) indices calculated  
    
3.  Transform computed in MakeInstanceTransform  
    
4.  Scale applied via MeshScale  
    
5.  Instance added to ISM pool  
    

* * *

Blueprint Examples
==================

### BP\_ISMArray\_WithAddedJitter

Example Blueprint included in your plugin:

*   Overrides MakeInstanceTransform  
    
*   Adds random XY offsets  
    
*   Great for natural spacing or foliage scattering  
    

* * *

Use Cases
=========

### Building Blocks / Voxels

3D X/Y/Z arrays with auto spacing.

### Tiling Materials

Perfect 2D XY grids for walls, floors, ceilings, and patterns.

### Sci-Fi Panels / Progress Bars

Use UpdateActiveInstances + custom data for a sleek UI-style progress meter.

### VFX Arrays

Procedural patterns, wave animations, pulsing, emissive grids.

### Modular Structure Generation

Large grids of repeated mesh elements—fast and memory-efficient.

* * *

Best Practices
==============

*   Use Auto Spacing for box-like meshes.
*   Use MaxInstances to keep preview responsive in editor.
*   For dynamic patterns, override OnInstanceCustomDataUpdated.  
    
*   To modify layout, override MakeInstanceTransform.  
    
*   Remember to set Num Custom Data Floats in the component settings before using custom data.

* * *

C++ Extension Example
=====================

float UMyCoolArray::OnInstanceCustomDataUpdated\_Implementation(int32 InstanceIndex)

{

    return InstanceIndex % 2 == 0 ? 1.0f : 0.0f; // even instances glow

}

FTransform UMyCoolArray::MakeInstanceTransform\_Implementation(int32 Linear, int32 X, int32 Y, int32 Z) const

{

    FTransform T;

    T.SetLocation(FVector(X \* 50.f, Y \* 50.f, Z \* 50.f));

    T.SetRotation(FQuat::MakeFromEuler(FVector(0,0,FMath::FRand() \* 360)));

    return T;

}

* * *

Blueprint Events Summary
========================

Event

Purpose

MakeInstanceTransform

Override to generate custom transforms per instance

OnInstanceCustomDataUpdated

Override to compute custom material data for each instance

* * *

Summary
=======

The World Arrays (ISM) plugin provides a complete, efficient, and flexible system for generating structured or fully customized ISM arrays in Unreal Engine.

It is ideal for:

*   Procedural generation  
    
*   UI meter meshes  
    
*   Pattern grids  
    
*   3D voxel-like structures  
    
*   Material-driven visual effects  
    
*   Any system requiring large quantities of instanced meshes  
    

Your component is fully extensible through both Blueprint and C++ and stays tightly integrated with core ISM workflows.