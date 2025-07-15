# XodDopplerFX
Chrome Sphynx Audio Doppler EFX 
////////////////////////////////////////////////////////////////////////////
// __Project ::(Z445-1):: DopplerEFX                                    
////////////////////////////////////////////////////////////////////////////

Title:  
DopplerEFX – Real-Time Spatial Doppler Audio Plugin

Definition:  
A stereo VST3 plugin for simulating Doppler-based motion using a bezier-driven path system.  
→ 1st desired outcome: Interactive GUI for shaping curved audio motion using bezier control points  
→ 2nd desired outcome: Real-time DSP modulation of pitch, pan, gain, and filtering along path  

// *---------------------------------*
// *---------------------------------*
// ((Step 1::Goals))
// *---------------------------------*
// *---------------------------------*

* Implement bezier curve interface to define stereo motion paths  
* Map curve parameters (XY) to Doppler pitch shift, pan, gain, and filter  
* Add controls for acceleration, Doppler intensity, and depth of field  
* Implement velocity-dependent audio modulation: pitch, volume, pan  
* Integrate smooth, sample-accurate DSP processing with low CPU usage  
* Create scalable plugin structure for eventual expansion to complex motion presets  

// *---------------------------------*
// *---------------------------------*
// ((Step 2::Diagnose Root Problems & Eliminate))
// *---------------------------------*
// *---------------------------------*

ROOT PROBLEM (1): No GUI pathing system to define real-time Doppler behavior  
SOLUTION (1): Use a 3-point quadratic bezier system with user-draggable control point

ROOT PROBLEM (2): Lack of modular DSP hooks for smooth pitch, pan, gain, and filter mapping  
SOLUTION (2): Use `SmoothedValue<T>` and centralized parameter update manager for real-time-safe automation  

ROOT PROBLEM (3): No visual feedback or interpolation framework for the path state  
SOLUTION (3): Build reusable `BezierCurve` class with sampled path state at discrete `t` values (0–1), used for parameter control  

// *---------------------------------*
// *---------------------------------*
// ((Step 3::Align & Execute))
// *---------------------------------*
// *---------------------------------*

KINGPIN:  
**Implement and validate a functional bezier path control component with 3 editable points and real-time rendering.**

This is the current bottleneck: no path = no dynamic motion system = no DSP control.  
Building this first ensures we can begin unit-testing pan, pitch, gain, and filtering logic as a function of t-position.  
Once the path system is in place, parameter mapping, animation preview, and DSP logic can be layered iteratively.  
Implementation must include:  
→ Interactive control points (P0, P1, P2)  
→ Curve rendering in GUI  
→ t-parameter sampling along the curve (0–1)  
→ Visual feedback for velocity (e.g., derivative length or spacing)

// *---------------------------------*
// *---------------------------------*
// Links:
// *---------------------------------*
// *---------------------------------*

* JUCE Framework: https://juce.com/  
* Bezier Math Ref: https://pomax.github.io/bezierinfo/  
* Plugin Format Reference: https://steinbergmedia.github.io/vst3_dev_portal/  
* DSP Planning Notes: ~/dev/dopplerEFX/dsp/  
* Curve Dev Sketches: ~/dev/dopplerEFX/gui/bezier_notes.md  

// *---------------------------------*
// *---------------------------------*
// Notes:
// *---------------------------------*
// *---------------------------------*

* Prior kingpin was: choose intuitive control model → settled on 3-point bezier with XY drag  
* All core DSP features (pitch, pan, gain, filter) require `t` → param mapping  
* Consider parameter abstraction early for clean unit testing (velocity map, pitch map, etc.)  
* All visual systems must sync with audio thread-safe values  

// *---------------------------------*
// *---------------------------------*
// Progress:
// *---------------------------------*
// *---------------------------------*

start 2025/07/15  
current 2025/07/15  

Freeze State:  
→ Core JUCE GUI layout scaffolded  
→ ParameterValueTree in place  
→ Initial velocity & depth sliders prototyped  

Next Step:  
→ Implement BezierCurve class  
→ Add drag interaction + rendering for P0, P1, P2  
→ Begin sampling curve and mapping `t → parameter`  

// *---------------------------------*
// *---------------------------------*
// Completed Form:
// *---------------------------------*
// *---------------------------------*

* GUI-based bezier trajectory control system  
* Real-time pan, pitch, gain, and filter mapped to spatial curve  
* Velocity and acceleration adjustable via control slider  
* Doppler effect intensity and depth-of-field slider integrated  
* Visually animated motion preview and path feedback  
* Modular code structure for expansion into 3D and particle paths

////////////////////////////////////////////////////////////////////////////
