# SolarEdge

Home tile for a SolarEdge site. It shows the latest power, today's energy, and the last 12 hours. Open it for the peak, this month, lifetime, and battery or grid when the site has them.

The picture is sample data: 4.2 kW, 18.4 kWh today, a made-up curve. It is not a reading from a real site.

## Sign in

Create a Site Access app at [developer.solaredge.com](https://developer.solaredge.com/) with `SITE_DATA` and `DEVICE_DATA`. The portal rejects `localhost`. Register `https://example.com/` exactly, including the trailing slash. After you approve, the browser opens the Example Domain page. Tap the address bar and copy the full address: it is that URI plus `?code=...`. Paste the whole address or just the code. Setup offers the same URI as the default, so press enter unless the app was registered with a different one. The two have to match character for character. The site id is the number in the monitoring URL.

The token never goes in this file. It stays in `~/.config/omarchy-solaredge/auth.json` (mode 600). SolarEdge replaces the refresh token on every use, and the reader writes the new one back before it asks for readings.

## Side note for building

Store path: `widgets/jenskock/solaredge/widget.owl`. The folder name is the GitHub login, lowercase, then a name of lowercase letters, digits and dashes. The folder holds only `widget.owl`, `preview.png` and this README.

The reader is inlined. On first run it installs `~/.local/bin/solaredge-sync`, so that name is not an Arch package. `curl` and `jq` are. Readings are `~/.config/omarchy-solaredge/data.json`, which the tile reads directly. A `details` or `force` file in that directory asks for the extra figures; the half-hour poll is an ordinary sync.

Two review notes are expected:

- `base64` builds the HTTP Basic header from the client id and secret. It does not decode a download.
- `chmod 700` is the config directory, `chmod 600` the token file, and `chmod 755` the installed reader.

Cloud samples are 15 minutes apart. Quarter-hour power covers at most 12 hours, so today's energy is a second call. Between 21:00 and 05:00 a day already fetched is kept and the live watts are shown as 0, which stays inside the free tier.

## License

MIT
