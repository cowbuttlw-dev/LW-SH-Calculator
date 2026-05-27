# Alliance Combat Simulator & Debuff Calculator: Readme Guide

This guide explains how each section, row, and column works inside your **Universal Rally Master & Combat Calculator** spreadsheet and web application. Use this guide to understand how the calculator turns raw squad stats into projected results, and how to utilize the different modes.

---

## 📊 Why Does 45M Raw Power Equal 54M Projected Damage Dealt?
If you completely turn off the debuff settings and run a neutral matchup (e.g., Tank Squad vs. Tank Boss), you will notice your **Projected Damage Dealt** is calculated at **54,000,000** even though your squad's **Raw Power** is **45,000,000**. 

This is an intentional feature of the calculation engine:
$$\text{Projected Damage Dealt} = \text{Net Effective Power} \times 1.2 \text{ (Tactical Skill Multiplier)} \times \text{Faction Counter Mod}$$

* **Net Effective Power:** In a general matchup without debuffs, your net power remains your full raw squad power (`45,000,000`).
* **Faction Counter Mod:** In a neutral matchup (e.g., Tank vs. Tank), there is no multiplier advantage or penalty (`1.0` or `100.0%`).
* **Tactical Skill Burst Multiplier (1.2x / +20%):** The calculation engine automatically factors in a **1.2x multiplier** to simulate the active combat performance of your squads. Once your frontline and backline heroes cycle through their active tactical skills, weapon buffs, and ultimate abilities, their damage throughput increases beyond their flat raw profile. 

---

## 📋 1. Target Environment Setup (User Inputs)
These are the light-blue inputs where you copy details directly from your in-game screen.

| Input Name | Cell | What It Is & How to Use It |
| :--- | :---: | :--- |
| **Target Virus Resistance Required** | `B5` | The target resistance of the level/boss (e.g., `3,400`). |
| **Your Current Virus Resistance** | `B6` | Your host/squad's current resistance level (e.g., `1,950`). |
| **Input Game Damage Penalty %** | `B7` | The damage nerf shown in-game (e.g., `86.0%` is input as `0.86`). |
| **Input Enemy Damage Increase %** | `B8` | The boss's damage buff shown in-game (e.g., `700.0%` is input as `7.00`). |
| **Suggested Target Base Power** | `B9` | The recommended power for the fight (e.g., `55,000,000`). |
| **Boss Maximum HP Pool** | `B10` | The total health points of the boss. (Entering this clears any `#DIV/0!` errors). |
| **Enemy Faction Type** | `B11` | *[Dropdown]* Select whether the boss is **Tank**, **Missile**, or **Air**. |
| **Debuff Mode Toggle** | `B12` | *[Dropdown]* Select **Active** to simulate virus debuffs, or **Disabled** to use this as a general-purpose combat calculator. |

---

## ⚡ 2. Live Performance Metrics (Calculated Outputs)
These are fully automated real-time calculations.

* **Current Resistance Capacity % (`E5`):** Your percentage completion of the required resistance target. If Toggle is set to *Disabled*, this defaults to `100.0%`.
* **Resistance Point Deficit (`E6`):** The exact number of resistance points you need to upgrade to reach the target threshold.
* **Active Squad Debuff (`E7`):** The real-time penalty modifier applied to your power output (shows `-0.0%` if toggle is *Disabled*).
* **Enemy Damage Multiplier (`E8`):** The actual damage scale of the boss. At `800.0%`, the boss hits 8 times harder than normal (100% base + 700% buff).
* **Theoretical Single Squad Target (`E9`):** The astronomical power a single squad would need to solo-clear this fight under the current active penalty.

---

## ⚔️ 3. Active Rally Squad Configurator (Main Matrix Columns)
This is where you set up your 5-player rally team.

* **Rally Deployment Slot (Column A):** Identifies squad position. **Slot 1 (Host)** determines the virus resistance level for everyone else in the rally.
* **Squad Composition / Name (Column B):** A text label for player names (e.g., "You", "Dave", "Eric") or squad setups.
* **Your Faction Type (Column C):** *[Dropdown]* Assign each player's primary unit class: **Tank**, **Missile**, or **Air**.
* **Raw Squad Power (Column D):** Type in each player's base squad power (e.g., `45,000,000`).
* **Net Effective Power (Column E):** `[Raw Squad Power] * (1 - Active Debuff %)` — What each squad's power behaves like after the virus penalty strips away their strength. If the Debuff Toggle is *Disabled*, this matches your raw power.
* **Faction Multiplier Modifier (Column F):** Automatically calculates the advantage based on the rock-paper-scissors mechanic compared to the boss type in `B11`:
  * **`120.0%`** (+20% damage) if your squad type counters the boss.
  * **`100.0%`** (neutral damage) if your types match or don't counter.
  * **`80.0%`** (-20% damage penalty) if the boss counters your squad type.
* **Projected Raw Damage Dealt (Column G):** `[Net Effective Power] * 1.2 (Tactical Skill Multiplier) * [Faction Multiplier]` — The total projected damage this player's squad will unleash on the boss.

---

## 📊 4. Impact Forecast on Boss Health Bar
This reveals your ultimate battle projection.

* **Total Combined Damage Applied to Boss (`B25`):** The total sum of all 5 players' individual projected damage outputs combined.
* **Estimated HP Percentage Stripped (`B26`):** The exact percentage of the boss's health bar your rally will destroy in a single run.
* **Estimated Rallies Required (`B27`):** The number of times you need to launch this identical rally to completely kill the boss.
