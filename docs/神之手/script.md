```c
Scriptname God_Suit_hand_power_script extends ActiveMagicEffect  

  

Spell Property Flames Auto

Spell Property Frostbite Auto

Spell Property Sparks Auto

  

ObjectReference objRef

  

Actor TheTarget

Actor TheCaster

  

Event OnEffectStart(actor akTarget, actor akCaster)

  objRef = akCaster as ObjectReference

  

  TheTarget = akTarget;

  TheCaster = akCaster;

  

  RegisterForAnimationEvent(akCaster, "weaponSwing")

  RegisterForAnimationEvent(akCaster, "weaponLeftSwing")

  ; RegisterForAnimationEvent(akCaster, "PowerAttackStop")

EndEvent

  
  

Event OnAnimationEvent(ObjectReference akSource, string asEventName)

  if (akSource == objRef)

    ;debug.Notification("===== asEventName ===== " + asEventName);

    if (asEventName == "weaponSwing" || asEventName == "weaponLeftSwing")

      int chooseSpell = Utility.RandomInt(0, 2)

      if(chooseSpell == 0)

        Flames.cast(objRef, none)

      elseif(chooseSpell == 1)

        Frostbite.cast(objRef, none)

      else

        Sparks.cast(objRef, none)

      endIf

      Utility.Wait(0.3)

      TheCaster.InterruptCast()

    ; elseif(asEventName == "PowerAttackStop")

      ; debug.Notification(TheTarget);

      ; debug.Notification(TheCaster);

      ; TheCaster.PushActorAway(TheTarget, 10)

    endIf

  endIf

EndEvent
```