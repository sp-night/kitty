<p align="center">
  <a href="https://sp-night.github.io">
    <img src="https://raw.githubusercontent.com/sp-night/sp-night.github.io/main/public/logo-noite.svg" width="120" alt="SP Night — the Pico do Jaraguá at dusk, aviation beacon lit, the city's lights at the foot of the range">
  </a>
</p>

<h1 align="center">SP Night for <a href="https://sw.kovidgoyal.net/kitty/">kitty</a></h1>

<p align="center">
  <strong>The sodium lamp turns the whole city this colour.</strong><br>
  A dark colour scheme with São Paulo as its reference — the sodium street lamp,<br>
  exposed concrete, the free span of the MASP, the drizzle before the rain.
</p>

<p align="center">
  <a href="https://sp-night.github.io"><strong>sp-night.github.io</strong></a>
  &nbsp;·&nbsp;
  <a href="https://sp-night.github.io/palette">palette</a>
  &nbsp;·&nbsp;
  <a href="https://sp-night.github.io/spec">spec</a>
  &nbsp;·&nbsp;
  <a href="https://sp-night.github.io/ports">ports</a>
</p>

---

## The flavours

All three are dark, by decision. The previews below are synthetic — drawn from the
palette itself, so they can never drift from what you install.

### Noite Paulista — `sp_night_noite.conf`

The city at 3am. Blue-violet dark, the sodium lamp burning warm on top.

![kitty themed with SP Night Noite Paulista](assets/preview-noite.svg)

### Garoa — `sp_night_garoa.conf`

The same window, seen through the drizzle. Flat grey — the garoa does not cool
the city down, it washes it out.

![kitty themed with SP Night Garoa](assets/preview-garoa.svg)

### Pico do Jaraguá — `sp_night_jaragua.conf`

The same night, seen from the city's highest point. Near-black surfaces, with
the forest left to the accents — and the red-and-white tower lit at the summit.

![kitty themed with SP Night Pico do Jaraguá](assets/preview-jaragua.svg)

## Install

kitty reads a theme through an `include` in its own config, so the file goes
next to `kitty.conf` and nothing overwrites it.

Grab the flavour you want (or all three):

```sh
mkdir -p ~/.config/kitty
curl -Lo ~/.config/kitty/sp_night_noite.conf \
  https://raw.githubusercontent.com/sp-night/kitty/main/themes/sp_night_noite.conf
```

Then add the include to `~/.config/kitty/kitty.conf`:

```conf
include sp_night_noite.conf
```

Reload with `ctrl+shift+f5` (`cmd+ctrl+,` on macOS), or open a new window.

> [!NOTE]
> Put the `include` after anything else that sets colours — kitty applies the
> last value it reads, so an earlier `background` in your own config wins.

Prefer a checkout? Clone and copy — the files are plain text, there is no build:

```sh
git clone https://github.com/sp-night/kitty.git
cp kitty/themes/*.conf ~/.config/kitty/
```

## What gets themed

| kitty key | Role | Meaning |
|---|---|---|
| `color0`…`color15` | `ansi.*` | the full 16-colour ANSI mapping |
| `background` / `foreground` | `ui.bg` / `ui.fg` | *laje* under the main text |
| `cursor` / `cursor_text_color` | `ui.cursor` / `ui.on_accent` | the *sódio* cursor, dark text inside it |
| `selection_background` / `_foreground` | `ui.selection` / `ui.fg` | *vidro*, glass reflecting the street |
| `url_color` | `ui.link` | links in *marginal*, the expressway sign |
| `active_border_color` / `inactive_border_color` | `ui.border_active` / `ui.border` | the focused split in *sódio*, the rest in *fiação* |
| `bell_border_color` | `diagnostic.warn` | a bell is a warning, not an accent |
| `active_tab_*` / `inactive_tab_*` | `ui.selection` / `ui.panel` | the active tab lifts to glass, the others stay concrete |
| `tab_bar_background` | `ui.bg_deep` | the tab bar recedes into the *vão* |
| `mark1_background`…`mark3_background` | `ui.accent` / `syntax.type` / `syntax.function` | three marks that have to be told apart, so they differ by hue |

No hex in this repo was picked by hand. Every value comes from the
[SP Night palette](https://sp-night.github.io/palette) through its role layer,
both published as data:
[`palette.json`](https://sp-night.github.io/palette.json) and
[`roles.json`](https://sp-night.github.io/roles.json). The contrast floors those
colours have to clear are [written down in the spec](https://sp-night.github.io/spec)
and enforced in CI.

## The mapping

[`kitty.conf.tmpl`](kitty.conf.tmpl) is the full record of which kitty key means which
role — the table above in complete form. The files in
[`themes/`](themes) are what it resolves to, one per flavour.

You never need it to use the theme: the shipped files are plain text and final.
It is here so the mapping survives, and so a retuned palette can be rolled
through this port without anyone re-deciding what a bell border means.

## License

[MIT](LICENSE)
