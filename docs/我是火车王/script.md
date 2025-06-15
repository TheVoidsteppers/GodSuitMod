```c
Scriptname God_Suit_Leeroy_Jenkins_script extends ActiveMagicEffect

Spell property godSuitParalysisSpell auto

Event OnEffectStart(actor Target, actor Caster)
	Game.ForceFirstPerson()

	debug.SendAnimationEvent(Caster as ObjectReference, "ShoutStart")
	debug.SendAnimationEvent(Caster as ObjectReference, "ShoutSprintMediumStart")	

	;godSuitPerkBashDisarmSpell.Cast(Caster, Caster)
	;godSuitMagicPushDownCloakSpell.Cast(Caster, Caster)

	Utility.Wait(0.45)
	; Cast a Paraly spell on the Caster
	godSuitParalysisSpell.Cast(Caster, Caster)
EndEvent

```