# Miniloaders

This mod introduces miniloaders, 1x1 entities that efficiently transfer a full
belt worth of items into and out of containers, including train cargo wagons.

![Miniloaders in action with cargo wagons](resources/wagon.png)

They use no Lua when running, keeping your factory's UPS healthy.

![Miniloader UPS usage](resources/ups_cost.png)

You can use them to feed your high-speed assemblers,

![Miniloader assembler feed](resources/assemblerdemo.png)

or put them in your bus as single-belt lane rebalancers.

![Miniloaders lane balancer](resources/rebalance.png)

Green and purple belts from Bob's Logistics are fully supported.

## Balancing

Miniloaders require stack inserter research, are relatively expensive to build,
and consume approximately the power of two fully-upgraded stack inserters.

## How it works

Each miniloader hides a set of very fast invisible inserters, one for each lane
of the belt.  Lua scripting adjusts pickup and drop points accordingly when the
direction of the miniloader is changed.

Since item movement is handled by inserters, there is no on_tick handler, no Lua
impact on UPS, and miniloaders will benefit from any future improvements to belt
and inserter performance made by Wube in the Factorio core.

## Filtering

Versions of miniloaders with and without filtering are available once the
appropriate technology has been researched.  As you would expect, to build a
miniloader capable of filtering, you must use filter inserters as ingredients.

Note that filter miniloaders behave like filter inserters, and not like vanilla
loaders: if no filters are set then no items will be moved. You must set at
least one filter.

## Known Issues

* The power usage UI counts each miniloader multiple times, since it shows the
  power used by the inserters, not the miniloaders themselves.
* Miniloaders cannot be fast-replaced due to the invisible entities blocking
  placement of the new entity.
* Miniloader arrows don't always appear correctly in blueprints.

## Ultimate Belts Caveats and Warnings

__Ultimate Belts support is in BETA state.__

Factorio core engine limitations restrict inserters pulling from belts to
60 items/second, or 4.5x yellow belt speed. Further, loader entities are
restricted to 120 items/second.

Miniloaders at "Ultra fast" and faster speeds use vanilla loader entities in
addition to inserters, giving a max throughput of ~180 items/second when
interacting with chests and other containers. They will _not_ give full
throughput when loading cargo wagons, and circuit control is disabled since
vanilla loaders cannot be circuit controlled.

## Acknowledgements

* Arch666Angel &mdash; for the original 2x1 loader graphics, cut down to 1x1
  with permission in versions through 1.5.x.
* Articulating &mdash; for the original Loader Snapping.
* Optera &mdash; for Loader Redux's revised and improved loader snapping code, adapted
  here for Miniloaders with permission.

## Version History

* 1.0.0 (2017-12-01):
    * Initial release.
* 1.1.0 (2017-12-03):
    * Add graphics and loader snapping.
* 1.1.1 (2017-12-05):
    * Fix some snapping issues (laying belts to the side of a miniloader, trying to snap to a player, sometimes snapping to the wrong direction when next to a large entities like assemblers).
* 1.1.2 (2017-12-06):
    * Fix critical crash bug when rotating miniloaders.
* 1.1.3 (2017-12-06):
    * Fix basic yellow miniloaders.  Oops.
    * Fix a case where items could be spilled onto adjacent tiles when snapping a miniloader to a belt.
* 1.1.4 (2017-12-11):
    * Remove orphan inserters left behind by yellow miniloaders if removed while 1.1.0-1.1.2 was installed.
    * Make snapping less aggressive.  Miniloaders should only turn 180 degrees, not 90 degrees, to better match behavior from Loader Redux.
* 1.1.5 (2017-12-14):
    * Remove the problematic separate force for miniloader inserters, and set a stack size override instead.
* 1.2.0 (2017-12-14):
    * Update to Factorio 0.16.
* 1.3.0 (2017-12-18):
    * Rebalance ingredient costs.
    * Make yellow miniloader accessible before oil.
* 1.4.0 (2018-01-07):
    * Redesign using 0.16 customized loader entities instead of underground belt to provide belt connectivity.
    * Add support for controlling miniloaders through the circuit network. 
    * Add optional filtering support for miniloaders.
* 1.4.1 (2018-01-09):
    * Fix crash when placing underground belt with a miniloader on the opposite side.
    * Fix migration issue from 1.2.0-1.3.0 causing belt items to spill on the ground.
* 1.4.2 (2018-01-09):
    * Fix broken migration of yellow miniloaders.
    * Fix broken localization of items in hand.
* 1.4.3 (2018-01-09):
    * Apply migration to saves with v1.4.1.
* 1.5.0 (2018-01-12):
    * Separate filter miniloaders into their own entities.
    * Fix crash when connecting miniloaders directly to arithmetic or decider combinators.
    * Existing miniloaders will lose their filtering capabilities. Sorry for the inconvenience!
* 1.5.1 (2018-01-14):
    * Enable filter inserter recipes when migrating from pre-1.5.0.
* 1.5.2 (2018-01-14):
    * Fix blueprints having duplicate overlapping miniloaders.  Any blueprints in your inventory should be fixed, but blueprints in chests may need to be cleared and re-created.
    * Fix building miniloaders with Nanorobots.
    * Disable PickerExtended's dolly feature, since it can only move parts of miniloaders, breaking them.
* 1.5.3 (2018-01-15):
    * Reenable PickerExtended dolly. Thanks to Nexela for the fix suggestion.
    * Fix setting a blueprint that includes no entities, only tiles.
* 1.5.4 (2018-01-17):
    * Fix crash when alt-selecting with blueprint.
    * Fix crash during blueprinting.
* 1.5.5 (2018-01-18):
    * Add compatibility with upgrade-planner.
    * Ghosts can now be placed over miniloaders marked for deconstruction.
* 1.5.6 (2018-01-19):
    * Change recipes to use lower tiers of miniloaders as ingredients.
    * Add BETA support for Ultimate Belts mod.  See caveats and warnings above.
* 1.5.7 (2018-01-22):
    * Make sure stack size override is reset on non-circuit-controlled inserters.
    * Potentional fix for reported Omnimatter mod incompatibility.
* 1.5.8 (2018-02-06):
    * Using Upgrade Planner on miniloaders now preserves complex items (configured blueprints, armor with inventory, etc.)
    * Fix building over an existing miniloader with a blueprint where that miniloader is connected to the circuit network.
* 1.5.9 (2018-02-06):
    * Remove stray debugging code.
* 1.5.10 (2018-02-08):
    * Shrink miniloader collision box.
    * Fix crash related to placing rail blueprints.
    * Fix crash related to rapidly drag-building blueprints.
* 1.5.11 (2018-02-20):
    * Fix event sync problem on joining a multiplayer server.
* 1.5.12 (2018-03-05):
    * Fix additional event sync corner cases on joining a multiplayer server.
    * Fix crash when mining a miniloader with an opened GUI.
    * Fix filter miniloader recipes to use previous tiers of filter miniloaders instead of unfiltered miniloaders.
* 1.5.13 (2018-03-06):
    * Remove stray debug logging to console.
    * Optimize graphics to reduce download size.
* 1.5.14 (2018-03-12):
    * Fix crash when mining miniloader in Factorio 0.16.29.
* 1.5.15 (2018-03-12):
    * Fix another crash when mining miniloaders in Factorio 0.16.29.
    * Add support for boblogistics inserter overhaul.
* 1.5.16 (2018-03-18):
    * Change ingredients when using boblogistics inserter overhaul.
* 1.5.17 (2018-03-31):
    * Significant overhaul to boblogistics support, now that Bob's top-tier belts are called Ultimate transport belts, introducing a conflict with the Ultimate Belts mod.
    * Increased speed of miniloader belt-to-container throughput, enabling them to keep up with fast transport belts.
* 1.5.18 (2018-04-01):
    * Increased miniloader inserter speed again slightly to better handle inline belt-to-belt use.
    * Fix load error with Ultimate Belts.
    * Fix a possible error when joining a multiplayer server.
* 1.5.19 (2018-04-04):
    * Fix compatibility with Ultimate Belts 0.16.4.
* 1.5.20 (2018-05-02):
    * Add filter miniloader support for Ultimate Belts.
    * Fix upgrade planner crash where loader belts have insufficient room for items.
    * Work around for bug in Creative Mode's instant deconstruction cheat.
    * Fix icon appearance when other mods add multi-layer icons to underground belts.
    * Fix case where mining the last entity connected to a miniloader via circuit left the miniloader inoperative.
* 1.5.21 (2018-05-24):
    * Fix Ultimate Belts miniloaders not yielding an item when mined.
    * Fix bug with Upgrade Planner integration that could sometimes cause upgraded miniloaders to not be returned to the player's inventory.
* 1.5.22 (2018-06-12):
    * Fix bug where placing a miniloader by hand over a configured blueprint ghost only configured one of the miniloader inserters.
* 1.5.23 (2018-07-26):
    * Fix crash when getting a bad on_put_item event from buggy other mods.
    * Fix wire connections not appearing on ghosts autoplaced when an entity dies.
* 1.6.0 (2018-09-21):
    * New vanilla-inspired graphics that don't overlap with adjacent buildings.
    * Fix some cases where miniloaders rarely snap to the wrong entity.
    * Remove references to priority-split usecase now that Factorio core supports splitter priority.
* 1.6.1 (2018-09-25):
    * Fix reversed colors in recent versions of boblogistics.
* 1.6.2 (2018-10-07):
    * Fix unintended removal when deconstructing tiles under miniloaders.
    * Restore filter icons in info mode.
    * Fix a case where robots could lose a mined miniloader.
    * Expose circuit connector graphics.
* 1.6.3 (2018-10-08):
    * Add support for FactorioExtended-Plus-Transport.