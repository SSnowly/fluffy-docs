---
sidebar_position: 1
title: Exports
description: Our Exports for developer usage
---


## updateHUD

 > Usage
```lua
exports.fluffy_hud:updateHud()
```
 > Description
 Used to forcefully make the hud reload the data

## toggleHud

> Usage
```lua
exports.fluffy_hud:toggleHud(state)
```
 > Params: `state`: Boolean (true/false)  
 > Description:
 Toggle the visibility of the hud

## toggleSeatbelt

> Usage
```lua
exports.fluffy_hud:toggleSeatbelt()
```
> Description: 
Toggles the built-in seatbelt, does not work if [config](config) useCustomSeatbelt  is false.

## getSetabeltState

> Usage
```lua
exports.fluffy_hud:getSeatbeltState()
```
 > Return: `state`: Boolean (true/false)   
 > Description: Returns if the seatbelt is on or off

