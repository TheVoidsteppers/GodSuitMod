```c
Scriptname God_Suit_reflect_script extends ActiveMagicEffect  

Actor TheTarget
Actor TheCaster

bool debounceReflect = false

EVENT OnEffectStart(Actor akTarget, Actor akCaster)
	TheTarget = akTarget;
  TheCaster = akCaster;
endEVENT


EVENT onHit(ObjectReference akAggressor, Form akSource, Projectile akProjectile, bool abPowerAttack, bool abSneakAttack, bool abBashAttack, bool abHitBlocked)
  bool aggressorIsActor = (akAggressor as Actor) as bool
  if (!TheCaster.isDead() && aggressorIsActor)
    ; If it was hit by a weapon it's either an arrow or melee attack
    if (akSource as Weapon)
      ; If it has this keyword then it's an arrow that hit us, if not then it's a melee attack
      if (akProjectile)
        ; debug.Notification("ARROW'D by bow " + akSource + " with arrow " + akProjectile)
      else
        ; debug.Notification("abPowerAttack " + abPowerAttack + ", abHitBlocked " + abHitBlocked)
        if (abPowerAttack && abHitBlocked)
          Actor reflectTarget = akAggressor as Actor
          ; debug.Notification("Blocked by weapon PowerAttack" + akSource)
          reflectTarget.PushActorAway(reflectTarget, 15)
        endif
      endif
      ; If not a weapon then lets check if it's a spell
    elseif(((akSource as Spell) as bool) || ((akSource as Enchantment) as bool))
      if (!debounceReflect)
        bool isBlocking = TheCaster.GetAnimationVariableBool("isBlocking") == TRUE
        ; debug.Notification("Blocked " + abHitBlocked + " " + isBlocking)
        debounceReflect = true
        if((akSource as Spell).IsHostile() && isBlocking)
          (akSource as Spell).cast(TheCaster, akAggressor)
        endif
        debounceReflect = false
      endif
    else
      ; debug.Notification("Hit by nothing?")
    endif
  endif
endEVENT

```