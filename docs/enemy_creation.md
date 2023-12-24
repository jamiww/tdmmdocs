- Prerequisites:
	- Enemy model 
	- Animations
	- Data for the enemy

#### Step 1: Setup
First, we need to set some things up. Make up an "Enemy ID" which will be used throughout the code base. This can be different from the enemy's name, but try to keep it close enough so that it's recognizable. Don't use spaces in the enemy ID.
Once you have an ID for the enemy, grab the model for the enemy, and insert it into the appropriate difficulty folder in `Assets/Models/Enemies`. If unsure, put the enemy model in `Assets/Models/Enemies/Global`. Try to avoid using the global folder, and use difficulty folders whenever possible. Make sure to rename the enemy model to your enemy ID.

![](https://github.com/jamiww/tdmmdocs/blob/main/EnemySetup1.png)

Adding the animation is pretty much the same, but you need to make a folder for the enemy instead. Locate the enemy animation folder (`Assets/Animations/Enemies`), and insert a folder into it. Change your new folder's name to your enemy ID. Once you do that, insert a new Animation into your enemy's folder, and name it `WALK`. Insert your animation's ID into the animation. This will be used as the walk animation for the enemy.

![](https://github.com/jamiww/tdmmdocs/blob/main/EnemySetup2.png)

Before we add the data, we need to set it up properly first. Locate the EnemyInfo folder
(`Assets/Data/EnemyInfo`) and create a new ModuleScript. Rename it to your enemy's ID.

#### Step 2: Adding data
This is what a sample enemy file looks like:
```lua
local Models = game.ReplicatedStorage.Assets.Models
local Enums = require(game.ReplicatedStorage.SharedModules.Enums)
local EnemyID = {
	Name = "TestEnemy",
	Description = "Test test test",
	Types = {Enums.EnemyType.Something},
	Model = Models.Enemies.GameMode.EnemyID,
	MaxHealth = 123,
	Defense = 123,
	Speed = 123,
	Immunities = {Enums.AttackType.Something},
	Vulnerabilities = {}
}

return EnemyID
```
This by itself will not work, you need to fill out those values. Here is what each value means, and what to put for it:
- `Name`: Enemy's name.
- `Description`: Enemy's description.
- `Types`: What kinds of enemy the enemy is.
- `Model`: Path to enemy's model.
- `MaxHealth`: Max health the enemy can have.
- `Defense`: Defense of the enemy, which decreases the amount of damage done from towers.
- `Speed`: How fast the enemy walks along the path in studs per second.
- `Immunities`: What AttackType(s) the enemy is immune/resistant to. For example, `Frozen` would be immune `{Enums.AttackType.Freeze}`. Leave as a blank table `{}` if there are no immunities.
- `Vulnerabilities `: What AttackType(s) the enemy is vulnerable to. For example, `Frozen` would be vulnerable `{Enums.AttackType.Burn}`. Leave as a blank table `{}` if there are no vulnerabilities.

#### Step 3: Testing your enemy
To test your new enemy, head over to the wave data. (`Assets/Data/WaveStructure`) Enter the `Easy` wave file, and scroll down to `[-1]`. Change the `EnemyID` and any other values you need to.

![](https://github.com/jamiww/tdmmdocs/blob/main/EnemySetup3.png)

Next, head over to the server wave file (`Server/Waves`). Set `Waves.CurrentWave = -1`. You can now play test your enemy!

![](https://github.com/jamiww/tdmmdocs/blob/main/TowerSetup4.png)

Adjust any values as you need to balance the enemy. You now have a working enemy!
