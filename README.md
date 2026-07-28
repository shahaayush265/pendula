# Pendula 🖊️

**Live Demo:** [https://shahaayush265.github.io/pendula](https://shahaayush265.github.io/pendula)

**Pendula** is a web-based, real-time physics visualization and motion tracking tool. It captures organic human input (like rolling a drawing tablet stylus or gently swinging a mouse) and evaluates it against the mathematical ideal of **Damped Simple Harmonic Motion (SHM)**.

![Pendula Interface Preview](https://via.placeholder.com/800x400.png?text=Pendula+Motion+Tracker)

## 📖 The Origin Story

Pendula was born out of a happy accident. One day, I left my graphics tablet stylus lying horizontally on the tablet surface. I accidentally nudged it, and it began to roll to and fro. I noticed that the cursor on my screen was mimicking this periodic motion flawlessly. Watching it gradually slow down, it struck me: the physical rolling of the slightly asymmetrical pen was actually a perfect real-world example of **Damped Simple Harmonic Motion**. I built Pendula to track, graph, and mathematically prove that exact observation.

## 🚀 How to Use

1. Click **Start Recording** (Wait for the 3-second delay to position your pen).
2. Physically place your stylus on its side and gently push it so it rolls back and forth.
3. Watch the **Blue Dot** (your cursor) and the **Orange Dot** (the real-time math prediction) map your path.
4. Let the pen settle completely. The app will Auto-Stop.
5. Review the mathematical parameters of the physical friction acting on your specific pen and click **Replay Motion** to see how closely physical reality matches the theory.

## 🧮 The Math

Pendula projects your 2D cursor movement onto a 1D timeline to extract these physical parameters:

- **$A$ (Amplitude):** Your initial displacement in pixels.
- **$\gamma$ (Damping):** The friction coefficient (how quickly the rolling pen slows down).
- **$\omega$ (Angular Frequency):** How fast the pen rocks back and forth.
- **$\phi$ (Phase):** The starting position offset.

## ✨ Features

## 🕵️ The "JEE Aspirant" Cheats (How to break the math)

As a JEE aspirant, you spend hundreds of hours studying the exact mechanics of Simple Harmonic Motion. A core concept in JEE physics is that **SHM is simply the 1D projection of Uniform Circular Motion**.

Knowing this, before I even tested the first version of the app, I suspected I could completely fool the curve-fitting algorithm. Since the app uses Principal Component Analysis (PCA) to find the primary axis and projects your 2D motion onto that 1D line, I realized I didn't actually have to draw a pendulum swing to get a 99% score.

Here are the three mathematical loopholes I used to break my own app:

### 1. The Spiral (90%+ Score)

If you draw concentric circles moving steadily inward, you are drawing a damped polar curve: $r(t) = A e^{-\gamma t}$.
When the PCA projects this 2D spiral onto a 1D axis, the math becomes:
$$x(t) = r(t) \cos(\omega t) = A e^{-\gamma t} \cos(\omega t)$$
This is _literally_ the exact equation for Damped SHM. The 1D shadow of a shrinking circle perfectly mimics a pendulum!

### 2. The Figure-8 (88%+ Score)

A Figure-8 is a Lissajous curve. If you draw it with a decreasing radius, its 1D projection across the primary axis generates a highly periodic, decaying wave. While slightly chaotic, it easily tricks the Simulated Annealing algorithm into finding a "good enough" local minimum that looks like Damped SHM.

### 3. The Straight Line (99% Score)

The most powerful cheat of all. The standard SHM equation is $x(t) = A e^{-\gamma t} \cos(\omega t + \phi)$.
If you simply swipe your mouse in a straight line and slow down to a stop, the algorithm drops the angular frequency ($\omega$) to `0` and sets the phase ($\phi$) to `0`, reducing the equation to:
$$x(t) = A e^{-\gamma t}$$
The math engine perfectly matches your straight swipe as a pure exponential decay!

### 🛡️ The Anti-Cheat Update

To fix these loopholes, Pendula now features a mathematical tripwire system:

- **Orthogonal Variance Check:** It calculates how much you move _perpendicular_ to the main PCA axis. If your perpendicular spread is >15% of your main spread, it knows you are drawing 2D shapes (Spirals/Figure-8s) instead of staying on a 1D line.
- **Path-Length Ratio Check:** A true pendulum swings back and forth, meaning the total distance the cursor travels must be far greater than the maximum spread of the swing. If the path length is roughly equal to the spread, the app knows you just drew a straight line.

_Try the pre-loaded `.motion` files in the "Cheats" menu to see the anti-cheat system in action!_

---

- **Omnidirectional 2D Tracking:** Swing your cursor in any direction. Pendula dynamically tracks your primary axis.
- **Live Predictive Fit:** A background optimization engine calculates a live mathematical prediction of where your pen _should_ be in real-time.
- **Deep Post-Analysis:** Once the motion settles, a secondary deep-fit calculation generates the absolute optimal model equation and outputs a "Similarity Score" ($R^2$ fit).
- **Overlay Replay:** Watch your raw, human motion race against the perfectly calculated mathematical model.
- **The `.motion` File Standard:** Save, export, and load your custom `.motion` telemetry files to build a personal library of physics experiments.
- **Glassmorphic UI:** Modern, responsive design featuring a seamless, auto-detecting Light/Dark mode.

## 📁 Creator Examples & Cheats

The repository includes a dedicated `/examples/` folder containing pristine tests and the cheat files mentioned above.

- **Note for local development:** If you want to load the `.motion` files from the UI, you must run a local web server (like VSCode Live Server or `python -m http.server`). Browsers block fetch requests to local directories for security reasons.

## 🛠️ Built With

- Vanilla HTML5 / CSS3 / ES6 JavaScript
- HTML Canvas API
- Custom implementation of Monte Carlo + Simulated Annealing optimization algorithms.
- _No external libraries or dependencies._
- JEE-level love :)
