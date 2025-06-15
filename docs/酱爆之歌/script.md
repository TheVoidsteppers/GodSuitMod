```c
Scriptname God_Suit_Magic_Jiang_Bao_script extends ActiveMagicEffect

Idle Property IdleStop  Auto
Idle Property IdleFluteStart  Auto
Idle Property IdleDrumStart  Auto
Idle Property IdleLuteStart  Auto

Scene Property BardSongsBallad01Scene auto
Scene Property BardSongsBallad01WithIntroScene auto
Scene Property BardSongsDrinkingSong01Scene auto
Scene Property BardSongsDrinkingSong01WithIntroScene auto
Scene Property BardSongsDrinkingSong03Scene auto
Scene Property BardSongsDrinkingSong03WithIntroScene auto
Scene Property BardSongsDrinkingSong02Scene auto
Scene Property BardSongsDrinkingSong02WithIntroScene auto
Scene Property BardSongsInstrumentalFlute01 auto
Scene Property BardSongsInstrumentalFlute02 auto
Scene Property BardSongsInstrumentalLute01 auto
Scene Property BardSongsInstrumentalLute02 auto
Scene Property BardSongsInstrumentalDrum01 auto
Scene Property BardSongsInstrumentalDrum02 auto
Scene Property BardSongsInstrumentalFluteonly01 auto
Scene Property BardSongsInstrumentalFluteonly02 auto

Bool StopSong = False

VoiceType Property FemaleYoungEager Auto 
voiceType Property MaleYoungEager Auto

Int Playing = 0 Conditional

Actor TheTarget
Actor TheCaster
Faction Property MagicCharmFaction Auto

Event OnEffectFinish(actor akTarget, actor akCaster)
	;debug.Notification("OnEffectFinish");

	TheTarget = akTarget;
  TheCaster = akCaster;

	akTarget.AddToFaction(MagicCharmFaction);

	akTarget.StopCombat();
	akTarget.PlayIdle(IdleStop);

	Int BardPlayType = Utility.RandomInt(1, 3);
	If BardPlayType == 1
		akTarget.PlayIdle(IdleFluteStart);
	EndIf
	If BardPlayType == 2
		akTarget.PlayIdle(IdleDrumStart);
	EndIf
	If BardPlayType == 3
		akTarget.PlayIdle(IdleLuteStart);
	EndIf
	PlaySong(akTarget)
	;debug.messageBox("===== Effect Start done =====")
EndEvent

int Function GetRandomSong(objectReference PassedBard)
	Int BardSongToPlay = Utility.RandomInt(2, 16)

	
	If PassedBard.GetVoiceType() == FemaleYoungEager &&  BardSongToPlay == 2		;If the song picked is "Age Of..." for FemaleYoungEager (who can't sing it) set it to "Ragnar" 
		BardSongToPlay = 1	
	EndIf
	If PassedBard.GetVoiceType() == MaleYoungEager &&  BardSongToPlay == 3			;If the song picked is "The Dragonborn..." for MaleYoungEager  (who can't sing it) set it to "Ragnar" 
		BardSongToPlay = 1
	EndIf

	; debug.Trace("Returning Random Song #"+BardSongToPlay)
	Return (BardSongToPlay)

EndFunction

Function PlaySong(objectReference Bard, Bool ChangeSettings = True)
	; 	debug.Trace("Function Called. Stopsong is " + Stopsong)

	if Changesettings == True	
		StopAllSongs()

		TheTarget.RemoveFromFaction(MagicCharmFaction);
	endif

	Playing = 1

	int SongToPlay = GetRandomSong(Bard)    			

	; debug.Trace("Executing Play Chosen function Song " + SongToPlay)

	If !Bard.Is3dLoaded()
		; debug.Trace("Bard has no 3D! Aborting song.")
		Playing = 0
		Return     
	Endif

	PlayChosenSong(SongToPlay)
	; debug.Notification("===== BardSongsBallad01WithIntroScene ===== ");
	Utility.Wait(1)
	StopSong = False
EndFunction

Function PlayChosenSong(Int ChosenSong)
	Int Intro = Utility.RandomInt(0, 1);
	;debug.Notification("===== PlayChosenSong ===== " + ChosenSong + "Intro: " + Intro);

	If ChosenSong == 1
		; debug.Trace("Playing Bard song 1: Ragnar The Red")
		If Intro == 0
				; debug.Trace("Playing Bard song 1: Ragnar The Red without intro")
			BardSongsDrinkingSong02Scene.Start()
		Else
				; debug.Trace("Playing Bard song 1: Ragnar The Red with intro")	
			BardSongsDrinkingSong02WithIntroScene.Start()
		EndIf
	EndIf

	If ChosenSong == 2
		; debug.Trace("Playing Bard song 2: Age of...")
		If Intro == 0
				; debug.Trace("Playing Bard song 2 without intro")
			BardSongsDrinkingSong03Scene.Start()
		Else
				; debug.Trace("Playing Bard song 2 with intro")
			BardSongsDrinkingSong03WithIntroScene.Start()
		EndIf
	EndIf

	If ChosenSong == 3
		; debug.Trace("Playing Bard song 3: The Dragonborn")
		If Intro == 0
				; debug.Trace("Playing Bard song 3 without intro")
			BardSongsDrinkingSong01Scene.Start()
		Else
				; debug.Trace("Playing Bard song 3 with intro")
			BardSongsDrinkingSong01WithIntroScene.Start()
		EndIf
	EndIf

	If ChosenSong == 4
		; debug.Trace("Playing Bard song 4: Flute1")
		BardSongsInstrumentalFlute01.Start()
	EndIf

	If ChosenSong == 5
			; debug.Trace("Playing Bard song 5: Flute2")
		BardSongsInstrumentalFlute02.Start()
	EndIf

	If ChosenSong == 6
			; debug.Trace("Playing Bard song 6: Lute1")
		BardSongsInstrumentalLute01.Start()
	EndIf

	If ChosenSong == 7
			; debug.Trace("Playing Bard song 7: Lute2")
		BardSongsInstrumentalLute02.Start()
	EndIf

	If ChosenSong == 8
			; debug.Trace("Playing Bard song 8: Drum1")
		BardSongsInstrumentalDrum01.Start()
	EndIf

	If ChosenSong == 9
			; debug.Trace("Playing Bard song 9: Drum2")
		BardSongsInstrumentalDrum02.Start()
	EndIf

	If ChosenSong == 10
		; debug.Trace("Playing Bard song 10: Tale of the Tongues")
		If Intro == 0
				; debug.Trace("Playing Bard song 10 without intro")
			BardSongsBallad01Scene.Start()
		Else
				; debug.Trace("Playing Bard song 1 with intro")
			BardSongsBallad01WithIntroScene.Start()
		EndIf
	EndIf

	If ChosenSong == 11
			; debug.Trace("Playing Bard song 11: FluteOnly1")
		BardSongsInstrumentalFluteonly01.Start()
	EndIf

	If ChosenSong == 12
			; debug.Trace("Playing Bard song 12: FluteOnly2")
		BardSongsInstrumentalFluteonly02.Start()
	EndIf

EndFunction

;--------------------------------------------------------------------------------------

Function StopAllSongs()
	;debug.Notification("StopAllSongs");

	StopSong = True

	BardSongsBallad01Scene.Stop()
	BardSongsBallad01WithIntroScene.Stop()

	BardSongsDrinkingSong01Scene.Stop()
	BardSongsDrinkingSong01WithIntroScene.Stop()

	BardSongsDrinkingSong02Scene.Stop()
	BardSongsDrinkingSong02WithIntroScene.Stop()

	BardSongsDrinkingSong03Scene.Stop()
	BardSongsDrinkingSong03WithIntroScene.Stop()

	BardSongsInstrumentalFlute01.Stop()
	BardSongsInstrumentalFlute02.Stop()

	BardSongsInstrumentalLute01.Stop()
	BardSongsInstrumentalLute02.Stop()

	BardSongsInstrumentalDrum01.Stop()
	BardSongsInstrumentalDrum02.Stop()

	BardSongsInstrumentalFluteOnly01.Stop()
	BardSongsInstrumentalFluteOnly02.Stop()
	
	Playing = 0
EndFunction

```