```c
Scriptname God_Suit_Magic_Trading_script extends ActiveMagicEffect  

Event OnEffectStart(Actor akTarget, Actor akCaster)
	; do nothing
EndEvent

Event OnEffectFinish(Actor akTarget, Actor akCaster)
	akTarget.ShowBarterMenu()
EndEvent

Function ShowBarterMenu() native
```