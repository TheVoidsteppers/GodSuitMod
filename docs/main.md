```c
Scriptname God_Suit_main_script extends Quest   

; 吸星大法
Spell Property godSuitAttractspell auto
; 哈姆林的遗志
Spell Property godSuitConjureSkeeverspell auto
; 波耶希亚的拥抱
Spell Property godSuitDA02ArmorPoisonCloakspell auto
; 除你武器
Spell Property godSuitDisarmMagicEffectspell auto
; 火焰爆炸
Spell Property godSuitMagicFireDmageFFSelfAreaspell auto
; 寒霜爆炸
Spell Property godSuitMagicFrostDmageFFSelfAreaspell auto
; 荆棘术
Spell Property godSuitMagicMajestyspell auto
; 飞龙探云手
Spell Property godSuitMagicPickpocketspell auto
; 倒地
Spell Property godSuitMagicpushdownspell auto
; 收手吧阿祖
Spell Property godSuitMagicStopItspell auto
; 万界交易术
Spell Property godSuitMagicTradingspell auto
; 解衣卸甲
Spell Property godSuitMagicUnequipspell auto
; 我是火车王
Spell Property godSuitLeeroyJenkins auto
; 快乐星球
Spell Property godSuitMagicStrikeFlyspell auto
; 造物-加林根
Spell Property godSuitMagicCreateJarrinRootspell auto
; 神之眼
Spell Property godSuitEyespell auto
; 死灵术
Spell Property godSuitDeadThrallspell auto


; add armor
; 神格
Armor Property godSuitHoodClothesCirclet auto
; 神威
Armor Property godSuitMajestyArmorClothes auto
; 荆棘
Armor Property godSuitReflectDamageArmorClothes auto
; 隐身戒指
Armor Property godSuitInvisibilityRing auto
; 不死戒指
Armor Property godSuitimmortalRing auto

Event OnInit()
	Game.GetPlayer().AddSpell(godSuitAttractspell)
	Game.GetPlayer().AddSpell(godSuitConjureSkeeverspell)
	Game.GetPlayer().AddSpell(godSuitDA02ArmorPoisonCloakspell)
	Game.GetPlayer().AddSpell(godSuitDisarmMagicEffectspell)
	Game.GetPlayer().AddSpell(godSuitMagicFireDmageFFSelfAreaspell)
	Game.GetPlayer().AddSpell(godSuitMagicFrostDmageFFSelfAreaspell)
	Game.GetPlayer().AddSpell(godSuitMagicMajestyspell)
	Game.GetPlayer().AddSpell(godSuitMagicPickpocketspell)
	Game.GetPlayer().AddSpell(godSuitMagicpushdownspell)
	Game.GetPlayer().AddSpell(godSuitMagicStopItspell)
	Game.GetPlayer().AddSpell(godSuitMagicTradingspell)
	Game.GetPlayer().AddSpell(godSuitMagicUnequipspell)
	Game.GetPlayer().AddSpell(godSuitLeeroyJenkins)
	Game.GetPlayer().AddSpell(godSuitMagicStrikeFlyspell)
	Game.GetPlayer().AddSpell(godSuitMagicCreateJarrinRootspell)
	Game.GetPlayer().AddSpell(godSuitEyespell)
	Game.GetPlayer().AddSpell(godSuitDeadThrallspell)

	Game.GetPlayer().AddItem(godSuitHoodClothesCirclet, 1)
	Game.GetPlayer().AddItem(godSuitMajestyArmorClothes, 1)
	Game.GetPlayer().AddItem(godSuitReflectDamageArmorClothes, 1)
	Game.GetPlayer().AddItem(godSuitInvisibilityRing, 1)
	Game.GetPlayer().AddItem(godSuitimmortalRing, 1)
EndEvent
```