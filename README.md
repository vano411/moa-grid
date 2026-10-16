[README.md](https://github.com/user-attachments/files/33522853/README.md)
# MOA Grid Target

An interactive MOA grid target that runs in the browser. Tap where each shot landed, and the page measures your group and tells you how far to adjust your sights.

**Live site:** https://vano411.github.io/moa-grid/

It is one self-contained file (`index.html`) with no build step, no server and no accounts.

## What it does

- **Mark shots on a grid.** Tap or click the target to place a numbered X for each shot. Undo the last shot or clear them all.
- **Measure the group.** Extreme spread (the widest center-to-center distance), mean radius, width and height, and the group center relative to your point of aim.
- **Work out sight corrections.** The page shows how many clicks to dial for windage and elevation. Set your click value in MRAD (0.05, 0.1, 0.2, 0.25) or MOA (1/8, 1/4, 1/2, 1). Handgun and iron-sight shooters can switch scope adjustments off with one checkbox.
- **Track more than one group.** Add up to 12 groups, each with its own name, distance, cartridge and conditions. A comparison table lists every group and marks the smallest.
- **Record the details.** Caliber, brand, bullet type, weight in grains, velocity, notes, wind speed, wind direction (clock position) and temperature.
- **Log off-grid shots.** Note the direction and, optionally, the distance from center. They are saved with the group and included in exports, but left out of group size because the grid cannot measure them.
- **Export your results.** Save an image (PNG) or a JSON file, for one group or for all groups.

## How the grid works

The target is printed at a fixed size. One big square is 1.047 in, which is 1 MOA at 100 yards. The grid spans 3 1/4 squares in each direction from the center.

Because MOA is an angle, the same paper covers a different number of MOA at each distance. When you change the distance, the axis labels rescale and every reading updates. For example, at 200 yd each big square is 0.5 MOA, and at 21 ft it is 14.3 MOA.

Distance can be entered in yards, meters or feet. Shots stay where you placed them on the paper, so changing the distance afterward recalculates their MOA values.

Group sizes are always shown in MOA, with inches or centimeters shown for the spread. 1 MRAD is 3.438 MOA.

## Using it

1. Set the distance and unit, and enter any cartridge or conditions you want to record.
2. Tap the grid for each shot. Use **Undo last** if you misplace one.
3. Read the group size and the **Dial to center** corrections on the right.
4. Add another group with **+ Add group** to compare loads, distances or sessions.
5. Use **Save image** or **Save JSON** under the shot list to keep the results.

Dial directions move the point of impact toward the center. "Right 2 clicks" means move the impact to the right.

## Exports

**Image (PNG).** One group or all groups, with a header showing the group name, cartridge, distance, conditions and results. Images always use a light, print-friendly look.

**JSON.** One file per export, with this structure:

```json
{
  "app": "MOA Grid Target",
  "formatVersion": 1,
  "exportedAt": "2026-10-15T20:00:00.000Z",
  "exported": "one group",
  "scope": { "unit": "MRAD", "clickValue": 0.1 },
  "groups": [
    {
      "name": "Group 1",
      "distance": { "value": 100, "unit": "yards" },
      "cartridge": { "caliber": "", "brand": "", "bulletType": "", "weightGrains": null, "velocityFps": null, "notes": "" },
      "conditions": { "windSpeed": null, "windSpeedUnit": "mph", "windFromOClock": null, "temperature": null, "temperatureUnit": "F" },
      "shots": [{ "number": 1, "rightMoa": 0.1, "upMoa": 0.2 }],
      "offGridShots": [],
      "results": {
        "shotCount": 1,
        "extremeSpreadMoa": null,
        "meanRadiusMoa": null,
        "centerRightMoa": 0.1,
        "centerUpMoa": 0.2,
        "dialToCenter": { "windage": {}, "elevation": {} }
      }
    }
  ]
}
```

- `rightMoa` and `upMoa` are measured from the point of aim, in MOA at the group's distance. Positive is right and up.
- The `scope` block and `dialToCenter` are left out when scope adjustments are switched off.
- Exporting all groups adds a `summary` with the group count and the smallest group.

The real files contain a few more fields than shown here, such as extreme spread in inches and centimeters, width and height.

## Your data

Everything is stored in your own browser (local storage) on the site where you opened the page. Nothing is sent to a server. This means:

- Saved groups stay on that device and browser only. They do not sync between devices.
- A copy opened from a file and the copy on the website keep separate data.
- Clearing site data for the page removes your saved groups. Export a JSON file first if you want a backup.

## Run it locally

Download `index.html` and open it in a browser. There is nothing to install.

## Host your own copy

The site is served by GitHub Pages straight from `index.html` in this repository. To update it, edit or replace that file and commit the change. The site refreshes in a minute or two.

The page loads its fonts from Google Fonts. If they are blocked, it falls back to system fonts.
