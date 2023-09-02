```c
Scriptname God_Suit_Magic_Pickpocket_Script extends ActiveMagicEffect  

Event OnEffectStart(Actor akTarget, Actor akCaster)
	; do nothing
EndEvent

Event OnEffectFinish(Actor akTarget, Actor akCaster)
	;do nothing
	akTarget.OpenInventory(true)
EndEvent

Function OpenInventory(bool abForceOpen = false) native
```