```c
Scriptname God_Suit__Attract_script extends activemagiceffect  

sound property IntroSoundFX auto ; create a sound property we'll point to in the editor
sound property OutroSoundFX auto ; create a sound property we'll point to in the editor


Event OnEffectStart(Actor Target, Actor Caster)
	if IntroSoundFX != none
		int instanceID = IntroSoundFX.play((target as objectReference))          ; play IntroSoundFX sound from my self
	endif
EndEvent


Event OnEffectFinish(Actor Target, Actor Caster)
	if OutroSoundFX != none
		int instanceID = OutroSoundFX.play((target as objectReference))         ; play OutroSoundFX sound from my self
	endif
endEvent

```