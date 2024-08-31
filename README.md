## Source SDK 2013 VS2022 Deferred

### What is this?

This is a fork of the [source-sdk-vs2022](https://github.com/Source-SDK-Resources/source-sdk-vs2022) repository merged with [SCell555's port](https://github.com/SCell555/sdk-2013-deferred) of [Biohazard90's deferred lighting implementation](https://github.com/jonathonracz/swarm-deferred-src) based on [Alien Swarm's](https://github.com/NicolasDe/AlienSwarm) deferred shading, via [Lambda Wars](https://github.com/Sandern/lambdawars). I tried to minimize the amount of changes made to the original repository to make it as painless as possible to implement, with some of my own minor tweaks/fixes/workarounds. Still very much a proof of concept rather than a full implementation.

![dm_lockdown0000](https://github.com/user-attachments/assets/cbec4453-7350-465e-8f53-1a5f806a1a72)

### How do I compile this?

It should work out of the box with VS2022. I would recommend migrating the shader pipeline to [SCell555's Shader Compile](https://github.com/SCell555/ShaderCompile) tool, but that's up to you.

### Notes

- Most things don't work right. Water, alpha masking/transparency, specular, etc. are not particularly functional.
- The server converts existing static lights into light_deferred_global and light_deferred entities on map load, but this is quite rudimentary. The intended use is to build maps based on deferred lighting (see deferred.fgd) from the ground up.
- Lights and shadows flicker often. Disabling visleaf culling (r_deferred_light_visleaf_cull) helps with the lights, but decreases performance.
- This implementation also supports basic, unstable radiosity (r_deferred_radiosity) as well as volumetrics (per-light flag) which actually look alright and don't bug out too much.
- Use the `-nodeferred` command line argument to disable deferred lighting. This causes some decals to flicker, although they also flicker with deferred lighting on, but in a different way.
- Console commands related to deferred lighting start with r_deferred. I added notes to some of the commands to better explain what they do (as far as I know).
- The repo includes diff patches (in unified format) to possibly help implement the changes to the files from the original repository.
- See the LICENSE file for more information regarding Valve Software's original Source SDK.
