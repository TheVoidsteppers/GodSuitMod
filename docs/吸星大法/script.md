```c
Scriptname God_Suit__Attract_script extends activemagiceffect  

Event OnEffectStart(actor akTarget, actor akCaster)
	akCaster.PushActorAway(akTarget, -40)

	;debug.messageBox("===== Effect Start done =====")
EndEvent

```