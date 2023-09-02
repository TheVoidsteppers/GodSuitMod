```c
Scriptname God_Suit_Magic_Stop_It_script extends ActiveMagicEffect  

Event OnEffectStart(actor akTarget, actor akCaster)
	akTarget.StopCombatAlarm()
	
	;debug.messageBox("===== Effect Start done =====")
EndEvent

```