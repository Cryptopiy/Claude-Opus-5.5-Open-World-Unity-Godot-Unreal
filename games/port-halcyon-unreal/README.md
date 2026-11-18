# Port Halcyon

> **Как запустить готовую сборку / How to run the ready-made build:** см. / see [HOW_TO_PLAY.md](../../HOW_TO_PLAY.md) в корне репозитория / in the repository root. Если ниже упоминаются другие файлы запуска — их в этом репозитории нет / if other launch files are mentioned below, they are not part of this repository.

Original single-player free-roam sandbox built in the existing Unreal Engine 5.8.2 project. No missions or campaign. The overall specification remains partially fulfilled; see FEATURE_MATRIX.md for the exact status.

## Run

Open **Packaged/Windows/Unreal_Opus5_5_GTA.exe**. Keep the entire Windows folder together; the small root EXE launches the game binary and requires its packaged content. Unreal Editor is not needed to play.

The game opens directly on Port Halcyon. Press **F1** for teleport, vehicle/weapon access, weather, time, wanted level and testing controls. Press **Esc** for pause, save/load and controls. First launch can have pipeline-cache hitches.

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


## World and roster

Approximately 600 x 600 m: Lumen Heights, Neon Row, Coral Strip, Saltworks Docks, Rustline, Palmetto Hills, Tidewater Park and Gullwing Field, with Halcyon Bay for boating/diving.

Cars: Pico Hatch, Meridian Sedan, Vortex GT, Brute 69, Ridgeback SUV, Haul 1500 Pickup, Courier Van, Halcyon PD Cruiser, Halcyon Cab, Rescue Ambulance, Engine 7 Fire Truck, Lugger Box Truck, Bastion Tactical. Two-wheel: Razor 600, Pedal BMX. Water: Wavecutter Speedboat. Air: Kestrel Helicopter, Kestrel PD Air, Gull Prop Plane, Swift Jet.

Weapons: fists, Tide Knife, Slugger Bat, Vex P9 Pistol, Hammer .44, Kite SMG, Breaker 12 Pump, Thunder Auto-12, Tern AR, Skiff Carbine, Heron DMR, Albatross Sniper, Frag Grenade, Gale Rocket Launcher, Mortar GL.

## Build and verification

`powershell -ExecutionPolicy Bypass -File Tools/package_windows.ps1`

Packaged runtime checks: 26 passed, 0 failed. Detailed evidence is in Docs/QA and Saved/GTALogs. Editor target and packaged Game target are built with the actual UE 5.8.2 installation, not a changed EngineAssociation.

Known limits: simple stylized art/animation, traffic congestion, occasional camera obstruction, incomplete taxi/cover/stealth/customization validation, no train system or autonomous emergency dispatch. See OPUS_5.5_FINAL_REPORT.md and FEATURE_MATRIX.md.
