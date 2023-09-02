```c
Scriptname God_Suit_Leeroy_Jenkins_script extends ActiveMagicEffect

Spell property godSuitParalysisSpell auto
Spell property godSuitFrostDmageFFSelfAreaSpell auto
Spell property godSuitFireDamgeFFSelfAreaSpell auto
Spell property godSuitVoiceSlowTimeSpell auto


;Spell property godSuitPerkBashDisarmSpell auto
;Spell property godSuitMagicPushDownCloakSpell  auto

Event OnEffectStart(actor Target, actor Caster)
	debug.SendAnimationEvent(Caster as ObjectReference, "ShoutStart")
	debug.SendAnimationEvent(Caster as ObjectReference, "ShoutSprintMediumStart")	

	;godSuitPerkBashDisarmSpell.Cast(Caster, Caster)
	;godSuitMagicPushDownCloakSpell.Cast(Caster, Caster)

	Utility.Wait(0.5)

	; Cast a Paraly spell on the Caster
	godSuitParalysisSpell.Cast(Caster, Caster)


	Utility.Wait(0.15)
	godSuitFrostDmageFFSelfAreaSpell.Cast(Caster, Caster)
	godSuitFireDamgeFFSelfAreaSpell.Cast(Caster, Caster)


	Utility.Wait(0.5)
	godSuitFrostDmageFFSelfAreaSpell.Cast(Caster, Caster)
	godSuitFireDamgeFFSelfAreaSpell.Cast(Caster, Caster)

	Utility.Wait(0.15)
	godSuitVoiceSlowTimeSpell.Cast(Caster, Caster)

	;debug.messageBox("===== Effect Start done =====")
EndEvent

```