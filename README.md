# Lodestar Guides for Polestar (unofficial)

The free World of Warcraft: Forever leveling guides of
[Lodestar](https://github.com/danielcosta42/lodestar) (levels 1 to 60, both
factions), converted to the guide format of
[Polestar](https://github.com/fitzforge/polestar).

This is a **community addon for Polestar**. It is **not made, endorsed or
supported by Lodestar's author or by Polestar**. Report problems with it here,
not to either of them.

## What's in it

86 leveling guides, the whole of Lodestar's `Leveling` library, in Polestar's
guide menu under Community guides. Each guide is one zone at a time, as in
Lodestar, and hands over to the next with `next` the way the original does.

| Faction | Guides | Start zones |
|---|---|---|
| Alliance | 47, levels 3-60 | Elwynn Forest (3-10), Dun Morogh (4-10), Teldrassil (4-11), Zephras Isle (5-12, Skyborne) |
| Horde | 39, levels 4-60 | Mulgore (4-10), Durotar (5-12), Tirisfal Glades (5-12), Zephras Isle (5-12, Skyborne) |

Lodestar's dungeon, class-quest, reputation, event and attunement guides are
not included.

## Install

1. Install **Polestar 0.2.6 or newer** first.
2. Download `PolestarPack_Lodestar-<version>.zip` from this project's
   [releases](https://github.com/petllama/lodestar-guides/releases) and unzip it
   into `Interface/AddOns/`, next to `Polestar`.
3. Restart the game. The guides show in Polestar's guide menu
   (`/polestar guides`) under Community guides; Options › Community guides
   (`/polestar packs`) turns the addon on or off.

You don't need Lodestar itself, and it's best not to run both guide addons at
once (both automate quest dialogs).

## How it differs from the original

The conversion is automatic. The route, the quests and the step notes are
Lodestar's; how they run is Polestar's. Both are built on the same open quest
data (QuestieDB), so every quest, NPC, item and object keeps its id. Known
differences:

- **Givers and spawns come from Polestar's data.** Accept and turn-in steps
  point at the quest giver Polestar knows. Kill and loot steps keep Lodestar's
  spot unless it is far from every spawn Polestar knows, in which case Polestar
  picks the nearest spawn.
- **Step conditions** become Polestar's `only` (class and race) and `when`
  (quest in the log, quest turned in, level, items in bags). One kind has no
  equivalent: "show this step once *any one* of these quests is turned in"
  (73 steps). Those steps always show; Polestar's quest data still keeps an
  accept hidden until the quest can really be taken.
- **Objectives** are tracked by the quest objective, so "use the item on
  them" steps finish when the quest log counts the objective.
- **Elite-only objectives** are optional, with a "group up" note, so a solo
  player isn't stuck on them. The step still lists them.
- **Flight paths:** Lodestar's "get the flight path from <flight master>"
  notes are Polestar flight-path goals that check off when you learn it.
- Quest automation, the arrow, map pins and the guide window are Polestar's,
  with its own settings. Lodestar's XP pace HUD, report card and other extras
  are not part of this.

[`reports/`](reports) lists every condition the conversion dropped
(`conversion.json`) and every automatic fix applied from Polestar's checks
(`lint-fixes.json`).

## Licence and attribution

The guides are an adaptation of Lodestar's leveling guides:

- **Source:** [danielcosta42/lodestar](https://github.com/danielcosta42/lodestar),
  the files `Guides/Leveling/*/*.lua`, at the commit named in
  [SOURCE.md](SOURCE.md). © 2026 Daniel Costa (danielcosta42).
- **Licence of the source:** MIT (full text in [LICENSE](LICENSE)). Lodestar's
  routes are generated from [QuestieDB](https://github.com/Questie/QuestieDB);
  thanks to the Questie team.
- **Changes:** converted to Polestar's `.guide` format: conditions rewritten,
  quest objectives, NPCs and items resolved against Polestar's reference data,
  and markup Polestar can't show turned into plain text. Lodestar's addon code
  isn't included.

This adaptation is released under the same **MIT** licence.

The built addon also contains facts from Polestar's reference data (quest,
NPC and map data), which Polestar's compiler places in it. Polestar's
[licence exception](https://github.com/fitzforge/polestar/blob/main/LICENSE-EXCEPTION.md)
lets a compiled pack carry them under the pack's own terms.

"Lodestar" names the source of the guides; no trademark rights are claimed.

## Building it

The pack is built from the `.guide` files in `guides/` with Polestar's own
tools (Node 24+, Lua 5.1, a Polestar clone with `npm link`, its reference data
built with `polestar data build` and `polestar travel build`):

```sh
polestar lint       # check the guides against the game's data
polestar playtest   # play every guide to the end in the real addon
polestar pack       # write the release zip to dist/
```

The `.guide` files are generated. Fix a problem in a guide by opening an issue
here: hand edits are lost at the next conversion from a newer Lodestar source.
