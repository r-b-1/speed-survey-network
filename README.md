# Speed Survey Network

A traffic-camera survey system that maps fixed roadway geometry, tracks vehicles
on public DOT feeds, and reports **estimated** speeds. The long-term aim is a
research instrument for how traffic actually moves — not a ticket camera, and
not a certified measuring device.

Minnesota is the first coverage area, using the public MnDOT / 511 camera
network. The same idea can later extend to other states.

**This repository is the public project page.** It has documentation and demos
only. The source, calibration data, and operator tools live in a separate
private repository and are not published here.

## Demo

[![Speed Survey Network Demo](https://img.youtube.com/vi/MlPGWtO9300/maxresdefault.jpg)](https://youtu.be/MlPGWtO9300)

▶️ **[Watch the full demo on YouTube](https://youtu.be/MlPGWtO9300)**

## What it does today

- Statewide Minnesota camera map from the live public catalog (on the order of
  a thousand cameras), with search and roadway filters.
- Live video or stills for cameras that publish a public feed.
- On-demand vehicle detection on any live camera (one active camera at a time).
- Estimated speeds only on cameras that have been surveyed and mapped, and only
  while the camera is verified to still be in its mapped pose.
- Desktop tools for tracing lanes, placing distance gates, and tuning detectors.

The first fully mapped speed site is **MnDOT C535-145** (I-535 at Garfield
Avenue, Duluth). Other cameras can be previewed; they do not report speeds until
an operator maps them.

Speeds are estimates derived from tracked vehicles crossing calibrated gates.
They are **not** legally certified measurements and are **not** intended for
enforcement.

## Why it exists

Public traffic cameras already watch the road. With a surveyed map of the
pavement in the frame, those same cameras can support transportation research:

- typical estimated speed versus the posted limit
- how that mix changes by hour, weekday, or season
- whether vehicles in dense groups tend to run slower or faster than isolated
  ones
- corridor-level studies once many cameras are mapped

The system is built so measurement **fails closed**: if a PTZ camera pans, tilts,
zooms, or its pose cannot be verified, speed timing is suspended until alignment
is restored.

## How it works (high level)

1. **Catalog** — load the public camera list and play the published stream.
2. **Survey** — an operator traces road edges, lane markings, and distance gates
   on a still or live frame. Distances are physical (for example, using standard
   skip-stripe spacing) and stored independently of pixel resolution.
3. **Track** — vehicles are detected and followed across those gates.
4. **Estimate** — elapsed time and known gate separation produce an estimated
   speed, labeled as such on the overlay.

A browser map is the public-facing workspace. A local survey process does the
computer-vision work; live detection and speed overlays are not computed inside
the hosted website itself.

## Current status

| Capability | State |
| --- | --- |
| Minnesota camera catalog and map | Working |
| AI preview on a selected live camera | Working (on-demand, typically one GPU session) |
| Estimated speeds | Working on mapped cameras while aligned |
| Mapped speed sites | One (C535-145); more require operator survey |
| Time-of-day / compliance studies | Planned |
| Multi-state coverage | Planned |
| Open source | No — implementation remains private |

## Research and product direction

Near term stays Minnesota: map more cameras so estimated speeds exist at more
sites, not only at one interchange.

Further out:

- **Statewide speed coverage** — treat every suitable MnDOT camera as a
  potential survey site, not a one-off demo.
- **Other states** — reuse the same survey + track + estimate pattern on other
  public DOT camera networks.
- **Time-of-day studies** — store estimated speeds (not identities) and summarize
  by hour, day of week, and season: share of vehicles below, near, or above the
  posted limit.
- **Platoons and grouping** — measure whether clustered vehicles tend to travel
  slower or faster than vehicles with more space.
- **Research exports** — corridor summaries and time series for analysis, with
  the same estimate / not-certified labeling.
- **Browser mapping** — let operators survey new cameras in the browser so
  coverage can grow without a desktop-only editor.

Operator review remains required. A complete geometry file is not proof that the
physical distances are correct.

## What this is not

- Not a police or red-light system.
- Not a certified speed measurement.
- Not a claim that every camera, in every weather and lighting condition, yields
  a trustworthy number.

If a camera has moved or cannot be aligned to its surveyed home pose, the
speedometer does not run.

## Source

The implementation is private and is not included in this repository.
