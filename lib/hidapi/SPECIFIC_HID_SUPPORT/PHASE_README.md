# PHASE Needle-less HID support 

FORK: github.com/cacherefresh/mixxx (main)
BRANCH: feature/yuvi/issue12886-Add_HID_SUPPORT


## Background: 
Phase already works out of the box with standard RCA -> Relative mode -> timecode vinyl with mixxx

### the NEW intended target way:
What we are doing is adding a HID dropdown so that we can skip the additional RCA -> soundcard-> input as timecode
this should help both REDUCING LATENCY for more natural turntablist feel, AND reduce extra wires/hardware. 

### The Old way:
Phase works exceptionally well with Mixxx, but it requires a traditional DVS audio routing setup because Mixxx does not support Phase’s native USB/HID mode. Since Phase communicates its data as an audible timecode signal via RCA cables, Mixxx treats it exactly like a standard timecode vinyl or CD.The exact workflow to set up and run Phase within Mixxx involves specific software configurations, signal emulation, and platform limitations.1. The Core Concept: Timecode EmulationBecause Mixxx does not natively read Phase data directly over a USB cable, you must configure the Phase Receiver to emulate an audio timecode signal that Mixxx natively understands.Open the Phase Manager software on a Mac or Windows PC (Phase configuration cannot be done directly inside Linux or Mixxx).Go to the settings and set the Phase Remotes to output Serato timecode (this uses a standard 1kHz tone that Mixxx tracks cleanly).Ensure the Phase Receiver outputs are configured to Line level (not Phono), as Phase outputs a strong pre-amplified digital signal.2. Audio Routing and HardwareYou need an audio interface (soundcard) or a DJ mixer with a built-in soundcard to bridge Phase and Mixxx.The Path: Connect the RCA outputs from the Phase Receiver into the Line inputs of your DVS soundcard or DVS-supported mixer. Connect that soundcard or mixer to your computer running Mixxx.Mixxx Settings: Open Mixxx, navigate to Preferences -> Sound Hardware, and choose the Input tab. Assign your soundcard's channels (e.g., Channels 1-2 for Deck 1, Channels 3-4 for Deck 2) under Vinyl Control 1 and Vinyl Control 2.3. Configuring Vinyl Control inside MixxxOnce the hardware routing is established, you need to match Mixxx's deck behavior to Phase's signal.Select Timecode Type: Under the Vinyl Control preferences pane in Mixxx, select Serato CDCO (Serato Timecode) to match what you assigned in Phase Manager.Use Relative Mode: You must set the virtual decks in Mixxx to Relative Mode. Because Phase uses wireless sensors rather than a physical groove on a vinyl record, it cannot track absolute positioning (needle drops). Relative mode allows Mixxx to track only the speed, direction, and scratches smoothly.Enable Control: Unhide the vinyl control interface in your Mixxx skin and click the Enable Vinyl Control button for each deck.4. Key Limitations to Keep in MindFirmware Updates: You cannot update Phase firmware or change internal receiver settings directly through Mixxx or Linux. You will need a Mac or Windows machine running Phase Manager whenever Phase releases an official update.Cue Points: Because you are locked into Relative Mode, moving the physical record to a different spot will not skip to that section of the track in Mixxx. You will want to map a secondary MIDI controller (like a pad controller or your keyboard) to trigger cue points and track browsing.


## PLAN:
 implement native USB/HID support for Phase within your own fork of Mixxx on GitHub. The Mixxx core team has actually opened an active tracking issue (GitHub Issue #12886) looking for an experienced developer to do exactly this.While your skills will make navigating the codebase straightforward, the true battle lies in reverse engineering and architecture.

### Steps
 1. The Core Concept: Timecode Emulation
Because Mixxx does not natively read Phase data directly over a USB cable, you must configure the Phase Receiver to emulate an audio timecode signal that Mixxx natively understands.Open the Phase Manager software on a Mac or Windows PC (Phase configuration cannot be done directly inside Linux or Mixxx).Go to the settings and set the Phase Remotes to output Serato timecode (this uses a standard 1kHz tone that Mixxx tracks cleanly).Ensure the Phase Receiver outputs are configured to Line level (not Phono), as Phase outputs a strong pre-amplified digital signal.

 2. Audio Routing and Hardware
You need an audio interface (soundcard) or a DJ mixer with a built-in soundcard to bridge Phase and Mixxx.The Path: Connect the RCA outputs from the Phase Receiver into the Line inputs of your DVS soundcard or DVS-supported mixer. Connect that soundcard or mixer to your computer running Mixxx.Mixxx Settings: Open Mixxx, navigate to Preferences -> Sound Hardware, and choose the Input tab. Assign your soundcard's channels (e.g., Channels 1-2 for Deck 1, Channels 3-4 for Deck 2) under Vinyl Control 1 and Vinyl Control 2

 3. Configuring Vinyl Control inside MixxxOnce the hardware routing is established, you need to match Mixxx's deck behavior to Phase's signal.Select Timecode Type: Under the Vinyl Control preferences pane in Mixxx, select Serato CDCO (Serato Timecode) to match what you assigned in Phase Manager.Use Relative Mode: You must set the virtual decks in Mixxx to Relative Mode. Because Phase uses wireless sensors rather than a physical groove on a vinyl record, it cannot track absolute positioning (needle drops). Relative mode allows Mixxx to track only the speed, direction, and scratches smoothly.Enable Control: Unhide the vinyl control interface in your Mixxx skin and click the Enable Vinyl Control button for each deck.

 4. Key Limitations to Keep in Mind:
  - Firmware Updates: You cannot update Phase firmware or change internal receiver settings directly through Mixxx or Linux. You will need a Mac or Windows machine running Phase Manager whenever Phase releases an official update.
  - Cue Points: Because you are locked into Relative Mode, moving the physical record to a different spot will not skip to that section of the track in Mixxx. You will want to map a secondary MIDI controller (like a pad controller or your keyboard) to trigger cue points and track browsing.
For that we can use github.com/cacherefresh/YuVi_Glow and an mpd226 or other standard midi device. 
  
