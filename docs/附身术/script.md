```c
Scriptname God_Suit_Possession_script extends activemagiceffect  

; -----
GlobalVariable Property God_Suit_Global_IsControlling Auto
Faction Property MagicCharmFaction Auto

; -----

Actor TheTarget
Actor TheCaster
Spell leftSpell
Spell rightSpell
Shout currentVoice

Float updaetRate = 1.0

Form righthand;
Form lefthand;
Perk Property invis auto;
Activator Property marker auto;

Idle Property OffsetStop  Auto  

float confidence;
float aggression;

bool active = false;

Faction[] tempFactionList
int[] tempFactionRank

MagicEffect Property God_Suit_Possession  Auto  

; -----

Event OnEffectStart(Actor akTarget, Actor akCaster)
  TheTarget = akTarget;
  TheCaster = akCaster;

	active = true;
  God_Suit_Global_IsControlling.Mod(1);

  RegisterForUpdate(updaetRate);

  int ileftHand = akCaster.GetEquippedItemType(0);
	int iRightHand = akCaster.GetEquippedItemType(1);
  if iLeftHand == 9
    leftSpell = akCaster.GetEquippedSpell(0);
    akCaster.UnequipSpell(leftSpell, 0);
  endif
  if iRightHand == 9
    rightSpell = akCaster.GetEquippedSpell(1);
    akCaster.UnequipSpell(rightSpell, 1);
  endif
  currentVoice = akCaster.GetEquippedShout();
  if currentVoice
    akCaster.UnequipShout(currentVoice);
  endif

  if (!akCaster.IsSneaking())
    akCaster.StartSneaking();
  endif
  akCaster.AddPerk(invis);

  Game.ForceThirdPerson();
  Game.DisablePlayerControls(false, false, true, false, false, true, true, true, 0);
  akTarget.SetPlayerControls(true);
  akTarget.EnableAI(true);
  Game.SetCameraTarget(akTarget);
  Game.SetPlayerAIDriven(true);

  tempFactionList = akTarget.GetFactions(-128, 127);	
	int i = 0
	while(i < tempFactionList.Length)
		tempFactionRank[i] = akTarget.GetFactionRank(tempFactionList[i])
	endwhile
	akTarget.RemoveFromAllFactions();
  akTarget.AddToFaction(MagicCharmFaction);

  akTarget.SetAttackActorOnSight(true);

  confidence = akTarget.GetAV("Confidence");
  aggression = akTarget.GetAV("Aggression");
  akTarget.SetAV("Confidence", 5);
  akTarget.SetAV("Aggression", 3);
  ; akTarget.StopCombat();
  akTarget.SetAlert(true);

  ; RegisterForControl("Activate");
  ; RegisterForAnimationEvent(akTarget, "JumpStart");
  ; RegisterForAnimationEvent(akTarget, "JumpFall");
  ; RegisterForAnimationEvent(akTarget, "JumpFallDirectional");

endEvent

Event OnEffectFinish(Actor akTarget, Actor akCaster)
	if (active)
		active = false;
		akTarget.SetPlayerControls(false);
		akTarget.EnableAI(true);
		Game.EnablePlayerControls(true, true, true, true, true, true, true, true, 0);
		Game.SetPlayerAIDriven(false);
		Game.GetPlayer().EnableAI(true);
		Game.SetCameraTarget(akCaster);
		akTarget.SetAV("Confidence", confidence);
		akTarget.SetAV("Aggression", aggression);
		; akTarget.StopCombat();

    int i = 0
		while(i < tempFactionList.Length)
			;debug.Notification(tempFactionRank);
			TheTarget.SetFactionRank(tempFactionList[i], tempFactionRank[i])
		endwhile
    TheTarget.RemoveFromFaction(MagicCharmFaction);

    akTarget.SetAttackActorOnSight(false);
    ; Debug.ToggleCollisions()
    ; akCaster.SetGhost(false);
	
		akCaster.RemovePerk(invis);

    if leftSpell
      akCaster.EquipSpell(leftSpell, 0)
    endif
    if rightSpell
      akCaster.EquipSpell(rightSpell, 1)
    endif
    if currentVoice
      akCaster.EquipShout(currentVoice)
    endif

    ; akCaster.moveto(akTarget)
	endif
  God_Suit_Global_IsControlling.Mod(-1);

  UnregisterForUpdate();
endEvent

; Event OnControlUp(string control, float HoldTime)
;   ; debug.messageBox("===== OnControlUp ===== " + control);
; 	if (control == "Activate")
; 		self.Dispel();
; 	endif
; endEvent

Event OnAnimationEvent(ObjectReference akSource, string asEventName)
  ; debug.Notification("===== OnAnimationEvent ===== " + asEventName);
  ; TheTarget.PlayIdle(OffsetStop)
	; ObjectReference ref = TheTarget.PlaceAtMe(marker, 1);
	; ref.KnockAreaEffect(0.1, 10);
	; ref.Delete();
endEvent

Event OnDying(Actor akKiller)
  Dispel();
EndEvent

; -----

Event OnUpdate()
  if !TheCaster.IsWeaponDrawn();
    Dispel();
    return
  endif
  if (active)
		TheTarget.SetAV("Confidence", 5);
		TheTarget.SetAV("Aggression", 3);
		TheTarget.SetAlert(true);
	endif
endEvent


EVENT onLoad()
  debug.Notification("onLoad")
  if !(TheCaster.hasMagicEffect(God_Suit_Possession))
    Dispel()
  endif
endEVENT
; -----
```