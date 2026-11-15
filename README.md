# Dark Sun Online: Crimson Sands - Windows Port (SDL2)

> **Download:** Grab the latest release build on the [**Releases**](../../releases) page.

This build (based on **v0.6**) includes an experimental **Single-player mode** for a full offline playthrough without an internet connection or servers.

The project is in **alpha**, so bugs are possible (and there will be some, no doubt).

---

## About

No AI was used in this project, everything was done with my own brains, hands, and experience.

That is why an old-as-time **HLE (High-Level Emulation)** approach was used: the loader loads the original game blob into memory (yes, you have to provide the original `mdark.exe` v2.8 and all the game data files) and patches all platform-dependent calls to a high-level wrapper (modern WinAPI and SDL2).

Instead of spending years manually reversing all the thousands of game functions (including the game logic and gamescript VM interpreter), only the low-level system boundaries were located and hooked: clib/stdlib calls and file I/O, Win16 dusty APIs, DOS interrupts, 1MB segment access, VGA segment and ports - all wrapped onto modern WinAPI and SDL2 abstraction.

### Cons of this approach

* **Antivirus false positives:** Such actions (specifically, setting `RWX` permissions on virtual memory segments, runtime inline hooks and patches, and subsequently executing the original game code loaded into a segment) trigger almost all antivirus software - so the port requires disabling your antivirus or adding it to exclusions, otherwise no miracle will happen.
* **x86-32 only:** The port is nailed down tight to the `x86-32` architecture (which is not an issue at this stage).

### Pros of this approach

* **100% human-written code:** For those who care about this - you can be sure that the entire port, including its general architecture, was written the old-fashioned way by a meatbag. No AI slop, though... humans make mistakes too, so bugs are definitely present, as well as possibly suboptimal solutions. Still, everything in this port, from the first line to the last, was written by a human by hand and with full awareness. Smash that like button if you get an uncanny valley feeling looking at the flood of AI-slop ports! :)
* **Lightweight:** The HLE code is small and optimized.
* **Fidelity:** HLE does not interfere with the original logic. All core algorithms are original, no assumptions, guesses, or simulations. Fidelity, so to speak. Including the bugs generously scattered by the original developers. Just like in the good old days :)
* **No wasted time:** It does not require spending tons of time on routine work like disassembling ALL of the original game code, since it is used directly in its original form.

---

## How to Play

### 1. Required Original Files

The port requires the original files and executable from the last official release of the **Dark Sun Online: Crimson Sands** client (so-called version `"2.8"`, build tag `"2.0:Sep 05 1997:12:07:23"`).

**Original hashes for vanilla v2.8 `Mdark.exe`:**
```
MD5:    c933508e291bb3ebfcc276344bdfd6ef
SHA256: d04ef090951cd2d3e51dc750f9eb024cfc57e902a6ad0f8763b89129ddc2bef7
```

### 2. Installation & Launch

1. Put all the port files (`dso-win.exe`, `SDL2.dll`, `SDL2_mixer.dll`, and the `cdaudio` folder) into your **DSO v2.8** directory.
2. Add the game folder to your **ANTIVIRUS EXCLUSIONS** beforehand (or disable your antivirus while playing).
3. Run `dso-win.exe`.

### 3. CD-Audio Music (Optional)

The port supports the original game's CD-Audio feature: to use it, place the OGG files named `track02.ogg` .. `track29.ogg` into the `cdaudio` subfolder.

### 4. Basic Controls

| Key / Shortcut | Action |
| :--- | :--- |
| **Middle Mouse** | Capture / release mouse cursor |
| **F12** | Toggle standard SDL2 bilinear filtering |
| **Alt + Enter** | Toggle Fullscreen |
| **Shift** | Skip the intro cinematic |
| **S, C, E** | Main menu shortcuts: **S**tart game, **C**reate character, **E**xit |
| **Alt + P** | In-game settings during gameplay |
| **F1** | Show in-game help |
| **F6**, **Alt + A** | Toggle character animations |
| **1 .. 9** | Select dialog options with NPCs or during events |

---

## Useful Links

* **Original Manual:** [darksunonline-manual.pdf (MOCAGH)](https://mocagh.org/ssi/darksunonline-manual.pdf)
* **Original FAQ by AVrignaud:** [GameFAQs Guide](https://gamefaqs.gamespot.com/pc/565241-dark-sun-online-crimson-sands/faqs/2245)
* **Project Website:** [dsoemu.pages.dev](https://dsoemu.pages.dev)
* **Dark Sun Online Project Community Discord:** [discord.gg/TDyzXXj4Pd](https://discord.gg/TDyzXXj4Pd)
---

*- crt0, 2024–2026*
