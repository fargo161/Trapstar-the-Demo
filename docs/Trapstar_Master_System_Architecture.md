# Trapstar Master System Architecture

**File:** `docs/Trapstar_Master_System_Architecture.md`  
**Project:** *Trapstar the Demo*  
**Purpose:** Master high-level system, resolution-flow, and technical-boundary reference  
**Status:** Architecture overview / living design truth / Phaser portability and contained-complexity pass  

---

## 1. Purpose of This Document

This document defines the high-level system architecture for *Trapstar the Demo*.

It is not a full Game Design Document and it is not a numeric implementation spec. Instead, it explains how the major systems fit together so future markdown files, GitHub commits, Codex work, the Phaser 3.90 demo implementation, and later production-engine migration can remain aligned.

The goal is to establish the shared design truth behind:

- The larger *Trapstar* game vision
- The bounded *Trapstar the Demo* scenario
- SEN loop philosophy
- BASED Vibes as action language
- Deal / Pressure / Ask as the universal action frame
- Hard / Soft information state
- The six Social Assets
- The six Hard Assets
- TIME COST as the universal action cost layer
- Energy, survival pressure, and combat-as-alert-state
- Game world map structure
- Demo engine / presentation direction
- Simulation-versus-presentation boundary
- Independent system responsibilities and explicit resolver glue
- Controlled action and consequence order
- Commands as authoritative changes and events as reports of completed changes
- Portability rules for data, IDs, save state, randomness, assets, and action resolution
- Run-card generation
- Future demo limits and win/save/lose conditions

Each major system and subsystem may later receive its own focused markdown with specific metrics, values, tables, and implementation rules.

---

## 2. Production Pipeline Role

This file is designed to support the working design and implementation loop:

```text
Chat / Nova
  -> GitHub Markdown Source of Truth
    -> Codex Planning + Code Generation
      -> Phaser 3.90 Demo Implementation
        -> Browser Build / Playtest
          -> Bug / Design Feedback
            -> Chat / Nova Review
              -> Updated GitHub Markdown
```

In this pipeline:

- **Chat / Nova** is used to reason through design, compare markdowns, simplify systems, and prepare repo-ready revisions.
- **GitHub** stores accepted markdown as the current design source of truth.
- **Codex** reads the repo markdowns and converts stable design into tasks, implementation plans, TypeScript data structures, tests, and code changes.
- **Phaser 3.90** is where the seven-week demo becomes playable and testable as a browser-based 2D game.
- **Browser builds and playtests** return bugs, screenshots, logs, unclear rules, balancing problems, and design feedback back into Chat / Nova for review.
- **Updated markdown** closes the loop by recording what changed, what became stable, and what still needs a dedicated reference file.
- **Action-resolution boundaries** ensure Codex implements interactions through small systems and explicit coordinators rather than burying all consequences inside scenes, sprites, NPC classes, or one universal manager.

Phaser 3.90 is the committed implementation target for the seven-week demo. It is not assumed to be the guaranteed engine for the full production project. The demo should therefore become a playable proof, behavioral reference, and migration specification whose core data and rules can survive a later engine change.

This master architecture file should be treated as the first high-level document to read before implementing detailed systems. It explains how the systems fit together, but focused subsystem markdowns should control exact numeric values, formulas, tables, and implementation rules when those files exist.

---

## 3. Source-of-Truth Status Tags

This document uses a few status concepts to separate stable architecture from unfinished implementation detail.

| Status | Meaning | Codex / Implementation Use |
|---|---|---|
| **Architecture Truth** | Accepted high-level design direction. | Safe to use for planning, naming, structure, and system relationships. |
| **Working Scenario** | Accepted demo premise or current playable target. | Safe to use when framing tasks, scenes, run setup, and test cases. |
| **Placeholder** | Present so the architecture has a clear slot for the system. | Do not invent exact formulas, thresholds, or full mechanics from this alone. |
| **Future Detail** | Requires its own focused markdown before detailed implementation. | Wait for or create the dedicated reference file before building deep logic. |
| **Implementation Target** | Stable enough to prototype at a high level, but still subject to refinement. | Safe for Codex and Phaser prototype planning when numeric details are not required. |

For now, this file uses these status concepts as a legend only. Later, major sections may receive explicit status labels when the repo needs stricter Codex guidance.

Pipeline rule:

```text
Do not treat a placeholder as a finished mechanic.
Do not invent missing numbers from this master file.
Use this file to understand structure, relationships, names, and design intent.
Use focused subsystem files for specific implementation metrics.
Keep portable simulation rules separate from Phaser-specific presentation code.
Keep each core system independently understandable and assign it one clear responsibility.
Use explicit action resolvers to coordinate cross-system consequences.
Do not hide authoritative state changes inside uncontrolled event chains.
Do not serialize or store direct Phaser objects as game-state truth.
```

---

## 4. Quick Architecture Summary

| Layer | Purpose |
|---|---|
| **Trapstar the Game** | Full social crime sim vision using SEN in a reactive urban environment. |
| **Trapstar the Demo** | Three-day stolen Contra shipment proof-of-concept with bounded variation. |
| **SEN** | Design philosophy: Structured, Emergent, Negotiated. |
| **BASED** | Action language built from five traits and 20 Vibes. |
| **Vibes** | Ordered two-trait action tones used to shape approach and future abilities. |
| **Deal / Pressure / Ask** | Universal player choice frame: the player chooses Deal, Pressure, or Ask as a strategic approach to the current situation. DPA symbolically maps to SEN but is not an ordered loop. |
| **Soft / Hard Info** | Information state: rumor or lead versus receipt, proof, or verified fact. |
| **Info Cards** | Standard unit for storing social and information state. |
| **Social Assets** | HEAT, REP, FAC, FAVOR, ACCESS, and LORE. |
| **Hard Assets** | Money, Contra, Weapons, Sustenance, Time, and Energy. |
| **TIME COST** | Placeholder for minute-cost rules attached to actions. |
| **Energy / Hunger / Tiredness** | Placeholder for survival pressure and combat health. |
| **Combat** | Alert/crisis state the player usually wants to resolve or exit quickly. |
| **Game World Map** | One-block, three-street, node-connected playable space. |
| **Portable Simulation Layer** | Engine-independent world state, run state, rules, action resolution, and consequences. |
| **Independent Systems** | Small rule owners for Info, REP, HEAT, TIME, inventory, missions, schedules, combat, and other bounded responsibilities. |
| **Explicit Resolver Glue** | Specialized coordinators that combine relevant systems for one action without making those systems directly control one another. |
| **Controlled Consequence Order** | A visible sequence from player intent through validation, state transition, secondary consequences, and presentation. |
| **Commands / Events Rule** | Commands request or apply authoritative world changes; events report completed changes to presentation and observers. |
| **Demo Engine / Presentation** | Phaser 3.90 browser-based 2D street presentation with direct movement and point-click/menu-based UI. |
| **Portability Rules** | Stable boundaries for data, IDs, save state, seeded randomness, assets, and action resolution. |
| **Run-Card Generator** | Starting truth generator for NPCs, factions, hidden info, resources, and run variables. |

This table is a reading guide. The sections below explain each layer in more detail without replacing future subsystem references.

---

## 5. Trapstar the Game

*Trapstar* is the larger game vision behind the demo.

At full scale, *Trapstar* is a **social crime simulation** set inside a reactive urban environment. The game is not built around traditional loot grinding or endless combat progression. It is built around social consequence, street-level pressure, resource scarcity, faction tension, police attention, and the player's ability to survive through negotiation.

The larger game uses the **SEN design philosophy** to make events feel lifelike without requiring an unlimited simulation.

```text
Structured rules create readable pressure.
Emergent reactions create believable change.
Negotiated choices let the player push, trade, survive, expose, or escape.
```

In the full game vision, the world should feel alive because people and factions react to what is known, what is proven, what is owed, what is feared, what is valuable, and what is risky.

The intended experience is:

- A compact but reactive social-crime environment.
- NPCs who respond to social assets, hard assets, pressure, and evidence.
- Factions with visible and hidden strengths, weaknesses, relationships, and vulnerabilities.
- Police pressure that turns careless movement, public violence, and dirty inventory into real danger.
- A player loop based on reading the block, choosing an approach, spending limited resources, and living with consequences.
- Simple stylized graphics that make the world readable rather than visually overloaded.
- Lore, faction identity, character roles, and Info Cards that pull the simulation together into a coherent setting.

The full *Trapstar* vision should eventually support larger scope, deeper systems, more locations, more NPC relationships, more faction dynamics, and more long-term consequences.

This master architecture file does not attempt to define that full game in detail. It uses the larger game vision as the design target that the demo is proving in bounded form.

---

## 6. Trapstar the Demo

*Trapstar the Demo* is the bounded proof-of-concept for the larger *Trapstar* design.

The demo narrows the full social crime sim into a focused run scenario:

```text
A Contra shipment has been stolen.
The player has three in-game days to find out what happened and resolve the situation.
```

The demo should prove that SEN-driven play can work inside a small, manageable scope.

Instead of simulating an entire city, the demo focuses on:

- One block.
- Three node-connected streets.
- A limited NPC roster.
- Two primary factions.
- Police-monitored pressure.
- A three-day time limit.
- A stolen Contra shipment as the central conflict.
- A narrowed set of Social Assets and Hard Assets.
- A run-card generator that changes starting roles, values, hidden information, and faction conditions.

The player is not simply solving a static mystery. Each run can begin with different starting truths.

The Run-Card Generator may change:

- Which NPC is guilty.
- Which NPC is lying.
- Which NPC is telling the truth.
- Which NPCs are monitored.
- Which faction has more strength.
- Which faction is under more pressure.
- Which Info Cards are soft rumors.
- Which receipts can harden those rumors into proof.
- Which routes, favors, access points, and risks exist at the start.

This creates replayability through **bounded variation**, not uncontrolled randomness.

The demo constraints are a feature, not a weakness. The narrowed scope makes the SEN loop testable:

```text
Read the block.
Find soft info.
Turn soft info into hard info.
Use BASED Vibes through the Deal / Pressure / Ask choice frame.
Spend Time.
Manage Energy.
Avoid or exploit HEAT.
Navigate faction REP, FAC strength, FAVOR, ACCESS, and LORE.
Resolve the stolen Contra shipment before the run collapses.
```

The demo should show that a small number of NPCs, factions, assets, and locations can still create dynamic play when their roles, starting values, relationships, and hidden information shift at the start of each run.

This master file defines the architecture that keeps the demo focused while preserving the larger design direction.

---

## 7. Core Design Stack

*Trapstar the Demo* is built as a bounded socioeconomic negotiation loop.

At the top level, the game is not about grinding combat or collecting loot. It is about reading a dangerous block, choosing how to approach people, managing limited resources, and negotiating through social, legal, physical, and time pressure.

```text
Run-Card Generator
  -> Starting World / NPC / Faction / Resource State
    -> SEN Philosophy
      -> Deal / Pressure / Ask Action Frame
        -> BASED Action Language
          -> Info Cards and Social Assets
            -> Hard Assets and Player State
              -> TIME COST and Consequence
                -> Updated World / NPC / Faction State
                  -> Next Negotiation Situation
```

The player is constantly asking:

```text
What do I know?
Who knows what?
Who can I trust, threaten, pay, avoid, or expose?
What will this cost in time, energy, money, reputation, or police attention?
```

Core relationship:

```text
SEN creates the situation.
DPA chooses the strategic frame.
BASED colors the manner of action.
A specialized resolver coordinates the relevant systems.
Each system calculates only its own responsibility.
A controlled state transition applies the combined result.
Time and secondary consequences make the choice costly.
The world updates.
```

### 7.1 Technical Architecture Stack

The gameplay architecture above should be implemented through a separate technical flow:

```text
Content Definitions
  -> Run-Card Generator
    -> Portable Runtime State
      -> Player Action Request
        -> Specialized Action Resolver
          -> Independent Rule Systems
            -> Ordered State Transition
              -> Secondary Consequence Processing
                -> Resolved Outcome
                  -> Presentation Adapter
                    -> Phaser Scene / Sprite / UI Feedback
                      -> Next Player Input
```

The presentation layer may request an action and display the result, but the portable simulation layer determines what the action means and how the game state changes.

### 7.2 Simulation-versus-Presentation Boundary

The architecture is divided into two major responsibilities.

**Portable Simulation Layer**

- Run generation and run seed handling
- Player, NPC, faction, location, inventory, and world state
- NPC truth, belief, knowledge, relationship, and objective state
- SEN situation progression
- Deal / Pressure / Ask requests and resolution
- BASED Vibe modifiers and future abilities
- Info Cards, Social Assets, and Hard Assets
- TIME COST, Energy, hunger, tiredness, and survival rules
- HEAT, police pressure, faction pressure, and consequence logic
- Win, loss, run-resolution, and save-state logic

**Phaser Presentation Layer**

- Phaser scenes and scene transitions
- Asset loading
- Sprites, layered character visuals, and animation playback
- Player input and pointer interaction
- Street movement, collision, and interaction zones
- Camera behavior and Y-depth sorting
- Dialogue panels, HUD, menus, and Info Card display
- Audio presentation
- Browser build and deployment

Governing rule:

```text
The Phaser layer sends player intentions to the simulation and displays resolved outcomes.
It does not own the rules that determine those outcomes.
Animations, dialogue panels, HUD changes, audio, and camera effects communicate consequences;
they do not independently create authoritative gameplay truth.
```

### 7.3 Contained Complexity: Independent Systems and Explicit Glue

The architecture should not attempt to eliminate all complexity. It should contain complexity inside clear boundaries.

Each core system should be independently understandable, testable, and responsible for one bounded category of rule.

Examples:

- **Info System** owns discovery, possession, truth state, disclosure, and information transfer.
- **Relationship System** owns personal, block, and faction REP calculations.
- **HEAT System** owns legal attention, monitoring, detention risk, and police-pressure consequences.
- **TIME System** owns action-minute costs, time advancement, and time-triggered checks.
- **Inventory System** owns Money, Contra, Weapons, Sustenance, and item transfers.
- **Mission System** owns stolen-shipment role truth, objectives, win conditions, and failure conditions.
- **Schedule System** owns where NPCs should be as in-game time changes.
- **Combat System** owns combat-state legality, damage, retreat, and crisis resolution.

These systems should not directly command one another. For example:

```text
The BASED System does not raise HEAT.
The HEAT System does not reveal Info Cards.
The Info System does not spend Time.
The TIME System does not play animations.
A Phaser NPC sprite does not directly change REP.
```

Cross-system actions should be coordinated by small, explicit pieces of project-specific glue.

Likely coordinators include:

```text
InteractionResolver
StreetActionResolver
CombatResolver
TravelResolver
EndOfDayResolver
RunSetupResolver
```

A resolver may know which systems must participate in a particular action. The underlying systems should not need intimate knowledge of one another.

The architecture must avoid a universal `TrapstarManager` that owns NPCs, dialogue, inventory, combat, TIME, HEAT, REP, factions, animation, missions, and save state at once. Session-level objects may hold references and coordinate lifecycle, but they must not absorb every rule.

Governing principle:

```text
Trapstar should not eliminate complexity.
It should contain complexity inside small systems, explicit coordinators,
portable state transitions, and a controlled order of consequence.
```

### 7.4 DPA, BASED, and Resolver Responsibility

DPA and BASED define player intent, but they do not own every system affected by that intent.

```text
DPA = which strategic frame the player chooses.
BASED = how the player expresses that approach.
Resolver = which rule systems participate and in what order.
Systems = how each bounded consequence is calculated.
State transition = what becomes authoritatively true.
Presentation = how the result is shown to the player.
```

A Pressure request may include the actor, target, selected BASED Vibe, demand, visible leverage, location, and witnesses. The `InteractionResolver` may then request calculations from BASED, Info, REP, HEAT, TIME, inventory, faction, and mission rules. No single participating system should own the entire interaction.

### 7.5 Controlled Action and Consequence Order

Every meaningful action should move through an understandable sequence.

```text
1. Receive player intent.
2. Validate the requested action against current state.
3. Lock or suspend conflicting input where necessary.
4. Gather the systems and context required for resolution.
5. Calculate the primary outcome using controlled randomness where relevant.
6. Apply one authoritative state transition.
7. Advance in-game TIME and process ordered secondary consequences.
8. Check schedules, HEAT thresholds, mission conditions, win/loss, and other triggered rules.
9. Produce a resolved-outcome record and presentation instructions.
10. Display the result through Phaser and restore player control.
```

This order may be refined in a dedicated implementation file, but critical consequences must not occur in an accidental order determined by scene update timing or listener registration.

Real-time Phaser clocks, animation duration, and frame updates are separate from the in-world TIME economy. A dialogue animation taking two real seconds does not determine whether the action costs eight in-game minutes.

### 7.6 Commands, Outcomes, and Events

The project may use events, including Phaser event emitters, but events must not become the only hidden explanation for critical game-state changes.

Governing rule:

```text
Commands change the world.
Events report what changed.
```

A command or action request asks the simulation to perform an authoritative operation. The resolver validates it, calculates it, and applies the resulting state transition. Afterward, events may notify presentation, audio, UI, analytics, logs, or other observers.

Preferred pattern:

```text
Pressure command
-> InteractionResolver
-> authoritative state transition
-> Outcome: HEAT increased, Info disclosed, REP changed, 12 minutes spent
-> events notify HUD, dialogue, audio, camera, and animation systems
```

Avoid this pattern:

```text
Pressure button emits an event
-> an unknown listener changes REP
-> another listener reveals Info
-> another listener spends Time
-> Time emits another event
-> another listener raises HEAT
-> another listener begins police occupation
```

Events may be used for presentation reactions and non-authoritative notifications. Critical rules should remain traceable through direct resolver calls, explicit outcomes, and ordered state transitions.

### 7.7 Definitions, Runtime State, Rules, and Presentation

Trapstar data should remain divided into four understandable categories:

| Category | Meaning |
|---|---|
| **Content Definitions** | Relatively stable design data describing NPCs, factions, items, locations, Info Cards, actions, Vibes, dialogue, animation metadata, and balancing values. |
| **Runtime State** | Mutable truth for the current run, including time, location, inventory, relationships, HEAT, known information, mission roles, conditions, and world flags. |
| **Rule Systems and Resolvers** | Code that validates actions, calculates consequences, and transforms current state into updated state. |
| **Presentation Objects** | Phaser scenes, sprites, animations, cameras, UI, audio, and effects that display state and collect player input. |

Definitions describe what things are. Runtime state describes what is currently true. Rule systems determine how truth may change. Presentation objects show those truths without becoming their authoritative owner.

---

## 8. SEN Philosophy

**SEN** means:

```text
Structured
Emergent
Negotiated
```

SEN is the underlying design philosophy that powers the whole demo.

### 8.1 Structured

The game world is bounded by visible and invisible structure:

- Limited map
- Limited time window
- Limited NPC cast
- Limited factions
- Limited resources
- Trackable hard assets
- Trackable social assets
- Clear action frames
- Defined consequences

Structure prevents the demo from becoming an unbounded simulation.

### 8.2 Emergent

Inside the structure, situations can change based on:

- NPC reactions
- Faction relationships
- Info discovery
- Soft information hardening into receipts
- HEAT escalation
- REP shifts
- Resource loss or gain
- Time passing
- Player choices during Ask / Deal / Pressure

Emergence gives the demo replayability and social texture without requiring infinite simulation.

### 8.3 Negotiated

The player does not simply choose from combat, stealth, or dialogue as separate game modes. Most meaningful actions are negotiated through context.

Negotiation happens through:

- What the player knows
- What the NPC believes
- What each side wants
- What each side can prove
- What each side can risk
- What assets are available
- Which BASED Vibe shapes the approach
- Whether the player Asks, Deals, or Pressures

SEN intersects with hard design most clearly through the universal action frame, but the frame is not itself a sequence.

```text
The world presents a structured situation.
Emergent pressure changes what is risky, urgent, or unstable.
The player negotiates the next move by choosing Deal, Pressure, or Ask.
The result updates assets, info, Vibe effects, risk, and consequence.
The changed situation becomes the next SEN state.
```

DPA is the choice the player makes inside the SEN loop.

### 8.4 SEN Loop and DPA Choice Frame

SEN and DPA are connected, but they are not the same kind of structure.

**SEN** is the design philosophy and world-state loop:

```text
Structured situation
-> Emergent reaction
-> Negotiated consequence
-> Updated situation
```

**Deal / Pressure / Ask** is the player-facing strategic choice frame.

DPA is not an ordered loop. The player does not cycle through Deal, then Pressure, then Ask. Instead, whenever the player faces a meaningful situation, the player chooses one of three strategic approaches:

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social choice
```

Every situation contains some mix of hard reality, dynamic pressure, and negotiated possibility. DPA lets the player decide which part of that situation to act through.

---

## 9. BASED as Action Language

**BASED** is the main action-language framework for *Trapstar the Demo*.

For the current architecture, BASED should be understood as **how a character acts**, not as a full personality simulation.

BASED is made of five traits:

```text
B = Belligerence
A = Aggression
S = Sociability
E = Empathy
D = Deception
```

A **Vibe** is an ordered two-trait pairing.

The first trait leads. The second trait modifies the expression.

Example:

```text
AB = Aggression leading into Belligerence
BA = Belligerence leading into Aggression
```

These are not the same.

All 20 Vibes are available in the demo as action language. Later ability files may define which Vibes have Street abilities, Dialogue abilities, or Both-use abilities.

---

## 10. BASED Vibe Matrix

Rows show the leading trait. Columns show the secondary trait. Self-pairs are excluded.

| Lead / Secondary | B | A | S | E | D |
|---|---|---|---|---|---|
| **B — Belligerence** | — | **BA: Reckless** | **BS: Instigating** | **BE: Condemning** | **BD: Extortive** |
| **A — Aggression** | **AB: Menacing** | — | **AS: Commanding** | **AE: Urgent** | **AD: Hustled** |
| **S — Sociability** | **SB: Irreverent** | **SA: Charismatic** | — | **SE: Compassionate** | **SD: Coaxing** |
| **E — Empathy** | **EB: Steadfast** | **EA: Boundaried** | **ES: Communal** | — | **ED: Deflecting** |
| **D — Deception** | **DB: Bluffing** | **DA: Predatory** | **DS: Insinuating** | **DE: Feigning** | — |

### Quick Vibe List

```text
BA = Reckless
BS = Instigating
BE = Condemning
BD = Extortive

AB = Menacing
AS = Commanding
AE = Urgent
AD = Hustled

SB = Irreverent
SA = Charismatic
SE = Compassionate
SD = Coaxing

EB = Steadfast
EA = Boundaried
ES = Communal
ED = Deflecting

DB = Bluffing
DA = Predatory
DS = Insinuating
DE = Feigning
```

---

## 11. Vibe Abilities Placeholder

Vibes are available as action language now.

Later, each Vibe may receive specific ability definitions.

Future ability categories:

| Ability Category | Meaning |
|---|---|
| **Street** | Used in movement, confrontation, combat-adjacent, public-space, or physical-world situations. |
| **Dialogue** | Used in conversation, interrogation, persuasion, deception, bargaining, or emotional leverage. |
| **Both** | Can function in both street and dialogue contexts. |

This master file does not define those abilities yet.

Future file:

```text
Trapstar_BASED_Ability_Reference.md
```

---

## 12. Universal Action Frame: Deal / Pressure / Ask

*Trapstar the Demo* uses one universal player choice frame:

```text
Deal
Pressure
Ask
```

Deal / Pressure / Ask is the player's recurring strategic choice at meaningful decision points.

It is not an ordered loop. The player does not have to Deal before applying Pressure, and the player does not have to apply Pressure before Asking. Instead, the player chooses whichever frame best fits the current situation, available information, social risk, hard assets, and desired outcome.

DPA symbolically maps to SEN:

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social choice
```

DPA defines the strategic request. BASED defines the manner of acting. Neither should directly own Info, REP, HEAT, TIME, inventory, mission, or presentation logic. A specialized resolver coordinates whichever systems the current action requires and returns one resolved outcome.

The same choice frame can operate in dialogue, street encounters, faction interactions, resource exchanges, investigation, combat-adjacent moments, and crisis states.

The order below follows the name of the frame, not a required gameplay sequence.

---

### 12.1 Deal

**Deal** is the Logos / Structured choice.

Deal means the player tries to move the situation through hard reality: exchange, proof, cost, debt, obligation, possession, trade, payment, or concrete risk.

Deal asks:

```text
What exists?
What is owed?
What can be paid?
What can be traded?
What can be proven?
What will this cost?
```

A Deal can involve:

- Money
- Contra
- Weapons
- Sustenance
- Information
- Favor
- Access
- Protection
- Silence
- Time
- Risk

Deal is the main exchange path. It can create opportunity, but it can also expose the player to HEAT, betrayal, bad prices, setup risk, or faction consequence.

---

### 12.2 Pressure

**Pressure** is the Pathos / Emergent choice.

Pressure means the player tries to move the situation by changing its emotional, social, or tactical force.

Pressure acts through fear, urgency, intimidation, exposure, shame, leverage, anger, panic, retaliation risk, or escalation.

Pressure asks:

```text
What is unstable?
Who is afraid?
Who can be pushed?
What can be exposed?
What will escalate?
Who will crack, fold, resist, or strike back?
```

Pressure can pursue:

- Confession
- Compliance
- Hidden information
- Faction secrets
- HEAT information
- Debt collection
- Access
- Retreat
- Silence
- Combat avoidance

Pressure is powerful but risky. It can raise HEAT, damage REP, trigger combat, harden resistance, or create future retaliation.

---

### 12.3 Ask

**Ask** is the Ethos / Negotiated choice.

Ask means the player tries to move the situation by creating a social opening: inquiry, appeal, request, patience, permission, trust, recognition, or relationship repair.

Ask asks:

```text
What can be requested?
Who might listen?
What can be admitted safely?
What can be opened without force?
What relationship, reputation, or context makes this possible?
```

Ask can pursue:

- Soft information
- Clarification
- Permission
- Warning
- Introduction
- Help
- Favor
- Access
- Relationship repair

Ask is usually the safest action path, but it may be limited by low REP, bad timing, secrecy, fear, faction pressure, or lack of leverage.

---

## 13. Information State: Soft Info and Hard Info

All information in the game can exist as either **Soft Info** or **Hard Info**.

This is separate from Hard Assets.

### 13.1 Soft Info

Soft Info is unconfirmed knowledge.

Examples:

- Rumor
- Claim
- Suspicion
- Lead
- Social read
- Tip
- Unverified story
- Emotional read
- Social impression

Soft Info can open possibilities, guide questions, create suspicion, or support light negotiation.

### 13.2 Hard Info

Hard Info is confirmed or provable knowledge.

Examples:

- Receipt
- Proof
- Witnessed event
- Confession
- Verified fact
- Confirmed access
- Physical evidence
- Recorded or documented claim

Hard Info can change permissions, prove accusations, force concessions, support stronger Pressure, unlock access, shift faction belief, or survive denial.

### 13.3 Key Rule

```text
Soft Info opens possibilities.
Hard Info changes what people will risk, believe, allow, or deny.
```

---

## 14. Info Cards

An **Info Card** is the standard unit for storing information in the demo.

Info Cards can represent what people know, believe, suspect, can prove, owe, permit, fear, hide, trade, or socially recognize.

Info Cards are used to carry the six Social Assets:

```text
HEAT
REP
FAC
FAVOR
ACCESS
LORE
```

Each Info Card should eventually identify:

```text
Asset Type
Scope
Subject
Visibility
State
Value
Summary
Meaning
Possible Uses
State Changes / Notes
```

All Info Card Values use a **1-5 scale**.

The 1-5 value range is shared for consistency, but each Social Asset defines that range differently. A **HEAT 5**, **REP 5**, **FAC 5**, **FAVOR 5**, **ACCESS 5**, and **LORE 5** do not mean the same thing. Their exact meanings will be defined later in each Social Asset's dedicated reference file.

---

## 15. The Six Social Assets

The six Social Assets are information-based assets that shape what characters and factions know, believe, permit, owe, fear, control, or can prove.

They are called Social Assets because they exist through relationships, knowledge, status, leverage, permission, or belief.

```text
HEAT
REP
FAC
FAVOR
ACCESS
LORE
```

Each Social Asset should receive its own detailed markdown later.

---

### 15.1 HEAT

**HEAT** represents police attention, suspicion, surveillance, enforcement pressure, or legal danger.

HEAT can attach to:

- Player
- NPC
- Block area
- Faction
- Location
- Event
- Deal
- Crime

HEAT answers:

```text
Who or what is being watched, suspected, exposed, or vulnerable to police action?
```

Future file:

```text
Trapstar_HEAT_System_Demo_Scope.md
```

---

### 15.2 REP

**REP** represents social standing and relationship quality.

REP can describe trust, fear, respect, dislike, shame, credibility, loyalty, contempt, or social weight.

REP has scope levels, including:

- Personal / NPC
- Block-wide
- Factional

REP answers:

```text
How does this person, block, group, or faction relate to the subject?
```

REP can describe:

- NPC relationship to player
- Player relationship to NPC
- Block-wide view of a subject
- One faction's relationship to another faction
- A faction's relationship to the player

Future file:

```text
Trapstar_REP_System_Demo_Scope.md
```

---

### 15.3 FAC

**FAC** represents one particular faction's elements, capacity, and world strength.

FAC does not mean general reputation by itself. REP and FAC are separate Social Assets.

FAC concerns a particular faction's:

- Members
- Size
- Hard assets
- Internal structure
- NPC member dynamics
- Organizational strong points
- Organizational weak points
- Access power
- Info power
- World strength
- Reputation strength as one element of that faction

FAC answers:

```text
What does this faction have, control, know, lack, protect, expose, or rely on?
```

Future file:

```text
Trapstar_FAC_System_Demo_Scope.md
```

---

### 15.4 FAVOR

**FAVOR** represents social or information-based debt.

FAVOR can exist between:

- Player and NPC
- NPC and NPC
- Player and faction
- Faction and faction
- NPC and faction

FAVOR may be soft or hard depending on whether the debt is informal, rumored, promised, witnessed, or explicitly confirmed.

FAVOR answers:

```text
Who owes whom, how strongly, and under what social conditions?
```

Future file:

```text
Trapstar_FAVOR_System_Demo_Scope.md
```

---

### 15.5 ACCESS

**ACCESS** represents reach, permission, influence, availability, entry, contact, or usable connection.

ACCESS can involve:

- Physical entry
- Social permission
- Faction tolerance
- Contra availability
- Info receipt availability
- Introduction routes
- Safe paths
- Backrooms
- Doors
- Stashes
- Brokers
- Protected spaces

ACCESS answers:

```text
Who can reach what, enter where, contact whom, obtain which resource, or move through which route?
```

Future file:

```text
Trapstar_ACCESS_System_Demo_Scope.md
```

---

### 15.6 LORE

**LORE** represents known, suspected, remembered, or discoverable facts about people, places, factions, routines, motives, history, and relationships.

LORE can be:

- Personal
- Block-wide
- Factional

LORE often feeds other Social Assets.

LORE answers:

```text
What is known, believed, suspected, remembered, or discoverable about the world?
```

Future file:

```text
Trapstar_LORE_System_Demo_Scope.md
```

---

## 16. The Six Hard Assets

Hard Assets are trackable resources with direct material, survival, legal, or action value.

Hard Assets are separate from Hard Info.

```text
Hard Info = confirmed information.
Hard Assets = trackable resources and values.
```

The six Hard Assets are:

```text
Money
Contra
Weapons
Sustenance
Time
Energy
```

Each Hard Asset should eventually receive detailed numeric rules.

---

### 16.1 Money

**Money** is cash currency.

Money can be used for:

- Deals
- Purchases
- Fines
- Bribes
- Sustenance
- Access
- Favor repayment
- Emergency solutions

Money answers:

```text
What can the player pay, lose, demand, save, or risk carrying?
```

---

### 16.2 Contra

**Contra** represents illicit substances and illegal trade goods.

Contra can be valuable, but it creates legal and social risk.

Contra can connect to:

- Deals
- Faction strength
- Police searches
- Dirty status
- HEAT escalation
- Access to certain NPCs
- Risky money flow

Contra answers:

```text
What illegal value is being carried, sold, hidden, traded, or exposed?
```

---

### 16.3 Weapons

**Weapons** are physical tools of threat, violence, defense, or leverage.

Weapons may be:

```text
Hot
Clean
```

A weapon's status affects its legal and social risk.

Weapons can connect to:

- Combat
- Pressure
- Police searches
- Dirty or Suspect status
- REP
- HEAT
- Faction conflict

Weapons answer:

```text
What force can be used, shown, hidden, confiscated, traced, or feared?
```

---

### 16.4 Sustenance

**Sustenance** supports player energy maintenance.

Sustenance can include food, drink, or other survival-maintenance items.

Sustenance connects to:

- Hunger
- Energy
- Time pressure
- Money
- Route planning
- Survival decisions

Sustenance answers:

```text
What can the player consume to keep going?
```

---

### 16.5 Time

**Time** is a Hard Asset because the player tracks it as a concrete value with real cost.

Time is measured in minutes.

Time connects to:

- Every meaningful action
- Hunger
- Tiredness
- Energy pressure
- Missed opportunities
- Deal timing
- Police exposure
- Investigation pacing
- Combat risk
- Run structure

Time answers:

```text
How much of the run is this action worth?
```

---

### 16.6 Energy

**Energy** is a Hard Asset and a player-state survival value.

Energy represents the player's ability to keep acting, endure stress, survive combat, and continue the run.

Energy connects to:

- Hunger
- Tiredness
- Sustenance
- Rest
- Combat health
- Action availability
- Permadeath

If the player reaches 0 Energy, the run ends in permadeath.

Energy answers:

```text
How much longer can the player physically keep going?
```

---

## 17. TIME COST Placeholder

TIME COST is the action-cost layer that will be fleshed out later.

Even though Time is one of the six Hard Assets, TIME COST deserves its own implementation section because it governs how actions consume minutes.

Actions that may cost minutes include:

- Asking questions
- Making Deals
- Applying Pressure
- Moving between spaces
- Searching
- Waiting
- Resting
- Eating or drinking
- Checking inventory
- Major combat moves
- Socially taxing events
- High-risk exchanges
- Escaping danger

Spending minutes can increase hunger and tiredness pressure.

Future file:

```text
Trapstar_TIME_Cost_System.md
```

---

## 18. Energy, Hunger, and Tiredness Placeholder

Energy is the player's functional survival value and combat health meter.

Hunger and tiredness pressure the player over time.

As the player spends minutes, hunger and tiredness can rise, which can limit available choices until the player consumes sustenance or rests.

Current high-level rule:

```text
Spend minutes -> hunger/tiredness pressure rises -> energy becomes harder to maintain -> choices narrow -> risk increases
```

If Energy reaches 0:

```text
Permadeath occurs.
The run ends.
```

Future file:

```text
Trapstar_Energy_Hunger_Tiredness_System.md
```

---

## 19. Combat Placeholder

Combat exists in *Trapstar the Demo*, but it is not the main grind loop.

Combat should be treated as an alert or crisis state.

Combat means:

```text
Something has escalated.
The player is exposed.
Energy is at risk.
Time is being spent.
HEAT may rise.
REP may change.
The player should resolve, escape, or end the confrontation quickly.
```

Combat may involve weapons, Vibes, Pressure, movement, retreat, and major action costs.

Combat should not become the primary reward loop for farming loot or experience.

Future file:

```text
Trapstar_Combat_Alert_State_Reference.md
```

---

## 20. Game World Map Placeholder

The game world is a bounded playable block.

For the current architecture, the block should be understood as:

```text
One block
Three node-connected streets
Multiple node exits
Interior and passage nodes
Hidden alley and shortcut nodes
```

The map is not meant to be an open city. It is a compact, readable socioeconomic space where people, routes, buildings, hidden paths, faction territory, police pressure, and resource access can collide.

The three streets should function as connected lanes or zones that support:

- Player movement
- NPC placement
- Police presence
- Faction pressure
- Public encounters
- Building exits
- Passage exits
- Hidden alley movement
- ACCESS-based traversal
- Deal / Pressure / Ask opportunities

Node exits can lead to:

- Buildings
- Rooms
- Backrooms
- Passages
- Hidden alleys
- Faction spaces
- Stashes
- Safe or risky shortcuts
- Investigation locations

This master file does not define the final map layout yet.

Future file:

```text
Trapstar_Map_World_Traversal_Reference.md
```

---

## 21. Demo Engine, Presentation, and Migration Boundary

### 21.1 Demo Engine Decision

*Trapstar the Demo* will use **Phaser 3.90** as the committed engine for the seven-week prototype.

The demo implementation should use:

```text
Phaser 3.90
TypeScript
Browser-based build
2D beat-em-up-style side/street presentation
WASD player movement
Pointer interaction support
Menu-based UI for choices, actions, inventory, and information
```

Phaser is selected because the demo is fully 2D, system-heavy, data-driven, well suited to TypeScript, compatible with rapid GitHub / Codex iteration, and easy to distribute as a browser build.

This decision applies to the demo. It does not guarantee that Phaser will remain the engine for the full production project. A later move to Phaser 4, Unity, Godot, or another production engine should be treated as a controlled migration based on the needs revealed by the playable demo.

### 21.2 Current Presentation Target

The player should be able to physically navigate the block while the deeper action logic remains menu-readable and system-driven.

The Phaser presentation layer should support:

- Street movement and belt-scroller-style X/Y traversal
- Node exits and interior transitions
- NPC interaction prompts and menus
- Deal / Pressure / Ask selection
- Info Card and inventory viewing
- Time, Energy, HEAT, and other essential HUD state
- Combat or alert-state presentation
- Context-sensitive UI choices
- Layered character sprites and synchronized animation playback
- Camera movement and Y-based visual depth sorting
- Browser deployment for course review and playtesting

### 21.3 Portable Simulation Responsibilities

The following systems must remain independent of Phaser scenes, sprites, cameras, containers, animation objects, and physics bodies:

- Run-Card generation
- Player, NPC, faction, location, and world state
- SEN, DPA, and BASED resolution
- Info Cards and asset values
- Truth, lie, guilt, belief, and knowledge state
- TIME COST and survival-state calculation
- HEAT, REP, FAC, FAVOR, ACCESS, and LORE changes
- Item, inventory, money, Contra, weapon, sustenance, and Energy changes
- Win, loss, run-end, and save-state rules
- Action validation, specialized resolver selection, and ordered consequence processing
- Resolved-outcome records suitable for tests, logs, presentation, and save verification

A Phaser scene may send an action request such as `pressure_npc`, `enter_location`, or `spend_item`, but the simulation layer decides whether that action is valid, which specialized resolver handles it, what each participating system contributes, what it costs, what outcome occurs, and what state changes follow.

The simulation should return an explicit resolved outcome rather than requiring presentation code to infer consequences from scattered state mutations.

### 21.4 Portability Rules

#### Data

Game content should be represented through portable data wherever practical. This includes:

- NPC definitions
- Faction definitions
- Location and node definitions
- Info Cards
- Items and inventory definitions
- Dialogue content
- Action and ability definitions
- Animation metadata
- Run-generation pools
- Balancing values

JSON is suitable for content data. TypeScript interfaces, types, and validation should define the required structures.

#### Stable IDs

Game systems should refer to entities through stable string IDs rather than direct Phaser references.

Examples:

```text
npc_marvin
faction_red
location_center_store
info_stolen_shipment_origin
item_warehouse_receipt
```

Direct references to Phaser sprites, scenes, containers, physics bodies, or animation objects must not become the source of truth for identity or game state.

#### Save State

Save data should contain plain, versioned game state rather than serialized Phaser objects.

A save-state schema may include:

```text
saveVersion
runSeed
currentDay
currentMinute
playerState
npcStates
factionStates
infoCards
inventory
locationStates
worldFlags
```

The save schema should be designed so old saves can be identified, migrated, repaired, or rejected deliberately when the data model changes.

#### Seeded Randomness

The Run-Card Generator should create or accept a reproducible run seed.

Seeded randomness supports:

- Exact bug reproduction
- Repeatable playtests
- Balancing comparisons
- Automated scenario tests
- Migration verification
- Shareable challenge runs if later desired

Random results that affect gameplay truth should come from the controlled run random source rather than scattered calls to uncontrolled randomness.

#### Asset Standards

Visual and audio assets should be standardized outside the engine.

Character and environment standards should define, where relevant:

- File and folder naming
- Frame dimensions
- Animation keys and frame order
- Shared character origins
- Ground anchors and visual pivots
- Layer alignment for body, clothing, hair, accessories, and weapons
- Collision-footprint guidance separate from full sprite bounds
- Modular panel and tile dimensions
- Export scale and transparency requirements

These standards should remain usable if the presentation layer is rebuilt in another engine.

#### Action Resolution

Core action resolution should follow a portable state-transition model wherever practical:

```text
Current State
+ Requested Action
+ Content Definitions
+ Controlled Random Source
-> Validation Result
-> Specialized Resolver
-> Participating System Calculations
-> Ordered State Transition
-> Resolved Outcome
+ Updated State
```

A resolved outcome should be able to identify, where relevant:

```text
success / failure / partial result
primary reason
state changes
asset transfers
Info disclosures
REP / HEAT / FAC / FAVOR / ACCESS / LORE changes
TIME spent
Energy or condition changes
witnesses and visibility
mission or schedule consequences
presentation cues
```

The exact schema belongs in a focused implementation reference, but the outcome should be explicit enough for automated tests, bug logs, save verification, replay debugging, and presentation playback.

This structure allows important systems to be tested without loading a Phaser scene and makes later migration easier to verify.

#### System Dependency Direction

Core systems should expose focused calculations or operations and should not reach sideways into unrelated systems to apply hidden changes.

Preferred dependency direction:

```text
Action Request
-> Resolver
-> Bounded Systems
-> State Transition
-> Outcome
-> Presentation / Notifications
```

Avoid circular system dependencies and avoid using Phaser scenes, sprites, or global event listeners as service locators for simulation rules.

#### Controlled Consequence Processing

Secondary effects caused by a completed state transition must be processed in a documented order. Examples include TIME advancement, hunger/tiredness pressure, NPC schedule movement, police occupation, faction reaction, mission updates, and win/loss checks.

The project may later use a consequence queue or ordered resolver phases, but the order must remain visible, testable, and independent of animation timing.

### 21.5 Permitted Phaser-Specific Code

Portability does not require the project to build a custom engine or avoid useful Phaser features.

Phaser-specific code is expected and permitted for:

- Rendering
- Input
- Movement
- Collision
- Cameras
- Animation playback
- Scenes and scene transitions
- UI presentation
- Audio playback
- Asset loading
- Browser build and deployment
- Event-based UI, audio, animation, and camera reactions after authoritative outcomes are known

Phaser events may report completed changes to presentation systems, but they should not secretly distribute the authoritative logic for TIME, HEAT, REP, Info disclosure, inventory transfer, or mission truth across unrelated listeners.

The project should not attempt to support multiple engines during the seven-week course or abstract every sprite operation behind a universal renderer.

Target principle:

```text
Disposable presentation code.
Reusable design, data, rules, tests, and assets.
```

### 21.6 Future Production Engine

The full project's production engine should be selected after the Phaser demo reveals the real needs of the larger game, including content-authoring requirements, animation complexity, platform targets, performance, tooling, team workflow, and long-term scope.

A future engine migration should aim to replace the presentation and engine-integration layer while preserving the accepted design truth, content data, simulation rules, test scenarios, save concepts, standardized assets, and behavioral expectations established by the demo.

Future files:

```text
Trapstar_Phaser_3_Implementation_Notes.md
Trapstar_Technical_Architecture_Reference.md
Trapstar_Action_Resolution_Reference.md
Trapstar_System_Glue_and_Dependency_Boundaries.md
Trapstar_Consequence_Order_Reference.md
Trapstar_Engine_Migration_Boundary.md
Trapstar_Asset_Standards_Reference.md
Trapstar_Save_Data_Schema.md
```

---

## 22. Run-Card Generator Placeholder

The Run-Card Generator is the setup system for each new run.

It sets the static and starting values that define the run before the player begins acting.

The Run Card may eventually establish:

- Starting player hard assets
- Starting Time and Energy values
- Starting hunger and tiredness pressure
- NPC roster
- NPC roles
- NPC starting REP
- NPC starting HEAT state
- Faction setup
- Faction strength
- Faction relationships
- Static hidden info network
- Soft info placement
- Hard receipt placement
- ACCESS routes
- FAVOR debts
- LORE distribution
- Starting block conditions
- Stolen package variables
- Police pressure conditions

The Run-Card Generator should create replayability through bounded variation, not uncontrolled randomness.

The generator should create or accept a reproducible run seed and return portable run-state data. It must not create Phaser sprites, scenes, physics objects, or other presentation objects directly.

It answers:

```text
What is true at the start of this run?
Who knows what?
Who has what?
Who is under pressure?
Which routes, resources, and relationships are available or hidden?
```

This master file does not define the final generator logic yet.

Future file:

```text
Trapstar_Run_Card_Generator_Reference.md
```

---

## 23. System Connection Matrix

This matrix shows how the major systems connect at a high level.

| System | Connects To | Main Function |
|---|---|---|
| **SEN** | All systems | Philosophy of bounded emergence and negotiation. |
| **BASED** | Ask / Deal / Pressure, Vibes, abilities | Defines action tone and approach. |
| **Vibes** | Actions, future abilities, social outcomes | Shape how actions are expressed. |
| **Deal** | Money, Contra, Weapons, Favor, Access, Hard Info, Time | Logos / Structured choice: acts through hard reality, exchange, proof, cost, debt, resources, and concrete risk. |
| **Pressure** | REP, HEAT, LORE, FAC, combat risk, Soft Info, Hard Info | Pathos / Emergent choice: acts through fear, urgency, exposure, intimidation, escalation, and dynamic social force. |
| **Ask** | Info, REP, FAVOR, ACCESS, LORE | Ethos / Negotiated choice: acts through inquiry, request, trust, permission, appeal, and social opening. |
| **Info Cards** | All Social Assets | Standard unit of social/information state. |
| **Soft Info** | Ask, rumor, leads, suspicion | Opens possibilities and questions. |
| **Hard Info** | Pressure, proof, access, faction belief | Changes what people will risk or accept. |
| **HEAT** | Police, movement, deals, combat, weapons, contra | Tracks legal attention and enforcement danger. |
| **REP** | NPCs, block, factions, player | Tracks social standing and relationship quality. |
| **FAC** | Factions, assets, structure, world strength | Tracks faction-specific capacity and vulnerabilities. |
| **FAVOR** | NPCs, player, factions | Tracks social and information debt. |
| **ACCESS** | Routes, doors, contacts, resources, receipts | Tracks reach, permission, and availability. |
| **LORE** | Investigation, motives, hidden truths | Tracks world facts and discoverable knowledge. |
| **Game World Map** | Movement, nodes, factions, police, ACCESS | Defines the bounded block and traversal structure. |
| **Content Definitions** | Run generation, systems, resolvers, presentation metadata | Describes relatively stable NPC, faction, item, location, Info, action, Vibe, dialogue, and asset data. |
| **Runtime State** | All simulation systems, saves, run progression | Stores the mutable authoritative truth of the current run without Phaser objects. |
| **Portable Simulation Layer** | Run state, world state, action resolution, save state | Owns engine-independent game truth and consequence logic. |
| **Specialized Action Resolvers** | DPA, BASED, Info, REP, HEAT, TIME, inventory, missions, schedules | Coordinate only the systems required for a particular action and return an explicit resolved outcome. |
| **Independent Rule Systems** | Resolvers, runtime state, focused subsystem data | Calculate bounded consequences without directly commanding unrelated systems. |
| **Ordered Consequence Processing** | TIME, schedules, police, factions, missions, win/loss | Applies secondary effects in a visible, documented, and testable order. |
| **Outcome Events** | Presentation, UI, audio, animation, logs | Report completed changes after authoritative resolution; they do not own critical rule execution. |
| **Presentation Adapter** | Simulation state, Phaser presentation | Converts player intentions into simulation requests and resolved outcomes into display instructions. |
| **Phaser Presentation Layer** | Scenes, sprites, input, movement, UI, audio | Displays current state and gathers player input without owning core outcome rules. |
| **Portability Rules** | Data, IDs, saves, seeds, assets, tests | Protects reusable game truth from unnecessary engine lock-in. |
| **Run-Card Generator** | Starting values, NPCs, factions, info, resources | Sets static and starting conditions for each new run. |
| **Money** | Deals, fines, bribes, sustenance | Tracks cash value. |
| **Contra** | Deals, HEAT, faction value | Tracks illicit trade value and legal risk. |
| **Weapons** | Combat, Pressure, HEAT | Tracks force and weapon legality. |
| **Sustenance** | Energy, hunger, time | Maintains player survival. |
| **Time** | Every action, hunger, tiredness | Measures action cost and run pressure. |
| **Energy** | Combat, survival, choice limits | Measures player endurance and health. |
| **Combat** | Energy, Time, HEAT, weapons, Pressure | Crisis state that must be resolved quickly. |

---

## 24. High-Level Gameplay Loop

The core loop can be summarized as:

```text
0. Generate the run card.
1. Enter the block.
2. Read the situation.
3. Move through streets, nodes, exits, buildings, passages, or hidden routes.
4. Identify what is known, unknown, soft, hard, risky, or valuable.
5. Choose one DPA frame for the situation:
   - Deal with hard reality.
   - Pressure the unstable situation.
   - Ask for a negotiated opening.
6. Choose a BASED Vibe that defines how the approach is expressed.
7. Submit a structured action request containing actor, target, frame, Vibe, offer or demand, leverage, and context where relevant.
8. Validate the request and route it through the appropriate specialized resolver.
9. Let each participating system calculate only its bounded consequence.
10. Apply one authoritative state transition.
11. Spend Time and process ordered secondary consequences such as schedules, HEAT thresholds, faction reactions, mission updates, and survival pressure.
12. Produce a resolved outcome for dialogue, UI, animation, audio, camera, logs, and tests.
13. Re-enter the world with a changed situation.
```

The loop is intentionally small but flexible.

The player is not meant to solve everything through one dominant path. At each meaningful situation, the player must continually decide whether to Deal, Pressure, or Ask, and what to spend, risk, believe, prove, or involve.

---

## 25. Future Detailed Reference Files

This master architecture file should be supported by focused markdown references as the design becomes more specific.

Planned or existing reference files:

```text
Trapstar_Master_System_Architecture.md
Trapstar_Info_Card_Reference.md
Trapstar_BASED_Trait_Vibe_Reference.md
Trapstar_BASED_Ability_Reference.md
Trapstar_HEAT_System_Demo_Scope.md
Trapstar_REP_System_Demo_Scope.md
Trapstar_FAC_System_Demo_Scope.md
Trapstar_FAVOR_System_Demo_Scope.md
Trapstar_ACCESS_System_Demo_Scope.md
Trapstar_LORE_System_Demo_Scope.md
Trapstar_Hard_Assets_Reference.md
Trapstar_TIME_Cost_System.md
Trapstar_Energy_Hunger_Tiredness_System.md
Trapstar_Combat_Alert_State_Reference.md
Trapstar_Map_World_Traversal_Reference.md
Trapstar_Phaser_3_Implementation_Notes.md
Trapstar_Technical_Architecture_Reference.md
Trapstar_Action_Resolution_Reference.md
Trapstar_System_Glue_and_Dependency_Boundaries.md
Trapstar_Consequence_Order_Reference.md
Trapstar_Engine_Migration_Boundary.md
Trapstar_Asset_Standards_Reference.md
Trapstar_Save_Data_Schema.md
Trapstar_Run_Card_Generator_Reference.md
```

Implementation / Pipeline Index Files:

```text
Trapstar_Codex_Implementation_Index.md
Trapstar_Data_Model_Index.md
```

Later master sections may also cover:

```text
Trapstar_Demo_Limitations.md
Trapstar_Win_Save_Lose_Conditions.md
Trapstar_Run_Structure_Reference.md
Trapstar_Save_System_Reference.md
```

---

## 26. Current Boundary of This Master File

This file intentionally avoids heavy numeric detail.

It does not yet define:

- Exact value thresholds
- Exact action costs
- Exact Energy formulas
- Exact hunger/tiredness rates
- Combat math
- Full faction generation
- Full run-card generation logic
- Exact action-request and resolved-outcome schemas
- Final specialized resolver list and dependency boundaries
- Exact secondary-consequence priority and queue behavior
- Exact save-schema fields and migration procedures
- Complete automated test coverage
- Full map layout
- Full Phaser implementation plan
- Final production-engine selection or migration plan
- Full ability list
- Win/save/lose implementation
- Demo limitations

Those details belong in future focused markdown files.

This file should remain the high-level architecture truth that keeps those future files compatible.

---

## 27. One-Sentence Design Truth

*Trapstar the Demo* is a bounded SEN-driven negotiation game where each run generates a dangerous one-block socioeconomic puzzle, and the player uses BASED Vibes through the Deal / Pressure / Ask choice frame to act on hard reality, dynamic pressure, and negotiated possibility while navigating Social Assets, Hard Assets, TIME COST, Energy pressure, faction tension, and police HEAT.

---

## 28. One-Sentence Technical Truth

*Phaser 3.90 presents the seven-week demo, while portable content definitions, authoritative runtime state, independent rule systems, explicit action resolvers, ordered consequences, reproducible tests, and standardized assets define the game beneath it and should survive any later production-engine migration.*

---

## 29. One-Sentence Architecture Principle

*Trapstar contains complexity by letting small systems own bounded rules, specialized resolvers coordinate their intersections, authoritative commands apply ordered state transitions, and events report completed outcomes to the Phaser presentation layer.*
