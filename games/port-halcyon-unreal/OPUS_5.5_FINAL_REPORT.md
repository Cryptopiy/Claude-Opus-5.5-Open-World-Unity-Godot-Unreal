# Port Halcyon — implementation and verification report

This is a playable Windows sandbox, not a claim that every requested extension is complete. FEATURE_MATRIX.md distinguishes WORKING, PARTIAL and NOT IMPLEMENTED. No campaign, missions or quests were added.

## Launch

**Packaged/Windows/Unreal_Opus5_5_GTA.exe**. Keep the whole Windows directory. Editor alternative: open Unreal_Opus5_5_GTA.uproject in the verified UE 5.8.2 installation and play PortHalcyon. F1 gives rapid access to vehicles, weapons and test settings.

| Control | Action |
|---|---|
| WASD / mouse | Move / camera; steer vehicle |
| Shift / Space / Ctrl or C | Sprint / jump, vault or handbrake / crouch, stealth |
| F / E | Enter, exit, carjack / interact, siren |
| LMB / RMB / R | Fire or melee / aim / reload (radio in vehicle) |
| Tab / wheel / 1–9 | Weapon wheel / select weapon |
| Q / X / B | Cover / dodge / block |
| V / middle mouse | First-person toggle / shoulder |
| H / L / T | Horn / lights / convertible roof |
| M / Up arrow | Map and waypoint / phone |
| Esc / F1 | Pause / benchmark menu |
| Arrows / Enter / Backspace | Navigate menus / select / back |
| Aircraft: Shift/Ctrl, WASD, Q/E | Throttle or helicopter lift, pitch/roll, yaw |
| Falling: F or Space | Deploy/cut parachute when equipped |


## Delivered systems and assets

- Original compact city: 3938 authored-mesh instances; zero missing city meshes reported at runtime. Districts: Lumen Heights, Neon Row, Coral Strip, Saltworks Docks, Rustline, Palmetto Hills, Tidewater Park, Gullwing Field and surrounding bay.
- On-foot control, camera, weapons/inventory, NPCs/traffic, police/witness/wanted/search logic, water/air/land vehicles, shops/garage menus, day/night/weather, HUD/map/phone, save/load and benchmark menu.
- Four character body variants, common centimetre rig, PhysicsAsset with 20 bodies and 19 constraints, 41 animation clips. Source Blender file and FBX exports retained.
- Twenty vehicle definitions, 14 weapon models plus fists, modular environment, weapon/accessory parts, rims and two open-top variants. Car body shapes now include sloping glass, wheel arches, trim and lamps.
- Original Blender gull/fish/deer assets and procedural local wildlife behavior; 51 synthesized sounds, including three simple radio loops.

Cars: Pico Hatch, Meridian Sedan, Vortex GT, Brute 69, Ridgeback SUV, Haul 1500 Pickup, Courier Van, Halcyon PD Cruiser, Halcyon Cab, Rescue Ambulance, Engine 7 Fire Truck, Lugger Box Truck, Bastion Tactical. Two-wheel: Razor 600, Pedal BMX. Water: Wavecutter Speedboat. Air: Kestrel Helicopter, Kestrel PD Air, Gull Prop Plane, Swift Jet.

Weapons: fists, Tide Knife, Slugger Bat, Vex P9 Pistol, Hammer .44, Kite SMG, Breaker 12 Pump, Thunder Auto-12, Tern AR, Skiff Carbine, Heron DMR, Albatross Sniper, Frag Grenade, Gale Rocket Launcher, Mortar GL.

## Verification

Editor compilation and BuildCookRun for Win64 Development succeeded. The root executable was launched with cooked content. Packaged runtime checks: 26 passed, 0 failed.

Measured packaged QA: mean 136.4 FPS, 95th-percentile frame 9.91 ms, 13518 sampled frames at 1280x720 on NVIDIA GeForce RTX 5070. Includes scripted test activity; not a minimum FPS guarantee.

Evidence: Saved/GTALogs/package_windows.log, codex_packaged_final.stdout.log, packaged Saved/GTATest/checks.txt and screenshots. Release copies are placed in Docs/QA. The initial packaged run also passed 14 checks. One earlier run recorded an audio-device swap error and then recovered; no project-wide hardware diagnosis is inferred from it.

## Limitations

The visual style is intentionally simple, but traffic avoidance, camera behavior near walls/exits and animation transitions still need polish. Cover/stealth/carjacking/drive-by/customization/taxi implementations have not all received complete scenario testing and are marked PARTIAL. Wildlife uses simple instanced motion and has no hunting/ecosystem simulation. There are no moving trains, autonomous ambulance/fire dispatch, fully interactive building interiors, full-body vehicle deformation or complete hobby/race suite. Synthesized audio is basic. These missing/partial items must not be presented as finished.

## Blender verification and recovery

Verified MCP namespace: `mcp__custom_blender_unreal_gta_opus55__*`; endpoint localhost:9882; Safe Mode preserved. Exact master file: `<local-path> Opus 5.5 GTA\Unreal Engine 5\Unreal_Opus5_5_GTA\UnrealOpus5.5GTA.blend`. Backups precede modifications; source saved after modeling/action/material changes. Important imported models were checked by bounds and game screenshots. No downloaded asset packs or alternative Blender instance were used.

## Project metrics (observation cutoff, not subscription billing)

- Original run: `opus55-ue5-gta-20261003T121438p0200`; initial OS timestamp **2026-10-03T12:14:38.938000+02:00**.
- Codex continuation: **2026-10-05T17:29:09.914160+02:00 → 2026-10-05T19:12:18.644145+02:00**, **01:43:08** (103.13 minutes).
- Calendar span from original start: **54:57:39** (54.961 hours), including pauses. Total active development time was not tracked and is unavailable.
- Recorded early pause: 2026-10-03 12:27:10.952 → 12:57:17.280 +02:00. Earlier Claude responses end at 2026-10-04T17:21:45.329Z; Codex resumed on October 5. Other pauses/interruption intervals are not fully measured.
- Requested model: Claude Opus 5.5. Actual recorded models: **claude-opus-5-5** and **gpt-6-astra**. This is a mixed-model project after the user switched agents.
- Exposed Codex reasoning setting(s): ['ultra']; Claude thinking budget not verified from accessible metadata.
- Claude: 720 deduplicated responses; uncached input **6,660,238**, cache read **241,338,840**, cache write **13,208,887** (all exposed as 5-minute), output including thinking **976,250**; total **262,184,215** tokens. Standard API equivalent **$160.4782**.
- Codex at 2026-10-05T17:11:27.384Z: inclusive input **33,164,053**, cached subset **32,510,208**, exposed cache write **0**, output **122,092**, reasoning subset **58,511**; total **33,286,145**. Standard API equivalent **$74.3301**.
- Combined observed total: **295,470,360 tokens**; token-only Standard API equivalent **$234.8083**. Counters measured from local task metadata; USD calculated from official rates. Work after the observation cutoff, including the final response, is excluded.
- Anthropic rates per million: uncached $4, 5-minute cache write $5, 1-hour $8, cache read $0.20, output $20. Verified 2026-10-05: [official Anthropic pricing](https://platform.claude.com/docs/en/about-claude/pricing). Exclusive token categories follow [Anthropic caching documentation](https://platform.claude.com/docs/en/build-with-claude/prompt-caching).
- GPT-6 Astra Standard rates per million: uncached $10, cached $1, cache write $12.50, output $50; above 272K input, input/cache rates double and output is multiplied by 1.5 for that request. Applied per recorded request length, not to the entire aggregate. Verified 2026-10-05: [official model pricing](https://developers.openai.com/api/docs/models/gpt-6-astra).
- Formula: sum exclusive category tokens × applicable per-million rate / 1,000,000. Streaming/cumulative events are deduplicated; reasoning and cache duration subtotals are not added twice. Zero-token synthetic Claude records are excluded from priced consumption. External tool fees unknown and excluded; no invented Blender/Unreal fee.
- Metadata-only sources: `Tools/Metrics/claude_project_usage.py`, `Tools/Metrics/codex_usage.py`, and the JSON snapshots in the Codex run directory. No conversation text or credentials are included.
