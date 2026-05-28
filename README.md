# External vs swap regret: a 3-action interactive demo

A single-page interactive comparison of two no-regret learning algorithms on a 3-action online learning problem:

- **EW** — Exponential Weights, the classic external-regret minimizer.
- **SDA** — Stationary Delegation Algorithm of Blum and Mansour (2007), which achieves swap regret by running k internal EW experts and playing the stationary distribution of their recommendations.

Companion to Section 4 of Hartline's review article *The Economics of No-Regret Learning Algorithms* (arXiv:2601.22079).

## Why 3 actions

With k = 2 actions, swap regret and external regret coincide as concepts — the only non-trivial swap is the transposition, which always reduces to one of the constant swaps. To see the two regret notions genuinely separate, you need k ≥ 3. This demo uses k = 3 with input on the probability simplex (a triangle).

## What it does

Click anywhere inside the triangle to set the round's payoff u = (u₁, u₂, u₃). The click position determines the payoff via barycentric coordinates: corners give payoff 1 to that action and 0 to the others; the centroid gives (1/3, 1/3, 1/3); etc.

The chart shows three regret curves:

- **EW external regret** — what EW is designed to minimize.
- **EW swap regret** — the same play sequence judged by the stronger swap benchmark. The gap between this and EW external regret is what swap regret penalizes that external regret ignores.
- **SDA swap regret** — SDA's behavior under the stronger benchmark.

Two preset adversaries are provided to make the separation easy to see:

- **Cycle through corners (10×)** — 10 rounds at (1,0,0), then 10 at (0,1,0), then 10 at (0,0,1). After 30 rounds all three cumulative payoffs are equal, so external regret is near zero. But swap regret is large because EW chased the leader and was concentrated on the wrong action at every transition.
- **Rock-paper-scissors (10×)** — cycles through (1, 0, ½), (½, 1, 0), (0, ½, 1) (normalized to sum to 1).

A learning rate slider replays the entire history through both algorithms with the new ε, so you can see immediately how that hyperparameter affects both regrets.


## Link

You can try the demo [here](https://anderartola.github.io/swap-regret-demo/).


## License

MIT.
