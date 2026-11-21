# The Fung Whoa Bus

Boston to Washington, D.C. for $15. No refunds. No questions.

A browser game about surviving an overnight discount bus: keep the bus running, your morale up, and your bladder in check, and reach D.C. by 5:00 AM.

## Play

Open `index.html` in a browser. There is no build step and there are no dependencies.

- **Arrow keys / WASD, or the on-screen buttons:** change lane, speed up, slow down
- **1–9:** pick a choice
- Each mini-game (tire change, rest stop dash, luggage, river crossing, hold on) shows its own controls

## Publish with GitHub Pages

In the repository on GitHub: **Settings → Pages → Build and deployment → Deploy from a branch**, pick `main` and `/ (root)`, and save. The game appears at `https://<user>.github.io/<repo>/` a minute or so later.

## Code layout

Everything lives in `index.html`. The script is organised into sections: data (seats, companions, items), state, UI, driving, events, stops, the mini-games (tire change, rest stop dash, luggage, river crossing, hold on), endings, and rendering.

To add a passenger who rides for one leg, add an entry to `RIDERS`. To add a road event, append an object to the `EVENTS` array:

```js
{ id: 'unique-id', title: 'Title', moving: true,
  text: `What happens.`,
  choices: [
    { label: 'A choice', go: () => { apply({ morale: 5, time: 10 }); return `What happened next.`; } },
    { label: 'Needs an item', item: 'tape', go: () => { useItem('tape'); return `...`; } },
    { label: 'Costs money', cost: 2, go: () => `...` },
  ] }
```

`apply()` accepts `morale`, `health`, `bladder`, `cash`, and `time` (minutes; negative is good).
