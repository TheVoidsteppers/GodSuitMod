```c
Scriptname God_Suit_Magic_Strike_Fly_script extends ActiveMagicEffect

Event OnEffectStart(actor akTarget, actor akCaster)
	akTarget.PushActorAway(akTarget, 30)
	
	;debug.messageBox("===== Effect Start done =====")
EndEvent

```