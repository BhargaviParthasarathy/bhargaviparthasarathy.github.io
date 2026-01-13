---
layout: page
title: travel
permalink: /travel/
description: Past and upcoming travels
nav: true
nav_order: 5
---

<!-- pages/travel.md -->
<div class="travel-container">
  <!-- Past Travel Section -->
  <section class="travel-section">
    <h2 class="section-title">Past Travel</h2>
    {% if site.data.travel.past_travel %}
      <div class="travel-items">
        {% for item in site.data.travel.past_travel %}
          <div class="travel-card past">
            <div class="travel-header">
              <h3 class="travel-title">{{ item.title }}</h3>
              <span class="travel-type" data-type="{{ item.type }}">{{ item.type }}</span>
            </div>
            <div class="travel-meta">
              <span class="travel-location">
                <i class="fas fa-map-marker-alt"></i> {{ item.location }}
              </span>
              <span class="travel-date">
                <i class="fas fa-calendar-alt"></i> {{ item.date }}
              </span>
            </div>
            <p class="travel-description">{{ item.description }}</p>
            {% if item.highlights %}
              <div class="travel-highlights">
                <strong>Highlights:</strong>
                <ul>
                  {% for highlight in item.highlights %}
                    <li>{{ highlight }}</li>
                  {% endfor %}
                </ul>
              </div>
            {% endif %}
          </div>
        {% endfor %}
      </div>
    {% else %}
      <p class="no-content">No past travel records yet.</p>
    {% endif %}
  </section>

  <!-- Upcoming Travel Section -->
  <section class="travel-section">
    <h2 class="section-title">Upcoming Travel</h2>
    {% if site.data.travel.upcoming_travel %}
      <div class="travel-items">
        {% for item in site.data.travel.upcoming_travel %}
          <div class="travel-card upcoming">
            <div class="travel-header">
              <h3 class="travel-title">{{ item.title }}</h3>
              <span class="travel-type" data-type="{{ item.type }}">{{ item.type }}</span>
            </div>
            <div class="travel-meta">
              <span class="travel-location">
                <i class="fas fa-map-marker-alt"></i> {{ item.location }}
              </span>
              <span class="travel-date">
                <i class="fas fa-calendar-alt"></i> {{ item.date }}
              </span>
            </div>
            <p class="travel-description">{{ item.description }}</p>
            {% if item.highlights %}
              <div class="travel-highlights">
                <strong>Plans:</strong>
                <ul>
                  {% for highlight in item.highlights %}
                    <li>{{ highlight }}</li>
                  {% endfor %}
                </ul>
              </div>
            {% endif %}
          </div>
        {% endfor %}
      </div>
    {% else %}
      <p class="no-content">No upcoming travel plans yet.</p>
    {% endif %}
  </section>
</div>

<style>
  .travel-container {
    max-width: 900px;
    margin: 2rem auto;
  }

  .travel-section {
    margin-bottom: 3rem;
  }

  .section-title {
    font-size: 1.8rem;
    font-weight: 600;
    color: var(--text-color);
    border-bottom: 2px solid var(--accent-color);
    padding-bottom: 1rem;
    margin-bottom: 2rem;
  }

  .travel-items {
    display: grid;
    gap: 1.5rem;
  }

  .travel-card {
    padding: 1.5rem;
    border-radius: 8px;
    border-left: 4px solid var(--accent-color);
    background-color: var(--card-background);
    transition: all 0.3s ease;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
  }

  .travel-card:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transform: translateY(-2px);
  }

  .travel-card.past {
    border-left-color: #888;
  }

  .travel-card.upcoming {
    border-left-color: var(--accent-color);
    background-color: var(--light-accent-background);
  }

  .travel-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.8rem;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .travel-title {
    font-size: 1.3rem;
    font-weight: 600;
    margin: 0;
    color: var(--text-color);
  }

  .travel-type {
    display: inline-block;
    padding: 0.3rem 0.8rem;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    background-color: var(--accent-color);
    color: white;
  }

  .travel-type[data-type="conference"] {
    background-color: #3498db;
  }

  .travel-type[data-type="research"] {
    background-color: #9b59b6;
  }

  .travel-type[data-type="personal"] {
    background-color: #27ae60;
  }

  .travel-meta {
    display: flex;
    gap: 1.5rem;
    margin-bottom: 1rem;
    flex-wrap: wrap;
    font-size: 0.9rem;
    color: var(--muted-text);
  }

  .travel-location,
  .travel-date {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .travel-description {
    margin-bottom: 1rem;
    color: var(--text-color);
    line-height: 1.6;
  }

  .travel-highlights {
    margin-top: 1rem;
    padding-top: 1rem;
    border-top: 1px solid var(--border-color);
  }

  .travel-highlights strong {
    display: block;
    margin-bottom: 0.5rem;
    color: var(--text-color);
  }

  .travel-highlights ul {
    margin: 0;
    padding-left: 1.5rem;
  }

  .travel-highlights li {
    margin-bottom: 0.3rem;
    color: var(--text-color);
  }

  .no-content {
    text-align: center;
    color: var(--muted-text);
    font-style: italic;
    padding: 2rem;
  }

  @media (max-width: 640px) {
    .travel-header {
      flex-direction: column;
      align-items: flex-start;
    }

    .travel-meta {
      flex-direction: column;
      gap: 0.5rem;
    }

    .section-title {
      font-size: 1.5rem;
    }

    .travel-title {
      font-size: 1.1rem;
    }
  }
</style>
