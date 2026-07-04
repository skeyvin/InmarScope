# InmarScope

Multi-protocol L-band satellite communications decoder for Windows.

Decodes Inmarsat Aero (Classic Aero, Aero-H/H+) and Inmarsat-C/EGC signals in real time using RTL-SDR, HackRF, or SDR++ server sources. Voice call recording, aircraft tracking, and message output in one application.

![screenshot.gif](screenshot.gif)

Windows Download: https://sarahsforge.dev/products/inmarscope

## Features

- **Inmarsat Aero** — 600/1200/8400 bps OQPSK signal decoding, voice AMBE decoding, ACARS/ADS-C/CPDLC message parsing
- **Inmarsat-C / EGC** — 1200 bps BPSK decoding with EGC SafetyNet/FleetNet message output
- **Dual-SDR voice follow** — dedicate a second RTL-SDR to automatically follow and record voice calls
- **Voice call recording** — WAV and OGG Vorbis output, tagged with aircraft ICAO
- **Live spectrum & waterfall** — real-time FFT with drag-to-place decoder placement
- **Embedded flight map** — tracks aircraft positions on globe.airplanes.live via Microsoft Edge WebView2
- **SBS/BaseStation output** — TCP server on port 30003 for virtual radar clients
- **JAERO-compatible output** — JSON dump, text log, and UDP forwarding
- **Country blacklist** — mute and skip recording for selected countries using ICAO address lookup

## Building

get libacars from ```github.com/szpajder/libacars/```
in ```libacars/libacars/CMakeLists.txt``` add the following after line 190
```target_link_libraries (acars ${acars_extra_libs})``` so it looks like 
```
add_library(acars SHARED ${acars_obj_files})
target_link_libraries (acars ${acars_extra_libs})
set_property (TARGET acars PROPERTY SOVERSION ${LA_VERSION_MAJOR})
set_target_properties(acars PROPERTIES OUTPUT_NAME "acars-${LA_VERSION_MAJOR}")
```
add imgui docking branch from ```https://github.com/ocornut/imgui```
and implot from ```https://github.com/epezent/implot```



Requires MSYS2/MinGW-w64 with the following:

```
pacman -S mingw-w64-x86_64-{cmake,ninja,gcc,glfw,rtl-sdr,hackrf,zstd,libogg,libvorbis}
```

Additional dependencies vendored in `third_party/`:
- Dear ImGui (docking branch)
- ImPlot
- jaero_dsp, mbelib, libacars, WebView2 SDK

Build:

```bash
cmake -S . -B build -G Ninja
ninja -C build
```

## License

See [LICENSE](LICENSE).
