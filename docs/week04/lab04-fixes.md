# Lab 04 — Fix log

Rule of thumb: constraints go down, sizes go up, parent sets position.

| # | Widget | Error / symptom | Rule broken | Fix |
|---|--------|-----------------|-------------|-----|
| 1 | StoreHeader | Overflow on the right at 320 dp | The Row gave the Column/Text unbounded width | `Expanded` around the Column + `maxLines` + ellipsis |
| 2 | StoreHeader | Rating text pushed past the edge | Too many non-flexible children in one Row | Moved the rating into the Column under the hours, `Flexible` + ellipsis |
| 3 | CategoryBar | Overflow on the right (6 chips) | A Row cannot scroll or wrap; it asked for more width than the parent has | Wrapped in horizontal `SingleChildScrollView` |
| 4 | PromoStrip / PromoCard | Overflow on the right (2 × 200 dp) | Hard-coded width ignores the width the parent gives | `Expanded` on each card; removed `SizedBox(width: 200)` |
| 5 | PromoCard | Text cut off / overflow at the bottom | Fixed `height: 150` and Text without limit | Removed fixed height, `IntrinsicHeight` + stretch in the strip, `maxLines` + ellipsis |
| 6 | PromoStrip | RangeError with 0 or 1 promo | Code assumed the data exists (`promos[0]`, `promos[1]`) | Strip only built if promos exist; `second` is nullable |
| 7 | MenuScreen body | Overflow at the bottom in landscape / keyboard | A Column of fixed-height blocks + `Expanded` list inside a short parent | One `CustomScrollView`: header, search, chips, promos and list all scroll together |
| 8 | MenuScreen list | 500 items built at once | `ListView(children: [...])` builds everything | `SliverList.builder` (lazy) |
| 9 | MenuTile | Overflow on the right with a long name | The Row gave the Column unbounded width; `Spacer` did not limit the name | `Expanded` around the name Column, `maxLines: 2` + ellipsis (Spacer removed) |
| 10 | MenuScreen | Breakpoint reacts to the window, not to the space given | `MediaQuery.sizeOf` reads the screen, not the parent's constraints; also `> 600` instead of `>= 600` | `LayoutBuilder`, `constraints.maxWidth >= 600` |
| 11 | MenuScreen grid | Cards overflow at the bottom, eager grid | `crossAxisCount: 4` fixed and default aspect ratio 1; `GridView.count` not lazy | `SliverGrid` with `MaxCrossAxisExtent` + `childAspectRatio`, lazy builder delegate |
| 12 | MenuCard | Overflow at the bottom, long name | Fixed image `height: 110` + Text without limit | Image in `Expanded` (takes leftover height), `maxLines` + ellipsis on name, price, button |
| 13 | CartBar | Overflow on the right | Fixed `height: 72`, unbounded Text, fixed button `width: 160` | `minHeight`, `Expanded` Text with `maxLines: 2`, button sized by its label |
| 14 | CartBar | Button under the gesture bar | Ignored the system padding the parent reports | `SafeArea(top: false)` inside a `ColoredBox` |
| 15 | MenuScreen body | Content under the notch in landscape | Ignored left/right insets | `SafeArea(top: false, bottom: false)` around the body |
| 16 | MenuScreen | Blank screen with zero items (and no result for a search) | Code assumed the data exists | `EmptyState` with icon, message, action, `key: const Key('empty-state')` |
| 17 | MenuScreen | Keyboard leaves no room on a short screen | Cart bar + keyboard + app bar ate the height | Cart bar hidden while the keyboard is open |

