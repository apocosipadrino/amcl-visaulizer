# AMCL Visualizer

Interactive Adaptive Monte Carlo Localization (AMCL) simulation in a single self-contained HTML file. No build step, no dependencies — open `index.html` in a browser.

## What it shows

A robot drives a waypoint loop in a 10×10 m map with two inner walls, sensing the walls with a 12-ray laser scan. The filter starts with particles spread uniformly over the map (global localization) and converges as scans arrive.

- **Predict**: particles propagate with a noisy motion model (odometry + noise).
- **Update**: particles are weighted by a Gaussian beam model comparing each particle's predicted scan with the real scan.
- **Resample**: KLD-sampling adapts the particle count to uncertainty (many particles when lost, few when confident).
- **Recovery**: random particles are injected when the sensor likelihood drops (fast/slow average likelihood, augmented MCL), so the filter recovers from the kidnapped-robot problem — try the **Kidnap robot** button.

## Controls

- **Auto / Step**: run continuously or one predict+update step at a time.
- **Kidnap robot**: teleport the robot to a random free pose; watch the particle count grow, injection rise, and the estimate re-converge.
- **Reset**: restart with a uniform particle cloud.
- **Max particles**: upper bound for KLD-sampling (100 minimum).
- **Motion noise / Sensor noise**: noise levels for the motion model and the laser scan.

## Notes

- The fast/slow likelihood averages use α_fast = 0.2 and α_slow = 0.02, tuned for the demo timescale (the textbook values assume thousands of updates).
- Enable GitHub Pages (Settings → Pages, deploy from main) to run it at https://apocosipadrino.github.io/amcl-visaulizer/
