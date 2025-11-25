# Mindfulness-Card-of-the-Day
:root{
  --bg: #e8f6ea;
  --text: #1f4b39;
  --muted: #4c7a63;
  --accent-1: #7bd39a;
  --accent-2: #4ca977;
  --accent-dark: #2f7c4a;
  --card-radius: 18px;
  --card-width: 260px;
  --card-height: 170px;
  --transition: 0.6s;
  --shadow: 0 8px 20px rgba(0,0,0,0.15);
}

* { box-sizing: border-box; }

body {
  margin: 0;
  padding: 0;
  background: var(--bg);
  color: var(--text);
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
}

.page {
  max-width: 900px;
  margin: 0 auto;
  padding: 32px 16px 60px;
  text-align: center;
}

/* Typographic scale with responsive sizing */
h1 {
  font-size: clamp(20px, 3.2vw, 32px);
  margin-bottom: 8px;
}

.subtitle {
  font-size: clamp(13px, 1.6vw, 15px);
  margin-bottom: 28px;
  color: color-mix(in srgb, var(--text) 70%, black 10%);
}

/* Card container: grid for better responsive wrapping */
.card-wrapper {
  display: grid;
  grid-auto-flow: column;
  grid-auto-columns: min-content;
  justify-content: center;
  gap: 18px;
  margin-bottom: 18px;
  align-items: center;
}

/* Small screens: stack or two-up */
@media (max-width: 640px) {
  .card-wrapper {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-auto-flow: row;
    gap: 12px;
    padding-inline: 8px;
  }
}

/* Card flip layout */
/* Use aspect-ratio so the card resizes nicely while keeping proportions */
.card {
  width: min(90vw, var(--card-width));
  aspect-ratio: 260 / 170;
  perspective: 1000px;
  cursor: pointer;
  display: inline-block;
  -webkit-tap-highlight-color: transparent;
  transition: transform 160ms ease; /* subtle press feedback */
  will-change: transform;
  /* Make the card focusable from keyboard (add tabindex in HTML) */
  outline: none;
}

/* Optional pressed scale for touch/active */
.card:active { transform: scale(0.995); }

/* inner 3D container */
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform var(--transition) cubic-bezier(.2,.9,.3,1);
  transform-style: preserve-3d;
  will-change: transform;
}

/* flipped state toggle (JS toggles .flipped on .card) */
.card.flipped .card-inner,
.card.is-flipped .card-inner {
  transform: rotateY(180deg);
}

/* faces */
.card-face {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  border-radius: var(--card-radius);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 16px;
  box-shadow: var(--shadow);
  overflow: hidden;
}

/* Front */
.card-front {
  background: linear-gradient(145deg, var(--accent-1), var(--accent-2));
  color: #ffffff;
  font-size: 18px;
  gap: 4px;
  padding-inline: clamp(12px, 2vw, 16px);
}

/* emoji scale uses clamp for responsiveness */
.card-front span.emoji {
  font-size: clamp(28px, 6vw, 32px);
  line-height: 1;
  display: block;
}

/* Back */
.card-back {
  background: #ffffff;
  color: var(--text);
  transform: rotateY(180deg);
  font-size: 16px;
  line-height: 1.4;
  padding-inline: clamp(12px, 2vw, 16px);
}

/* minor visual hint text */
.hint {
  font-size: 13px;
  color: var(--muted);
  margin-bottom: 10px;
}

/* Controls */
.controls {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
  margin-top: 12px;
}

/* Buttons */
button {
  border: none;
  border-radius: 999px;
  padding: 9px 18px;
  font-size: 14px;
  cursor: pointer;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  background: #fff;
  color: var(--accent-dark);
  transition: transform 140ms ease, box-shadow 140ms ease, opacity 120ms ease;
}

button:hover { opacity: 0.94; transform: translateY(-2px); }

/* Primary / secondary specific */
#new-card-btn {
  background: var(--accent-dark);
  color: #fff;
}

#flip-back-btn {
  background: #fff;
  color: var(--accent-dark);
  border: 1px solid color-mix(in srgb, var(--accent-dark) 15%, transparent);
}

/* Focus styles (accessible) */
button:focus-visible,
.card:focus-visible {
  outline: 3px solid color-mix(in srgb, var(--accent-dark) 35%, white 65%);
  outline-offset: 4px;
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}

/* today label */
.today-label {
  font-size: 14px;
  margin-bottom: 6px;
  color: #32654d;
}

/* reduced-motion support */
@media (prefers-reduced-motion: reduce) {
  .card-inner,
  button,
  .card { transition-duration: 0.01ms !important; animation-duration: 0.01ms !important; }
}
