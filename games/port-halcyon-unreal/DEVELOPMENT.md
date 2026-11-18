# Development — Port Halcyon

Current state: playable packaged build with an implemented sandbox and remaining limitations listed in FEATURE_MATRIX.md. Historical blocked-state documents are preserved in Docs/Archive; their old completion/absence statements do not describe the current build.

## Engine and project

Project: `<local-path> Opus 5.5 GTA\Unreal Engine 5\Unreal_Opus5_5_GTA`. Engine: `W:/Unreal Engine 5/UE_5.8`, Build.version 5.8.2, CL 56702186. Existing `.uproject` retained with EngineAssociation 5.8. One runtime C++ module, Unreal_Opus5_5_GTA. PythonScriptPlugin, EditorScriptingUtilities and ModelingToolsEditorMode are enabled; Enhanced Input, Navigation, AI, UMG/Slate, PhysicsCore and AudioMixer are module dependencies. Editor-only automation also uses PhysicsUtilities and AssetRegistry.

DX12 SM6, Lumen, VSM, Substrate; hardware ray tracing is disabled. Current atlas/VSM budgets inherited from diagnostics are conservative. Instanced city geometry and distance-based population updates suit this compact map. Vehicles use project-owned raycast wheels and Chaos rigid bodies; they are not a ChaosVehicles plugin implementation.

## Runtime architecture

GTAGameMode owns city/environment/population/wanted services. GTACharacter/GTAPlayerCharacter provide movement, vitals, weapons and interaction. GTAAnimInstance samples authored clips in a native animation proxy. GTAVehicle implements seats, physics, damage and customization; NPC controllers follow a lane graph and navigation. Slate drawing inside UMG presents HUD and menus. GameInstance/SaveGame persist profile, transform and settings. GTAWildlife uses bounded instanced fauna. Core logic is C++, with editor asset automation in Tools/Unreal.

## Verified Blender route

Only `mcp__custom_blender_unreal_gta_opus55__*` was used. Host endpoint: **localhost:9882**, BLENDER_MCP_SAFE_MODE=1. Actual MCP get_addon_status/get_scene_info and read-only bpy.data.filepath returned `<local-path> Opus 5.5 GTA\Unreal Engine 5\Unreal_Opus5_5_GTA\UnrealOpus5.5GTA.blend`. Blender 5.2.2 LTS, addon protocol 7 with compatibility fallback. No connector reconfiguration or other project scenes were used. The initial Codex backup SHA256 matched: `38F2A9B3C911F0A210D66BC8133A6EB85EA42A079112EA1E63CBF33020578DCB`.

Canonical source: UnrealOpus5.5GTA.blend (192 objects, 186 named mesh assets and 41 retained authored actions at the final MCP check). Backups: SourceAssets/BlenderBackups. Metre-based static models export at global_scale=1 with scene units=1; do not multiply by 100 again. Corrected individual exports and exact-name import live in Tools/Blender/export_gameplay_corrected.py and Tools/Unreal/import_corrected.py. Collision is regenerated from current bounds after scale changes.

Characters use temporary centimetre copies for consistent bone/mesh/animation units (export_characters_cm.py); original metre source remains editable. import_characters_cm.py binds an explicitly saved common Skeleton and PhysicsAsset. Source actions use fake users, avoiding loss of the 37 previously unsaved clips. Recovered actions and exports are project-owned, not downloaded assets.

Only one Unreal writer runs at a time. Use Tools/ue_python.ps1 for commandlets, Tools/package_windows.ps1 for packaging and Tools/Unreal/launch_test.ps1 for runtime checks. Tools/finalize_windows.ps1 sequences asset import, package and test. Older diagnostic scripts are not the release path.

## Controls

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


## Changes in the Codex continuation

Fixed the missing OverlapResult include; rebuilt Editor; corrected 100x static mesh units; rebuilt stale collisions; restored 41 source animation actions; rebuilt the character pipeline with consistent units, shared skeleton, materials and physics; improved 13 car bodies and two convertible versions; added missing bicycle/motorcycle rims; synthesized/imported 51 sounds; stabilized suspension damping; fixed pause-menu input; added position/settings persistence and fauna; added packaged-build automation and assertions. Corrected both pier origins to the shoreline/deck surface, aligned seated pelvis height with the authored Drive clip, and reset ragdoll physics on vehicle entry. Knockdown recovery rejects implausible remote positions. Parachute QA validates the actual local trajectory, not only deployment/vertical speed.

Packaged runtime checks: 26 passed, 0 failed.
