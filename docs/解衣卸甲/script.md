```c
Scriptname God_Suit_Magic_Unequip_script extends ActiveMagicEffect  


Event OnEffectStart(actor akTarget, actor akCaster)
	akTarget.UnequipAll()

	;debug.messageBox("===== Effect Start done =====")
EndEvent

```