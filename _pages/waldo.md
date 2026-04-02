---
layout: page
title: where's waldo
permalink: /waldo/
nav: false
description: Find Waldo in a photo.
waldo_image: /assets/img/waldo/waldo-scene.svg
waldo_x: 68
waldo_y: 42
waldo_tolerance: 6
clues:
  - "Look near bright reds and whites."
  - "Waldo likes crowded edges more than open space."
  - "Try scanning in a loose spiral from the center."
---

<div class="waldo-wrap">
  <p class="waldo-intro">
    Click the image where you think Waldo is hiding. If you are close enough, you win.
  </p>

  <div class="waldo-toolbar" role="group" aria-label="Waldo controls">
    <button id="waldoRevealBtn" class="waldo-btn" type="button">Reveal Waldo</button>
    <button id="waldoResetBtn" class="waldo-btn waldo-btn-secondary" type="button">Reset</button>
  </div>

  <p class="waldo-status" id="waldoStatus" aria-live="polite">Ready when you are.</p>

  <div class="waldo-board" id="waldoBoard">
    <img
      id="waldoImage"
      src="{{ page.waldo_image }}"
      alt="Where's Waldo scene"
      loading="lazy"
    />
    <div id="waldoTarget" class="waldo-target" aria-hidden="true"></div>
    <div id="waldoGuess" class="waldo-guess" aria-hidden="true"></div>
  </div>

  {% if page.clues and page.clues.size > 0 %}
    <section class="waldo-clues" aria-label="Waldo clues">
      <h3>Clues</h3>
      <ul>
        {% for clue in page.clues %}
          <li>{{ clue }}</li>
        {% endfor %}
      </ul>
    </section>
  {% endif %}
</div>

<style>
.waldo-wrap {
  --waldo-accent: #d9480f;
  --waldo-accent-soft: #ffe8cc;
  --waldo-ink: #2f2f2f;
  max-width: 860px;
  margin: 0 auto;
}

.waldo-intro {
  color: var(--waldo-ink);
  margin-bottom: 0.75rem;
}

.waldo-toolbar {
  display: flex;
  gap: 0.6rem;
  flex-wrap: wrap;
  margin: 0.7rem 0;
}

.waldo-btn {
  border: 1px solid var(--waldo-accent);
  background: var(--waldo-accent);
  color: #fff;
  border-radius: 999px;
  padding: 0.42rem 0.9rem;
  font-size: 0.93rem;
  cursor: pointer;
}

.waldo-btn:hover,
.waldo-btn:focus-visible {
  filter: brightness(0.95);
}

.waldo-btn-secondary {
  background: #fff;
  color: var(--waldo-accent);
}

.waldo-status {
  margin: 0.35rem 0 0.75rem;
  padding: 0.45rem 0.7rem;
  border-left: 4px solid var(--waldo-accent);
  background: var(--waldo-accent-soft);
}

.waldo-board {
  position: relative;
  border: 1px solid #ddd;
  border-radius: 0.5rem;
  overflow: hidden;
  background: #f5f5f5;
}

.waldo-board img {
  width: 100%;
  display: block;
  cursor: crosshair;
}

.waldo-target,
.waldo-guess {
  position: absolute;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  transform: translate(-50%, -50%);
  display: none;
}

.waldo-target {
  border: 3px solid #00a63e;
  background: rgba(0, 166, 62, 0.2);
  box-shadow: 0 0 0 5px rgba(0, 166, 62, 0.15);
}

.waldo-guess {
  border: 3px solid #1a73e8;
  background: rgba(26, 115, 232, 0.2);
}

.waldo-clues {
  margin-top: 1rem;
}

.waldo-clues h3 {
  margin: 0 0 0.35rem;
  font-size: 1.05rem;
}

@media (max-width: 640px) {
  .waldo-target,
  .waldo-guess {
    width: 22px;
    height: 22px;
  }
}
</style>

<script>
(function () {
  const board = document.getElementById('waldoBoard');
  const image = document.getElementById('waldoImage');
  const status = document.getElementById('waldoStatus');
  const target = document.getElementById('waldoTarget');
  const guess = document.getElementById('waldoGuess');
  const revealBtn = document.getElementById('waldoRevealBtn');
  const resetBtn = document.getElementById('waldoResetBtn');

  if (!board || !image || !status || !target || !guess) {
    return;
  }

  const waldoX = Number('{{ page.waldo_x | default: 50 }}');
  const waldoY = Number('{{ page.waldo_y | default: 50 }}');
  const tolerance = Number('{{ page.waldo_tolerance | default: 7 }}');

  function placeMarker(marker, xPercent, yPercent) {
    marker.style.left = xPercent + '%';
    marker.style.top = yPercent + '%';
    marker.style.display = 'block';
  }

  function hideMarker(marker) {
    marker.style.display = 'none';
  }

  function updateStatus(text) {
    status.textContent = text;
  }

  function distanceInPercent(x1, y1, x2, y2) {
    const dx = x1 - x2;
    const dy = y1 - y2;
    return Math.sqrt(dx * dx + dy * dy);
  }

  image.addEventListener('click', function (event) {
    const rect = image.getBoundingClientRect();
    const x = ((event.clientX - rect.left) / rect.width) * 100;
    const y = ((event.clientY - rect.top) / rect.height) * 100;

    placeMarker(guess, x, y);

    const missDistance = distanceInPercent(x, y, waldoX, waldoY);
    if (missDistance <= tolerance) {
      placeMarker(target, waldoX, waldoY);
      updateStatus('Nice find! You spotted Waldo.');
    } else {
      updateStatus('Close, but not Waldo yet. Keep looking.');
    }
  });

  revealBtn.addEventListener('click', function () {
    placeMarker(target, waldoX, waldoY);
    updateStatus('Waldo revealed. Click reset to play again.');
  });

  resetBtn.addEventListener('click', function () {
    hideMarker(target);
    hideMarker(guess);
    updateStatus('Board reset. Ready when you are.');
  });
})();
</script>
