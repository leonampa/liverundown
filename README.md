# 🎭 LiveRundown

LiveRundown is an open-source, real-time theatrical rundown engine coded with Gemini 3.1 Pro and Claude Sonnet 4.6, designed to replace static paper scripts for backstage crews. Built for low-latency, multi-device synchronization, it ensures stage managers, lighting operators, and audio technicians stay locked to the exact same cue line globally, compiled as a single HTML file, hosted on Netlify, and powered by Firebase.

### See live: [https://leonampa.github.io/liverundown](https://leonampa.github.io/liverundown)
> Real-time global device syncing is disabled to protect my Firebase free-tier usage limits from public API abuse. The UI navigation, hardware key bindings, and markdown parser are fully functional locally.

<img width="1191" height="1022" alt="image" src="https://github.com/user-attachments/assets/12e23f69-13c5-48c6-a1ed-5437a8d380f6" />


## The Problem  
During theatrical productions involving large ensembles (50+ cast and production crew members), traditional script management breaks down:

* **The "Lost Tracker" Dilemma:** While a Stage Manager or Prompter can keep a finger on a static paper script or PDF, actors moving on stage must look up and use props, immediately losing track of their current line.
* **The Rehearsal Burn Rate:** Up to 5 minutes per scene transition is lost simply getting a massive cast aligned on the correct script index, stalling creative momentum.
* **The Communication Void:** Static PDFs cannot communicate immediate pacing adjustments or line progressions from the tech desk to backstage in real-time.



## The Solution: LiveRundown  
LiveRundown digitizes markdown scripts and processes them into a high-visibility, deterministic grid interface. Operating on a broadcaster-receiver architecture powered by a low-overhead real-time database sync, any crew member or actor can track the exact line progression from their individual mobile devices or workstation terminals.



## Key Features

* **Deterministic State Synchronization:** Real-time global index tracking powered by Firebase. When the operator advances the script at front-of-house, the entire ensemble’s viewport updates; instantaneously, worldwide.
* **Universal Markdown/Google Docs Parser:** Seamlessly handles standard raw inputs. Even unformatted, new-line-separated text structures like `ACTOR (action) Dialogue` are natively parsed, tokenized, and beautified into clean UI modules.
* **Backstage Prompting Engine:** Optimized for mobile browser responsiveness, allowing backstage actors to monitor cue indicators, and scene positions instantly from their phones before stepping onto the stage.
* **Hardware Macro Integration:** Native key-binding hooks supporting external hardware inputs (such as a Stream Deck mapped to mechanical inputs like `F13` or `ArrowDown`) for seamless tactile progression.
* **Intelligent Scroll Anchoring:** Leverages modern DOM manipulation techniques (`scrollIntoView`) to cleanly focus active cues without interfering with structural layouts or causing UI jitter.



## Architecture \& Tech Stack  
The engineering philosophy behind LiveRundown prioritizes ultra-low friction deployment and maximum device compatibility. Backstage environments often rely on varying cell signals, older smartphones, and legacy hardware.

* **Frontend:** Vanilla HTML5, CSS3 Variables, ES6 JavaScript.
* **Database \& Synchronization:** Firebase Realtime Database
* **Deployment Infrastructure:** Netlify



## Setup

* Go to [Firebase](console.firebase.google.com), and log in with any Google account
* Click "Create a project", name it, disable Google Analytics, click Create Project
* Click "+ Add app", click "</>"/Web, give your app a name, do **NOT** check "Also set up Firebase Hosting", click "Register"
* Firebase now shows you a firebaseConfig object. It looks like a block of JavaScript with an apiKey, authDomain, etc. Copy the whole thing onto a notepad. Click "Continue to console".
* In the left sidebar, go to "Databases \& Storage" → "Realtime Database", click "Create Database"
* Choose the server location closest to you 
* Click "Start in test mode", click "Enable", and copy the URL that ends with "firebasedatabase.app"
* Go to Rules, change whatever is there, to the below block, click Save

~~~JSON
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
~~~

* Download index.html from this repo, open it, and edit the Firebase config on lines 354-362
* Place index.html and your script.md on a folder, and upload the folder as-is on Netlify
* Visit the given URL on two tabs/windows/devices, and check to see if it works like it should

## How to use
### Navigation
* Tap / click anywhere: Advance one line
* Double-tap a line: Jump directly to that line
* Arrow Down / F13: Advance one line
* Arrow Up: Go back one line

### Sync
* **Open the SYNC button** (bottom-right of the dashboard)
* **To broadcast:** toggle "Broadcast my index?" on, optionally set your name
* **To follow:** leave the toggle off and tap a broadcaster from the Available broadcasts list
* **To disconnect:** tap the active broadcaster again
