# PRD: Night Shift

> Online co-op hospital horror. Real-time patient care × tower defense × horde defense.
> Status: concept, pre-MVP (2026-10-21). Team: Navo, dcai (doctors), dyang (playtester), Albert, Andy, Li (devs).

## 1. Overview

By day, an understaffed hospital admits patients and restocks, and the players decide how many patients to risk taking on. By night, something is wrong with the patients. 2–6 players treat them by running multi-step treatment protocols against a deterioration timer. Patients they fail flatline and rise as "the turned." Treated patients pay out insurance money, which buys barricades and equipment to hold the hallways against the turned and against outside horde waves. Survive until the 7am shift change, collect rewards from the patients who made it, and do it again.

**Pitch:** *Keep your patients alive. The ones you lose come back for you.*

## 2. Problem

- Friend-group co-op games (Lethal Company, R.E.P.O., PEAK, Barotrauma) either have shallow loops or brutal onboarding. dcai bounced from Barotrauma on the mod download before ever playing.
- Real-time co-op juggling under a timer is reliably funny to play and watch, but existing games in that space have no persistence, no horror, and no reason to defend anything.
- Our unfair advantage: **two real doctors** writing the cases and protocols. The medical content is authentic and funny in ways nobody else can fake.

## 3. How it works

### Core loop (one day + night = one round)

```
TREATMENT   treat patients ──► $$ insurance payout
     ▲                               │
     │                               ▼
untreated patients turn       TOWER DEFENSE  buy barricades / equipment
spawn INSIDE your walls              │
     ▲                               ▼
     └──── time spent fighting ◄── HORDE DEFENSE  fight waves directly
```

### Five interlocks (what makes this one game instead of three)

1. **Hallways are both your care routes and the enemy's path.** Barricades route the horde but also block gurney routes.
2. **Two horde sources.** External waves hit the doors on a schedule. Failed patients spawn *behind* the defenses, so walling up and waiting doesn't work.
3. **Saved patients fight back.** A discharged patient defends with a mop for 60 seconds.
4. **The horde attacks stations.** A destroyed pharmacy means no meds until it's repaired.
5. **Screamers speed up patient timers.** The horde pressures the treatment loop directly.

### Treatments are protocols (doctors write these)

| Condition | Protocol |
|---|---|
| Chest pain | EKG → aspirin (pharmacy) → wheel to cath lab |
| Broken arm | X-ray → splint (supply closet) → cast station |
| Overdose | Narcan → monitor → don't leave them alone |

Carry one item at a time. Gurneys need 2 people unless one of them is an Orderly-type upgrade.

### Soft roles (pick freely, duplicates allowed)

Everyone can do every task. A role makes you much better at one thing.

| Role | Better at | Signature | Non-role fallback |
|---|---|---|---|
| Doctor | Diagnose fast, always right | Code call: revive one flatlining patient | "WebMD": 3x slower, wrong 25% of the time |
| Nurse | Carry 2 items, give meds fast | Sees nearby patient timers | Timers visible only on the board |
| Security | 2x damage vs the turned | Places barricades | Shove = short stun |
| Maintenance | Builds and repairs fast | Restores power instantly | Repairs at a quarter of the speed |

The **timer board** is a physical station on the map. Whoever stands there sees every patient timer and becomes the team's caller.

### Day / night cycle

One **day + night = one round**. Day is calm and about decisions. Night is when everything happens.

| Phase | Length | What happens |
|---|---|---|
| Morning report | 30s | Survivors discharged, rewards paid, fines charged, rating updated |
| **Day** | ~3 min, no enemies | Admit patients, restock, build/repair barricades, treat walk-ins for small cash |
| Dusk | 30s | Last call. Admissions close, doors lock |
| **Night** | 5–8 min | Admitted patients deteriorate, ambulances bring emergencies, horde waves hit |

#### Day: admissions (the push-your-luck)

The admissions desk shows a queue of patient cards:

| Card field | Example |
|---|---|
| Condition | Chest pain (3 steps) |
| Overnight risk | Low / Med / **High** (how fast their timer runs at night) |
| Payout | $400 |
| Occupation | Electrician |

- **Beds are capacity.** Admitting past your bed count puts patients on **hallway gurneys**. They sit in the enemy's path, block your own routes, and are the first thing the horde grabs.
- Every admitted patient is both **revenue and a possible enemy.** The greedier the day, the more could turn at night.

#### Day: restock

Spend money at the supply desk: meds, sedatives (which are also dart-gun ammo), barricade materials, nail-gun ammo, weapon repairs. Deliveries arrive instantly during the day. Nothing can be bought at night.

#### Night timeline

| Time | Patients | Horde |
|---|---|---|
| 11pm–1am | Admitted patients start deteriorating | None |
| 1–3am | Ambulance emergencies arrive | Small waves |
| 3am | Trauma surge | Huge wave |
| 4–6am | Leftovers | Stragglers + failures |
| 7am | Shift change → morning report | — |

#### Rewards for overbooking

Each layer rewards a different time horizon:

| Layer | Reward | Why it matters |
|---|---|---|
| 1. Payout | Cash scales with risk: high-risk patients pay 3–5x | Baseline. More money means more barricades and ammo tomorrow |
| 2. **Occupation perks** (the main hook) | A patient who **survives to morning** gives a perk based on their job | Admitting becomes a *choice about who*, not just how many |
| 3. Hospital rating | Stars go up with saves and down with deaths and fines | A higher rating draws a better patient pool next day: higher payouts, rarer perks |
| 4. Cure research | Critical patients who survive add progress toward a cure | Campaign win condition. Reach 100% and the outbreak ends |

**Occupation perk examples:**

| Patient | Perk if they survive the night |
|---|---|
| Electrician | Next night's first power cut fixes itself |
| Cop | Leaves you their sidearm (a pistol, not in any locker) |
| Contractor | 3 free barricades |
| Pharma rep | 30% off restock tomorrow |
| Retired nurse | Joins as an NPC nurse for one night |

#### Death & turning penalties (any source)

**Base penalty, every death:**

| # | Penalty | When |
|---|---|---|
| 1 | No payout (patients only pay on discharge) | Instant |
| 2 | Their occupation perk is lost | Instant |
| 3 | They turn after a **10-second window** | 10s later |
| 4 | Malpractice fine × cause multiplier | Morning report |
| 5 | Rating drops, so tomorrow's patient pool is worse | Morning report |

**The 10-second window:** a flatline starts a countdown, and the team picks one:

- **Code them:** Doctor's revive or defib paddles. They're back and every penalty is cancelled.
- **Morgue run:** two people wheel the body to the morgue. They don't turn, but the fine still applies.
- **Do nothing:** they rise inside the walls, often next to other patients.

**Cause multipliers (on the fine):**

| Cause | Fine | Why |
|---|---|---|
| Timer ran out | 1x | Neglect |
| Killed by the horde (Runner grab, bed attacked) | 0.5x | Insurance covers half; Security failed |
| Died on a hallway gurney | 1.5x | Overbooking was the team's choice |
| Wrong treatment (WebMD guess, wrong med) | 2x | Actual malpractice |
| Friendly fire | 3x + an incident report naming the player | Comedy |

**Contagion:** a turned patient who bites a living patient turns them too. One neglected bed can take out a ward in about 30 seconds, so a single death is dangerous even without a big fine.

**Lose conditions:**

1. ICU overrun (ICU lives reach 0): the night is lost.
2. Rating hits 0 stars: the state shuts the hospital down and the campaign ends.

**Guardrail against a hopeless run:** fines can push money negative, but debt only blocks the shop. It never removes beds or roles, so a bad night stays recoverable.

**Morning report** lists every death with its cause, e.g. *"Bed 3: chest pain, WebMD misdiagnosis, −$800, nurse: Andy."*

The decision every day: *"the electrician is high-risk and we're out of beds. Hallway gurney?"*

#### Emblems (run-long team bonuses)

Emblems are permanent, team-wide bonuses that last the whole run, like Slay the Spire relics. Occupation perks are one-shot. Emblems are what makes each run play differently.

**How you get them:**

| Source | Offer |
|---|---|
| Day shop | 1–2 random emblems, expensive (competes with restocking) |
| Morning report: perfect night (zero deaths) | Pick 1 of 3 |
| Critical patient survives | Pick 1 of 3, higher rarity |
| Cure milestone (25/50/75%) | Pick 1 of 2 **trade-off emblems** |

Purchases go to a team vote at the shop, so emblems create arguments.

**Build-around emblems** (change how you play, not +10% stats):

| Emblem | Effect |
|---|---|
| Magnet Hospital | Runners ignore hallway gurneys. Enables an overbooking strategy |
| Teaching Hospital | Non-doctors' WebMD is never wrong (still slow) |
| Blood Bank | Every turned you kill drops a blood bag (heals players or counts as a treatment step) |
| Pneumatic Tubes | Send any item between any two stations instantly |
| Union Contract | Everyone gets a second belt slot |

**Trade-off emblems** (big upside, real cost, like Slay the Spire's boss relics):

| Emblem | Upside | Cost |
|---|---|---|
| Private Equity Buyout | +100% payouts | Lose one bed every night |
| Experimental Trial | Patient timers run 2x slower | Every death rises as a Brute, not a Shambler |
| Skeleton Crew | Restock 50% off | The timer board is disabled |

**Design rules:** each emblem hooks into one game event (`on_admit`, `on_patient_death`, `on_enemy_killed`, `on_power_cut`, `on_restock`). Emblems are data (`.tres`) that subscribe to a global event bus, so adding one is a data file plus at most one small script. Target **20–30 emblems** for a Steam demo, about 10 at M4.

### Enemies

| Enemy | Behavior | Pressures |
|---|---|---|
| Shambler | Slow, comes in numbers | Tower defense |
| Runner | Ignores players, grabs patients | Treatment |
| Brute | Smashes barricades | Tower defense |
| Crawler | Uses vents, skips the maze | Inside defense |
| Screamer | Speeds up nearby patient timers | Treatment |

### Weapons (improvised from the hospital)

**Hands rule:** every player has a **hands** slot (one item *or* one weapon) and a **belt** slot (one one-handed melee weapon). Ranged weapons take both hands. Holding a gun means you're not carrying meds, and pushing a gurney means you're unarmed.

**Shared supply:** ammo comes from the same supply as treatment. Every sedative fired at the turned is one a patient doesn't get.

| Melee | Feel | Hook |
|---|---|---|
| Bedpan | Fast, weak, short stun | Belt-sized, always on you |
| IV pole | Long reach, sweeping arc | Good at holding a doorway |
| Fire extinguisher | Knockback cone, limited charges | Also puts out fires from power faults |
| Defib paddles | Big stun burst, slow recharge | Doctors get 2x stun. The same charge revives patients |
| Bone saw | High damage, slow wind-up | Loud: draws nearby enemies |

| Ranged | Feel | Hook |
|---|---|---|
| Syringe dart gun | Slows/sedates | Uses sedatives from the pharmacy (shared with patients) |
| Nail gun | Steady damage | Ammo made by Maintenance from supply crates |
| Flare gun | Low damage, burns | Lights up a dark area for 20s, best during power cuts |
| Saline sprayer | Pushback stream | Refills at any sink, no shared supply |
| Tranq rifle | One-shots a Brute, very slow reload | Only one per hospital, found mid-night |

Security deals 2x damage with every weapon, so anyone can fight, but Security fights best. Weapons spawn in fixed lockers (security office, maintenance closet, OR) and can be dropped and passed to teammates.

**Netcode:** melee and ranged hits are detected on the attacker's client and confirmed by the host (co-op, so trust the client for responsiveness). Projectiles are host-simulated, and clients show tracers and effects immediately.

### Horror through lighting

The view is top-down 2D with a camera that follows each player. Each player has their own fog of war and only sees inside their flashlight cone. When the power cuts, the hospital goes black and only flashlight cones remain. Maintenance restoring power literally reveals the map.

## 4. Technical approach

| Layer | Choice |
|---|---|
| Engine | Godot 4, GDScript |
| View | Top-down 2D, `PointLight2D` + shadows for flashlights and power cuts |
| Networking | Godot high-level multiplayer (`MultiplayerSynchronizer`, `MultiplayerSpawner`, RPCs) |
| Transport | ENet in dev, Steam Networking via GodotSteam in release, behind one abstraction |
| Host model | Listen server (one player hosts), no dedicated servers, $0 infra |
| Lobbies | GodotSteam lobbies + friend invites. One click to join, no IPs, no mods |
| Voice (post-MVP) | Steam voice → `AudioStreamPlayer2D` for proximity chat |
| Repo | Standalone GitHub repo, Git LFS for art/audio |
| CI | GitHub Actions: `godot-ci` export → `steam-deploy` to a beta branch |

### Netcode rules

1. The host is authoritative. Clients send inputs.
2. Own-player movement is predicted locally. Interactions (grab, treat, build) are confirmed by the host, and the first request to arrive wins.
3. Enemies path on a shared flow field toward the ICU. The host sends spawn events plus 10–20Hz snapshots, and clients interpolate.
4. No networked rigidbody physics. Gurneys and carried items are kinematic.
5. Test locally with 2 Godot instances (Debug → Customize Run Instances). Use Steam test app ID 480 until the $100 Steam Direct fee is paid.

### Content is data

Conditions, enemies, towers, roles and night timelines are Godot Resources (`.tres`) that can be edited in the inspector, so the doctors can add a case without touching code. Behavior lives in code, numbers live in data.

## 5. v1 scope (MVP: 4–5 weekends)

- 2 players online (ENet, direct connect)
- 1 hospital map: entrance, 3 beds, pharmacy, ICU, 2 hallways
- 2 roles: Doctor + Security
- 3 conditions, written by Navo and dcai
- 1 tower: barricade
- 2 weapons: IV pole (melee) + syringe dart gun (ranged, uses shared sedatives), with the hands/belt rule
- 2 enemies: Shambler (outside) + turned patient (inside)
- One day: choose from 5 patient cards with 3 beds + 1 hallway-gurney slot, 3-item restock shop, cash payout only
- One 5-minute night with a single "3am" wave
- Death penalty basics: no payout, the 10-second window (revive or morgue run), turning, flat fine
- Win/lose screen

**The MVP answers two questions:** does "my barricade is blocking my own gurney" create fun tension, and is admitting a 4th patient onto a hallway gurney tempting enough to argue about?

## 6. Out of scope (for v1)

- Local co-op (explicitly dropped; online only)
- Steam integration, lobbies, achievements
- Proximity voice
- Nurse and Maintenance roles, power cuts and lighting horror
- Runner/Brute/Crawler/Screamer enemies
- Cause multipliers, contagion, occupation perks, emblems, hospital rating, cure research, multi-day campaign, rearranging the hospital layout
- Night modifiers (flu season, full moon, storm)
- 3D art

## 7. Risks & unknowns

| Risk | Mitigation |
|---|---|
| Three loops feel like three minigames | MVP tests the barricade-vs-gurney interlock first. If it isn't tense, rethink before adding content |
| Netcode with 300+ enemies | Flow field + snapshots from day 1, no per-enemy physics |
| Team attrition (6 busy people, 2 of them doctors) | Weekend-sized milestones, a playable build every PR, nobody blocks anyone (content is data) |
| Onboarding friction loses players before they play | One-click Steam invite, small build, no mods |
| Balance (too easy/too hard) | dyang is the "is it fun for a normal person" gate on every milestone |
| Revenue split disputes if it ships | One-page signed agreement before Steam setup |
| "Turned patients" reads as tasteless to the doctors | Doctors own the tone. They're the ones writing the cases |

## 8. Done means

**MVP done:** two people on separate machines play a full 5-minute night online, treat at least one patient end-to-end, place a barricade, fight a wave, and someone laughs. dyang plays it without instructions beyond "you're a doctor, save people."

**Roadmap after MVP:**

| Milestone | Adds | Est. |
|---|---|---|
| M2: 4 players | Steam lobbies, Nurse + Maintenance, power cuts + flashlights | +4 weekends |
| M3: Full night | All 5 enemies, all 10 weapons, full timeline, 8–10 conditions, occupation perks, cause multipliers + contagion | +6 weekends |
| M4: Campaign | Multi-day runs, ~10 emblems, hospital rating, cure research win condition, layout editing, night modifiers | +6 weekends |
| M5: Steam demo | Proximity voice, achievements, store page, Next Fest | +4 weekends |

## 9. Open questions

**Everyone**
- E1. Goal: just for us, or aim for Steam?
- E2. How many hours a week can each person realistically give?
- E3. Tone: funny-scary or actually scary? How gory?
- E4. Art style: pixel art or clean flat shapes?
- E5. Is "Night Shift" the name?

**Doctors**
- D1. 3 conditions treatable in exactly 3 steps (for the MVP)
- D2. Weirdest case that turned out to be something dumb?
- D3. Which jobs would make funny occupation perks?
- D4. What inaccuracy would make you cringe, and what's fine to fudge?

**Game design**
- G1. Camera: top-down, third person, or first person? (Current plan: top-down; first person is scariest but hides the map)
- G2. What happens when a player dies? Spectate until morning, or come back as a turned?
- G3. Friendly fire: on, off, or only the bone saw?
- G4. How many days in a full campaign? (One day + night ≈ 10 min)
- G5. Is the hospital layout fixed, or rearranged between days?

**Devs**
- V1. Who owns what: networking, gameplay systems, content tools?
- V2. Lock in Godot, or does anyone want to argue for Unity?
- V3. Which night works for a weekly playtest?
