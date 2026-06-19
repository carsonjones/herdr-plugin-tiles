# hedr tiles

a tiny herdr plugin for pane management

| action         | what it does                                  | suggested key      |
|----------------|-----------------------------------------------|--------------------|
| `h-wide`       | horizontal split, current pane = left **6/10**| `prefix+y`         |
| `h-narrow`     | flip → current pane = left **4/10**          | `prefix+shift+y`   |
| `h-even`       | revert → horizontal **50/50**                | `prefix+alt+y`     |
| `v-top-small`  | vertical split, current pane = top **1/5**    | `prefix+u`         |
| `v-top-large`  | flip → current pane = top **4/5**            | `prefix+shift+u`   |
| `v-even`       | revert → vertical **50/50**                  | `prefix+alt+u`     |

`prefix+y` = horizontal, `prefix+u` = vertical
`shift` modifier: **flips** the big/small side
`alt` modifier **reverts** to an even 50/50 split

## install

```sh
herdr plugin install github.com/carsonjones/herdr-plugin-tiles
```

## keybindings

add to `~/.config/herdr/config.toml` (this repo's `herdr/config.toml`). these keys avoid herdr's built-in defaults: `prefix+y` = horizontal, `prefix+u` = vertical, with `shift` to flip and `alt` to revert to 50/50.

```toml
[[keys.command]]
key = "prefix+y"
type = "plugin_action"
command = "local.tiles.h-wide"
description = "tile: horizontal, current 6/10 left"

[[keys.command]]
key = "prefix+shift+y"
type = "plugin_action"
command = "local.tiles.h-narrow"
description = "tile: horizontal flip, current 4/10 left"

[[keys.command]]
key = "prefix+alt+y"
type = "plugin_action"
command = "local.tiles.h-even"
description = "tile: horizontal revert, even 50/50"

[[keys.command]]
key = "prefix+u"
type = "plugin_action"
command = "local.tiles.v-top-small"
description = "tile: vertical, current 1/5 top"

[[keys.command]]
key = "prefix+shift+u"
type = "plugin_action"
command = "local.tiles.v-top-large"
description = "tile: vertical flip, current 4/5 top"

[[keys.command]]
key = "prefix+alt+u"
type = "plugin_action"
command = "local.tiles.v-even"
description = "tile: vertical revert, even 50/50"
```


## local dev

```
# clone this repo
herdr plugin link .
herdr plugin action list --plugin herdr.tiles   # verify it loaded
```

> **editing actions?** after you change `herdr-plugin.toml` (add/rename/remove
> an action), re-run `herdr plugin link <path>` to re-register the action list.
> `herdr server reload-config` only re-reads keybindings — it does **not**
> refresh plugin actions, so new actions will fail with `plugin action not
> found` until you re-link. verify with `herdr plugin action list --plugin
> local.tiles`.

> **note:** requires a herdr build whose socket API exposes the plugin runtime
> (`plugin.*` requests). On herdr 0.7.0 the `herdr plugin …` CLI exists but the
> daemon may reject `plugin.link` with `unknown variant 'plugin.link'` — that
> build can't load plugins yet. the pane primitives the plugin uses
> (`pane split`/`resize`/`layout`/`get`) all work, so you can run it directly:
>
> ```sh
> HERDR_PANE_ID=$(herdr pane current 2>/dev/null) python3 tile.py h 0.6
> ```

