# Herdr Drop plugin for Omarchy

An Omarchy Shell bar widget for
[Herdr Drop](https://github.com/lixenstrand/omarchy-herdr-drop). It shows live
Herdr agent status, toggles the persistent drop-down, and draws a connector
that follows the active Omarchy popup theme.

[![Herdr Drop on a full Omarchy desktop](https://raw.githubusercontent.com/lixenstrand/omarchy-herdr-drop/main/assets/herdr-drop-demo-laptop.gif)](https://github.com/lixenstrand/omarchy-herdr-drop)

## Requirements

- Omarchy Quattro with third-party shell plugin support
- [Herdr](https://herdr.dev/)
- [Herdr Drop v1.6.2 or newer](https://github.com/lixenstrand/omarchy-herdr-drop/releases/tag/v1.6.2)
- `jq`, `hyprctl`, and `socat`
- Optional connected-panel behavior: a bar implementing Shibumi host contract
  v1 or newer

## Install

Install [Herdr Drop v1.6.2](https://github.com/lixenstrand/omarchy-herdr-drop/releases/tag/v1.6.2)
first and select its documented community-plugin installation. The base owns
the command, Hyprland rules, theme hook, and connected-panel visual profile.

That installation applies the same connected-panel look as the bundled
integration: 6 px corners, a matched top gap, 1 px themed border, 94% opacity,
and the top-edge animation. It does not install a second copy of this plugin.

Then add and enable this plugin:

```bash
omarchy plugin add \
  https://github.com/lixenstrand/omarchy-herdr-drop-plugin.git \
  --enable
```

Choose a bar section when Omarchy asks. The default is `center`.

If you previously installed the bundled connector with
`./install.sh --shibumi`, remove that owned plugin directory first:

```bash
omarchy plugin remove io.github.lixenstrand.herdr-drop
omarchy plugin add \
  https://github.com/lixenstrand/omarchy-herdr-drop-plugin.git \
  --enable
```

Removing the shell plugin does not remove the Herdr Drop base integration.

## Settings

Configure the widget entry in `~/.config/omarchy/shell.json`:

```json
{
  "id": "io.github.lixenstrand.herdr-drop",
  "privacyMode": false,
  "animateSheep": true
}
```

- `privacyMode`: hides workspace labels and terminal titles from the tooltip.
- `animateSheep`: disables spatial icon motion while keeping status colors.

## Update

```bash
omarchy plugin update io.github.lixenstrand.herdr-drop
```

## Remove

```bash
omarchy plugin remove io.github.lixenstrand.herdr-drop
```

Remove the base integration separately from its checkout when desired:

```bash
cd ~/.local/share/omarchy-herdr-drop
./uninstall.sh
```

## Validate

```bash
./test/run
```

## Security

Omarchy plugins execute unsandboxed inside the long-running shell process.
Review the repository before enabling it. This plugin reads local Herdr and
Hyprland state and starts no network client; the persistent socket connection
targets Herdr's local Unix socket.

## License

MIT
