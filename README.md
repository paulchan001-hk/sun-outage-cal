# AsiaSat Sun Outage Calculator

Static page for GitHub Pages. No build step and no server.

The timing logic follows the AsiaSat website script `sun-outage-cal.min.js`. Frequency and orbital slot are free inputs, so the page also covers Ka-band and any GEO longitude.

## What it does

Estimate the dates and GMT times when the Sun passes through a receive antenna beam pointed at a geostationary satellite.

- Fleet presets: AsiaSat 5 (100.5° E), AsiaSat 6 (120° E), AsiaSat 7 (105.5° E), AsiaSat 8 (105.3° E), AsiaSat 9 (122° E).
- Any other GEO slot can be typed in. East is positive, West is negative.
- C, Ku and Ka, or any downlink frequency from 1 to 50 GHz.
- Single station and batch CSV.
- Local time and GMT. The AsiaSat website prints GMT.

## Match the AsiaSat website

Use an AsiaSat fleet slot and the website frequencies:

- C-band: 3.62 GHz
- Ku-band: 11 GHz

Compare the GMT column, not the local-time column. Hong Kong local time is GMT+8.

A custom frequency or a non-fleet slot will not match the website. The website script has no Ka-band and no time base for other longitudes.

## Method

From `sun-outage-cal.min.js`:

- Outage angle: `AOA = 11 / (D × f) + 0.25` degrees. `D` is antenna diameter in metres, `f` is downlink frequency in GHz, and 0.25° is the solar radius.
- Number of days from `AOA` and their declination step of 0.257534°.
- Station and satellite geometry with Earth radius 6,378.1599 km and GEO radius 42,164.196 km.
- Equinox day placement, equation of time, and a GMT solar-noon base.
- Fleet slots use the script’s exact GMT constants. Any other slot uses 12:00 GMT minus longitude/15.

Not modelled: inclination, station-keeping, link margin, or the difference between a 3 dB crossing and carrier failure. Treat the result as a planning estimate, about 5 to 10 minutes, as on the AsiaSat page.

## Publish

1. Put `index.html` at the repository root.
2. GitHub → Settings → Pages → Deploy from a branch → `main` → `/ (root)`.
3. The page is `https://<user>.github.io/<repo>/`.

## Batch CSV

Columns:

`id, site, lat, lat_hemisphere, lon, lon_hemisphere, orbital_slot_east, year, band, frequency_ghz, antenna_m, timezone`

- Hemisphere values are whole words: `North`, `South`, `East`, `West`.
- Band is `C`, `Ku`, `Ka` or `Custom`. Frequency is still required.
- Time zone is the UTC offset used for local time. GMT is always calculated.

A sample is in `sun-outage-template.csv`.

## Notes

- Season text is `Around Mar-Apr` and `Around Sep-Oct`, with a plain hyphen. The CSV download includes a UTF-8 mark so Excel does not misread it.
- AsiaSat 8 is preset at 105.3° E, matching the website calculator rather than the 105.5° E fleet-page figure. Confirm the live slot before an operational notice.
