# GTA V Linux Framework - Native Function Reference

This document details the native GTA V functions exposed by the Linux Framework JavaScript API. These native functions allow direct interaction with the GTA V game engine.

## Table of Contents

1. [Introduction](#introduction)
2. [Player Functions](#player-functions)
3. [Vehicle Functions](#vehicle-functions)
4. [Entity Functions](#entity-functions)
5. [World Functions](#world-functions)
6. [UI Functions](#ui-functions)
7. [Camera Functions](#camera-functions)
8. [Weapon Functions](#weapon-functions)
9. [Utility Functions](#utility-functions)
10. [Input/Control Functions](#input-control-functions)

## Introduction

The GTA V Linux Framework exposes native game functions through a JavaScript API. These functions interact directly with the GTA V game engine, allowing you to modify game behavior and create custom experiences.

All native functions are available through the global `native` object.

Example usage:
```javascript
// Get player position
const playerPed = native.getPlayerPed(-1);
const position = native.getEntityCoords(playerPed);
console.log(`Player is at: ${position.x}, ${position.y}, ${position.z}`);

// Spawn a vehicle
const vehicleHash = native.getHashKey("adder");
native.requestModel(vehicleHash);
// Wait until the model is loaded
native.waitForModelLoad(vehicleHash, 5000).then(() => {
    const vehicle = native.createVehicle(vehicleHash, position.x, position.y, position.z, 0, true, false);
    native.setPlayerIntoVehicle(native.getPlayerPed(-1), vehicle, -1);
});
```

## Player Functions

### getPlayerPed(playerId)
Returns the player's ped handle.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
- **Returns**: Number - The player's ped handle

### isPlayerDead(playerId)
Checks if the player is dead.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
- **Returns**: Boolean - True if the player is dead

### getPlayerHealth(playerId)
Gets the player's health.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
- **Returns**: Number - The player's health value

### setPlayerHealth(playerId, health)
Sets the player's health.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
  - `health` (Number): Health value to set
- **Returns**: void

### getPlayerWantedLevel(playerId)
Gets the player's current wanted level.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
- **Returns**: Number - Wanted level (0-5)

### setPlayerWantedLevel(playerId, wantedLevel, disableNoMission)
Sets the player's wanted level.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
  - `wantedLevel` (Number): Wanted level to set (0-5)
  - `disableNoMission` (Boolean): True to disable "no mission" property
- **Returns**: void

### givePlayerWeapon(playerId, weaponHash, ammoCount, equipNow, isHidden)
Gives a weapon to the player.
- **Parameters**:
  - `playerId` (Number): Usually -1 for the local player
  - `weaponHash` (Number): Hash of the weapon to give
  - `ammoCount` (Number): Amount of ammo
  - `equipNow` (Boolean): Whether to equip immediately
  - `isHidden` (Boolean): Whether the weapon is hidden
- **Returns**: void

## Vehicle Functions

### createVehicle(modelHash, x, y, z, heading, isNetwork, netMissionEntity)
Creates a vehicle at the specified location.
- **Parameters**:
  - `modelHash` (Number): Hash of the vehicle model
  - `x` (Number): X coordinate
  - `y` (Number): Y coordinate
  - `z` (Number): Z coordinate
  - `heading` (Number): Direction the vehicle faces (in degrees)
  - `isNetwork` (Boolean): Whether the vehicle is networked
  - `netMissionEntity` (Boolean): Whether it's a mission entity
- **Returns**: Number - Handle to the created vehicle

### getVehiclePedIsIn(ped, lastVehicle)
Gets the vehicle a ped is in.
- **Parameters**:
  - `ped` (Number): Handle of the ped
  - `lastVehicle` (Boolean): True to get the last vehicle instead of current
- **Returns**: Number - Handle to the vehicle

### setVehicleEngineOn(vehicle, turnOn, instantly, disableAutoStart)
Turns a vehicle's engine on or off.
- **Parameters**:
  - `vehicle` (Number): Handle of the vehicle
  - `turnOn` (Boolean): True to turn on, false to turn off
  - `instantly` (Boolean): Whether the change should happen instantly
  - `disableAutoStart` (Boolean): Disable auto-start
- **Returns**: void

### setVehicleMaxSpeed(vehicle, speed)
Sets the maximum speed for a vehicle.
- **Parameters**:
  - `vehicle` (Number): Handle of the vehicle
  - `speed` (Number): Maximum speed
- **Returns**: void

### setPlayerIntoVehicle(ped, vehicle, seatIndex)
Places a ped into a vehicle.
- **Parameters**:
  - `ped` (Number): Handle of the ped
  - `vehicle` (Number): Handle of the vehicle
  - `seatIndex` (Number): Seat index (-1 for driver)
- **Returns**: void

## Entity Functions

### getEntityCoords(entity)
Gets the coordinates of an entity.
- **Parameters**:
  - `entity` (Number): Handle of the entity
- **Returns**: Object - {x, y, z} coordinates

### setEntityCoords(entity, x, y, z, xAxis, yAxis, zAxis, clearArea)
Sets the coordinates of an entity.
- **Parameters**:
  - `entity` (Number): Handle of the entity
  - `x` (Number): X coordinate
  - `y` (Number): Y coordinate
  - `z` (Number): Z coordinate
  - `xAxis` (Boolean): Keep X axis
  - `yAxis` (Boolean): Keep Y axis
  - `zAxis` (Boolean): Keep Z axis
  - `clearArea` (Boolean): Clear the area
- **Returns**: void

### getEntityHeading(entity)
Gets the heading of an entity.
- **Parameters**:
  - `entity` (Number): Handle of the entity
- **Returns**: Number - Heading in degrees

### setEntityHeading(entity, heading)
Sets the heading of an entity.
- **Parameters**:
  - `entity` (Number): Handle of the entity
  - `heading` (Number): Heading in degrees
- **Returns**: void

### freezeEntityPosition(entity, toggle)
Freezes or unfreezes an entity's position.
- **Parameters**:
  - `entity` (Number): Handle of the entity
  - `toggle` (Boolean): True to freeze, false to unfreeze
- **Returns**: void

### deleteEntity(entity)
Deletes an entity.
- **Parameters**:
  - `entity` (Number): Handle of the entity
- **Returns**: void

## World Functions

### getGroundZFor_3dCoord(x, y, z, ignoreWater)
Gets the ground Z coordinate for a given X, Y, Z position.
- **Parameters**:
  - `x` (Number): X coordinate
  - `y` (Number): Y coordinate
  - `z` (Number): Z coordinate
  - `ignoreWater` (Boolean): Whether to ignore water
- **Returns**: Number - Ground Z coordinate

### setWeatherTypeNow(weatherType)
Sets the weather type immediately.
- **Parameters**:
  - `weatherType` (String): Weather type (e.g., "CLEAR", "RAIN", "THUNDER")
- **Returns**: void

### setClockTime(hour, minute, second)
Sets the game clock time.
- **Parameters**:
  - `hour` (Number): Hour (0-23)
  - `minute` (Number): Minute (0-59)
  - `second` (Number): Second (0-59)
- **Returns**: void

### getHashKey(str)
Gets the hash key for a string.
- **Parameters**:
  - `str` (String): String to hash
- **Returns**: Number - Hash key

## UI Functions

### showNotification(message)
Shows a notification in the upper-left corner.
- **Parameters**:
  - `message` (String): Message to display
- **Returns**: void

### showHelpText(message, beep)
Shows help text at the bottom of the screen.
- **Parameters**:
  - `message` (String): Message to display
  - `beep` (Boolean): Whether to play a beep sound
- **Returns**: void

### showSubtitle(message, duration)
Shows a subtitle at the bottom of the screen.
- **Parameters**:
  - `message` (String): Message to display
  - `duration` (Number): Duration in milliseconds
- **Returns**: void

### drawText(text, x, y, scale, fontId, color, centered)
Draws text on the screen.
- **Parameters**:
  - `text` (String): Text to draw
  - `x` (Number): X screen coordinate (0.0-1.0)
  - `y` (Number): Y screen coordinate (0.0-1.0)
  - `scale` (Number): Text scale
  - `fontId` (Number): Font ID
  - `color` (Object): RGB color {r, g, b, a}
  - `centered` (Boolean): Whether to center the text
- **Returns**: void

## Camera Functions

### createCam(camType, p1)
Creates a camera.
- **Parameters**:
  - `camType` (String): Camera type
  - `p1` (Boolean): Unknown parameter
- **Returns**: Number - Camera handle

### setCamCoord(cam, posX, posY, posZ)
Sets a camera's coordinates.
- **Parameters**:
  - `cam` (Number): Camera handle
  - `posX` (Number): X coordinate
  - `posY` (Number): Y coordinate
  - `posZ` (Number): Z coordinate
- **Returns**: void

### setCamActive(cam, active)
Sets a camera as active or inactive.
- **Parameters**:
  - `cam` (Number): Camera handle
  - `active` (Boolean): Active state
- **Returns**: void

### renderScriptCams(render, ease, easeTime, p3, p4)
Renders script cameras.
- **Parameters**:
  - `render` (Boolean): Whether to render
  - `ease` (Boolean): Whether to ease
  - `easeTime` (Number): Ease time
  - `p3` (Boolean): Unknown parameter
  - `p4` (Boolean): Unknown parameter
- **Returns**: void

## Weapon Functions

### giveWeaponToPed(ped, weaponHash, ammoCount, isHidden, equipNow)
Gives a weapon to a ped.
- **Parameters**:
  - `ped` (Number): Handle of the ped
  - `weaponHash` (Number): Hash of the weapon to give
  - `ammoCount` (Number): Amount of ammo
  - `isHidden` (Boolean): Whether the weapon is hidden
  - `equipNow` (Boolean): Whether to equip immediately
- **Returns**: void

### removeWeaponFromPed(ped, weaponHash)
Removes a weapon from a ped.
- **Parameters**:
  - `ped` (Number): Handle of the ped
  - `weaponHash` (Number): Hash of the weapon to remove
- **Returns**: void

### setCurrentPedWeapon(ped, weaponHash, equipNow)
Sets the current weapon for a ped.
- **Parameters**:
  - `ped` (Number): Handle of the ped
  - `weaponHash` (Number): Hash of the weapon
  - `equipNow` (Boolean): Whether to equip immediately
- **Returns**: void

## Utility Functions

### requestModel(modelHash)
Requests a model to be loaded.
- **Parameters**:
  - `modelHash` (Number): Hash of the model
- **Returns**: void

### hasModelLoaded(modelHash)
Checks if a model has loaded.
- **Parameters**:
  - `modelHash` (Number): Hash of the model
- **Returns**: Boolean - True if the model is loaded

### waitForModelLoad(modelHash, timeout)
Waits asynchronously for a model to load.
- **Parameters**:
  - `modelHash` (Number): Hash of the model
  - `timeout` (Number): Maximum time to wait in milliseconds
- **Returns**: Promise - Resolves when model is loaded or rejects on timeout

### wait(ms)
Waits for a specified amount of time.
- **Parameters**:
  - `ms` (Number): Time to wait in milliseconds
- **Returns**: Promise - Resolves after the specified time

## Input/Control Functions

### isControlPressed(padIndex, control)
Checks if a control is pressed.
- **Parameters**:
  - `padIndex` (Number): Input device (usually 0)
  - `control` (Number): Control ID
- **Returns**: Boolean - True if the control is pressed

### isControlJustPressed(padIndex, control)
Checks if a control was just pressed.
- **Parameters**:
  - `padIndex` (Number): Input device (usually 0)
  - `control` (Number): Control ID
- **Returns**: Boolean - True if the control was just pressed

### disableControlAction(padIndex, control, disable)
Disables or enables a control action.
- **Parameters**:
  - `padIndex` (Number): Input device (usually 0)
  - `control` (Number): Control ID
  - `disable` (Boolean): Whether to disable the control
- **Returns**: void

### registerKeyMapping(key, commandName, description)
Registers a key mapping for a command.
- **Parameters**:
  - `key` (String): Key to map (e.g., "T", "F5")
  - `commandName` (String): Name of the command
  - `description` (String): Description of what the command does
- **Returns**: Boolean - True if successful

### registerCommand(commandName, handler)
Registers a command that can be triggered by key mappings.
- **Parameters**:
  - `commandName` (String): Name of the command
  - `handler` (Function): Function to call when command is triggered
- **Returns**: Boolean - True if successful