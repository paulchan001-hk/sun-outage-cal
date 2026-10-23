# AsiaSat Sun Outage Calculator



The is AsiaSat tool for user to estimate sun-outage period according to different frequency and orbital slot.

## What it does

Estimate the dates and GMT times when the Sun passes through a receive antenna beam pointed at a geostationary satellite.

- Fleet presets: AsiaSat 5 (100.5° E), AsiaSat 6 (120° E), AsiaSat 7 (105.5° E), AsiaSat 8 (105.5° E), AsiaSat 9 (122° E).
- Any other GEO slot can be typed in. East is positive, West is negative.
- C, Ku and Ka, or any downlink frequency
- Single station and batch CSV.
- Local time and GMT

## Method

- Outage angle: `AOA = 11 / (D × f) + 0.25` degrees. `D` is antenna diameter in metres, `f` is downlink frequency in GHz, and 0.25° is the solar radius.
- Number of days from `AOA` and their declination step of 0.257534°.
- Station and satellite geometry with Earth radius 6,378.1599 km and GEO radius 42,164.196 km.
- Equinox day placement, equation of time, and a GMT solar-noon base.
- Fleet slots use the script’s exact GMT constants. Any other slot uses 12:00 GMT minus longitude/15.

Not modelled: inclination, station-keeping, link margin, etc.

## Batch CSV

Columns:

`id, site, lat, lat_hemisphere, lon, lon_hemisphere, orbital_slot_east, year, band, frequency_ghz, antenna_m, timezone`

- Hemisphere values are whole words: `North`, `South`, `East`, `West`.
- Band is `C`, `Ku`, `Ka` or `Custom`. Frequency is still required.
- Time zone is the UTC offset used for local time. GMT is always calculated.

A sample is in `sun-outage-template.csv`.
