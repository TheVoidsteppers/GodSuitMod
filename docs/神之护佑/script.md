```c
Scriptname God_Suit_immortal_script extends ActiveMagicEffect  

actor property selfRef auto hidden

Spell property DragonhideSpell auto
Spell property EbonyfleshSpell auto
Spell property IronfleshSpell auto
Spell property StonefleshSpell auto


MagicEffect property DragonhideMagicEffect auto
MagicEffect property EbonyfleshMagicEffect auto
MagicEffect property IronfleshMagicEffect auto
MagicEffect property StonefleshMagicEffect auto

float HPStart = 0.90
float HPHurt = 0.70
float HPWarning = 0.40
float HPDanger = 0.10


EVENT OnEffectStart(Actor Target, Actor Caster)
	selfRef = caster
endEVENT


EVENT onHit(ObjectReference akAggressor, Form akSource, Projectile akProjectile, bool abPowerAttack, bool abSneakAttack, bool abBashAttack, bool abHitBlocked)
  if (!selfRef.isDead())
    float ActorValuePercentage = selfRef.getActorValuePercentage("Health")
    if (ActorValuePercentage <= HPDanger)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect))
        DragonhideSpell.Cast(selfRef, selfRef)
      endif
    elseif (ActorValuePercentage <= HPWarning)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect))
        EbonyfleshSpell.Cast(selfRef, selfRef)
      endif
    elseif (ActorValuePercentage <= HPHurt)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect) && !selfRef.HasMagicEffect(IronfleshMagicEffect))
        IronfleshSpell.Cast(selfRef, selfRef)
      endif
    elseif (ActorValuePercentage <= HPStart)
      if (!selfRef.HasMagicEffect(DragonhideMagicEffect) && !selfRef.HasMagicEffect(EbonyfleshMagicEffect) && !selfRef.HasMagicEffect(IronfleshMagicEffect) && !selfRef.HasMagicEffect(StonefleshMagicEffect))
        StonefleshSpell.Cast(selfRef, selfRef)
      endif
    endif
  endif
endEVENT
```