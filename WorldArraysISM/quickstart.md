---
title: Quickstart
nav_order: 2
---

# Quickstart Tutorial

Follow this short guide to build your first World Arrays ISM setup.

---

## 1. Add a World Arrays ISM Component

In your Actor:

1. Add **InstancedStaticMeshArrayComponent**
2. Assign a **Static Mesh**
3. Set the **Array Type** (X, XY, 3D, etc.)

---

## 2. Choose Array Size

Set:

- TotalInstancesX  
- TotalInstancesY  
- TotalInstancesZ  

Example:
X: 10
Y: 5
Z: 1

---

## 3. Choose Spacing

Set:
SpacingX = 100
SpacingY = 100
SpacingZ = 100

Or enable:
bAutoSpacing = true


---

## 4. Build the Array

Click the **ConstructArray** button (or run in BeginPlay):



ConstructArray()


Your array is created instantly.

---

## 5. Updating Active Instances

### Activate the first N instances



UpdateActiveInstances(AmountActive = 25, CustomDataIndex = 0)


### Activate based on percentage



UpdateActivePercent(0.5)


---

## 6. Adding Custom Per-Instance Values

Override:



OnInstanceCustomDataUpdated(int InstanceIndex)


Example (linear gradient):



return InstanceIndex / (GetInstanceCount() - 1);


Call:



UpdateArrayCustomData()


---

## 7. Customizing Transforms

Override:



MakeInstanceTransform(Index, IndexX, IndexY, IndexZ)


You can apply:

- Random rotation  
- Added offsets  
- Per-layer variation  

Example:



Rotation.Yaw += RandomFloatInRange(-10, 10);





