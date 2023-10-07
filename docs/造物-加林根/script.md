```c
Scriptname God_Suit_Magic_Create_Stuff_script extends ActiveMagicEffect  

ingredient property stuff auto

Event OnEffectFinish(Actor akTarget, Actor akCaster)
	akCaster.AddItem(stuff, 1)
EndEvent

```