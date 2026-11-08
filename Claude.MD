# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Cloud Cost Quest – The Road to 100% Cloud Efficiency** is a browser-based HTML5 Snakes and Ladders game developed for CenITex Connect, an organisation-wide customer demonstration event.

The game demonstrates FinOps principles and the importance of continuously managing and optimising cloud consumption across AWS, Azure, OCI and VMware environments.

The game uses a familiar Snakes and Ladders concept to make cloud financial management engaging and accessible to both technical and non-technical customers.

**Core message:**

"Spend smarter. Not just less. Make every cloud dollar count."

### Objectives

- Create a fun, interactive and visually appealing FinOps game.
- Demonstrate common cloud cost inefficiencies and optimisation opportunities.
- Make FinOps concepts understandable without requiring technical knowledge.
- Keep gameplay to approximately 60–90 seconds, with the complete experience taking 1–3 minutes.
- Provide an engaging customer experience suitable for CenITex Connect demonstrations.
- Run directly in a browser without backend or installation dependencies.

## Project Status

This is a new game development project.

Development priorities:

1. Implement the complete Snakes and Ladders game mechanics.
2. Incorporate FinOps snakes, ladders and interactive event cards.
3. Add CenITex Connect branding and visual polish.
4. Implement responsive desktop and touchscreen support.
5. Add optional enhancements such as sound and local high scores.

## Commands

### Running the Game

Open the game directly in a browser:
```bash
# Open in default browser (Windows)
start index.html

# Or open in specific browser
chrome.exe index.html
msedge.exe index.html
```

### Testing

Manual testing in browser:
- Open browser DevTools (F12) to check for console errors
- Test all game flows from welcome to completion
- Verify animations and transitions
- Test on different screen sizes using browser DevTools responsive mode

### Development

For local development with live reload (optional):
```bash
# If using Python's built-in server
python -m http.server 8000
# Then open http://localhost:8000

# If using Node.js http-server
npx http-server -p 8000
```

Note: The game runs entirely in the browser and requires no build process.

## File Structure

Keep the structure simple with no subfolders:

```
Snakes-Ladder-Connect/
├── index.html              # Main game file (self-contained HTML, CSS, JS)
├── CLAUDE.md               # This file
└── README.md               # User-facing documentation (optional)
```

**Implementation:** Single `index.html` file with inline CSS and JavaScript. All game logic, styling, and configuration should be contained within this one file.

## Architecture

### Technology Stack

Use:
- HTML5.
- CSS3.
- Vanilla JavaScript.
- HTML5 Canvas or CSS-based board rendering.

Choose the simplest approach that delivers a polished and maintainable game.

Avoid unnecessary frameworks, backend services, databases, authentication and external APIs.

### Implementation Approach

Prefer a single self-contained HTML file containing HTML, CSS and JavaScript.

Separate files are acceptable if they improve maintainability without introducing unnecessary complexity.

Keep game logic separate from visual rendering and UI handling.

Suggested logical components:

- GameController
- GameBoard
- Player
- DiceManager
- MovementManager
- SnakeAndLadderManager
- EventCardManager
- ScoreManager
- UIManager

Keep the implementation simple and avoid unnecessary abstraction.

---

## Game Concept and Mechanics

### 1. Game Objective

The objective is to navigate a 100-square Snakes and Ladders board and reach square 100, representing the completion of the Cloud Cost Quest.

Players roll a dice and move across the board.

- Landing on a ladder moves the player forward.
- Landing on a snake moves the player backwards.
- Landing on a designated event square triggers an interactive FinOps event card.
- The first player to reach square 100 wins.

The game should use a traditional Snakes and Ladders movement pattern.

### 2. Game Board

Create a colourful 10 × 10 board containing 100 numbered squares.

Board requirements:
- Number squares sequentially from 1 to 100.
- Use the traditional alternating left-to-right and right-to-left numbering pattern.
- Display snakes and ladders visually across the board.
- Display a player token clearly.
- Highlight the current player position.
- Provide visually distinct colours for snakes, ladders and special event squares.
- Ensure all square numbers remain readable.

The board should have a modern cloud-themed appearance rather than looking like a children's board game.

Use subtle cloud, currency, server and financial optimisation graphics where appropriate.

### 3. Player

Implement single-player gameplay initially.

The player should be represented by a friendly cloud-themed character or mascot.

Player behaviour:
- Starts at square 1.
- Moves according to the dice result.
- Animates movement across the board.
- Automatically climbs ladders.
- Automatically slides down snakes.
- Displays the current position clearly.

Use smooth animations when moving between squares.

The game should feel responsive and rewarding.

### 4. Dice

Implement a virtual six-sided dice.

Requirements:
- Dice generates a random value between 1 and 6.
- Include a Roll Dice button.
- Animate the dice when rolled.
- Display the resulting number clearly.
- Prevent multiple rolls while an animation or player movement is in progress.
- Automatically move the player after the dice result is generated.

The dice should be large and visually prominent.

### 5. Board Movement

Implement traditional Snakes and Ladders rules.

- Players move forward based on the dice result.
- Landing on a ladder moves the player to its destination square.
- Landing on a snake moves the player to its lower destination square.
- Display a short notification explaining the snake or ladder event.
- Ensure player movement and special movements are animated.
- Do not allow the player to move beyond square 100.

**Winning rule:** The player must roll the exact number required to reach square 100. If the dice result would take the player beyond 100, the player remains in the current position and must roll again.

Example: At position 97, player needs to roll exactly 3 to win. Rolling 4, 5, or 6 means staying at 97.

This rule should be easily configurable via `GAME_CONFIG.rules.exactToWin = true/false`.

---

## FinOps Game Content

The game must communicate practical FinOps principles through snakes, ladders and event cards.

### 6. Snakes – Cloud Cost Inefficiencies

Snakes represent inefficient cloud consumption and poor financial management practices.

Implement the following snake events:

| Inefficiency | Description |
|---|---|
| Idle Instances | Leaving development and test instances running overnight or during weekends. |
| Overprovisioned Workloads | Running oversized EC2 instances, Azure VMs or OCI compute resources. |
| No Autoscaling | Paying for maximum capacity even when workload demand is low. |
| Orphaned Resources | Unattached disks, unused IP addresses, abandoned snapshots and forgotten resources. |
| No Commitment Discounts | Not considering Savings Plans, Reserved Instances or equivalent commitment-based pricing for predictable workloads. |
| Wrong Storage Tier | Keeping infrequently accessed data in expensive high-performance storage. |
| Excessive Data Transfer | Poor architecture causing unnecessary cross-region or cross-zone data transfer charges. |
| No Cost Governance | Lack of cost controls, budgets, ownership and accountability. |
| Uncontrolled Consumption | Resources being provisioned without sufficient cost oversight or review. |

When a player lands on a snake:
- Animate the player sliding down.
- Display the inefficiency name.
- Show a short explanation.
- Show how many squares were lost.
- Provide a clear visual indication of the negative outcome.

Use negative visual styling such as red or orange.

### 7. Ladders – FinOps Efficiencies

Ladders represent positive FinOps practices that improve cloud cost efficiency.

Implement the following ladder events:

| Efficiency | Description |
|---|---|
| Automated Shutdown | Automatically shutting down non-production workloads outside business hours. |
| Rightsizing | Matching compute resources to actual utilisation and performance requirements. |
| Autoscaling | Dynamically scaling resources based on workload demand. |
| Savings Plans and Reservations | Using commitment-based pricing for predictable workloads. |
| Storage Lifecycle Management | Moving data automatically to lower-cost storage tiers based on access patterns. |
| Cost Visibility and Tagging | Implementing consistent tagging, budgets and cost allocation across teams and applications. |
| Continuous Optimisation | Regularly reviewing resource utilisation and implementing cost optimisation recommendations. |
| FinOps Ownership | Encouraging teams to take responsibility for their cloud consumption. |
| Architecture Optimisation | Selecting appropriate cloud services and architectures to avoid unnecessary costs. |
| Forecasting and Budgets | Establishing budgets and identifying unexpected spending early. |

When a player lands on a ladder:
- Animate the player climbing upwards.
- Display the efficiency name.
- Show a short explanation.
- Show how many squares were gained.
- Provide a clear visual indication of the positive outcome.

Use positive visual styling such as green or blue.

---

## 8. Suggested Snake and Ladder Positions

Use the following initial positions to create a balanced game.

| Type | Start | Destination | Event |
|---|---:|---:|---|
| Ladder | 4 | 18 | Automated Shutdown |
| Snake | 23 | 7 | Idle Instances |
| Ladder | 9 | 31 | Rightsizing |
| Snake | 34 | 16 | Overprovisioning |
| Ladder | 21 | 42 | Autoscaling |
| Snake | 48 | 26 | No Commitment Discounts |
| Ladder | 40 | 59 | Storage Optimisation |
| Snake | 62 | 45 | Orphaned Resources |
| Ladder | 51 | 72 | Cost Visibility and Tagging |
| Snake | 78 | 55 | No Cost Governance |
| Ladder | 71 | 91 | Continuous Optimisation |
| Snake | 95 | 75 | Uncontrolled Consumption |

These positions are initial configuration values and may be adjusted to improve gameplay balance.

Requirements:
- Ensure ladders always move upwards.
- Ensure snakes always move downwards.
- Prevent overlapping or visually confusing board elements.
- Avoid placing multiple events on the same square.
- Keep the board balanced so players have a reasonable chance of completing the game within the target duration.

All snake and ladder positions should be configurable centrally rather than hardcoded into game logic.

---

## 9. FinOps Event Cards

Introduce interactive FinOps event cards to add variety and educational value.

Certain board squares should be designated as event squares.

When the player lands on an event square:
- Display a visually engaging event card.
- Show whether the event is positive or negative.
- Display a short scenario.
- Explain the financial or operational impact.
- Apply the corresponding movement bonus or penalty.
- Provide a Continue button.

Event cards should be short enough to read within 5–8 seconds.

### Positive Event Examples

**Event: Automated Shutdown**

Status: Good Decision

"Your development environment now shuts down automatically every evening and over weekends. Great work reducing unnecessary compute consumption!"

Action: Move forward 5 squares.

**Event: Rightsizing Success**

Status: Cost Optimisation

"You reviewed workload utilisation and reduced oversized virtual machine instances. You're getting more value from your cloud spend!"

Action: Move forward 4 squares.

**Event: FinOps Ownership**

Status: Great Practice

"Your application teams now understand and take responsibility for their cloud consumption."

Action: Move forward 5 squares.

### Negative Event Examples

**Event: Forgotten Resources**

Status: Cost Inefficiency

"You discovered 15 unattached disks still generating charges. Time to clean up your cloud environment!"

Action: Move backwards 5 squares.

**Event: Unexpected Cloud Bill**

Status: Cost Alert

"Your monthly cloud expenditure exceeded budget because nobody was monitoring consumption."

Action: Move backwards 4 squares.

**Event: Overprovisioned Environment**

Status: Missed Opportunity

"Your application is running on oversized compute instances despite consistently low utilisation."

Action: Move backwards 5 squares.

### Event Card Configuration

- Store event card content centrally.
- Support multiple positive and negative events.
- Allow event positions and movement adjustments to be configured.
- Avoid repetitive messages during a single game where practical.
- Ensure event cards do not cause infinite movement loops.
- Keep event interactions optional and quick enough to maintain the 1–3 minute game duration.

---

## 10. Game Flow and User Interface

### Welcome Screen

Display:
- Game title: CLOUD COST QUEST.
- Subtitle: THE ROAD TO 100% CLOUD EFFICIENCY.
- CenITex Connect branding.
- Short introduction.
- Start Game button.

Suggested introduction:

"Can you achieve cloud cost efficiency?

Roll the dice, climb the ladders of good FinOps practices and avoid the snakes of cloud cost inefficiencies. Your goal is to reach 100!"

### Instructions Screen

Display simple instructions:

1. Roll the dice.
2. Move across the board.
3. Climb ladders to improve cost efficiency.
4. Avoid snakes that represent unnecessary cloud expenditure.
5. Watch out for FinOps event cards.
6. Reach square 100 to complete your Cloud Cost Quest.

Include a Start Game button.

### Gameplay Screen

Display:
- 10 × 10 game board.
- Player character and current position.
- Large animated dice.
- Roll Dice button.
- Current position indicator.
- Brief event notifications.
- Game title or branding.

The player should be able to understand what is happening without needing additional instructions.

### Game Over / Results Screen

When the player reaches square 100, display a celebratory completion screen.

Include:
- Mission Completed message.
- Final position: 100/100.
- Number of ladders climbed.
- Number of snakes encountered.
- Positive FinOps practices encountered.
- Cost inefficiencies encountered.
- Total dice rolls.
- Play Again button.
- Return to Welcome Screen button.

### Final Completion Message

Display:

"100% CLOUD COST QUEST!

Congratulations! You've completed your journey towards cloud cost efficiency.

You've navigated the challenges, avoided unnecessary cloud expenditure and discovered the value of FinOps.

Spend smarter. Not just less."

Include a final educational message:

"FinOps is a continuous journey of visibility, accountability and optimisation. The goal isn't simply to spend less, but to maximise the value of every cloud dollar."

Important: 100% represents completion of the game, not a claim that real-world cloud costs can be optimised to 100%.

---

## 11. Visual Design and Branding

### Design Style

Use a modern, colourful and polished board-game aesthetic.

The game should look professional enough for a customer-facing demonstration while remaining fun and approachable.

Suggested design:
- Colourful 10 × 10 board.
- Modern cloud-themed graphics.
- Friendly cloud player mascot.
- Visually distinctive snakes and ladders.
- Animated dice.
- Smooth player movement.
- Positive and negative event card styling.
- Celebration effects when reaching square 100.

Use green or blue for positive FinOps practices and orange or red for cost inefficiencies.

Avoid excessive text and visual clutter.

### CenITex Connect Branding

Support configurable:
- CenITex Connect event name.
- Organisation logo.
- Organisation branding and colours.
- AWS, Azure, OCI and VMware references.

Use placeholders where actual logos are unavailable.

Branding should be configurable without changing game logic.

### Responsive Layout

Support:
- Standard 16:9 desktop browsers.
- Laptop screens.
- Large touchscreen displays.

Requirements:
- No vertical scrolling during gameplay.
- Board numbers must remain readable.
- Dice and controls must be easy to interact with.
- Layout must adapt to different screen sizes.

---

## 12. Technical Requirements

### Browser Support

Support current versions of:
- Google Chrome.
- Microsoft Edge.

### Performance

- Smooth animations.
- Minimal loading time.
- No unnecessary network requests.
- No significant CPU usage when idle.
- Responsive to browser resizing.
- Restart without refreshing the browser.

### Configuration

All game configuration should be defined in a single JavaScript object at the top of the game logic:

```javascript
const GAME_CONFIG = {
  board: {
    size: 100,
    rows: 10,
    cols: 10
  },
  snakes: [
    { start: 23, end: 7, name: "Idle Instances", description: "..." },
    // ... more snakes
  ],
  ladders: [
    { start: 4, end: 18, name: "Automated Shutdown", description: "..." },
    // ... more ladders
  ],
  eventCards: [
    { position: 15, type: "positive", title: "...", description: "...", movement: 5 },
    // ... more events
  ],
  branding: {
    title: "CLOUD COST QUEST",
    subtitle: "THE ROAD TO 100% CLOUD EFFICIENCY",
    eventName: "CenITex Connect",
    logoUrl: ""
  },
  animations: {
    diceRollDuration: 800,
    playerMoveDuration: 300,
    snakeSlideDuration: 600,
    ladderClimbDuration: 600
  },
  rules: {
    exactToWin: true,  // Must roll exact number to reach 100
    startPosition: 1
  },
  sounds: {
    enabled: false,
    muted: true
  }
};
```

Avoid hardcoding configuration values throughout the game logic. All game content and behavior should reference this central configuration object.

### Security and Privacy

The game must:
- Run entirely in the browser.
- Not connect to real cloud environments.
- Not make AWS, Azure, OCI or VMware API calls.
- Not require cloud credentials.
- Not collect customer information.
- Not transmit player data externally.
- Not use external analytics.
- Not require internet connectivity during gameplay.

All cloud scenarios must be fictional game representations.

---

## 13. Optional Enhancements

Implement only after the core game is complete.

### Sound Effects
- Dice rolling.
- Ladder climbing.
- Snake sliding.
- Event card notifications.
- Winning celebration.

Provide a mute toggle. Do not autoplay audio before user interaction.

### Fullscreen
Provide a fullscreen option for large CenITex Connect displays.

### Local High Scores
Optionally maintain a local record of:
- Fastest completion time.
- Fewest dice rolls.
- Highest number of positive events encountered.

Use browser storage only. Do not introduce backend dependencies.

### Cloud Provider Branding
Optionally display AWS, Azure, OCI and VMware references throughout the game to reinforce the multi-cloud context.

---

## 14. Acceptance Criteria

The game is considered complete when:

1. Welcome and instructions screens work correctly.
2. A 10 × 10 board displays all 100 numbered squares.
3. Traditional alternating board numbering is implemented.
4. The player starts at square 1.
5. Dice rolls generate values between 1 and 6.
6. Player movement follows dice results correctly.
7. Snakes move players backwards.
8. Ladders move players forwards.
9. Snake and ladder movements are animated.
10. Event cards display the correct FinOps scenarios and apply their movement adjustments.
11. The player cannot move beyond square 100.
12. The player wins when reaching square 100 under the configured winning rule.
13. The results screen displays game statistics and the completion message.
14. The game can be restarted without refreshing the browser.
15. Animations and interactions work smoothly.
16. The game works on Chrome and Edge.
17. The game works locally without internet connectivity.
18. The complete experience takes approximately 1–3 minutes.
19. The benefits of FinOps and cloud cost optimisation are clearly communicated.
20. No browser console errors occur during normal gameplay.

---

## 15. Quick Testing Checklist

Before considering a development phase complete, verify:

**Phase 1 - Core Game:**
- [ ] Game loads without console errors
- [ ] Dice generates values 1-6 consistently
- [ ] Player moves the correct number of squares
- [ ] Board numbering follows alternating pattern (1-10 L→R, 11-20 R→L, etc.)
- [ ] Snakes move player backwards to correct destination
- [ ] Ladders move player forwards to correct destination
- [ ] Cannot move beyond square 100
- [ ] Win condition triggers at square 100
- [ ] "Play Again" restarts the game correctly

**Phase 2 - FinOps Experience:**
- [ ] All snake descriptions display correctly
- [ ] All ladder descriptions display correctly
- [ ] Event cards appear on designated squares
- [ ] Event card movements apply correctly
- [ ] Statistics track correctly throughout game

**Phase 3 - CenITex Connect Experience:**
- [ ] Branding displays correctly
- [ ] Animations are smooth (no janky movement)
- [ ] Game is playable on 1920x1080 resolution
- [ ] Game is playable on 1366x768 resolution
- [ ] Touch interactions work on touchscreen (if available)
- [ ] Game completes in 1-3 minutes on average

---

## 16. Deliverables

Provide:

- Complete playable HTML5 game.
- Source code.
- README with instructions for running locally.
- Instructions for hosting on an internal web server or GitHub Pages.
- Brief documentation explaining how to configure:
  - CenITex Connect branding.
  - Snakes and ladders.
  - Event cards.
  - Dice and winning rules.
  - Game animations and settings.

---

## 17. Development Instructions

Build the game incrementally.

**Phase 1 – Core Game**
- Welcome and instructions screens.
- 10 × 10 board.
- Dice rolling.
- Player movement.
- Snake and ladder mechanics.
- Win condition.
- Results screen.
- Replay functionality.

**Phase 2 – FinOps Experience**
- FinOps snake and ladder descriptions.
- Interactive event cards.
- Positive and negative notifications.
- Final educational messaging.
- Game statistics.

**Phase 3 – CenITex Connect Experience**
- CenITex Connect branding.
- Visual polish.
- Animations and transitions.
- Responsive desktop and touchscreen layout.
- Fullscreen support.

**Phase 4 – Optional Enhancements**
- Sound effects.
- Local high scores.
- Additional visual effects.

### Developer Guidelines

- Build a fully playable game rather than a mockup.
- Prioritise simple, reliable and intuitive gameplay.
- Keep code readable and maintainable.
- Use sensible defaults where requirements are unspecified.
- Keep game content and board configuration separate from core game logic.
- Test dice movement, board numbering, snake and ladder transitions, event cards and winning conditions.
- Ensure animations do not allow multiple dice rolls or conflicting player movements.
- Avoid unnecessary dependencies and complexity.
- Verify the game works locally before considering development complete.
- Update this file when significant architectural or development decisions are made.

The final deliverable must be a polished, fully playable HTML5 Snakes and Ladders game that makes FinOps concepts memorable and enjoyable for customers attending CenITex Connect.