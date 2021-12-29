## No-Bling DOTA "GlanceValue" restoration mod  
#### We have not reached TF2 levels of visual diarrhea in 2020 but we're getting awfully close...  

### Glance  
<table>  
  <tr>  
    <td><img src="https://i.imgur.com/yeN2UfR.png"></td>  
    <td><img src="https://i.imgur.com/crjotHs.png"></td>  
  </tr>  
  <tr>  
    <td><img src="https://i.imgur.com/JShyXKs.png"></td>  
    <td><img src="https://i.imgur.com/vT1ihiw.png"></td>  
  </tr>  
</table>  

### About  
A competent companion to *Settings -- Video -- Effects Quality* with the main focus on GlanceValue.  
No-Bling<sup>tm</sup> mod is economy-friendly, gracefully disabling particle spam while leaving hats model untouched _by default_.  
Might say it even helps differentiate great artistic work, shadowed by the particle effects galore Valve slaps on top.  

#### Before you ask about VAC:  
Don't worry, this is a perfectly safe, well intended, hats friendly, good behaviour cosmetic-only mod,  
optimally swapping just original Valve authored files with no 3^rd party content alteration whatsoever,  
and whitelist-able at a glance...  

### How to use  
Get the repository as zip, extract all files  
Execute `No-Bling-builder.bat` script on Windows or `No-Bling-builder.sh` on Linux  
Then add launch option `-tempcontent` if not already present.  
Run the script before launching DOTA to have an always up to date mod and prevent schema mismatch errors.  
A desktop shortcut is created to run the builder quicker, without compiling and with previous choices.  

### Back in Beta  
Choices are a work in progress - not as feature-rich and complete as the old script, but we will get there..  
Filters on the other hand are more complex and useful.  

#### Getting started with user filters  
Script uses a rather block first, white-list later aproach, so various issues need to be corrected via hard-coded filters.  
Most filters use item numbers (ids) but also generic hero and slot names.  
Basically:  
~ See generated `items_reference.txt` with only the relevant items included and portraits section removed.  
~ Search for a partial item name; note item "number", note `used_by_heroes`, note `item_slot` (if missing, assume "weapon").  
~ Use details learned above to create your user filters exceptions in a `No-Bling-filters.txt` file:  
``` cpp
"user-filters"
{
  keep_item "12930,13456"  // keep item id 12930 : Eminence of Ristul and 13456 : Crown of the One True King
}
```

A more advanced `No-Bling-filters.txt` file example with resource replacement:  
``` cpp
"user-filters"
{
  keep_soundboard "TI10_Ceeeb,Brutal"      // see scripts/chat_wheel.txt
  keep_rarity     "legendary,ancient"
  keep_slot       "head,voice"
  keep_hero       "npc_dota_hero_crystal_maiden,npc_dota_rattletrap_cog"
  keep_item       "12930,13456,12,38"
  keep_model      "4004,6054"
  keep_visuals    "4004"
  keep_ability    "7978"
  keep_ambient    "6694"

  // replace id1 with id2 content or { defined manually }
  38 7385
  12 {
    "model_player"    "models/items/kunkka/kunkka_shadow_blade/kunkka_shadow_blade.vmdl"
    "visuals"
    {
      "asset_modifier0"
      {
        "type"    "particle"
        "asset"   "particles/units/heroes/hero_kunkka/kunkka_weapon_glow_ambient.vpcf"
        "modifier"    "particles/econ/items/kunkka/kunkka_weapon_shadow/kunkka_weapon_glow_shadow_ambient.vpcf"
      }
      "asset_modifier3"
      {
        "type"    "particle_create"
        "modifier"    "particles/units/heroes/hero_kunkka/kunkka_weapon_glow_ambient.vpcf"
      }
    }
  }

  // Can also make use of the internal filters format:
  replace_item {
    246 { visuals{} }
    247 246
  }
  replace_visuals {
    6972 5712                              // explicit id1 "visuals" = id2 "visuals"
    npc_dota_hero_furion { weapon 4159 }   // generic hero - slot "visuals"  = id2 "visuals"
  }
  keep_asset {
    npc_dota_hero_warlock ability_ultimate // generic keep hero - slot having "type" "particle"
  }
  keep_modifier {
    npc_dota_hero_skywrath_mage weapon     // generic keep hero - slot having "type" "particle_create"
    particles/units/heroes/hero_juggernaut/juggernaut_blade_generic.vpcf -
  }
}
```

#### TODO  
Expand choices; populate internal filters; fix visual issues; seek feedback;  thank you for your patience!  

Published under [MIT](LICENSE) license.  
