# Trapstar Master System Architecture

**Project:** Trapstar the Demo  
**Purpose:** Master high-level system reference  
**Status:** Architecture overview / living design truth

---

## 1. Purpose

This document defines the high-level system architecture for *Trapstar the Demo*.

It is not a full GDD and it is not a numeric implementation spec. It explains how the major systems fit together so future markdown files, Codex tasks, GitHub commits, and Unity implementation can stay aligned.

The goal is to establish the shared design truth behind:

- the bounded Trapstar the Demo scenario
- the SEN loop philosophy
- BASED traits and Vibes as action language
- Deal / Pressure / Ask as the universal player choice frame
- Soft / Hard information state
- Social Assets and Hard Assets
- TIME COST and Energy pressure
- combat as an alert/crisis state
- map, traversal, engine, and run-card direction

Focused subsystem files should control exact numbers, formulas, tables, and implementation details when those files exist.

---

## 2. Production Pipeline Role

The active production spine is:

```text
Chat / Nova
  -> GitHub Markdown Source of Truth
    -> Codex Planning + Code Generation
      -> Unity Implementation
        -> Playtest / Bug / Design Feedback
          -> Chat / Nova Review
            -> Updated GitHub Markdown
```

GitHub stores accepted markdown as the current source of truth. Codex should use this file for architecture context, then implement from bounded task files in `codex_tasks/`.

Pipeline rule:

```text
Do not treat a placeholder as a finished mechanic.
Do not invent missing numbers from this master file.
Use focused subsystem files for specific implementation metrics.
```

---

## 3. Quick Architecture Summary

| Layer | Purpose |
|---|---|
| **Trapstar the Demo** | Three-day Stolen Package proof-of-concept centered on a missing Contra shipment/package and bounded variation. |
| **SEN** | Design philosophy: Structured, Emergent, Negotiated. |
| **BASED** | Action language built from five traits and 20 Vibes. |
| **Vibes** | Ordered two-trait action tones used to shape approach and future abilities. |
| **Deal / Pressure / Ask** | Universal player choice frame. The player chooses Deal, Pressure, or Ask as a strategic approach to the current situation. DPA symbolically maps to SEN but is not an ordered loop. |
| **Soft / Hard Info** | Information state: rumor or lead versus receipt, proof, or verified fact. |
| **Info Cards** | Standard unit for storing social and information state. |
| **Social Assets** | HEAT, REP, FAC, FAVOR, ACCESS, and LORE. |
| **Hard Assets** | Money, Contra, Weapons, Sustenance, Time, and Energy. |
| **TIME COST** | Minute-cost rules attached to meaningful actions. |
| **Energy / Hunger / Tiredness** | Survival pressure and combat health direction. |
| **Combat** | Alert/crisis state the player usually wants to resolve or exit quickly. |
| **Game World Map** | One-block, three-street, node-connected playable space. |
| **Engine / Presentation** | Unity 2D beat-em-up-style movement with menu-based interaction. |
| **Run-Card Generator** | Starting truth generator for NPCs, factions, hidden info, resources, and run variables. |

---

## 4. Trapstar the Demo

*Trapstar the Demo* is the bounded proof-of-concept for the larger Trapstar design.

The main playable scenario is **Stolen Package**:

```text
A Contra shipment/package has gone missing.
The player has three in-game days to find out what happened and resolve the situation.
```

The demo focuses on:

- one block
- three node-connected streets
- a limited NPC roster
- two primary factions
- police-monitored pressure
- a three-day time limit
- the Stolen Package case as the central conflict
- a narrowed set of Social Assets and Hard Assets
- a run-card generator that changes starting roles, values, hidden information, and faction conditions

The player is not simply solving a static mystery. Each run can begin with different starting truths.

The run card may change:

- which NPC is guilty
- which NPC is lying
- which NPC is telling the truth
- which NPCs are monitored
- which faction has more strength
- which faction is under more pressure
- which Info Cards are soft rumors
- which receipts can harden those rumors into proof
- which routes, favors, access points, and risks exist at the start

This creates replayability through bounded variation, not uncontrolled randomness.

---

## 5. Core Design Stack

Trapstar the Demo is built as a bounded socioeconomic negotiation loop.

```text
Run-Card Generator
  -> Starting World / NPC / Faction / Resource State
    -> SEN Philosophy
      -> BASED Action Language
        -> Deal / Pressure / Ask Choice Frame
          -> Info Cards and Social Assets
            -> Hard Assets and Player State
              -> TIME COST and Consequence
                -> Updated World / NPC / Faction State
                  -> Next Negotiation Situation
```

Core relationship:

```text
SEN creates the situation.
BASED colors the approach.
DPA chooses the strategic frame.
Assets and Info determine the consequence.
Time makes the choice costly.
The world updates.
```

The player is constantly asking:

```text
What do I know?
Who knows what?
Who can I trust, threaten, pay, avoid, or expose?
What will this cost in time, energy, money, reputation, or police attention?
```

---

## 6. SEN Philosophy

**SEN** means:

```text
Structured
Emergent
Negotiated
```

SEN is the underlying design philosophy that powers the demo.

### 6.1 Structured

Structured systems are the visible and invisible hard rules of the world:

- limited map
- limited time window
- limited NPC cast
- limited factions
- limited resources
- trackable hard assets
- trackable social assets
- clear action frames
- defined consequences

Structure prevents the demo from becoming an unbounded simulation.

### 6.2 Emergent

Emergent systems are pressure created by the current state:

- NPC reactions
- faction relationships
- info discovery
- soft information hardening into receipts
- HEAT escalation
- REP shifts
- resource loss or gain
- time passing
- player choices

Emergence gives the demo replayability and social texture without requiring infinite simulation.

### 6.3 Negotiated

Negotiated systems are the player-facing choices made inside the current situation.

Negotiation happens through:

- what the player knows
- what the NPC believes
- what each side wants
- what each side can prove
- what each side can risk
- what assets are available
- which DPA frame the player chooses
- which BASED trait or Vibe colors the approach

SEN intersects with hard design most clearly through the universal choice frame, but the frame is not itself a sequence.

```text
The world presents a structured situation.
Emergent pressure changes what is risky, urgent, or unstable.
The player negotiates the next move by choosing Deal, Pressure, or Ask.
The result updates assets, info, Vibe effects, risk, and consequence.
The changed situation becomes the next SEN state.
```

### 6.4 SEN Loop and DPA Choice Frame

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

## 7. BASED as Action Language

**BASED** is the main action-language framework for Trapstar the Demo.

BASED should be understood as **how a character acts**, not as a full personality simulation.

BASED is made of five traits:

```text
B = Belligerence
A = Aggression
S = Sociability
E = Empathy
D = Deception
```

A **Vibe** is an ordered two-trait pairing. The first trait leads. The second trait modifies the expression.

Example:

```text
AB = Aggression leading into Belligerence
BA = Belligerence leading into Aggression
```

These are not the same.

Rows show the leading trait. Columns show the secondary trait. Self-pairs are excluded.

| Lead / Secondary | B | A | S | E | D |
|---|---|---|---|---|---|
| **B — Belligerence** | — | **BA: Reckless** | **BS: Instigating** | **BE: Condemning** | **BD: Extortive** |
| **A — Aggression** | **AB: Menacing** | — | **AS: Commanding** | **AE: Urgent** | **AD: Hustled** |
| **S — Sociability** | **SB: Irreverent** | **SA: Charismatic** | — | **SE: Compassionate** | **SD: Coaxing** |
| **E — Empathy** | **EB: Steadfast** | **EA: Boundaried** | **ES: Communal** | — | **ED: Deflecting** |
| **D — Deception** | **DB: Bluffing** | **DA: Predatory** | **DS: Insinuating** | **DE: Feigning** | — |

All 20 Vibes are available in the demo as action language. Later ability files may define which Vibes have Street abilities, Dialogue abilities, or Both-use abilities.

Future file:

```text
Trapstar_BASED_Ability_Reference.md
```

---

## 8. Universal Action Frame: Deal / Pressure / Ask

Trapstar the Demo uses one universal player choice frame:

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

The same choice frame can operate in dialogue, street encounters, faction interactions, resource exchanges, investigation, combat-adjacent moments, and crisis states.

The order below follows the name of the frame, not a required gameplay sequence.

### 8.1 Deal

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

A Deal can involve money, Contra, weapons, sustenance, information, favor, access, protection, silence, time, or risk.

Deal is the main exchange path. It can create opportunity, but it can also expose the player to HEAT, betrayal, bad prices, setup risk, or faction consequence.

### 8.2 Pressure

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

Pressure can pursue confession, compliance, hidden information, faction secrets, HEAT information, debt collection, access, retreat, silence, or combat avoidance.

Pressure is powerful but risky. It can raise HEAT, damage REP, trigger combat, harden resistance, or create future retaliation.

### 8.3 Ask

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

Ask can pursue soft information, clarification, permission, warning, introduction, help, favor, access, or relationship repair.

Ask is usually the safest action path, but it may be limited by low REP, bad timing, secrecy, fear, faction pressure, or lack of leverage.

---

## 9. Information State

All information can exist as **Soft Info** or **Hard Info**.

Soft Info is unconfirmed knowledge: rumor, claim, suspicion, lead, social read, tip, unverified story, emotional read, or social impression.

Hard Info is confirmed or provable knowledge: receipt, proof, witnessed event, confession, verified fact, confirmed access, physical evidence, or documented claim.

Key rule:

```text
Soft Info opens possibilities.
Hard Info changes what people will risk, believe, allow, or deny.
```

An **Info Card** is the standard unit for storing information in the demo. Info Cards can represent what people know, believe, suspect, can prove, owe, permit, fear, hide, trade, or socially recognize.

---

## 10. Social Assets

The six Social Assets are information-based assets that shape what characters and factions know, believe, permit, owe, fear, control, or can prove.

```text
HEAT
REP
FAC
FAVOR
ACCESS
LORE
```

- **HEAT** represents police attention, suspicion, surveillance, enforcement pressure, or legal danger.
- **REP** represents social standing and relationship quality.
- **FAC** represents one faction's elements, capacity, and world strength.
- **FAVOR** represents social or information-based debt.
- **ACCESS** represents reach, permission, influence, availability, entry, contact, or usable connection.
- **LORE** represents known, suspected, remembered, or discoverable facts about people, places, factions, routines, motives, history, and relationships.

---

## 11. Hard Assets

Hard Assets are trackable resources with direct material, survival, legal, or action value.

```text
Money
Contra
Weapons
Sustenance
Time
Energy
```

Hard Info is confirmed information. Hard Assets are trackable resources and values.

Time is measured in minutes. Energy is the player-state survival value and combat health meter. If Energy reaches 0, the run ends.

---

## 12. TIME COST, Energy, and Combat

TIME COST is the action-cost layer. Actions that may cost minutes include asking questions, making Deals, applying Pressure, moving, searching, waiting, resting, eating or drinking, checking inventory, major combat moves, high-risk exchanges, and escaping danger.

Current high-level Energy rule:

```text
Spend minutes -> hunger/tiredness pressure rises -> energy becomes harder to maintain -> choices narrow -> risk increases
```

Combat exists, but it is not the main grind loop. Combat should be treated as an alert or crisis state.

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

---

## 13. Game World, Engine, and Run Card

The game world is a bounded playable block:

```text
One block
Three node-connected streets
Multiple node exits
Interior and passage nodes
Hidden alley and shortcut nodes
```

The map is not an open city. It is a compact, readable socioeconomic space where people, routes, buildings, hidden paths, faction territory, police pressure, and resource access can collide.

The presentation target is:

```text
Unity 2D
Beat-em-up-style side/street presentation
WASD player movement
Point-click interaction support
Menu-based UI for choices, actions, inventory, and information
```

The Run-Card Generator sets the static and starting values that define the run before the player begins acting.

It may establish starting hard assets, time and energy values, NPC roster, NPC roles, NPC REP and HEAT states, faction setup, hidden info network, soft info placement, hard receipt placement, ACCESS routes, FAVOR debts, LORE distribution, and police pressure conditions.

---

## 14. System Connection Matrix

| System | Connects To | Main Function |
|---|---|---|
| **SEN** | All systems | Philosophy of bounded emergence and negotiation. |
| **BASED** | Deal / Pressure / Ask, Vibes, abilities | Defines action tone and approach. |
| **Vibes** | Actions, future abilities, social outcomes | Shape how actions are expressed. |
| **Deal** | Money, Contra, Weapons, Favor, Access, Hard Info, Time | Logos / Structured choice: acts through hard reality, exchange, proof, cost, debt, resources, and concrete risk. |
| **Pressure** | REP, HEAT, LORE, FAC, combat risk, Soft Info, Hard Info | Pathos / Emergent choice: acts through fear, urgency, exposure, intimidation, escalation, and dynamic social force. |
| **Ask** | Info, REP, FAVOR, ACCESS, LORE | Ethos / Negotiated choice: acts through inquiry, request, trust, permission, appeal, and social opening. |
| **Soft Info** | Ask, rumor, leads, suspicion | Opens possibilities and questions. |
| **Hard Info** | Pressure, proof, access, faction belief | Changes what people will risk or accept. |
| **HEAT** | Police, movement, deals, combat, weapons, contra | Tracks legal attention and enforcement danger. |
| **REP** | NPCs, block, factions, player | Tracks social standing and relationship quality. |
| **Time** | Every action, hunger, tiredness | Measures action cost and run pressure. |
| **Energy** | Combat, survival, choice limits | Measures player endurance and health. |

---

## 15. High-Level Gameplay Loop

```text
0. Generate the run card.
1. Enter the block.
2. Read the situation.
3. Move through streets, nodes, exits, buildings, passages, or hidden routes.
4. Identify what is known, unknown, soft, hard, risky, or valuable.
5. Choose a BASED Vibe approach.
6. Choose one DPA frame for the situation:
   - Deal with hard reality.
   - Pressure the unstable situation.
   - Ask for a negotiated opening.
7. Spend Time.
8. Risk or exchange Social Assets and Hard Assets.
9. Update Info Cards, REP, HEAT, FAC, FAVOR, ACCESS, LORE, resources, and player state.
10. Re-enter the world with a changed situation.
```

The player is not meant to solve everything through one dominant path. At each meaningful situation, the player must continually decide whether to Deal, Pressure, or Ask, and what to spend, risk, believe, prove, or involve.

---

## 16. One-Sentence Design Truth

*Trapstar the Demo* is a bounded SEN-driven negotiation game where each run generates a dangerous one-block socioeconomic puzzle, and the player uses BASED Vibes through the Deal / Pressure / Ask choice frame to act on hard reality, dynamic pressure, and negotiated possibility while navigating Social Assets, Hard Assets, TIME COST, Energy pressure, faction tension, and police HEAT.
