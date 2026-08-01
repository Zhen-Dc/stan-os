# Case Study — FemLink-Style Motion Graphic

This is the source case study that the `motion-graphics` skill is built around. Preserved verbatim as ground truth — the SKILL.md technique catalog and FemLink scene-arc template trace directly back to this breakdown. When deciding whether a new technique belongs in the skill, ask: does it serve one of these six scenes?

---

## Scene 1: The Problem (0:00 - 0:02)

**Visuals:** The text "FOR YEARS" appears, followed by a pink circular dial filling up to 80%. A neumorphic panel slides in with social media icons and a rising graph line.

**Techniques Used:**

- **Radial Wipe / Stroke Animation:** The pink dial is animated by changing the "Stroke End" percentage from 0 to 80%.
- **Trim Paths:** The pink line graph on the panel uses a similar technique; a path is drawn, and its endpoint is animated from left to right.
- **Scale & Opacity Keyframing:** The social media icons pop in using a quick scale animation (from 0% to 110%, then resting at 100% to create a "bounce" or "overshoot" effect).

## Scene 2: The Transition (0:03 - 0:05)

**Visuals:** The text "Today" is on screen, and a pink pill-shape wipes across to reveal the words "we change that".

**Techniques Used:**

- **Track Mattes / Masking:** The pink pill acts as a mask. As it moves along the X-axis (position animation), it reveals the text underneath it.

## Scene 3: The Reveal (0:05 - 0:09)

**Visuals:** The "Introducing" button morphs into the "FemLink" logo, which is then surrounded by orbiting icons. The central logo then zooms in massively to transition to the next scene.

**Techniques Used:**

- **Rotation:** The outer ring of icons is parented to a central anchor point and rotated continuously.
- **Match Cut / Zoom Transition:** The logo scales up so large that the pink background fills the entire screen, acting as a seamless wipe to the next white background scene.

## Scene 4: The Interface (0:09 - 0:14)

**Visuals:** A mock UI layout appears with a search bar, a video player, and chat bubbles that pop up sequentially.

**Techniques Used:**

- **Position Easing:** The UI elements slide into the frame. The motion starts fast and slows down as it reaches its final resting place (this is called "Ease Out").
- **Anchor Point Scaling:** The chat bubbles scale up from 0 to 100%, but their anchor points are set to their bottom corners, making them look like they are growing out of the user's avatar.

## Scene 5: The Tech/Engine (0:14 - 0:19)

**Visuals:** A circular chip diagram appears with pulsing lines. It transitions into an angled, 3D-looking radar animation with rings dropping downward as a percentage counter drops to 0%.

**Techniques Used:**

- **Pulsing Expressions/Loops:** The opacity and scale of the glowing rings around the chip are looped to expand and fade continuously.
- **2.5D Animation:** The radar rings are likely 2D circles tilted in 3D space (rotating the X-axis) and animated moving down the Y-axis.
- **Number Counter Effect:** The percentage text is linked to a slider control that animates down from 46% to 0%.

## Scene 6: The Lockout & Outro (0:19 - 0:25)

**Visuals:** A login screen appears. When the "Login" button is pressed, an "Access denied!!" button shakes violently. The scene fades back to the main logo.

**Techniques Used:**

- **Wiggle / Shake Animation:** The "Access denied!!" button uses a rapid position shift left and right. In code, this would be a CSS keyframe animation moving translateX back and forth by a few pixels. In After Effects, it's a simple wiggle(frequency, amplitude) expression.

---

## How to replicate this method

If you want to edit your video using this exact method, you need to focus on **Easing**. Nothing in this video moves at a constant, robotic speed. Every single animation has an "Ease" applied to it — meaning it accelerates smoothly and decelerates smoothly.

1. **Design the Assets First:** Use a program like Figma or Adobe Illustrator to draw all your buttons, graphs, and logos. Use drop shadows (light shadow on top left, dark shadow on bottom right) to get that soft "Neumorphic" look.
2. **Import & Keyframe:** Bring those assets into your video editor. Set your starting position keyframe, and your ending position keyframe.
3. **Apply Easing:** Highlight your keyframes and apply "Easy Ease" (or customize the speed graph if your software allows it).
