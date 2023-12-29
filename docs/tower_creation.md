- Prerequisites:
	- Tower model 
	- Animations
	- Data for the tower

#### Step 1: Setup
First, we need to set some things up. Make up a "Tower ID" which will be used throughout the code base. This can be different from the tower's name, but try to keep it close enough so that its recognizable. Don't use spaces in the tower's ID. 
Once you have an ID for the tower, grab the model for the tower, and insert it into `Assets/Models/Towers`. Make sure to rename the tower model to your tower ID.

![](https://github.com/jamiww/tdmmdocs/blob/main/TowerSetup1.png)

Adding the animation is pretty much the same, but you need to make a folder for the tower instead. Locate the tower animation folder (`Assets/Animations/Towers`), and insert a folder into it. Change your new folder's name to your tower ID. Once you do that, insert a new Animation into your tower's folder, and name it `FIRE`. Insert your animation's ID into the animation. This will be used whenever the tower shoots/does an action.

![](https://github.com/jamiww/tdmmdocs/blob/main/TowerSetup2.png)

Before we add the data, we need to set it up properly first. Locate the TowerData folder
(`Assets/Data/TowerInfo`) and create a new ModuleScript. Rename it to your tower's ID.

#### Step 2: Adding data
This is what a sample tower file looks like:
```lua
local Models = game.ReplicatedStorage.Assets.Models
local Enums = require(game.ReplicatedStorage.SharedModules.Enums)
local towerId = {
	Name = "<tower name>",
	Description = "<tower description>",
	PlaceIcon = "rbxassetid://<id>",
	Price = <price>, 
	UpgradePrice = <price to upgrade>, 
	PlaceClearance = <radius of placement>, 
	
	Model = Models.Towers.<tower id>,
	TowerType = "<tower type>",
	Advantages = {Enums.AttackType.<any type>, Enums.AttackType.<any type>},
	
	Range = <range>,
	Data = {
		<key> = <value>,
		<key 2> = <value 2>,
	}
}

return towerId
```
This by itself will not work, you need to fill out those values. Here is what each value means, and what to put for it:
- `Name`: Tower's name.
- `Description`: Tower's description.
- `PlaceIcon`: Icon that will be used in the tower bar, and most likely in the shop.
- `Price`: How much the tower costs to buy.
- `UpgradePrice`: How much it costs to upgrade the tower. Set this to nil if it's the last upgrade or there are no upgrades.
- `PlaceClearance`: Radius (studs from center of circle) of the circle used for placement collisions.
- `Model`: Path to tower's model.
- `TowerType`: What kind of tower the tower is. `Projectile` shoots things, and `Generator` makes money. You'll most likely want to use `Projectile`.
- `Advantages`: What AttackType(s) the tower is. For example, `Pyro` would be `{Enums.AttackType.Burn}`. Leave as a blank table `{}` if there is no special attack types.
- `Range`: How far the tower can see, as a radius (studs from center of circle)
- `Data`: Table of special values that is unique to each TowerType. Shouldn't ever be a blank table.
##### Data types:
- `Projectile`:
	- `FireRate`: Delay between each shot fire (in seconds)
	- `Damage`: How much damage each projectile does.
	- `SETUP`: **ONLY SET IF YOU KNOW WHAT YOU ARE DOING!!** Function used when tower is made. `Tower` object is passed as a parameter, like `function(tower) end`.
- `Generator`:
	- `Delay`: Delay between money generations (in seconds)
	- `MoneyGenerated`: Amount of money generated each generation
  	- `HealthGenerated` Amount of health generated at the end of each round
  	- `SETUP`: **ONLY SET IF YOU KNOW WHAT YOU ARE DOING!!** Function used when tower is made. `Tower` object is passed as a parameter, like `function(tower) end`.
#### Step 3: Making upgrades
Creating upgrades is easy. Create new ModuleScripts under your tower's data module, and number them `1` to however many upgrades you need.

![](https://github.com/jamiww/tdmmdocs/blob/main/TowerSetup3.png)

Within the new upgrade modules, you can update whatever values you need to. You do not have to update the `UpgradePrice`, but it is advised to do so for balancing reasons. Not including it will default to the last upgrade's (or the starting) `UpgradePrice` value. Updating the Data table is the same as setting it normally, but just update the values. Here is an example of an upgrade module:
```lua
local TestUpgrade1 = {
	UpgradePrice = 550,
	Range = 16,
	Data = {
		FireRate = 1,
		Damage = 2,
	}
}

return TestUpgrade1
```
#### Step 4: Testing your tower
To test your new tower, head over to the client settings. (`Client/Settings`) Set one of the `TowerSlot#ID` values to your tower's ID.

![](https://github.com/jamiww/tdmmdocs/blob/main/TowerSetup4.png)

You can now play test and use the tower. Adjust any values as needed to balance the tower.
