# HPBar & HP Tracker Mod

This mod displays a HP bar and info about the target being aimed at. It also provides a HP tracker for boss monsters that is visible for all players including spectators.

This mod is designed to work with all mods (sans those that come with their own HP bars, e.g. WoC and DnD) and provides special name pretty-printing for popular Complex Doom mods (LCA, RM, HAF, Ark, ILCA) and RGA2. Server hosts can further customize the behavior via cvars to support other mods.

## CVars

* `hpbar_style` (user): Choose how the HP bar is displayed. (default: 1)
  * 0: Disable HP bars.
  * 1: Show a full HP bar with monster infomation at top.
  * 2: Show target HP percentage under the crosshair.
* `hpbar_threshold` (server): Only display HP bars for monsters with more spawn HP than this value. It can be used to reduce bandwidth usage (as health info for lesser monsters won't be sent over the network) or to reduce visual clutter when fighting monsters of different levels. (default: 0)
* `hpbar_tracker` (server): Set whether to enable the HP tracker. (default: true)
* `hpbar_tracker_x` (server): The x position of the HP tracker, from 0.0 (left) to 1.0 (right). (default: 0.02)
* `hpbar_tracker_y` (server): The y position of the HP tracker, from 0.0 (top) to 1.0 (bottom). (default: 0.58)
* `hpbar_tracker_threshold` (server): Set the minimal spawn health monsters must have to appear in the global tracker. (default: 2000)
* `hpbar_show_friendly` (user): Set whether to show HP bars for friendly targets. (default: false)
* `hpbar_rekt` (server): Set whether to count and show the number of players killed by a monster. You need to restart the map after altering this variable to apply the changes. (default: true)
* `hpbar_announcer` (user): Whether to play announcer messages and voices when monsters achieve certain kills. (default: true)

### `hpbar_name_*`

Server hosts can customize the display name of monsters by setting the `hpbar_name_$actor` cvar. This can be useful if you are loading mods that aren't supported by hpbar yet or want to change the default formatting set by hpbar. For example, you can make Cacodemons (actor name: `Cacodemon`) to be displayed as `Hissy` by setting:

```
set hpbar_name_Cacodemon Hissy
```

### `hpbar_track_*`

You can control whether a monster is tracked by the HP tracker by setting `hpbar_track_$actor` to `1` (always track) or `-1` (never track). This takes precedence over `hpbar_tracker_threshold` which allows you to set it on a per monster basis. For instance, to always track Cacodemons:

```
set hpbar_track_Cacodemon true
```

### `hpbar_map_*`

This provides a normalization mapping from actor names to actor names to be used in `hpbar_name_*` and `hpbar_track_*`. For example, HAF replaces `LegendaryImp` with the slightly modified `LegendaryImp2`, so we provide a mapping `hpbar_map_LegendaryImp2` to `LegendaryImp` and `LegendaryImp2` will now reuse the display name and tracking rules of `LegendaryImp`.

## Notes for Modders

To support customized names for monsters in your mod, simply add the name to be displayed in the `TAG` property of the monster actor. Monsters with the `BOSS` flag set is also tracked by default regardless of its HP.

## Source

https://github.com/pkmx/hpbar

## Credits

* Graphics for HP bar: Wrath of Cronos (Thetis)
* Announcer sounds: Unreal Tournament (Epic Games)
