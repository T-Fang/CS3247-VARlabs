# VarLabs @NUS

## miniProject2

In this assignement, we are tasked to create three levels to inspire three different responses from the viewer, and each experience should leverage the dynamic power of Blueprint.

Specifically, we want to inspire three responses:

- Lean (HW_Lean)
  - Inspire the viewer to lean in for better perspective.
- Dip (HW_Dip)
  - Inspire the viewer to dip, dodge, duck, dive, and/or dodge.
- Left (HW_Left)
  - Inspire the user to look left/right or up/down repeatedly.

Below are some descriptions of my projects (Spoilers ahead, if possible, please try out the projects before continuing):

### Lean (HW_Lean)

<img width="803" alt="Lean" src="https://user-images.githubusercontent.com/61874388/152423840-2d732b1b-02fe-4995-9998-f528b4c0e100.png">

It's dawn time. You just witnessed a fight scene between two furious men, you saw an axe flying toward one of the men. After 2 seconds, there were two dead bodies lying on the ground. Since you are peeping through a window, you did not really get the full picture: "Why did I hear gun shot", "How did the other man die", etc. Driven by curiosity, you decided to lean forward...



Handmade blueprints:

- All exterior parts of the house (walls, windows, roof, floor):
  - base meshes: block, window, door
- Flickering lights `BP_Flickering_CeilingLight` (point light combined with ceiling light)
  - used a "flickering" timeline to change light intensity
- Axe `BP_Axe_1`
  - set the direction to throw  (`direction` variable) when the game start
  - in `Event Tick`, Move the axe towards the `direction` and rotate it if it has not been blocked (`isAxeMoving` is True)
  - keep a boolean variable `isAxeMoving` and set it to false when it overlaps with something.
- Axe man `BP_Axe_Man_WithBlood`
  - play throwing sound when he throws the axe
  - scream and fall to the ground when he get shot by gun
  - show blood stain after him being shot
- Gun man `BP_Gun_Man_WithBlood`
  - Similar to Axe man except he doesn't throw an axe



### Dip (HW_Dip)

<img width="801" alt="Dip" src="https://user-images.githubusercontent.com/61874388/152423861-0a830eea-c11b-4776-a981-102c95660678.png">

You are a gang member who recently disobeyed an important order from your boss and cost him a fortune. The boss was pissed off and sentenced you to death. However, it seems like in his opinion, brutally killing you with axes instead guns is more satisfying to him. Although you knew there was no escape, you tried to dodge the axes coming at you...



Handmade blueprints:

- All exterior parts of the house (walls, windows, roof, floor):

  - base meshes: block, window, door

- Flickering lights `BP_Flickering_CeilingLight2` (point light combined with ceiling light)

  - used a "flickering" timeline to change light intensity

- Axe `BP_Axe_2`

  - keep the throwing direction in `direction` (aim for player's head) and decide a random speed (`speed`) when the game starts
  - delay a random number of seconds before an axe is thrown

  - in `Event Tick`, Move the axe towards the `direction` and rotate it if it has not been blocked (`isAxeMoving` is True)
  - keep a boolean variable `isAxeMoving` and set it to false when it overlaps with something that is not Axe

- Executioner `BP_Axe_Man_With_Spotlight`

  - after the boss finished his sentence, two Rect Lights will light up, outlining the shapes of the executioners as well as the axes.

- Boss `BP_Boss_With_Furniture`

  - keep a Text Render that displays words of the boss, update the text of the Text Render correspondingly after some delays.

- Gun man `BP_Gun_Man`

  - similar to previous gun man blueprint in `HW_Lean`

Imported Blueprints (Meshes):

- Table
- Lamp on the table
- Commode
- Production lights props (used together with actual lights)
- Chairs



### Left (HW_Left)

<img width="794" alt="Left" src="https://user-images.githubusercontent.com/61874388/152423880-e508e83a-da6b-486c-8863-da8d87ca46c4.png">

You are in space now, being chased by numerous enemy spaceships. To make things worse, they are coming from everywhere, leaving you little room to espace. Will you be able to found a way out?...



Handmade blueprints:

- Level blueprint:
  - keeps a function `SpawnSpaceship` to spawn space ship around the player
  - set a timer to repeatedly call `SpawnSpaceship`
  - `SpawnSpaceship`:
    - check whether the current number of spaceships is less than 25, if it is, we will spawn a spaceship
    - The location/distance of the spaceship is randomly determined within a reasonable range.
    - The spaceship is spawned such that it is always pointing towards the origin (the player's location)
- Spaceship `BP_Spaceship`:
  - After `Event BeginPlay`, we set the direction ( `direction` ) of the spaceship such that it is moving towards the player's location (origin) and choose a random reasonable number for the `speed`
  - In `Event Tick`, we first check if the spaceship is closed enough to the player, if not, the spaceship will continue moving. Otherwise, we destroy the spaceship so that spaceships won't keep accumulating and affect the computer's performance.



## miniProject3

In this miniProject, we are expected to design a level that allows the player to “touch” the environment with gaze and simple input.

- Create *at least* **two new interactable actors** that **respond to player trace**
- Build a **new level** (HW_Creative) that meaningfully incorporates your interactable actors.



Here's what I've come up with:

The game looks like a normal "Whack a Mole" game at the beginning. However, if a player has accumulated a certain number of points via hitting the mole with a hammer, he will reach the next stage. During the second phase, the arcade machine on which the player played his "Whack a Mole" game becomes the "mole" to hit! In a way, the floor itself is an arcade machine. Finally, if the player has hit enough arcade machines, the lights will suddenly went down and the floor will start to rise. When the player finally get to the ground, he will discover that a giant hammer, which is similar to the one that the player is holding, is waiting above his head...



Here's a few things that you can check out:

- Interactable actors:
  - Mole
  - Arcade Machine
- Sequence:
  - HammerSequence
  - GrassHoleAndBigHammerSequence
- Timeline:
  - PopUp timeline in "Mole" and "Arcade Machine", which uses a custom curve "Curve_Mole"
  - Flikering timeline in the "Flickering Round Light"



