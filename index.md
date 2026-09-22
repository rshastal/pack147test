
---
layout: default
navbarText: Grosse Pointe Park, MI
title: Cub Scout Pack 147
---

<!-- HERO -->
<section class="relative overflow-hidden">
  <div class="absolute inset-0">
    <img src="{{ '/assets/images/hiking-together.jpg' | relative_url }}"
         alt="Cub Scouts hiking together"
         class="object-cover w-full h-full"
         fetchpriority="high" decoding="async">
    <div class="absolute inset-0 bg-gradient-to-r from-slate-950/80 via-slate-900/55 to-slate-900/25"></div>
  </div>

  <div class="relative max-w-6xl px-4 py-24 mx-auto sm:py-32 lg:py-36">
    <div class="max-w-3xl text-white">
      <p class="mb-3 text-sm font-bold tracking-[0.22em] uppercase text-cub-gold">
        Cub Scout Pack 147 · Grosse Pointe Park
      </p>
      <h1 class="m-0 text-5xl font-extrabold tracking-tight text-white sm:text-6xl lg:text-7xl">
        Adventure Begins Here
      </h1>
      <p class="max-w-2xl mt-5 text-xl leading-relaxed text-white/90">
        A place for kids to explore, build confidence, make friends, and discover what they can do.
      </p>
      <div class="flex flex-wrap gap-3 mt-8">
        <a href="{{ '/join/' | relative_url }}"
           class="inline-flex items-center justify-center px-6 py-3 font-bold transition rounded-xl bg-cub-gold text-cub-blue hover:bg-yellow-300">
          Join Pack 147
        </a>
        <a href="{{ '/calendar/' | relative_url }}"
           class="inline-flex items-center justify-center px-6 py-3 font-bold text-white transition border rounded-xl border-white/40 bg-white/10 hover:bg-white/20">
          Upcoming Events
        </a>
      </div>
    </div>
  </div>
</section>

<!-- YEAR AT A GLANCE -->
<!-- YEAR AT A GLANCE -->
<!-- YEAR AT A GLANCE -->
<section class="px-4 py-14 bg-slate-50 sm:px-6 sm:py-16 lg:px-8">
  <div class="max-w-6xl mx-auto overflow-hidden shadow-sm rounded-3xl bg-cub-blue">
    <div class="grid items-center gap-10 px-6 py-10 sm:px-10 sm:py-14 lg:grid-cols-[1.1fr_1fr] lg:gap-14 lg:px-14">

      <!-- Program Overview Preview -->
      <div class="order-2 lg:order-1">
        <div class="relative max-w-[95%] mx-auto py-5">
          <a href="{{ '/assets/docs/pack147-2026-2027-year-at-a-glance.pdf' | relative_url }}"
             target="_blank"
             rel="noopener"
             class="block overflow-hidden transition bg-white rounded-xl shadow-2xl hover:scale-[1.01]">

            <img
              src="{{ '/assets/images/pack147-year-at-a-glance.png' | relative_url }}"
              alt="Pack 147 2026–27 Year at a Glance"
              class="block w-full h-auto"
              loading="lazy">

          </a>
        </div>
      </div>

      <!-- Copy -->
      <div class="order-1 lg:order-2">
        <p class="mb-3 text-sm font-bold tracking-[0.22em] uppercase text-white/70">
          The year ahead
        </p>

        <h2 class="m-0 text-4xl font-extrabold tracking-[0.05em] uppercase text-cub-gold sm:text-5xl">
          2026–27 at a glance
        </h2>

        <p class="max-w-xl mt-5 text-lg leading-relaxed text-blue-50">
          From Pack and Den meetings to campouts, Pinewood Derby, Blue &amp; Gold,
          outdoor adventures and more, see what's ahead for Pack 147 this year.
        </p>

        <a href="{{ '/assets/docs/pack147-2026-2027-year-at-a-glance.pdf' | relative_url }}"
           target="_blank"
           rel="noopener"
           class="inline-flex items-center justify-center px-6 py-3 mt-7 font-bold transition rounded-xl bg-cub-gold text-cub-blue hover:bg-yellow-300">
          View the Program Overview
        </a>

        <p class="mt-3 mb-0 text-sm text-blue-100/80">
          Click the preview or button to view the full-size schedule.
        </p>
      </div>

    </div>
  </div>
</section>

<!-- EVENTS -->
{%- assign now_epoch = site.time | date: "%s" -%}
{%- assign upcoming = '' | split: '' -%}
{%- for p in site.pages -%}
  {%- if p.url and p.url contains '/events/' and p.event -%}
    {%- assign ev_iso = p.event.start.dateTime | default: p.event.start.date -%}
    {%- if ev_iso -%}
      {%- assign ev_epoch = ev_iso | date: "%s" -%}
      {%- if ev_epoch >= now_epoch -%}
        {%- assign upcoming = upcoming | push: p -%}
      {%- endif -%}
    {%- endif -%}
  {%- endif -%}
{%- endfor -%}
{%- assign upcoming = upcoming | sort: 'event.sort_key' -%}

<section class="bg-white">
  <div class="max-w-6xl px-4 py-16 mx-auto sm:py-20">
    <div class="flex flex-col gap-3 sm:flex-row sm:items-end sm:justify-between">
      <div>
        <p class="mb-2 text-sm font-bold tracking-[0.2em] uppercase text-cub-blue/60">Pack 147 calendar</p>
        <h2 class="m-0 text-4xl font-extrabold text-cub-blue">Coming Up</h2>
      </div>
      <a href="{{ '/calendar/' | relative_url }}" class="font-bold text-cub-blue hover:underline">
        Full Calendar →
      </a>
    </div>

    {% if upcoming.size > 0 %}
      <div class="grid gap-5 mt-8 md:grid-cols-2 lg:grid-cols-3">
        {% for p in upcoming limit: 6 %}
          {%- assign ev_iso = p.event.start.dateTime | default: p.event.start.date -%}
          {%- assign end_iso = p.event.end.dateTime | default: p.event.end.date -%}
          {%- assign ev_day = ev_iso | date: "%Y-%m-%d" -%}
          {%- assign end_day = end_iso | date: "%Y-%m-%d" -%}

          <article class="flex flex-col p-6 transition bg-slate-50 rounded-2xl ring-1 ring-slate-200 hover:shadow-md">
            <p class="m-0 text-sm font-bold tracking-wide uppercase text-cub-blue/60">
              {{ ev_iso | date: "%a • %b %-d" }}
              {%- if end_iso and end_day != ev_day -%}
                – {{ end_iso | date: "%a • %b %-d" }}
              {%- endif -%}
            </p>

            <h3 class="mt-3 mb-0 text-xl font-bold text-slate-900">
              <a href="{{ p.url | relative_url }}" class="hover:underline">
                {{ p.title | default: "Pack Event" }}
              </a>
            </h3>

            {%- assign loc = p.event.location | default: p.location | default: p.venue -%}
            {% if loc and p.layout contains "public" %}
              <p class="mt-3 mb-0 text-sm text-slate-600">{{ loc }}</p>
            {% endif %}

            {% if p.event.start.dateTime and end_iso and end_day == ev_day %}
              <p class="mt-2 mb-0 text-sm text-slate-500">
                {{ p.event.start.dateTime | date: "%-I:%M %p" }}
                {% if p.event.end and p.event.end.dateTime %}
                  – {{ p.event.end.dateTime | date: "%-I:%M %p" }}
                {% endif %}
              </p>
            {% endif %}

            <div class="mt-auto pt-5">
              <a href="{{ p.url | relative_url }}" class="font-bold text-cub-blue hover:underline">
                Event Details →
              </a>
            </div>
          </article>
        {% endfor %}
      </div>
    {% else %}
      <div class="p-8 mt-8 text-center rounded-2xl bg-slate-50 ring-1 ring-slate-200">
        <h3 class="m-0 text-xl font-bold text-slate-900">See what's coming up with Pack 147.</h3>
        <p class="mt-2 mb-5 text-slate-600">Pack meetings, den activities, service projects and special events are on our calendar.</p>
        <a href="{{ '/calendar/' | relative_url }}"
           class="inline-flex items-center justify-center px-5 py-3 font-bold text-white transition rounded-xl bg-cub-blue hover:opacity-90">
          Open Pack Calendar
        </a>
      </div>
    {% endif %}
  </div>
</section>

<!-- WHY CUB SCOUTING -->
<section class="bg-slate-50">
  <div class="grid items-center max-w-6xl gap-12 px-4 py-16 mx-auto lg:grid-cols-2 sm:py-20">
    <div>
      <p class="mb-2 text-sm font-bold tracking-[0.2em] uppercase text-cub-blue/60">More than meetings</p>
      <h2 class="m-0 text-4xl font-extrabold text-cub-blue">Why Cub Scouting?</h2>
      <p class="mt-5 text-lg leading-8 text-slate-700">
        Scouting America welcomes families to discover outdoor adventure, community, and character. In Pack 147, kids build confidence and leadership through hands-on experiences — and have a lot of fun doing it.
      </p>

      <div class="grid gap-3 mt-7 sm:grid-cols-2">
        <div class="p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <p class="m-0 font-bold">🌲 Outdoor Adventure</p>
          <p class="mt-1 mb-0 text-sm text-slate-600">Hikes, campouts and outdoor skills.</p>
        </div>
        <div class="p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <p class="m-0 font-bold">🧪 STEM & Creativity</p>
          <p class="mt-1 mb-0 text-sm text-slate-600">Build, experiment and discover.</p>
        </div>
        <div class="p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <p class="m-0 font-bold">🤝 Friendship & Service</p>
          <p class="mt-1 mb-0 text-sm text-slate-600">Work together and help the community.</p>
        </div>
        <div class="p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <p class="m-0 font-bold">✨ A Place to Belong</p>
          <p class="mt-1 mb-0 text-sm text-slate-600">New families can jump in and get involved.</p>
        </div>
      </div>

      <a href="{{ '/about/' | relative_url }}"
         class="inline-flex items-center justify-center px-5 py-3 mt-7 font-bold text-white transition rounded-xl bg-cub-blue hover:opacity-90">
        Learn About Pack 147
      </a>
    </div>

    <div class="grid grid-cols-2 gap-4">
      <img src="{{ '/assets/images/crafting.jpg' | relative_url }}" alt="Parent and child working on a craft"
           class="object-cover w-full h-48 shadow-sm rounded-2xl sm:h-56" loading="lazy" decoding="async">
      <img src="{{ '/assets/images/cleanup.jpg' | relative_url }}" alt="Pack members at a community cleanup"
           class="object-cover w-full h-48 mt-6 shadow-sm rounded-2xl sm:h-56" loading="lazy" decoding="async">
      <img src="{{ '/assets/images/smores.jpg' | relative_url }}" alt="S'mores at a Scout activity"
           class="object-cover w-full h-48 -mt-6 shadow-sm rounded-2xl sm:h-56" loading="lazy" decoding="async">
      <img src="{{ '/assets/images/goo.jpg' | relative_url }}" alt="Scouts doing a science activity"
           class="object-cover w-full h-48 shadow-sm rounded-2xl sm:h-56" loading="lazy" decoding="async">
    </div>
  </div>
</section>

<!-- WHAT WE DO -->
<section class="bg-white">
  <div class="max-w-6xl px-4 py-16 mx-auto sm:py-20">
    <div class="max-w-3xl mx-auto text-center">
      <p class="mb-2 text-sm font-bold tracking-[0.2em] uppercase text-cub-blue/60">A year full of adventure</p>
      <h2 class="m-0 text-4xl font-extrabold text-cub-blue">What We Do</h2>
      <p class="mt-4 text-lg text-slate-600">A look at some of the experiences Pack 147 families share throughout the year.</p>
    </div>

    <div class="grid gap-6 mt-10 sm:grid-cols-2 lg:grid-cols-4">
      <article class="overflow-hidden transition bg-white shadow-sm rounded-2xl ring-1 ring-slate-200 hover:shadow-md">
        <img src="{{ '/assets/images/hiking-with-adults.jpg' | relative_url }}" alt="Scouts and adults hiking outdoors"
             class="object-cover w-full h-44" loading="lazy" decoding="async">
        <div class="p-5">
          <h3 class="m-0 text-lg font-bold">Outdoor Skills</h3>
          <p class="mt-2 mb-0 text-sm leading-6 text-slate-600">Hikes, campouts, nature study and leave-no-trace basics.</p>
        </div>
      </article>

      <article class="overflow-hidden transition bg-white shadow-sm rounded-2xl ring-1 ring-slate-200 hover:shadow-md">
        <img src="{{ '/assets/images/pinewood.jpg' | relative_url }}" alt="Pinewood Derby activity"
             class="object-cover w-full h-44" loading="lazy" decoding="async">
        <div class="p-5">
          <h3 class="m-0 text-lg font-bold">STEM & Creativity</h3>
          <p class="mt-2 mb-0 text-sm leading-6 text-slate-600">From Pinewood Derby cars to hands-on projects, Scouts design, build and discover.</p>
        </div>
      </article>

      <article class="overflow-hidden transition bg-white shadow-sm rounded-2xl ring-1 ring-slate-200 hover:shadow-md">
        <img src="{{ '/assets/images/food-drive.jpg' | relative_url }}" alt="Pack community service"
             class="object-cover w-full h-44" loading="lazy" decoding="async">
        <div class="p-5">
          <h3 class="m-0 text-lg font-bold">Community Service</h3>
          <p class="mt-2 mb-0 text-sm leading-6 text-slate-600">Service days and projects that teach Scouts how they can make a difference.</p>
        </div>
      </article>

      <article class="overflow-hidden transition bg-white shadow-sm rounded-2xl ring-1 ring-slate-200 hover:shadow-md">
        <img src="{{ '/assets/images/ball-game.jpg' | relative_url }}" alt="Pack families having fun together"
             class="object-cover w-full h-44" loading="lazy" decoding="async">
        <div class="p-5">
          <h3 class="m-0 text-lg font-bold">Fun & Friendship</h3>
          <p class="mt-2 mb-0 text-sm leading-6 text-slate-600">Games, campfires and traditions that bring Scouts and families together.</p>
        </div>
      </article>
    </div>
  </div>
</section>

<!-- LEADERS + DEN FINDER -->
<section class="bg-slate-50">
  <div class="grid max-w-6xl gap-12 px-4 py-16 mx-auto lg:grid-cols-2 sm:py-20">

    <!-- LEADERS -->
    <div markdown="1">
      {% include leaders.md %}
    </div>

    <!-- DEN FINDER -->
    <div>
      <p class="mb-2 text-sm font-bold tracking-[0.2em] uppercase text-cub-blue/60">
        Kindergarten through fifth grade
      </p>

      <h2 class="m-0 text-4xl font-extrabold text-cub-blue">
        Find Your Den
      </h2>

      <p class="mt-4 text-slate-600">
        Meetings are organized by grade so Scouts grow through the program with kids their age. New families are welcome.
      </p>

      <div class="grid gap-3 mt-7">

        <div class="flex items-center justify-between p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <div>
            <p class="m-0 font-bold">Lions</p>
            <p class="mt-1 mb-0 text-sm text-slate-500">Kindergarten</p>
          </div>
          <p class="m-0 text-sm font-semibold text-cub-blue">Wednesdays</p>
        </div>

        <div class="flex items-center justify-between p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <div>
            <p class="m-0 font-bold">Tigers</p>
            <p class="mt-1 mb-0 text-sm text-slate-500">1st Grade</p>
          </div>
          <p class="m-0 text-sm font-semibold text-cub-blue">Wednesdays</p>
        </div>

        <div class="flex items-center justify-between p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <div>
            <p class="m-0 font-bold">Wolves</p>
            <p class="mt-1 mb-0 text-sm text-slate-500">2nd Grade</p>
          </div>
          <p class="m-0 text-sm font-semibold text-cub-blue">Wednesdays</p>
        </div>

        <div class="flex items-center justify-between p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <div>
            <p class="m-0 font-bold">Bears</p>
            <p class="mt-1 mb-0 text-sm text-slate-500">3rd Grade</p>
          </div>
          <p class="m-0 text-sm font-semibold text-cub-blue">Wednesdays</p>
        </div>

        <div class="flex items-center justify-between p-4 bg-white rounded-xl ring-1 ring-slate-200">
          <div>
            <p class="m-0 font-bold">Webelos &amp; Arrow of Light</p>
            <p class="mt-1 mb-0 text-sm text-slate-500">4th–5th Grade</p>
          </div>
          <p class="m-0 text-sm font-semibold text-cub-blue">Wednesdays</p>
        </div>

      </div>

      <div class="flex flex-wrap items-center gap-4 mt-7">
        <a href="https://docs.google.com/forms/d/e/1FAIpQLSeOEj-jI40fscwo9memaMbL9ConldTthiJvY-vEp3hdWp7MAQ/viewform"
           target="_blank"
           rel="noopener"
           class="inline-flex items-center justify-center px-5 py-3 font-bold text-white transition rounded-xl bg-cub-blue hover:opacity-90">
          Ask a Question
        </a>

        <a href="mailto:gppack147@gmail.com"
           class="font-bold text-cub-blue hover:underline">
          gppack147@gmail.com
        </a>
      </div>

    </div>
  </div>
</section>

<section class="bg-cub-gold">
<div class="grid items-center max-w-6xl gap-8 px-4 py-14 mx-auto lg:grid-cols-[1fr_auto] sm:py-16">
<div>
<p class="mb-2 text-sm font-bold tracking-[0.2em] uppercase text-cub-blue/70">Come see what it's like</p>
<h2 class="m-0 text-4xl font-extrabold text-cub-blue">Ready to Explore?</h2>
<p class="max-w-2xl mt-4 mb-0 text-lg text-cub-blue/80">
New to Scouting? We'll help your family find the right den and get started.
</p>
</div>

<a href="{{ '/join/' | relative_url }}"
class="inline-flex items-center justify-center px-7 py-4 font-extrabold text-white transition rounded-xl bg-cub-blue hover:opacity-90">
Join Pack 147
</a>
</div>
</section>
