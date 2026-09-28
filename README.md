# Frustum Visualizer

Visualise what a fixed camera can see of a sports field. Position and aim a camera, set its field of view, and see its viewing frustum and ground coverage in 3D, with the covered area and nearest/farthest distances.

## Run it

It's a static site with no build step, but it must be served over HTTP because it loads `sports.json`:

    npx serve .

Then open the printed URL (e.g. http://localhost:3000).

## Features

- 20 sports with accurate field markings: football, cricket, tennis, basketball, ice hockey, baseball, table tennis and more
- Resize any field; markings rescale sensibly
- Camera position, pitch/yaw/roll and horizontal/vertical FOV
- 3D orbit view with Top/Side/Iso/From-camera presets
- Settings are saved automatically, and the address bar is always a shareable link ("Share visualisation")

## Adding a sport

Sports are defined in [`sports.json`](sports.json): standard size, surface shape and markings in metres. See [REQ-004](requirements/2026-09-28-sport-markings-sports-json.md) for the format.

## Contributing

PR's welcome! Work follows a requirements-first process. See [AGENTS.md](AGENTS.md) and [requirements/](requirements/_index.md).

Found a problem or have an idea? [Raise a bug / Request a feature](https://github.com/nickgrealy/frustrum-visualiser/issues/new/choose).
