+++
+++

 # Scatter Bombs ![image](/image/Scatter_Bombs.png) 


Effects
---------


* For the current room, rotates every enemy and pickup 90 degrees and moves its sprite up and left.
	+ Enemy hitboxes remain the same.
* Increases one of Isaac's [stats](/wiki/Attributes "Attributes") and decreases another. Possible stat changes include:
	+ ± 1 flat [damage](/wiki/Damage "Damage")
	+ ±0.5 [tears](/wiki/Tears "Tears")
	+ ±0.2 [speed](/wiki/Speed "Speed")
		- (Removed in Repentance) Also affects maximum speed (may never exceed 2.0)
	+ ±0.2 [shot speed](/wiki/Shot_speed "Shot speed")
	+ ±1 [luck](/wiki/Luck "Luck")
	+ (Removed in Repentance) ±0.5 [range](/wiki/Range "Range")
	+ (Added in Repentance) ±1.50 [range](/wiki/Range "Range")
* Adds random tear effects for the current room.
* Distorts the music for the current room.


Synergies
-----------


* (Added in Repentance)[![image](/image/Book_of_Virtues.png)](/wiki/Book_of_Virtues "Book of Virtues") [Book of Virtues](/wiki/Book_of_Virtues "Book of Virtues"): Spawns a special wisp on the middle ring that is otherwise undistinguishable from a normal wisp. These wisps' tears have a 5% chance of transforming any non-boss enemy into random wisps.
* (Added in Repentance)[![image](/image/Rock_Bottom.png)](/wiki/Rock_Bottom "Rock Bottom") [Rock Bottom](/wiki/Rock_Bottom "Rock Bottom"): The stats are locked to the highest number achieved, rendering the stat downs behind the scene immaterial.


Notes
-------


* (Added in Repentance) If the tear stat reaches a negative number, there will be an integer overflow, which will max out the tear rate at the 120 cap; if the tear stat is boosted back into a positive number, it will replace the value obtained previously.
* If Rock Bottom is obtained while Tear Rate is overflowed, it will stay at 120 even if boosts are obtained.


