---
title: API Reference
nav_order: 3
---

# API Reference

This section documents all public Blueprint & C++ functions in  
`UInstancedStaticMeshArrayComponent`.

---

## 🎛 Array Core Functions

### `ConstructArray()`
Builds the array using all settings.

### `SetNewMax(NewMax)`
Reconstructs array with a max-instance limit.

### `SetMaxInstancesToArray()`
Auto-computes MaxInstances = X*Y*Z based on ArrayType.

### `GetMaxPossibleInstances() → int32`
Returns how many instances the array *could* have.

---

## 🔄 Instance Updating

### `UpdateInstancesPercent(float Percent)`
Rebuilds the array with Percent * MaxPossibleInstances.

### `UpdateActiveInstances(int AmountActive, int CustomDataIndex)`
Sets inactive/active states per instance.

### `UpdateActivePercent(float Percent, int CustomDataIndex)`
Sets active states by percentage.

---

## 🎨 Custom Data

### `UpdateArrayCustomData(int CustomDataIndex)`
Iterates through all instances and calls  
`OnInstanceCustomDataUpdated()` for each.

### `OnInstanceCustomDataUpdated(int InstanceIndex)`
BlueprintNativeEvent — return a custom float value.

Example uses:
- Progress bars
- Heatmaps
- Color ramps
- Oxygen/energy meters
- Wind animation

---

## 🧱 Transform Overrides

### `MakeInstanceTransform(...)`
BlueprintNativeEvent — override to modify transforms.

Arguments include:
- LinearIndex  
- IndexX  
- IndexY  
- IndexZ  

Useful for:
- Random per-row jitter  
- Wave offsets  
- Auto-rotation  
