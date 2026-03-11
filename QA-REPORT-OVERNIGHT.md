# Mow Money QA Report — Overnight 2026-03-10

## QA Cycle 1 (10:45 PM CDT)

### Testing Environment
- Chrome browser, 390×844 viewport (iPhone simulation)
- URL: mowmoney.hooteye.com (v3.3.1)
- Fresh game start as "QA Tester"

### ✅ Working Well
1. **Title screen** — Clean, loads fast
2. **Tutorial** — Shows on first game, 6 steps, skip works
3. **Dashboard** — Player name shown ("Hey QA Tester"), stats cards clear and readable
4. **Competitor section** — 3 competitors with avatars, threat levels, stats
5. **Jobs screen** — Contract cards show customer name, address, yard type, difficulty, gas estimate, satisfaction
6. **Bottom nav** — 7 tabs (Home, Jobs, Shop, Crew, Skills, Map, Stats) all accessible
7. **Mowing HUD** — Health bar, % mowed, timer, yard name all visible and clear
8. **Yard rendering** — Scaled correctly (Large Yard = 88% of screen), house/fence/obstacles rendered
9. **Auto-edged borders** — Pre-cut grass visible around edges (~16% coverage at start)
10. **Throttle slider** — Visible on right side, labeled "SPD"
11. **Beezer blocked on Week 1-2** — ✅ Fixed (was showing before)
12. **Bonus Run card** — Visible on dashboard

### 🐛 Bugs Found

#### CRITICAL: Mower can spawn on/near obstacles
- Mower spawns at center of yard (yardW/2, yardH*0.6)
- If an obstacle is at that position, mower starts stuck
- Collision constantly triggers, preventing movement
- **Fix:** Check spawn position against obstacles and nudge if overlapping

#### HIGH: Mower movement feels slow/stuck on Large Yards
- With Toro starter mower: very slow, hard to cover ground
- 14px grass cells + base speed 4.5 means fewer cells to cut but mower feels sluggish
- After 35 seconds of holding ArrowUp, only went from 16% to 17%
- The collision boundary fix helped but movement still feels off on larger yards
- **Suggestion:** Increase base speed to 6-7, or reduce grass cells to 12px

#### MEDIUM: Joystick invisible on iOS
- Touch area exists (50% width, 60% height, bottom-left) but no visible indicator
- Dynamic joystick base appears on touch, but first-time users don't know where to touch
- **Suggestion:** Show a subtle ghost/hint indicator on the left side when mowing starts

#### LOW: 7 nav tabs may be too many for small screens
- Home, Jobs, Shop, Crew, Skills, Map, Stats all visible
- On 390px width, some tab labels might get cramped
- Works OK in desktop simulation but should verify on actual iPhone

#### LOW: Weekly costs ($274) > Weekly revenue ($349) on week 1
- Starting with 3 contracts but high expenses (mower loan, gas, insurance)
- New players might feel underwater immediately
- Not a bug, but gameplay balance question

### 📝 Gameplay Observations
1. Auto-edged borders work great — starts you at 16% and focuses gameplay on the interior
2. Dashboard is information-rich but may feel overwhelming on first play
3. Competitor section on dashboard takes a lot of vertical space
4. The "Mow 3 remaining yards first" button at bottom of dashboard isn't very discoverable
5. Contract cards look professional — nice touch with the address/difficulty/gas breakdown

### 🔧 Recommended Fixes (Priority Order)
1. Fix mower spawn collision (check obstacles, nudge mower to clear spot)
2. Increase mower base speed by 30-40%
3. Add joystick hint indicator (ghost circle on left side)
4. Test on actual iPhone for touch responsiveness
5. Consider collapsing competitor section on dashboard by default
