# Herdr Drop plugin for Omarchy

An Omarchy Shell bar widget for
[Herdr Drop](https://github.com/lixenstrand/omarchy-herdr-drop). It shows live
Herdr agent status, toggles the persistent drop-down, and draws a connector
that follows the active Omarchy popup theme.

## Requirements

- Omarchy Quattro with third-party shell plugin support
- [Herdr](https://herdr.dev/)
- [Herdr Drop v1.5.0 or newer](https://github.com/lixenstrand/omarchy-herdr-drop/releases)
- `jq`, `hyprctl`, and `socat`
- Optional connected-panel behavior: a bar implementing Shibumi host contract
  v1 or newer

## Install

Install the Herdr Drop base integration first. The base owns the command,
Hyprland rules, and theme hook:

```bash
git clone https://github.com/lixenstrand/omarchy-herdr-drop.git \
  ~/.local/share/omarchy-herdr-drop
cd ~/.local/share/omarchy-herdr-drop
./install.sh
```

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
