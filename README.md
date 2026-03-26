# 🥗 Nutrition Tracker Skill

A personal nutrition, calorie, and workout tracker skill for Claude Code and other SKILL.md-compatible AI assistants.

Track your food, macros, workouts, and weight — all in plain text files, no apps needed.

---

## ✨ Features

- **Smart onboarding** — calculates your BMR, TDEE, and macro goals on first run
- **Food logging** — text or photo, single product or full meal at once
- **Personal product database** — save your go-to products with exact macros, add new ones in one message
- **Unknown products** — Claude uses its own knowledge as fallback, marks as "(approx.)"
- **Daily summary** — calories and macros left, progress bars, water tracker
- **Workout logging** — gym sessions, cardio, any activity
- **Weekly stats** — weight trend, average calories, goal compliance
- **Fix entries** — edit or delete a logged item
- **"What should I eat?"** — suggests foods based on what's left in your daily budget
- **Weight update with auto-recalculation** — change ≥ 1 kg recalculates TDEE and goals
- **Goal change** — switch between cutting, bulking, maintaining anytime
- **Multilingual** — responds in the user's language (English, Russian, Uzbek, etc.)

---

## 🚀 Installation

### Claude Code
```bash
# Option 1: personal (all projects)
git clone https://github.com/YOUR_USERNAME/macros-log ~/.claude/skills/macros-log

# Option 2: project-level
git clone https://github.com/YOUR_USERNAME/macros-log .claude/skills/macros-log
```

### OpenAI Codex CLI
```bash
git clone https://github.com/YOUR_USERNAME/macros-log ~/.codex/skills/macros-log
```

### Claude.ai (web/mobile)
Download the `.skill` file from [Releases](../../releases) and install via Settings → Skills.

---

## 💬 Usage examples

The skill activates automatically when you mention food, calories, workouts, or weight. No slash commands needed.

**First run — onboarding:**
```
You: hi, want to track my nutrition
Skill: Hi! I'm your nutrition tracker. What's your name?
```

**Log a meal:**
```
You: had breakfast: 3 eggs, 100g oatmeal, 250ml milk
Skill: ✅ Breakfast logged:
  Eggs ×3 (180g)  → 283 kcal | P:23g F:20g C:2g
  Oatmeal 100g    → 88 kcal  | P:3g  F:1.5g C:15g
  Milk 250ml      → 130 kcal | P:7g  F:6g   C:12g
  ─────────────────────────────────────────
  Total:            501 kcal | P:33g F:28g  C:29g

📊 Today: 501 / 2350 ███░░░░░░░ 21% (left: 1849)
```

**Add a product to your database:**
```
You: add product: Best cottage cheese — 150 kcal/100g, p14 f8 c4
Skill: ✅ Best cottage cheese — 150 kcal/100g | P:14g F:8g C:4g — added to your database
```

**Daily summary:**
```
You: summary
Skill: 📅 March 26 (Thu) — gym
  Calories:  1840 / 2350  ████████░░ 78%  (left: 510)
  Protein:    142g / 175g  ████████░░ 81%
  ...
```

**Suggest what to eat:**
```
You: what can I eat for dinner? 600 kcal and 40g protein left
Skill: Here are some options:
  - 300g chicken breast → 495 kcal, 93g protein ✅
  - 200g cottage cheese + 100g buckwheat → 462 kcal, 40g protein ✅
```

---

## 📁 File structure

```
macros-log/
├── SKILL.md          # Skill instructions for Claude
├── my-profile.md     # Your physical data, TDEE, macro goals
├── my-products.md    # Your personal product database
└── food-log.md       # Daily food and activity log
```

All data is stored in plain Markdown files — readable, editable, portable.

---

## 🌍 Compatibility

| Platform | Status |
|----------|--------|
| Claude Code | ✅ |
| OpenAI Codex CLI | ✅ |
| Claude.ai (web/mobile) | ✅ |
| Other SKILL.md-compatible assistants | ✅ |

---

## 📄 License

MIT — use freely, modify, share.
