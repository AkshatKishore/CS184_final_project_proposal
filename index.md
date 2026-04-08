# Campanile

**Group Members:**  
Shivani Wadhwa, Roopa Srinivas, Akshat Kishore Shrivastava, Kushagra Srivastava  

---

## Summary

We are building a real-time, interactive renderer of UC Berkeley’s Campanile—reconstructed from photographs using photogrammetry and rendered under physically accurate lighting driven by real solar geometry, atmospheric scattering models, and dynamic weather simulation.

There will be a time-of-day slider that can change the scene from sunrise to sunset, change the sky color, the shadow direction, and the surface appearance in real time. At the top of every hour, the bells ring. The demo runs entirely in the browser with no installation required.

---

## Problem Description

Rendering a real-world landmark is much harder than it looks. Completing the geometry is the easy part. What makes a scene feel real is the lighting: the precise color of the sky at a given time of day, the direction and softness of shadows, and how materials respond to environmental changes (e.g., dry vs. rain-soaked surfaces).

Reproducing this requires implementing real atmospheric and material physics on the GPU.

The core technical challenge is to develop a physically based rendering system in which every visual parameter is derived from accurate physical models rather than manually authored values.

- Sun position will be computed using solar declination equations tied to Berkeley’s GPS coordinates (37.87°N, 122.26°W) and the user-selected date and time  
- Sky color will be generated through the Preetham atmospheric scattering model  
- Surface materials dynamically switch between dry and wet BRDFs based on weather  
- Volumetric fog and rain particles attenuate light through the scene  

Each weather state has its own physically grounded configuration:

- **Clear:** directional sun + skylight dome  
- **Rain:** participating medium, exponential visibility falloff, wet BRDFs, rain particles  

All visual states emerge from physical inputs, not hand-tuned presets.

The main engineering challenge is integrating these systems into a real-time browser renderer that supports smooth interaction at high frame rates on consumer hardware.

---

## Goals and Deliverables

The demo will run live at the poster session. A visitor can interact with time and weather and observe real-time changes.

### Plan to Deliver

- A photogrammetry-reconstructed or hand-modeled 3D mesh of the Campanile, optimized for WebGL  
- Physically-based sky rendering using the Preetham model  
- Real solar positioning (date, time, latitude/longitude)  
- **Time-of-day slider:** continuous 24-hour cycle with correct lighting and shadows  
- **Date slider:** seasonal sun variation via solar declination equations  
- Dry and wet BRDFs for stone materials (rain darkening + specular highlights)  
- Weather system with at least:
  - Clear
  - Rain (particles, reflections, volumetric mist)  
- Bell chime system:
  - Westminster quarter-hour chimes  
  - Full carillon at noon and 6pm  
  - Time-triggered + visible bell animation  
- Interactive camera (orbit, zoom, pan)  
- Stable performance on a mid-range MacBook Pro  
- Side-by-side comparisons with real photos for validation  

---

### Hope to Deliver

- Full 24-hour time-lapse video including stars and moon  
- Additional weather:
  - Overcast
  - Snow
  - Dense fog  
- Surrounding scene:
  - Esplanade
  - Trees
  - Sather Gate  
- Night sky with procedural stars + moonlight shadows  
- Path-traced offline reference images for validation  
- Post-processing:
  - Bloom
  - Atmospheric haze  

---

## Schedule

### Week 1 (Apr 7–14) — Foundation
- Set up Three.js + WebGL project
- Acquire Campanile geometry (photogrammetry via Meshroom or manual fallback)
- Render textured mesh with orbit camera
- Implement HTML sliders (time/date)
- Read Preetham et al.
- Assign subsystem ownership

---

### Week 2 (Apr 14–20) — Milestone
- Implement solar position equations (declination, hour angle, azimuth, altitude)
- Anchor to Berkeley GPS (37.87°N, 122.26°W)
- Implement Preetham sky shader
- Connect UI to lighting system
- Add shadow mapping

**Milestone Deliverable:**  
A full day cycle with correct sun movement, shadows, and sky color.

---

### Week 3 (Apr 21–28)
- Implement dry/wet BRDF materials
- Build rain particle system
- Add volumetric mist
- Implement overcast sky model
- Add bell audio + timing logic
- Connect all controls to UI
- Identify performance bottlenecks

---

### Week 4 (Apr 28–May 4) — Final
- Optimize performance
- Fix rendering artifacts
- Record demo video
- Write final report webpage
- Prepare presentation
- Submit by May 4, 11:59 PM
- Work on stretch goals if possible

---

## Resources

### References

- Preetham, Shirley, Smits (1999) — *A Practical Analytic Model for Daylight*  
- Hosek & Wilkie (2012) — *Full Spectral Sky-Dome Radiance*  
- Nishita et al. (1993) — Atmospheric scattering  
- Oren & Nayar (1994) — Reflectance model for rough surfaces  
- NVIDIA GPU Gems 2, Ch. 16 — Atmospheric scattering  
- PBRT (Pharr, Jakob, Humphreys), Ch. 11 — Volume scattering  
- Meshroom / AliceVision — photogrammetry pipeline  
- UC Berkeley Carillon schedule — bell timing  
- Inigo Quilez — procedural rendering techniques  

---

### Computing Platform

- **Language:** JavaScript (ES2020), GLSL  
- **Framework:** Three.js (WebGL 2.0)  
- **Audio:** Tone.js  
- **UI:** dat.GUI or Tweakpane  
- **Hosting:** GitHub Pages  
- **Hardware:** MacBook Pro (Apple Silicon M1/M2/M3)  

---

### Links

- http://music.berkeley.edu  
- http://iquilezles.org  

---

### Notes

- All physically-based shading implemented from scratch in GLSL  
- No reliance on prebuilt rendering frameworks for lighting  
- Campanile mesh created via photogrammetry or manual modeling (not asset stores)
