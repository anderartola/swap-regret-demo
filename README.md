# External vs swap regret: an interactive demo

A single-page interactive comparison of two no-regret learning algorithms on a 2-action online learning problem:

- **EW** — Exponential Weights, the classic external-regret minimizer.
- **SDA** — Stationary Delegation Algorithm of Blum and Mansour (2007), which achieves swap regret by running k internal EW experts and playing the stationary distribution of their recommendations.

Companion to Section 4 of Hartline's review article *The Economics of No-Regret Learning Algorithms* (arXiv:2601.22079).

## What it does

Click anywhere in the unit square to set the round's payoff vector u = (u₁, u₂). Both algorithms commit to a distribution *before* seeing u, then observe the full payoff vector. The display shows:

- Each algorithm's current action distribution, both as horizontal bars next to the algorithm's name and as bars along the edges of the square.
- The two SDA experts' individual recommendations (expert a is the internal EW that "owns" action a).
- A running plot of EW's external regret, SDA's swap regret, and SDA's external regret over time.
- A slider to adjust the learning rate ε. Changing ε replays the full payoff history through both algorithms with the new rate so you can see the effect immediately.

## Running locally

It's a single HTML file with no build step. Just open it:

```bash
# Option 1: open directly
open index.html  # macOS
xdg-open index.html  # Linux

# Option 2: serve it (recommended; some browsers restrict file:// for canvas)
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying to GitHub Pages

1. Create a new GitHub repository (public if you want free Pages hosting).
2. Push these files to the `main` branch:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```
3. On GitHub, go to your repo's **Settings → Pages**.
4. Under **Source**, select **Deploy from a branch**, choose `main` and `/ (root)`, then click **Save**.
5. Wait a minute or two. Your site will be live at `https://<your-username>.github.io/<your-repo>/`.

That's it — no Jekyll config, no build action, no dependencies to install. The page loads Chart.js from a CDN at runtime.

## File structure

```
.
├── index.html      # The entire app: HTML, CSS, JS
└── README.md       # This file
```

## Customizing

The full app is in `index.html`. Two things you might want to change:

- **Number of actions.** Currently hardcoded to k = 2 because that lets the action distribution display naturally along the edges of a 2D payoff square. Generalizing to k > 2 would require a different visualization for both the payoff input (the unit square only works for k = 2) and the action distributions.
- **Learning rate range.** The slider in the controls row is set to `min="0.05" max="1.0" step="0.05"`. Adjust those attributes to widen or narrow the range.
- **Color scheme.** All colors are defined as CSS variables at the top of the `<style>` block, with a `prefers-color-scheme: dark` block for automatic dark mode.

## License

MIT. Do what you want with it.
