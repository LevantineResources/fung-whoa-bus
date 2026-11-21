# The Fung Whoa Bus

Boston to Washington, D.C. for $15. No refunds. No questions.

A browser game about surviving an overnight discount bus: keep the bus running, your morale up, and your bladder in check, and reach D.C. by 5:00 AM.

## Play

Open `index.html` in a browser. There is no build step and there are no dependencies.

- **Space / tap the road:** yell "POTHOLE!" so the driver hops the bus over it
- **1–9:** pick a choice
- **Arrow keys / WASD / tap:** move during the rest stop dash

## Publish with GitHub Pages

In the repository on GitHub: **Settings → Pages → Build and deployment → Deploy from a branch**, pick `main` and `/ (root)`, and save. The game appears at `https://<user>.github.io/<repo>/` a minute or so later.

## Code layout

Everything lives in `index.html`. The script is organised into sections: data (seats, companions, items), state, UI, driving, events, stops, the two mini-games (tire change, rest stop dash), endings, and rendering.

To add a road event, append an object to the `EVENTS` array:

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
