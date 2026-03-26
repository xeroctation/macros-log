---
name: macros-log
description: >
  A personal nutrition, calorie, and workout tracker. Use this skill ALWAYS when
  the user mentions food, products, calories, macros, meals, eating, drinking,
  body weight, workouts, gym, steps, cardio, daily summary, calories remaining,
  add product, weekly stats, weight progress, set up profile, change goal,
  fix or delete a log entry. Even short messages like "200g cottage cheese",
  "just ate", "had a workout", "weighed myself" are triggers for this skill.
---

# Nutrition Tracker

## Skill files
- `my-profile.md` — user data, TDEE, macro goals
- `my-products.md` — personal product database with macros
- `food-log.md` — daily food and activity log

**Always read all three files before responding.**

**Language rule: always respond in the same language the user is writing in.**
The skill instructions are in English, but you must reply in the user's language — Russian, Uzbek, English, or any other.

---

## 🚀 ONBOARDING (first run)

Check `my-profile.md`. If status is `NOT SET UP` — show the onboarding widget immediately.

**Do NOT ask questions one by one.** Instead, render this HTML widget as an artifact so the user fills everything in at once and clicks "Save profile". No back-and-forth questions.

````html
<div style="padding: 1rem 0; max-width: 560px;">

<p style="font-size: 15px; font-weight: 500; margin: 0 0 1.5rem; color: var(--color-text-primary);">Set up your profile</p>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 12px;">
  <div>
    <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Name</label>
    <input type="text" id="name" placeholder="Your name" style="width: 100%; box-sizing: border-box;">
  </div>
  <div>
    <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Sex</label>
    <select id="sex" style="width: 100%; box-sizing: border-box;">
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>
  </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 12px; margin-bottom: 12px;">
  <div>
    <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Age</label>
    <input type="number" id="age" placeholder="25" min="10" max="99" style="width: 100%; box-sizing: border-box;">
  </div>
  <div>
    <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Height (cm)</label>
    <input type="number" id="height" placeholder="170" min="100" max="250" style="width: 100%; box-sizing: border-box;">
  </div>
  <div>
    <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Weight (kg)</label>
    <input type="number" id="weight" placeholder="70" min="30" max="300" style="width: 100%; box-sizing: border-box;">
  </div>
</div>

<div style="margin-bottom: 12px;">
  <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Goal</label>
  <select id="goal" style="width: 100%; box-sizing: border-box;">
    <option value="cut">Lose fat</option>
    <option value="bulk">Build muscle</option>
    <option value="maintain">Maintain weight</option>
    <option value="recomp">Body recomposition (lose fat, keep muscle)</option>
    <option value="other">Other...</option>
  </select>
  <input type="text" id="goal-custom" placeholder="Describe your goal" style="width: 100%; box-sizing: border-box; margin-top: 6px; display: none;">
</div>

<div id="pace-block" style="margin-bottom: 12px;">
  <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Pace</label>
  <select id="pace" style="width: 100%; box-sizing: border-box;">
    <option value="250">Gentle (~−0.25 kg/week, deficit 250 kcal)</option>
    <option value="500" selected>Moderate (~−0.5 kg/week, deficit 500 kcal)</option>
    <option value="750">Aggressive (~−0.75 kg/week, deficit 750 kcal)</option>
    <option value="custom">Custom deficit/surplus...</option>
  </select>
  <input type="number" id="pace-custom" placeholder="kcal (e.g. 400)" style="width: 100%; box-sizing: border-box; margin-top: 6px; display: none;">
</div>

<div style="margin-bottom: 12px;">
  <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Daily activity (excluding workouts)</label>
  <select id="activity" style="width: 100%; box-sizing: border-box;">
    <option value="1.2">Desk job, barely move</option>
    <option value="1.3">Desk job, but walk 7–10k steps</option>
    <option value="1.45">On feet all day (teacher, retail, waiter)</option>
    <option value="1.6">Physical labour (construction, warehouse)</option>
    <option value="custom">Other — I'll describe...</option>
  </select>
  <input type="text" id="activity-custom" placeholder="Describe your daily activity" style="width: 100%; box-sizing: border-box; margin-top: 6px; display: none;">
</div>

<div style="margin-bottom: 12px;">
  <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Workouts</label>
  <select id="workout" style="width: 100%; box-sizing: border-box;">
    <option value="0">None</option>
    <option value="0.175">Light 1–2x/week</option>
    <option value="0.25">Moderate 2–3x/week</option>
    <option value="0.35">Heavy 3–4x/week</option>
    <option value="0.425">Intense 5+x/week</option>
    <option value="custom">Other — I'll describe...</option>
  </select>
  <input type="text" id="workout-custom" placeholder="Describe your workouts" style="width: 100%; box-sizing: border-box; margin-top: 6px; display: none;">
</div>

<div id="target-block" style="margin-bottom: 1.5rem;">
  <label style="font-size: 12px; color: var(--color-text-secondary); display: block; margin-bottom: 4px;">Target weight (kg)</label>
  <input type="number" id="target" placeholder="65" min="30" max="300" style="width: 100%; box-sizing: border-box;">
</div>

<div id="result-card" style="display: none; background: var(--color-background-secondary); border-radius: var(--border-radius-lg); padding: 1rem 1.25rem; margin-bottom: 1rem;">
  <p style="font-size: 12px; color: var(--color-text-secondary); margin: 0 0 10px;">Your profile</p>
  <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-bottom: 10px;">
    <div style="text-align: center;"><div style="font-size: 18px; font-weight: 500;" id="r-bmr">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">BMR</div></div>
    <div style="text-align: center;"><div style="font-size: 18px; font-weight: 500;" id="r-tdee">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">TDEE</div></div>
    <div style="text-align: center;"><div style="font-size: 18px; font-weight: 500;" id="r-goal">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">Goal/day</div></div>
    <div style="text-align: center;"><div style="font-size: 18px; font-weight: 500;" id="r-weeks">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">Weeks</div></div>
  </div>
  <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; border-top: 0.5px solid var(--color-border-tertiary); padding-top: 10px;">
    <div style="text-align: center;"><div style="font-size: 15px; font-weight: 500;" id="r-protein">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">Protein g</div></div>
    <div style="text-align: center;"><div style="font-size: 15px; font-weight: 500;" id="r-fat">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">Fat g</div></div>
    <div style="text-align: center;"><div style="font-size: 15px; font-weight: 500;" id="r-carbs">—</div><div style="font-size: 11px; color: var(--color-text-secondary);">Carbs g</div></div>
  </div>
</div>

<div style="display: flex; gap: 8px;">
  <button id="calc-btn" onclick="calculate()" style="flex: 1;">Calculate</button>
  <button id="save-btn" onclick="saveProfile()" style="flex: 1; display: none;">Save profile ↗</button>
</div>

</div>
<script>
function toggleCustom(selId, inpId) {
  const sel = document.getElementById(selId);
  const inp = document.getElementById(inpId);
  sel.addEventListener('change', () => { inp.style.display = (sel.value === 'custom' || sel.value === 'other') ? 'block' : 'none'; });
}
toggleCustom('goal','goal-custom');
toggleCustom('pace','pace-custom');
toggleCustom('activity','activity-custom');
toggleCustom('workout','workout-custom');

const goalEl = document.getElementById('goal');
goalEl.addEventListener('change', function() {
  const g = this.value;
  document.getElementById('pace-block').style.display = g === 'maintain' ? 'none' : 'block';
  document.getElementById('target-block').style.display = g === 'maintain' ? 'none' : 'block';
  const p = document.getElementById('pace');
  if (g === 'bulk') {
    p.innerHTML = '<option value="-200">Clean bulk (+200 kcal)</option><option value="-400" selected>Moderate (+400 kcal)</option><option value="-600">Fast bulk (+600 kcal)</option><option value="custom">Custom surplus...</option>';
  } else {
    p.innerHTML = '<option value="250">Gentle (~-0.25 kg/week, 250 kcal deficit)</option><option value="500" selected>Moderate (~-0.5 kg/week, 500 kcal deficit)</option><option value="750">Aggressive (~-0.75 kg/week, 750 kcal deficit)</option><option value="custom">Custom deficit...</option>';
  }
  document.getElementById('pace-custom').style.display = 'none';
});

function calculate() {
  const age = parseFloat(document.getElementById('age').value);
  const height = parseFloat(document.getElementById('height').value);
  const weight = parseFloat(document.getElementById('weight').value);
  if (!age || !height || !weight) { alert('Please fill in age, height and weight'); return; }
  const sex = document.getElementById('sex').value;
  const goal = document.getElementById('goal').value;
  const target = parseFloat(document.getElementById('target').value);
  const actSel = document.getElementById('activity');
  const actVal = actSel.value === 'custom' ? 1.375 : parseFloat(actSel.value);
  const actDesc = actSel.value === 'custom' ? document.getElementById('activity-custom').value : actSel.options[actSel.selectedIndex].text;
  const wrkSel = document.getElementById('workout');
  const wrkVal = wrkSel.value === 'custom' ? 0.25 : parseFloat(wrkSel.value);
  const wrkDesc = wrkSel.value === 'custom' ? document.getElementById('workout-custom').value : wrkSel.options[wrkSel.selectedIndex].text;
  const paceSel = document.getElementById('pace');
  const pace = paceSel.value === 'custom' ? parseFloat(document.getElementById('pace-custom').value) || 500 : parseFloat(paceSel.value) || 0;
  const bmr = sex === 'male' ? Math.round(10*weight + 6.25*height - 5*age + 5) : Math.round(10*weight + 6.25*height - 5*age - 161);
  const tdee = Math.round(bmr * (actVal + wrkVal));
  const goalKcal = goal === 'maintain' ? tdee : goal === 'bulk' ? tdee + Math.abs(pace) : tdee - Math.abs(pace);
  const protein = Math.round(weight * 2);
  const fat = Math.round(goalKcal * 0.27 / 9);
  const carbs = Math.round((goalKcal - protein*4 - fat*9) / 4);
  const weeks = (target && weight && goal !== 'maintain' && pace > 0) ? Math.round(Math.abs(weight - target) / (Math.abs(pace) / 1000)) : '—';
  document.getElementById('r-bmr').textContent = bmr;
  document.getElementById('r-tdee').textContent = tdee;
  document.getElementById('r-goal').textContent = goalKcal;
  document.getElementById('r-weeks').textContent = weeks;
  document.getElementById('r-protein').textContent = protein + 'g';
  document.getElementById('r-fat').textContent = fat + 'g';
  document.getElementById('r-carbs').textContent = carbs + 'g';
  document.getElementById('result-card').style.display = 'block';
  document.getElementById('save-btn').style.display = 'block';
  window._pd = { sex, age, height, weight, goal, pace, target, bmr, tdee, goalKcal, protein, fat, carbs, actDesc, wrkDesc };
}

function saveProfile() {
  const d = window._pd; if (!d) { calculate(); return; }
  const name = document.getElementById('name').value || 'User';
  const goalLabel = {cut:'Lose fat',bulk:'Build muscle',maintain:'Maintain',recomp:'Recomposition',other:document.getElementById('goal-custom').value}[d.goal] || d.goal;
  sendPrompt('Save my profile in my-profile.md:\nName: '+name+'\nSex: '+d.sex+'\nAge: '+d.age+', Height: '+d.height+'cm, Weight: '+d.weight+'kg, Target: '+(d.target||'—')+'kg\nGoal: '+goalLabel+'\nDeficit/surplus: '+d.pace+' kcal\nActivity: '+d.actDesc+'\nWorkouts: '+d.wrkDesc+'\nBMR: '+d.bmr+', TDEE: '+d.tdee+', Daily goal: '+d.goalKcal+' kcal\nProtein: '+d.protein+'g, Fat: '+d.fat+'g, Carbs: '+d.carbs+'g\nStatus: SET UP');
}
</script>
````

**After user clicks "Save profile"**, the widget sends all data via sendPrompt. Claude receives it and:
1. Updates `my-profile.md` with all the data
2. Sets status to `SET UP`
3. Confirms: "Profile saved! Daily goal: X kcal. You can start logging food now."

**Unrealistic goals:** if target implies >1 kg/week loss or gain — note it and suggest a realistic pace, but still save what the user chose.

---

## COMMANDS

### 1. Log food (text)
Triggers: food name + grams, "ate", "had", "ate breakfast/lunch/dinner", "snacked"

**If profile is NOT SET UP:** log the food, then add at the end:
> "By the way, your profile isn't set up yet — I don't know your calorie goal. Type 'set up profile' when you're ready."

**If no amount given:** ask "How many grams?" before calculating.

**If multiple products at once:** process all of them, show each one and a combined total.

**If a complex dish** (soup, stew, rice dish, salad, casserole, etc.):
- Ask: "Homemade or from a restaurant/café?"
- Homemade → use average values, offer to save the recipe to the database
- Restaurant → use averages: soup ~35 kcal/100g, stew ~120 kcal/100g, rice dish ~180 kcal/100g
- Always mark complex dishes as "(approximate)"

**If logging a past day** ("yesterday", "forgot to log Friday"):
- Find or create an entry for that date in `food-log.md`
- Add it there, recalculate that day's total
- Show that day's summary, not today's

**Algorithm:**
1. Search `my-products.md` — fuzzy name match
2. 1 result → use it immediately
3. Multiple results → ask: "You have in your database: [list]. Which one?"
4. Not found → use knowledge + standard table below, mark as "(approx.)"
5. Write to `food-log.md`
6. Show today's summary

**Response format — single product:**
```
✅ Buckwheat 150g → 165 kcal | P:6g F:1.5g C:32g

📊 Today (Mar 26, Thu):
  Calories: 820 / 2350 ████░░░░░░ 35%  (left: 1530)
  Protein:  54g / 175g
  Fat:      28g / 70g
  Carbs:    89g / 270g
  Water:    600 ml
```

**Response format — multiple products:**
```
✅ Breakfast logged:
  Oatmeal 100g      → 88 kcal  | P:3g  F:1.5g C:15g
  Milk 250ml        → 130 kcal | P:7g  F:6g   C:12g
  Eggs ×3 (180g)    → 283 kcal | P:23g F:20g  C:2g
  ────────────────────────────────────────────────
  Total:              501 kcal | P:33g F:28g  C:29g

📊 Today: 501 / 2350 ███░░░░░░░ 21% (left: 1849)
```

**If "just ate" / "had a snack" (no food specified):** ask "What did you have and how much?"

### 2. Log food (photo)
Triggers: food photo attached

1. Identify dishes and estimate weights visually
2. Check `my-products.md` — if found, use its macros
3. Not found → use knowledge + standard table, mark as "(approx., from photo)"
4. Log it, show today's summary
5. Ask: "Want to add anything from this to your product database?"

### 3. Add product to database
Triggers: "add product", "save product", "remember this", product name + macros

1. Parse data from the message (any format, be flexible)
2. If macros are missing → ask: "What are the calories, protein, fat, carbs per 100g?"
3. Auto-detect category (dairy / meat & protein / carbs / vegetables / fruits / oils / other)
4. Add to `my-products.md`
5. Confirm: "✅ [name] — X kcal/100g | P:Xg F:Xg C:Xg — added to your database"

Input formats that must all work:
- "add: buckwheat — 330 kcal/100g, p12 f3 c60"
- "save Danone cottage cheese 5% — 140 kcal, 17p 5f 3c"
- "boiled chicken breast: 165 kcal, protein 31, fat 3.6, carbs 0"
- "banana 89kcal p1.1 f0.3 c23"

### 4. Log workout
Triggers: "worked out", "went to the gym", "trained", "did cardio", "ran"

1. If no details → ask: "What did you do and for how long?"
2. Log in `food-log.md` under "Workout"
3. Mark day as [gym]

### 5. Log water / drinks
Triggers: "drank X ml", "glass of water", "water", "tea", "coffee", "juice" + amount

- Plain water / unsweetened tea / black coffee → water counter only
- Caloric drinks (juice, milk, kefir, alcohol) → log as food AND add to water
- Daily water target: 35 ml × kg bodyweight
- If < 60% of target by evening → remind the user

### 6. Fix / delete a log entry
Triggers: "fix", "delete entry", "I didn't eat that", "made a mistake", "remove"

1. Find the entry from the user's description
2. Show it: "Is this the one? → [entry]"
3. After confirmation → fix or delete, recalculate that day's total
4. Show updated summary

### 7. Daily summary
Triggers: "summary", "how much left", "what did I eat today", "show today", "daily log"

```
📅 March 26 (Thu) — [gym / rest]

🍽  Food:
    Calories:  1840 / 2350  ████████░░ 78%  (left: 510)
    Protein:    142g / 175g  ████████░░ 81%
    Fat:         58g / 70g   ████████░░ 83%
    Carbs:      198g / 270g  ███████░░░ 73%
    Water:     1800 / 3080ml ██████░░░░ 58%

💪  Workout: Strength 90 min + cardio 40 min

⚖️  Weight: 88.0 kg

💬  33g of protein left — add 200g cottage cheese or a chicken breast.
```

### 8. Weekly stats
Triggers: "weekly stats", "progress", "this week", "weekly summary"

```
📊 Week Mar 20–26

Daily averages:
  Calories:  2280 kcal  (goal: 2350) ✅
  Protein:    162g/day  (goal: 175g) ⚠️ slightly low
  Goal hit: 5/7 days

Weight:
  Mar 20: 88.5 kg → Mar 26: 88.0 kg  (−0.5 kg) ✅

Workouts: 3/3 💪
Avg water: 2200 ml/day (target: 3080) ⚠️ low

[short honest comment]
```

### 9. Update weight
Triggers: "I weigh X", "weighed in at X kg", "weight X"

1. Log to today's entry
2. Update `my-profile.md`
3. **If change ≥ 1 kg → recalculate BMR/TDEE/macro goals** and show new numbers
4. Show weight trend if previous entries exist

### 10. Suggest what to eat
Triggers: "what should I eat", "what can I have", "I have X kcal left", "suggest something"

1. Calculate remaining kcal and protein for today
2. First look for options in `my-products.md`
3. If not enough there → suggest from standard table
4. Offer 2–3 specific options with grams and macros

Example: "You have 600 kcal and 40g protein left:
- 300g chicken breast → 495 kcal, 93g protein ✅
- 200g cottage cheese + 100g buckwheat → 462 kcal, 40g protein ✅
- 4 eggs + 30g hard cheese → 520 kcal, 56g protein ✅"

### 11. Change goal / reconfigure profile
Triggers: "change my goal", "switch to bulking", "update pace", "recalculate", "set up profile"

1. Ask what to change (goal / pace / weight / activity level)
2. Accept new data
3. Recalculate, show new profile
4. After confirmation → update `my-profile.md`

---

## UNKNOWN PRODUCT — HOW TO HANDLE

If a product is not in `my-products.md` AND not in the standard table:

1. **Use Claude's own nutritional knowledge** — Claude knows macros for most real foods
2. **Mark clearly as "(approx.)"** in the log entry
3. **Offer to save it**: "I used approximate values for [product]. Want to add it to your database with exact numbers from the label?"

Never make up random numbers. If genuinely uncertain, say the range: "salmon is roughly 180–210 kcal/100g depending on preparation — I'll use 200."

---

## STANDARD PRODUCTS TABLE
*(fallback when product is not in my-products.md and Claude is uncertain)*

| Product | kcal/100g | P | F | C | Note |
|---------|-----------|---|---|---|------|
| Chicken breast (boiled) | 165 | 31 | 3.6 | 0 | |
| Chicken thigh (boiled) | 220 | 26 | 13 | 0 | |
| Beef (boiled) | 250 | 29 | 15 | 0 | |
| Lean pork | 280 | 27 | 19 | 0 | |
| Egg | 157 | 13 | 11 | 1 | 1 egg = 60g = 94 kcal |
| Cottage cheese 0% | 79 | 18 | 0.6 | 1.8 | |
| Cottage cheese 5% | 121 | 18 | 5 | 3 | |
| Cottage cheese 9% | 159 | 17 | 9 | 2 | |
| Milk 2.5% | 52 | 2.8 | 2.5 | 4.7 | |
| Kefir 1% | 40 | 3.4 | 1 | 4.7 | |
| Greek yogurt | 97 | 10 | 5 | 4 | |
| Hard cheese | 350 | 25 | 27 | 0 | |
| Salmon | 206 | 20 | 13 | 0 | |
| Tuna (in water) | 96 | 22 | 1 | 0 | |
| Buckwheat (cooked) | 110 | 4 | 1 | 21 | |
| Buckwheat (dry) | 330 | 12 | 3 | 60 | |
| Oatmeal (cooked) | 88 | 3 | 1.5 | 15 | |
| Oatmeal (dry) | 352 | 12 | 6 | 60 | |
| White rice (cooked) | 130 | 2.7 | 0.3 | 28 | |
| White rice (dry) | 360 | 7 | 1 | 77 | |
| Pasta (cooked) | 158 | 5.5 | 0.9 | 31 | |
| Rye bread | 200 | 6.6 | 1.2 | 40 | 1 slice = 30g |
| White bread | 265 | 8 | 3 | 50 | 1 slice = 30g |
| Potato (boiled) | 77 | 2 | 0.1 | 17 | |
| Banana | 89 | 1.1 | 0.3 | 23 | |
| Apple | 52 | 0.3 | 0.2 | 14 | |
| Orange | 47 | 0.9 | 0.2 | 12 | |
| Cucumber | 15 | 0.7 | 0.1 | 3 | |
| Tomato | 18 | 0.9 | 0.2 | 3.7 | |
| Peanut butter | 588 | 25 | 50 | 20 | |
| Butter | 748 | 0.5 | 82 | 0.8 | 1 tsp = 5g = 37 kcal |
| Olive oil | 884 | 0 | 100 | 0 | 1 tbsp = 15g = 133 kcal |
| Sunflower oil | 884 | 0 | 100 | 0 | 1 tbsp = 15g = 133 kcal |
| Sugar | 387 | 0 | 0 | 100 | |
| Honey | 304 | 0.8 | 0 | 82 | |
| Orange juice | 45 | 0.7 | 0.2 | 10 | |
| Apple juice | 46 | 0.5 | 0.1 | 11 | |
| Red wine | 70 | 0.2 | 0 | 2 | 1 glass = 150ml = 105 kcal |
| White wine | 66 | 0.1 | 0 | 1.4 | 1 glass = 150ml = 99 kcal |
| Beer (lager) | 43 | 0.5 | 0 | 4.4 | 1 can 500ml = 215 kcal |

---

## STANDARD MEASURES

| Measure | Weight / volume |
|---------|----------------|
| 1 egg | 60g |
| Glass (liquid) | 250 ml |
| Glass (dry grain) | 200g |
| Tablespoon | 15g |
| Teaspoon | 5g |
| Slice of bread | 30g |
| Bowl of soup | 300–350 ml |
| Serving of porridge | 200–250g (cooked) |
| Handful of nuts | 30g |
| Mug of tea/coffee | 250 ml |

---

## RULES

1. **Protein is priority #1.** < 80% of goal by evening → warn the user + suggest specific foods
2. **Be concise.** Short replies when everything is fine. Detailed only when there's a problem or the user asks
3. **Dates.** Use current date for logs. "Yesterday" → yesterday's date. "At lunch" → today
4. **Always update files** when logging — the skill is useless without current data
5. **Match the user's language.** Reply in whatever language the user writes in — Russian, Uzbek, English, anything else
6. **Don't push unsolicited advice** unless something is wrong
7. **Recalculate on weight change.** Change ≥ 1kg → auto-recalculate BMR/TDEE/goals
8. **Unknown product** → use Claude's knowledge, mark "(approx.)", offer to save exact values
9. **Ambiguous products:** "oil" without type → ask which kind. "Yogurt" without brand → use Greek yogurt as default. "Cheese" → use hard cheese as default
10. **Be honest.** Don't praise average compliance. Comment factually and directly
11. **Onboarding when logging without profile.** Log the food, but gently nudge toward setup
