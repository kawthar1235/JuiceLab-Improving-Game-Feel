# JuiceLab — Improving Game Feel

**SWE 402 — Game Development**

**Assignment 3: Improving Game Feel**

## 1. Student Information

- **Student Name:** kawthar alkhawajah
- **Student ID:** 202168810
- **Unity Version:** 6000.5.10f1
- **Project:** JuiceLab — Brick Breaker
- **Assignment Type:** Individual

## 2. Project Overview

This project focuses on improving the game feel of a basic Brick Breaker game by introducing visual effects, reactive animations, event-based audio, and interface feedback.

The main objective is to transform the original game into a more responsive, satisfying, and visually engaging experience while preserving its core gameplay mechanics.

The project contains two scenes:

- **Before:** The original game without additional feedback effects.
- **After:** The improved game featuring five feedback techniques.

The original gameplay mechanics, including ball speed, paddle controls, collision behavior, scoring, and lives, remain unchanged.

## 3. Intended Game Feel

**Selected Style: Playful and Bouncy**

The intended experience is energetic, responsive, and satisfying.

The improvements emphasize important gameplay events through short animations, colorful particles, distinctive sounds, and clear visual feedback.

The effects were designed to enhance the player's experience without distracting from the ball or changing the original gameplay mechanics.

## 4. Implemented Improvements

| Improvement | Trigger | Implementation File / Object | Purpose |
|---|---|---|---|
| 1. Brick Particle Effect | `BrickDestroyed` | `BrickParticleFeedback.cs` / `BrickBreakParticles` Prefab | Displays colorful particles when a brick is destroyed, making successful hits more satisfying. |
| 2. Paddle Squash & Stretch | `BallHitPaddle` | `PaddleSquashFeedback.cs` / Paddle Visual | Briefly stretches and compresses the paddle to emphasize ball contact without modifying physics. |
| 3. Event-Based Audio | `BallHitPaddle`, `BrickDestroyed`, `BallLost` | `GameAudioFeedback.cs` | Generates three distinguishable sounds for paddle contact, brick destruction, and ball loss. |
| 4. Score Pulse Animation | `ScoreChanged` | `ScorePulseFeedback.cs` / Score Text | Briefly enlarges the score display when points are earned, emphasizing the score change. |
| 5. Ball Trail | Ball movement | Trail Renderer / Ball Visual | Creates a short fading trail behind the ball, improving movement visibility and emphasizing speed. |

### 4.1 Brick Particle Effect

A particle system is triggered whenever a brick is destroyed.

The effect appears at the brick's position and uses the brick's color to maintain visual consistency.

The particle effect is instantiated using the `BrickDestroyed` event and automatically destroyed after its lifetime.

**Key Settings:**
- Start Lifetime: 0.4 seconds
- Start Speed: 3
- Start Size: 0.12
- Burst Count: 15
- Looping: Disabled

### 4.2 Paddle Squash & Stretch

A reactive squash-and-stretch animation was implemented to provide immediate visual feedback when the ball hits the paddle.

Only the paddle's visual child is animated, preserving the original collider and physics behavior.

**Key Settings:**
- Squash Duration: 0.15 seconds
- Squash Amount: 0.25

The paddle returns to its original appearance after each collision.

### 4.3 Event-Based Audio

Three distinct sound effects were generated programmatically using C# and Unity's AudioClip system.

- **Paddle Hit:** A short bouncing sound.
- **Brick Destruction:** A sharper, higher-frequency sound.
- **Ball Loss:** A descending sound indicating a missed ball.

Each sound is triggered by its corresponding `GameEvents` event.

The sounds are played using `AudioSource.PlayOneShot()` to support repeated gameplay events.

The ball-loss sound volume was adjusted after playtesting to improve clarity.

### 4.4 Score Pulse Animation

The score display briefly increases in size whenever points are earned.

**Key Settings:**
- Pulse Scale: 1.3
- Pulse Duration: 0.2 seconds

The animation automatically returns the score display to its original scale.

The existing HUD system remains responsible for updating the actual score value.

### 4.5 Ball Trail

A Trail Renderer was added to the ball's visual representation.

The trail creates a short fading effect behind the moving ball.

**Key Settings:**
- Trail Time: 0.18 seconds
- Minimum Vertex Distance: 0.05
- Width: 0.15

This technique improves the visibility of the ball's movement while maintaining the original gameplay behavior.

## 5. Before and After Comparison

### Before

The original game contains the basic Brick Breaker mechanics:

- Ball and paddle movement.
- Brick destruction.
- Score tracking.
- Life tracking.

However, gameplay events have minimal visual and audio feedback.

### After

The improved version includes:

- Particle effects during brick destruction.
- Reactive paddle animation.
- Three event-based sound effects.
- Animated score feedback.
- A fading trail behind the ball.

These improvements make gameplay events more noticeable and satisfying without modifying the core mechanics.

## 6. Playtest and Revision

### Playtest Method

One participant played both the Before and After versions and provided feedback on satisfaction, clarity, and distracting or difficult-to-notice effects.

### Observations

The participant found the After version more satisfying because of its additional visual and audio feedback.

The participant specifically mentioned that the ball trail made the ball's movement clearer and easier to follow.

However, the ball-loss sound was difficult to notice compared with the other effects.

### Revision

Based on the participant's feedback, the ball-loss sound playback volume was increased.

**Original setting:**

`audioSource.PlayOneShot(loseSound, 0.65f);`

**Revised setting:**

`audioSource.PlayOneShot(loseSound, 1.0f);`

This adjustment improved the prominence of the ball-loss sound without modifying the gameplay mechanics or other sound effects.

### Result After Revision

After applying and testing the revision, the ball-loss sound became more noticeable and provided clearer feedback when the player lost a ball.

The revised sound was tested during gameplay and was found to be an improvement over the original setting.

## 7. Testing and Verification

The following behaviors were tested in the After scene:

| Test | Result |
|---|---|
| Brick destruction triggers particles | Passed |
| Particle effects disappear after completion | Passed |
| Paddle animation reacts to collisions | Passed |
| Paddle returns to its original scale | Passed |
| Paddle contact sound plays | Passed |
| Brick destruction sound plays | Passed |
| Ball-loss sound plays | Passed |
| Score updates and pulse animation works | Passed |
| Ball trail appears during movement | Passed |
| Lives decrease when the ball is lost | Passed |
| Core gameplay remains functional | Passed |
| Before scene remains unmodified | Passed |

The effects were tested during normal gameplay and repeated collisions.

## 8. How to Run the Project

### Requirements

- Unity Editor 6000.5.10f1
- Unity Hub

### Instructions

1. Clone or download this GitHub repository.
2. Open Unity Hub.
3. Select **Add → Add project from disk**.
4. Select the project folder containing `Assets`, `Packages`, and `ProjectSettings`.
5. Wait for Unity to import the project.
6. Open one of the following scenes:

   - `Assets/_Project/Scenes/Before.unity`
   - `Assets/_Project/Scenes/After.unity`

7. Select a 16:9 Game view.
8. Press **Play** to start the game.

### Controls

| Control | Action |
|---|---|
| Mouse Movement | Move paddle horizontally |
| A / D | Move paddle left or right |
| Left / Right Arrow Keys | Move paddle left or right |

The ball launches automatically.

Stop and restart Play mode to begin a fresh gameplay session.

## 9. Project Structure

```text
Assets/
└── _Project/
    ├── Scenes/
    │   ├── Before.unity
    │   └── After.unity
    ├── Scripts/
    │   └── Core/
    │       ├── GameEvents.cs
    │       └── ImpactInfo.cs
    └── Feedback/
        ├── Prefabs/
        │   └── BrickBreakParticles.prefab
        ├── Audio/
        ├── BrickParticleFeedback.cs
        ├── PaddleSquashFeedback.cs
        ├── GameAudioFeedback.cs
        └── ScorePulseFeedback.cs
```

The After scene contains a `FeedbackManager` object that manages the event-based feedback components.

The Ball Trail is configured using Unity's Trail Renderer component.

## 10. Demonstration Video

**Video Duration:** 2–3 minutes

**Video Link:** https://drive.google.com/file/d/1MI-UpSiUIW1GMfQheLn63XYQwFR1zlV8/view?usp=sharing

The demonstration includes:

1. Original Before gameplay.
2. Improved After gameplay and all five feedback techniques.
3. Explanation of an implemented script and a tuned parameter.
4. Playtest observations and the ball-loss audio revision.

## 11. AI Use Statement

I used ChatGPT (OpenAI) as a learning and development assistant throughout this assignment.

One of the most valuable things I learned was a new approach to creating game sound effects. Instead of downloading audio files from external sources, ChatGPT introduced me to the idea of generating sounds programmatically using C# scripts in Unity. Through this process, I learned how to use `AudioClip.Create()` to generate different sound effects for paddle collisions, brick destruction, and ball loss.

ChatGPT also helped me understand and implement the feedback scripts, organize my ideas, and structure and write the README documentation.

I integrated and tested the suggested implementations in Unity and made adjustments based on gameplay testing and playtest feedback, including improving the ball-loss sound volume.

Overall, AI assistance helped me explore a new technical approach, develop my understanding of Unity's audio system, and document my work more clearly.

## 12. Assets, Tools, and Credits

**Unity Engine**
- Used for game development, physics, rendering, animation, audio, and particle systems.

**Course Starter Project**
- JuiceLab-Dead-Starter, provided for SWE 402 Assignment 3.
- Original starter project and gameplay foundation.
- Original source credit and MIT license retained.

**Custom Feedback Implementation**
- Unity Particle System for brick destruction.
- Unity Trail Renderer for ball movement.
- C# coroutines for paddle and score animations.
- Programmatically generated AudioClips for event-based audio.

**AI Tool**
- OpenAI ChatGPT, used for development assistance and documentation.

No external sound-effect files were required because the audio feedback was generated programmatically.

## 13. Conclusion

This project demonstrates how visual, audio, animation, and interface feedback can significantly improve the feel of a game without changing its underlying mechanics.

The five implemented improvements make the Brick Breaker experience more responsive, readable, and satisfying.

The Before and After comparison highlights the importance of game feel, while the playtest revision demonstrates how user feedback can guide meaningful improvements.
