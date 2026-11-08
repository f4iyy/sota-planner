# SOTA Planner

A small, single-file web app to estimate the duration of a [SOTA](https://www.sota.org.uk/) (Summits on the Air) outing and to **back-plan** your departure time. Available in English and French.

No installation, no dependencies, no server: just open `sota-planner.html` in a browser (desktop or phone).

## Features

- **Forward planning** – enter your departure time and get a step-by-step itinerary with the return time.
- **Back-planning** – enter a target time and the app tells you when to leave. The target can be:
  - being back home,
  - reaching summit N,
  - starting the activation of summit N,
  - finishing the activation of summit N.
- **1 to 6 summits** per outing, each with its own hike, drive and activation times.
- **Summary** – total time, hiking time, activation time and a colour-coded breakdown bar.
- **Time limit warning** – optionally enter a limit (e.g. sunset); the app warns you if the descent ends after it.
- **Copy / print** – copy the itinerary as plain text, or print it / save it as PDF.
- **Languages** – switch between English and French with the flags at the top. The choice is remembered.
- Settings are saved in your browser (`localStorage`); nothing is sent anywhere.

## Usage

1. Open `sota-planner.html` in a browser.
2. Pick a **mode**:
   - *I leave at…* – set the departure time.
   - *I want to be there at…* – choose a goal and the time you want to reach it.
3. Set the **number of summits** and the drive times (outbound and return; tick *Return same as outbound* to mirror them).
4. For each summit, enter the **hike up**, **hike down** (or tick *Down same as up*), **activation time**, and, from the second summit on, the **drive from the previous summit**.
5. Adjust the **prep & rest times** (all values in minutes):

   | Setting | Default |
   |---|---|
   | Prep before the outbound drive / after the return | 10 |
   | Prep before a hike (up or down) | 5 |
   | Prep before driving between summits | 5 |
   | Setup before / pack-up after the activation | 20 |
   | Rest at the summit | 15 |

6. Read the **itinerary** on the right (or below on a phone). In back-planning mode, the goal step is highlighted and the big card shows the departure time you need.
7. Use **Copy plan** to paste it into a message, or **Print / PDF**.

Times past midnight are shown with a `+1d` suffix.

## How the itinerary is built

For each outing the steps are chained in this order:

1. Departure → prep → drive there
2. For each summit: *(from summit 2: prep → drive from previous summit)* → prep → hike up → rest → setup → **activation** → pack-up → hike down
3. Prep → drive back → prep → arrival home

The total duration does not depend on the start time, so back-planning simply subtracts the time elapsed before the chosen goal from your target time.
