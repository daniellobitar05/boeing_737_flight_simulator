📌 Overview

FlightBob is a mini-game written entirely in MIPS Assembly for the CSC312 Computer Architecture course.
The game runs on the MARS Emulator using the Bitmap Display, Keyboard MMIO, and optional MIDI audio.

Your goal is simple:

✔ Control the aircraft using W (up) and S (down)
✔ Collect items scattered on the map
✔ Reach the target zone
✔ Display a win screen with sound effects

The project demonstrates low-level programming concepts such as memory-mapped I/O, bitmap rendering, random number generation, collision detection, and game loop control.

🎮 Game Features
1. Welcome Screen

The game displays a static welcome/splash screen on the bitmap display.

User must press SPACE to start the game.

2. Player Control

Controlled using:

W → Move the aircraft upward

S → Move the aircraft downward

Movement updates the player’s bitmap sprite in real time.

3. Collectibles System

Three collectibles are placed randomly across the screen.

When the player intersects their area, they are removed.

Score increments each time a collectible is collected.

4. Collision Detection

Uses multiple sampling points around the sprite for accurate collision detection.

Prevents false negatives or positives due to sprite dimensions.

5. Victory Condition

When all collectibles are collected OR the player reaches the final zone:

A victory screen is drawn.

A short MIDI melody is played.

The game ends cleanly.

🖥 Requirements
Software

MARS MIPS Emulator
(must enable Bitmap Display & Keyboard/MMIO)

Bitmap Display Settings
Setting	Value
Unit Width	4 pixels
Unit Height	4 pixels
Display Width	128 units
Display Height	128 units
Base Address	0x10008000
Keyboard MMIO
Component	Address
Control Register	0xFFFF0000
Data Register	0xFFFF0004
📂 Project Structure
FlightBob/
│
├── flightbob.asm         # Main MIPS assembly game file
├── README.md             # Documentation
├── assets/
│   ├── welcome_screen.hex
│   ├── game_background.hex
│   ├── victory_screen.hex
│   └── sprites/...

🧠 How the Game Works
1. Game Loop

The main loop performs:

Read keyboard input

Move the player

Redraw background

Redraw collectibles

Draw player sprite

Check collisions

Update score

2. Memory-Mapped Graphics

Every pixel is stored as a 32-bit hex color.
Drawing means writing directly to VRAM (0x10008000 + offset).

3. Player Sprite

The aircraft is drawn using manual sw instructions forming a pixel-art pattern.

4. Random Collectibles

MARS syscall 42 generates random values.
These are aligned and drawn at offset positions.

⌨ Controls
Key	Action
SPACE	Start game
W	Move Up
S	Move Down
🏆 Victory Sequence

Once all collectibles are collected, or the player reaches the target:

✔ The screen is cleared
✔ Victory image is displayed
✔ A full melody plays using MIDI syscalls
✔ Program exits gracefully

🛠 Tech Concepts Demonstrated

Memory-mapped I/O

Bitmap graphics rendering

Stack usage & register management

Random number generation

Collisions using absolute distance

Clean modular assembly program design


📜 How to Run

Open flightbob.asm in MARS

Open Bitmap Display → Configure settings

Open Keyboard MMIO Simulator

Click Connect to MIPS

Run the program

Enjoy the game!


✔ License

This project is for educational and academic purposes only.
