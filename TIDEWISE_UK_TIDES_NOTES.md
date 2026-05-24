# TideWise UK Tide Support Notes

These notes are for a future TideWise discussion about adding UK tide support. They come from the RiverWise UK Environment Agency work, but UK tide support should be researched as its own provider problem.

## Short Version

RiverWise proved that TideWise should add international data through explicit provider adapters, not by stretching NOAA-specific code paths.

For UK tides, do not assume the Environment Agency flood-monitoring API is the right source. It is useful for rivers, flood gauges, and level stations, but it is not a proper tide prediction provider.

## What RiverWise Taught Us

- Provider logic should be isolated behind small adapter functions/classes.
- The visual editor should change by provider instead of showing every possible field.
- Station discovery needs guided dropdowns, not a raw search box.
- Bulk station-list endpoints may not include the same fields as station detail endpoints.
- Some APIs return a single object where other responses return an array.
- Picker lists should filter for likely usable stations, but selected stations still need deeper validation.
- Unit labels from provider APIs should be preserved, but explained when they are technical.
- Debug data should stay hidden from normal users and be YAML/console-only.
- Do not expose provider-specific rough edges as normal user choices.

## UK Tide Provider Research Needed

Potential directions to investigate:

- UKHO Admiralty EasyTide or other UK Hydrographic Office tide products.
- Official public APIs, if available, for tide predictions and tidal stations.
- Data licensing and redistribution limits for UK tide predictions.
- Whether client-side fetching is allowed from Home Assistant Lovelace without CORS issues.
- Whether any provider offers current observed tide height, not only predictions.
- Whether station metadata includes latitude/longitude, time zone, units, datum, and prediction intervals.

## Why Environment Agency Is Not Enough For TideWise

The Environment Agency flood-monitoring API can expose water-level readings at river, flood, and some tidal/estuarine stations, but it does not appear to provide the same product TideWise needs:

- Tide predictions.
- Next high/low tide times.
- A tide curve suitable for a 24-hour tide chart.
- NOAA CO-OPS-style prediction intervals.
- Tide-current predictions.

It may be useful as an optional observed-water-level source in some areas, but it should not be treated as the main UK TideWise tide provider.

## Suggested TideWise Architecture

Add a provider layer such as:

```js
const TIDEWISE_PROVIDERS = {
  noaa_coops: {
    label: "US NOAA CO-OPS",
    loadStations,
    loadPredictions,
    loadObservations,
    normalizeStation,
    normalizePrediction,
  },
  uk_tides: {
    label: "UK tides",
    loadStations,
    loadPredictions,
    loadObservations,
    normalizeStation,
    normalizePrediction,
  },
};
```

Keep NOAA station fields and UK station fields separate where needed:

```yaml
provider: noaa_coops
station: "8661070"
```

Possible UK shape:

```yaml
provider: uk_tides
uk_station: "..."
```

## Visual Editor Lessons

For UK support, the TideWise editor should:

- Let the user choose a provider first.
- Show a UK-specific station picker after provider selection.
- Load station options from an official station list if available.
- Filter by station name, water body, town/area, and station code.
- Keep manual station entry as an escape hatch.
- Use a real dropdown with disabled placeholders.
- Avoid requiring users to know codes before setup.
- Update the title from station metadata after selection.

## Validation Rules

For any UK station candidate, validate:

- Station has an ID/reference.
- Station has a display name.
- Station has tide prediction data, not only observed level data.
- Prediction times parse correctly.
- Units/datum are present or safely described.
- Time zone handling is correct for UK daylight saving time.
- CORS works from a Lovelace card.

If direct browser fetch is blocked, TideWise may need one of:

- Home Assistant REST sensors.
- A lightweight custom integration backend.
- A proxy/helper endpoint.

## User-Facing Copy

Use clear wording:

```text
UK tide support is provider-dependent. TideWise needs an official source that allows browser/API access to tide predictions.
```

Avoid implying Environment Agency river-level readings are tide predictions.

## First Implementation Goal

A realistic first UK TideWise milestone:

- Pick one official UK tide prediction source.
- Load a station list.
- Render next high/low tides.
- Render a 24-hour prediction curve.
- Keep fishing score optional/disabled until weather and marine context sources are understood.

## Open Questions

- What official UK tide prediction API is available and legally usable?
- Does it support browser-side CORS?
- Does it provide enough interval data for TideWise charts?
- Does it include current observed tide height?
- Are predictions free for public dashboard use?
- Can HACS users outside the UK access it reliably?

## Bottom Line

RiverWise gives TideWise the adapter pattern and editor lessons. It does not provide the UK tide data source. TideWise UK support should start with data-provider research, licensing, and CORS testing before UI work.
