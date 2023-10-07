```c
Scriptname God_Suit_immortal_script extends ActiveMagicEffect  

actor property selfRef auto hidden

Spell property FastHealingSpell auto
Spell property CloseWoundsSpell auto
Spell property godSuitHealRate700spell auto
Spell property godSuitHealRate500spell auto
Spell property godSuitHealRate300spell auto
Spell property godSuitHealRate100spell auto

Spell property DragonhideSpell auto
Spell property EbonyfleshSpell auto
Spell property IronfleshSpell auto
Spell property StonefleshSpell auto


MagicEffect property DragonhideMagicEffect auto
MagicEffect property EbonyfleshMagicEffect auto
MagicEffect property IronfleshMagicEffect auto
MagicEffect property StonefleshMagicEffect auto

float HP90 = 0.90
float HP70 = 0.70
float HP60 = 0.60
float HP30 = 0.30


EVENT OnEffectStart(Actor Target, Actor Caster)
	selfRef = caster
endEVENT


EVENT onHit(ObjectReference akAggressor, Form akSource, Projectile akProjectile, bool abPowerAttack, bool abSneakAttack, bool abBashAttack, bool abHitBlocked)
  if (!selfRef.isDead())
    float ActorValuePercentage = selfRef.getActorValuePercentage("Health")
    if (ActorValuePercentage <= HP30)
      CloseWoundsSpell.Cast(selfRef, selfRef)
      godSuitHealRate700spell.Cast(selfRef, selfRef)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect))
        DragonhideSpell.Cast(selfRef, selfRef)
        ;debug.Notification("20% DragonhideSpell Cast")
      endif
      ;debug.Notification("20% Effect, current health " + ActorValuePercentage)
    elseif (ActorValuePercentage <= HP60)
      FastHealingSpell.Cast(selfRef, selfRef)
      godSuitHealRate500spell.Cast(selfRef, selfRef)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect))
        EbonyfleshSpell.Cast(selfRef, selfRef)
        ;debug.Notification("40% EbonyfleshSpell Cast")
      endif
      ;debug.Notification("40% Effect, current health " + ActorValuePercentage)
    elseif (ActorValuePercentage <= HP70)
      godSuitHealRate300spell.Cast(selfRef, selfRef)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect) && !selfRef.HasMagicEffect(IronfleshMagicEffect))
        IronfleshSpell.Cast(selfRef, selfRef)
        ;debug.Notification("60% IronfleshSpell Cast")
      endif
      ;debug.Notification("60% Effect, current health " + ActorValuePercentage)
    elseif (ActorValuePercentage <= HP90)
      godSuitHealRate100spell.Cast(selfRef, selfRef)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect) && !selfRef.HasMagicEffect(IronfleshMagicEffect) && !selfRef.HasMagicEffect(StonefleshMagicEffect))
        StonefleshSpell.Cast(selfRef, selfRef)
        ;debug.Notification("80% StonefleshSpell Cast")
      endif
     ;debug.Notification("80% Effect, current health " + ActorValuePercentage)
    endif
  endif
endEVENT
```