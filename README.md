# TripSync
Adaptive group travel planner that auto-replans your itinerary when things change mid-trip. Built for Codenection 2026.


# TripSync by Obsidian

- **Team members:** Pavithiran, Krishnaraj, Rakesh
- **Problem Statement:** Lifestyle Track - Planning an Escape (Travel Planner)
- **Video Presentation:** [Unlisted YouTube Link]
- **Presentation Slides:** [Public Link]

---

## 1. Project Overview

### The Problem

Planning a trip means juggling flights, accommodation, budgets, activities, and everyone's individual preferences - usually scattered across five different apps and a group chat. Most existing travel apps solve only one piece of this: they handle bookings, or budgeting, or itineraries, but not all three together. Group trips make it worse, since aligning schedules, budgets, and preferences across multiple people is genuinely difficult by hand. And when something changes mid-trip - a delayed flight, bad weather, a closed venue - existing platforms offer little real help adjusting the plan.

**Stakeholders:** young adults and university students traveling in groups, who typically have limited planning experience, mismatched budgets, and shared logistics (transport, accommodation) that need to stay coordinated.

**Existing solutions and where they fall short:** apps like Wanderlog and TripIt handle itinerary organization well, but treat the itinerary as a static document - once a flight is delayed or a venue is closed, the user is left to manually rebuild the plan themselves. None of the major travel-planning apps offer real-time, automatic replanning that accounts for group preferences, budget, and travel time simultaneously.

### Our Solution

**TripSync** is an adaptive group travel planner that doesn't just help you build an itinerary - it keeps that itinerary alive when reality changes. Travelers each set their own budget and interests, TripSync merges them into a single AI-generated itinerary, and when something disrupts the plan mid-trip, TripSync automatically recalculates the affected schedule while preserving group preferences and budget constraints.

**Feature set:**
- Group preference sync - combine multiple travelers' budgets and interests into one plan
- AI-generated itinerary - day-by-day plan matched to combined group preferences and budget
- Budget dashboard - per-category spend tracking and per-person cost split
- Disruption detection - simulate real-world changes (flight delay, weather, closures)
- Auto-replanning engine - recalculates the itinerary transparently, showing what was removed, moved, or added

---

## 2. Ideation & Process

### 2.1 Ideas We Considered

| Idea | Why it was dropped / kept |
|---|---|
| **TripSync - adaptive group travel planner (Chosen)** | Directly targets the problem statement's explicit gap: "when something changes mid-trip, there's rarely any real help... in adjusting." Differentiates from every existing itinerary app by treating the plan as living, not static. |
| **Group-aware travel planner** | Kept and refined further - solved for combining multiple travelers' preferences and budgets into one itinerary, but didn't yet address the mid-trip disruption gap named in the problem statement. |
| Generic AI itinerary generator | Dropped - "tell us your destination and budget, AI generates an itinerary" is one of the most common hackathon travel concepts; wouldn't differentiate from existing submissions or existing apps. |
| Beating the Burnout (stress & workload manager) | Dropped - while a strong problem fit, it risked reading as "CareSync AI 2.0 with a student-workload skin," reusing the same wellbeing-tracker-plus-AI-summary pattern as a prior project. Chose to demonstrate range instead. |

### 2.2 Ideation Boards

<p align="center">
  <img src="ideation-04-idea-exploration.svg" alt="Idea exploration funnel" width="650" />
</p>
<p><em>Shows the narrowing path from the Lifestyle track down to TripSync, including the two intermediate ideas that were dropped along the way and why.</em></p>

<p align="center">
  <img src="ideation-01-problem-tree.svg" alt="Problem tree" width="650" />
</p>
<p><em>Breaks down why group travel planning is hard - three root causes (budgets, tastes, sudden changes) and the consequences each one creates.</em></p>

<p align="center">
  <img src="ideation-02-solution-mindmap.svg" alt="Solution mindmap" width="650" />
</p>
<p><em>TripSync's five functional pillars: group sync, budget, maps, AI itinerary generation, and disruption handling.</em></p>

<p align="center">
  <img src="ideation-03-user-flow.svg" alt="User flow" width="650" />
</p>
<p><em>The end-to-end loop a traveler moves through: plan the trip, get an AI itinerary, travel, hit a disruption, and get an automatic replan.</em></p>

### 2.3 Mentor Consultation

| Date | Mentor | Feedback Received | What Was Changed |
|---|---|---|---|
| [ ] | [ ] | [ ] | [ ] |

*To be completed after mentor session(s) during the hackathon.*

---

## 3. Design & Prototype

**UI Prototype:** [Public Figma Link]

Key screens (see full spec for all 9):

| Screen | Interaction |
|---|---|
| Trip setup | Enter destination, dates, budget, and number of travelers |
| Group preferences | Each traveler picks interest tags; TripSync shows the combined group overlap |
| AI-generated itinerary | Day-by-day plan with a "why this plan" match explanation (budget fit, preference match, travel time) |
| Trip dashboard | Shared hub view - budget progress, day-by-day load, links to itinerary/budget/group |
| Disruption alert | Simulated flight delay; single clear "Replan my trip" action |
| Replanned itinerary | Transparent breakdown of what was removed, moved, and added, with updated arrival time and budget impact |

---

## 4. What Makes It Different

- **Auto-replanning, not just itinerary generation.** The core twist: TripSync treats a disruption (flight delay, weather, venue closure) as a trigger for automatic, transparent replanning - showing exactly what changed and why, rather than asking the user to manually rebuild the plan.
- **Group preference merging, made visible.** Rather than one person picking for the group, TripSync visually shows each traveler's individual interests being combined into a single "group match" score on the itinerary.
- **Own scoring logic, not just an AI black box.** Budget fit, travel-time efficiency, and preference matching are computed with explicit logic; the AI layer is used for itinerary generation and plain-language explanation, not for decisions that need to be defensible (budget, timing).

---

## 5. Technical Architecture & Feasibility

### Tech stack

| Layer | Choice | Why | Constraints |
|---|---|---|---|
| Frontend | Flutter | Prior experience (CareSync AI); single codebase for mobile | - |
| Backend/data | Firebase / Firestore | Free tier sufficient for demo; already used in a prior project | Quota limits under heavy testing |
| AI layer | Gemini (via Vertex AI) | Reused pattern from CareSync AI's daily-summary feature | Free-tier model access needs provisioning ahead of time |
| Disruption trigger | Mocked (manual "simulate disruption" action) | Avoids dependency on a live flight-status API for the demo | Not a real integration - explicitly scoped as a simulation |
| Maps/places (stretch) | Google Places / Routes API | Only if time allows after core loop is built | Requires API key setup and quota awareness |

### Build plan & scope

**In scope for the hackathon:**
- Trip setup, group preference input, AI-generated itinerary
- Budget dashboard
- Simulated disruption trigger and auto-replan flow with transparent change breakdown

**Explicitly out of scope:**
- Real flight-status or booking integrations
- Live multi-user accounts with real-time sync (simulated with mock traveler profiles instead)
- Payment processing

Keeping the disruption trigger mocked and the map/routing APIs as stretch goals keeps the core "plan → disrupt → replan" loop achievable solo within the hackathon timeframe.
