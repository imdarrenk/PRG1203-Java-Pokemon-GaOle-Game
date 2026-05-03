# Pokémon GA-OLE — PRG1203 Group Assignment

**Course:** PRG1203 Introduction to Object-Oriented Programming
**Assignment:** Group Assignment

A turn-based Pokémon battle game built in Java, playable entirely in the console.

---

## How to Compile & Run

```bash
# Compile all Java files
javac *.java

# Run the game
java Game
```

> Requires Java 14 or later.

---

## Gameplay

1. Enter your player name.
2. Choose **2 starter Pokémon** from Charizard, Blastoise, or Venusaur.
3. Explore locations, battle wild Pokémon, collect items, and grow your team.

### Main Menu Options

| Option | Description |
|--------|-------------|
| Battle | Enter a random location and fight a wild Pokémon |
| View Team | See your active battle team and caught Pokémon |
| Items | Use items from your inventory |
| Shop | Spend coins on Poké Balls, potions, and more |
| Scores | View the top 5 high scores |
| Exit | Quit the game |

---

## Features

### Turn-Based Battle System
- Each turn choose to **Attack**, use an **Item**, **Switch** Pokémon, or **Run**.
- 70% chance to successfully flee.
- Wild Pokémon counter-attacks each turn.
- Battle ends when either side faints or the player escapes.

### Type Effectiveness (Fire / Water / Earth)
- Fire beats Earth, Earth beats Water, Water beats Fire — dealing **1.5× damage**.
- The matchup is shown on screen each turn.

### Weather System
Each location has a fixed weather condition that boosts certain types by **1.2×**:

| Weather | Effect |
|---------|--------|
| Sunny | Boosts Fire-type moves |
| Rainy | Boosts Water-type moves |
| Sandstorm | Boosts Earth-type moves |
| Hail | Damages non-Water types |
| Clear | No special effects |

### Locations & Wild Pokémon
| Location | Weather | Wild Pokémon |
|----------|---------|--------------|
| Volcano | Sunny | Magmar (Fire) |
| Ocean | Rainy | Gyarados (Water) |
| Tundra | Hail | Glalie (Water) |
| Desert | Sandstorm | Sandslash (Earth) |
| Meadow | Clear | Fearow (Earth) |

### Pokémon Evolution
A Pokémon evolves after winning **3 battles**, permanently gaining:
- +20 Max HP
- +5 Attack
- +5 Defense

### Catching Pokémon
After defeating a wild Pokémon you can attempt to catch it using a Poké Ball from your inventory. Each ball tier has a different base catch rate:

| Ball | Catch Rate |
|------|-----------|
| Poké Ball | 40% |
| Great Ball | 60% |
| Ultra Ball | 80% |

Catch rate scales further based on the target's remaining HP and rarity.

### Item System
All items extend the abstract `Item` class:

| Item | Effect | Shop Price |
|------|--------|-----------|
| Health Potion | Restores +30 HP to one Pokémon | 20 coins |
| Attack Boost | +15 ATK for 3 turns | 30 coins |
| Poké Ball | Used to catch wild Pokémon | 50 coins |
| Great Ball | Higher catch rate | 20 coins |
| Ultra Ball | Even higher catch rate | 30 coins |
| Mystery Box | Grants 3 random rewards | 50 coins |

### Mystery Box
Opening a Mystery Box awards **3 random rewards**, each randomly chosen from:
- A random item (Health Potion, Attack Boost, or a Poké Ball)
- 20–70 bonus coins
- A stat buff: HP heal or a bonus battle victory (towards evolution)

**Free Mystery Boxes** can drop after any battle win if:
- Random 15% chance triggers, or
- The defeated wild Pokémon was Rare, or
- You won with any Pokémon below 25% HP.

### Score System
Scores are saved to `scores.txt` and the top 5 are displayed in the Scores menu.

Score per battle is calculated as:
- **Base:** 100 points
- **HP Bonus:** up to +50 points based on remaining HP
- **Difficulty Bonus:** based on the wild Pokémon's combined ATK + DEF
- **Turn Penalty:** −2 points per turn taken (minimum final score: 50)

---

## Class Overview

| Class | Responsibility |
|-------|---------------|
| `Game` | Main controller — game loop, shop, battle flow |
| `Player` | Manages the player's team, inventory, coins, and score |
| `Pokemon` | Pokémon stats, damage, healing, status effects, evolution |
| `Battle` | Turn-based battle logic, damage calculation, scoring |
| `Place` | Location with fixed weather and native wild Pokémon |
| `Weather` | Weather type and its in-battle effect description |
| `Item` | Abstract base class for all usable items |
| `HealthPotion` | Restores HP to a chosen Pokémon |
| `AttackBoost` | Temporarily raises a Pokémon's attack |
| `Pokeball` | Used to catch wild Pokémon; tiered catch rates |
| `MysteryBox` | Randomised multi-reward item |
| `ScoreManager` | Reads/writes `scores.txt`; displays high scores |

### OOP Concepts Demonstrated
- **Inheritance** — `HealthPotion`, `AttackBoost`, `Pokeball`, and `MysteryBox` all extend `Item`.
- **Abstraction** — `Item` declares the abstract `applyEffect()` method enforced by every subclass.
- **Polymorphism** — items are stored as `List<Item>` and dispatched via `applyEffect()` without casting.
- **Encapsulation** — all fields are `private`; state is accessed only through getters/setters.

