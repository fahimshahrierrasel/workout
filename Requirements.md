# Product Requirements Document (PRD) & Project Brief: APEX Split

**Project Name:** APEX Split — 7-Day Workout Information & Protocol Viewer  
**Document Version:** 1.0  
**Status:** Approved for Implementation  
**Target Platforms:** Responsive Web (Desktop & Mobile First)  
**Primary Design System:** APEX Split Dark Theme (`Space Grotesk`, `#CCFF00` High-Voltage Lime Accent, Obsidian Slate surfaces)

---

## 1. Executive Summary & Vision

### 1.1 Product Mission
**APEX Split** is an informational, zero-friction workout reference application designed to provide lifters and athletes with instant access to their structured 7-day training schedule without the cognitive load or friction of set/rep logging, timer countdowns, or completion tracking.

### 1.2 Core Philosophy: "Zero Tracking, Instant Instruction"
Most modern fitness applications burden users with input-heavy logging flows (entering weights, tick boxes, rest timers, progression math). APEX Split operates strictly as an **authoritative digital field manual**:
- Open the app → automatically view today's specific routine.
- Need form clarification? → 1-tap direct access to validated YouTube execution tutorials.
- Need absence management? → Clear, non-guilt resumption playbook.

---

## 2. Target Audience & User Personas

### 2.1 Persona: The Structured Lifter ("Alex")
- **Profile:** Intermediate lifter who already knows their working weights or tracks them elsewhere, but wants a fast, clean workout reference on their phone or laptop.
- **Pain Point:** Frustrated by bloated apps that force them to log every set or nag them with notifications while at the gym.
- **Goal:** Glance at the exercise order, target rep schemes, intensity cues, and watch a 30-second form reminder when needed.

---

## 3. Product Goals & Success Metrics

### 3.1 Key Objectives
1. **Zero-Friction Access:** Time to view today's workout on load must be < 1 second.
2. **Context-Aware Presentation:** Automatically detect local client day-of-week and switch to the active workout tab.
3. **Execution Clarity:** Provide direct video form lookup for 100% of programmed movements.
4. **Resilience & Habit Preservation:** Provide actionable guidance when gym consistency is disrupted (3–5 day absences).

### 3.2 Non-Goals (Explicit Exclusions)
- ❌ No set/weight/RPE logging forms.
- ❌ No exercise completion checkmarks or scratchpads.
- ❌ No active countdown rest timers or stopwatch popups.
- ❌ No user accounts or authentication walls required for core reference utility.

---

## 4. Information Architecture & Content Specifications

### 4.1 7-Day Training Split Matrix (Monday Start)

| Day | Routine | Focus Group | Exercises / Focus Points |
| :--- | :--- | :--- | :--- |
| **Day 1 (Mon)** | **PUSH** | Chest, Shoulders, Triceps | 1. Seated Machine Chest Press (3–4 × 8–12)<br>2. Incline DB Press (3–4 × 8–12)<br>3. Shoulder Press (3–4 × 8–12)<br>4. DB Lateral Raises (3–4 × 12–15)<br>5. Triceps Pushdown (3–4 × 10–12)<br>6. Triceps Dips (3 × 8–12) |
| **Day 2 (Tue)** | **PULL** | Back, Rear Shoulders, Biceps | 1. Lat Pulldown (3–4 × 8–12)<br>2. Seated Cable Row (3–4 × 8–12)<br>3. Chest-Supported Row (3 × 8–12)<br>4. Face Pulls (3 × 12–15)<br>5. DB Biceps Curl (3 × 10–12)<br>6. Hammer Curl (3 × 10–12) |
| **Day 3 (Wed)** | **LEGS & ABS** | Quads, Hamstrings, Glutes, Calves, Core | 1. Goblet Squat (3–4 × 8–12)<br>2. Leg Press (3–4 × 10–12)<br>3. Lying Leg Curl (3 × 10–12)<br>4. Calf Raises (3–4 × 12–15)<br>5. Plank (3 × 30–60 sec)<br>6. Hanging Knee Raises (3 × 10–15) |
| **Day 4 (Thu)** | **REST & RECOVERY** | Systemic Recovery | • Sleep Optimization (7–9 hrs)<br>• Hydration & Electrolytes<br>• Protein & Nutrient Timing<br>• Light Movement / Walking |
| **Day 5 (Fri)** | **CHEST, BACK & ARMS** | Upper-Body Strength | 1. Bench Press (3 × 8–12)<br>2. Cable Fly (3 × 10–15)<br>3. Lat Pulldown (3 × 8–12)<br>4. Seated Cable Row (3 × 8–12)<br>5. Biceps Curl (3 × 10–12)<br>6. Triceps Extension (3 × 10–12) |
| **Day 6 (Sat)** | **SHOULDERS & LEGS** | Deltoids & Lower Body | 1. Shoulder Press (3 × 8–12)<br>2. DB Lateral Raises (3 × 12–15)<br>3. Reverse Pec Deck Fly (3 × 12–15)<br>4. Leg Extension (3 × 10–12)<br>5. Leg Curl (3 × 10–12)<br>6. Calf Raises (3 × 12–15) |
| **Day 7 (Sun)** | **REST & RECOVERY** | Cycle Reset | • Neurological De-load<br>• Nutritious Meals<br>• Optional Active Walking<br>• Preparation for Next Microcycle |

---

## 5. Functional Feature Requirements

### 5.1 Day Selector & Automated Scheduling Engine
- **Requirement 5.1.1 (Client Time Detection):** On DOM mount, inspect the user's local day via `new Date().getDay()`.
  - Sunday (0) → Select Day 7
  - Monday (1) → Select Day 1
  - Tuesday (2) → Select Day 2 ... through Saturday (6) → Select Day 6
- **Requirement 5.1.2 (Visual Badging):** Render a high-contrast `TODAY` pill/chip on the tab corresponding to the current calendar day.
- **Requirement 5.1.3 (Interactive Switching):** Allow manual switching across all 7 days with seamless tab transition without full page reloads.

### 5.2 Exercise Detail Presentation
- **Requirement 5.2.1 (Index & Structure):** Display numerical sequencing (`01` through `06`), exact movement name, set × rep target schema, and biomechanical execution cue (e.g., *RPE 8.5*, *Full Stretch*, *Controlled Eccentric*).
- **Requirement 5.2.2 (YouTube Form Integration):**
  - Every exercise card/row features an accessible button with the YouTube brand emblem and direct link.
  - Links open a URL of format: `https://www.youtube.com/results?search_query=how+to+do+[Exercise+Name]+proper+form` in `target="_blank"` with `rel="noopener noreferrer"`.
  - Mobile targets must maintain a minimum touch target area of 48×48px.

### 5.3 Contingency Protocol: "Missed Gym Protocol (3–5 Days)"
- **Core Principle:** Highlight the Golden Rule: *"Don't restart the entire plan or try to make up missed workouts. Resume from where you left off."*
- **Absence Duration Table:**
  - **1–2 Days:** Continue with next scheduled workout.
  - **3–5 Days:** Resume next workout in split at normal load (attenuate slightly if fatigued).
  - **6–10 Days:** Return at 80–90% load and slightly reduced volume.
  - **>10–14 Days:** Gradual ramp-up with lighter weights and fewer sets.
- **Practical Field Scenario:** Concrete walkthrough of missing 4 days after Day 2 (Pull), demonstrating sequential continuation to Day 3 (Legs & Abs).

### 5.4 Standard Training Guidelines & Coach Notes
- Provide 6 foundational principles: Warm-up protocol, Rest intervals (60–120s), Weight selection criteria, Progressive overload definition, Consistency over guilt, and Training frequency flexibility.
- Include personalization disclaimer reminding users to calibrate volume to personal recovery capability.

---

## 6. UI/UX & Responsive Layout Specifications

### 6.1 Desktop Layout (`DESKTOP` Screen Artifact)
- **Header:** Sticky/fixed top bar with APEX brand emblem, navigation anchors (*Overview*, *Daily Schedule*, *Missed Gym Guide*, *Guidelines*), and live day status indicator.
- **Schedule Viewer:** Horizontal 7-column day selector cards above a structured, tabular exercise matrix.
- **Reference Sections:** Full-width analytical tables and high-legibility multi-column guideline cards.

### 6.2 Mobile Layout (`MOBILE` Screen Artifact)
- **Header:** Compact top app bar with day indicator and athlete profile icon.
- **Touch Selector:** Horizontal scrollable/swipable day tabs with large active state contrasts.
- **Card-Stack Architecture:** Vertical stacked exercise tiles with prominent index pills and right-aligned red YouTube action triggers.
- **Collapsible Drawers:** Collapsible accordion modules for *Missed Gym Protocol* and *General Guidelines* to eliminate screen clutter and minimize scrolling during active gym sessions.

---

## 7. Design System & Tech Stack Reference

- **Color Tokens:**
  - Base Dark: `#0c0e11` (Deep Obsidian)
  - Card/Container Surface: `#111317` & `#1a1c1f`
  - Accent / Brand Highlight: `#ccff00` (Electric Lime)
  - Action / Video Guide: `#ff0000` / `#dc2626` (YouTube Red)
  - Text Primary: `#ffffff`
  - Text Secondary: `#9ca3af` / `#6b7280`
- **Typography:** Space Grotesk / Tabular Numerals for set & rep precision.
- **Delivery Artifacts on Canvas:**
  - Desktop Implementation: `{{DATA:SCREEN:SCREEN_4}}`
  - Mobile Implementation: `{{DATA:SCREEN:SCREEN_2}}`
  - Canonical Master Split: `{{DATA:SCREEN:SCREEN_6}}`
  - Design Tokens & System: `{{DATA:DESIGN_SYSTEM:DESIGN_SYSTEM_1}}`

---

## 8. Rollout & Maintenance Considerations

- **Cross-Browser Date Compatibility:** Validate client timezone handling for `Date.getDay()` across iOS Safari, Android Chrome, and Desktop Web.
- **PWA & Offline Capability (Recommended Next Phase):** Enable service worker caching so lifters in basements or gym dead zones have 100% offline access to the workout tables.
- **Deep-linking:** Optional hash parameters (e.g., `#day-push`, `#day-pull`) to allow saving specific bookmarks directly to the phone home screen.