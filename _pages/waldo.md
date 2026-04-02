---
layout: page
title: where's waldo
permalink: /waldo/
nav: false
---

{% assign conference_photos = site.static_files
	| where_exp: "f", "f.path contains '/assets/img/Conference Photos/'"
	| where_exp: "f", "f.extname == '.jpg' or f.extname == '.jpeg'"
	| sort: "name"
	| reverse %}

<p>Some places I have been to, some people I have met.</p>

{% if conference_photos.size > 0 %}
	<div class="conference-gallery" role="list" aria-label="Conference photos">
		{% for photo in conference_photos %}
			{% assign photo_url = photo.path | relative_url | replace: ' ', '%20' %}
			{% assign file_label = photo.basename | replace: '-', ' ' | replace: '_', ' ' %}
			<figure class="conference-card" role="listitem">
				<img src="{{ photo_url }}" alt="{{ file_label }}" loading="lazy" />
				<figcaption>{{ file_label }}</figcaption>
			</figure>
		{% endfor %}
	</div>
{% else %}
	<p>No conference photos found yet in <strong>/assets/img/Conference Photos/</strong>.</p>
{% endif %}

<style>
.conference-gallery {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
	gap: 1rem;
	margin-top: 1rem;
}

.conference-card {
	margin: 0;
	border: 1px solid #ddd;
	border-radius: 10px;
	overflow: hidden;
	background: #fff;
}

.conference-card img {
	width: 100%;
	height: 240px;
	object-fit: cover;
	display: block;
}

.conference-card figcaption {
	font-size: 0.95rem;
	padding: 0.6rem 0.75rem;
	border-top: 1px solid #eee;
}
</style>
