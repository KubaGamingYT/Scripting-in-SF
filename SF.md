In this document i'll show you how to script in .SF.

# Basics

Hello, welcome to this guide. I'm still working on it if you have any questions add me on discord: jakub8413_.

Here are some basics and how to make good scripts.

# 1. Always first use variables such as
```
Global Character cPlayer1;
Global Character cPlayer2;
```
- This makes the game know the script is about cPlayer1 or cPlayer2. If you only want to make the script for the cPlayer1 you don't need to use Global Character cPlayer2.

- Other basic variables:
```
Character c;
Vehicle v;
Job fFlowMutex("Flow_Setup");
Number nDirection(lFrankLobbySpawn.GetDirection());
Text tLightsOn("Light_On_");
Sound sMainIntro_01_40_Mayor("MainIntro_01_40_Mayor");
Gizmo gBankMCut("M03_BankMinicut");
Locator lFrankMove("Story_02_FrankMove", wlTheCity);
Timer scriptTimer(0);
Bool bPlayer1(false);
Position positionPos(0, 0, 0);
HotSpot hMissionStart("Flow5.13_GotoBank", wlCity);
Area aStartFighting("Story_A3_M9_HospitalRoof"); 	
Message mBarrel ("msg_level.KickBarrel", wlMissionLevel);
AttackManager amHelipadFight;
```

- If you want to use variables between scripts use Global before the variable name.

Examples:
```
Global Character c;
Global Vehicle v;
Global Bool b;
Global Number n;

// etc.
```

# 2. States. 

- We use them after variables. You can name the State whatever you want.

- To change states from one to another we use:
```
goto MainB();
```

- And that's how States look:
```
State MainB() { // you can change the MainB to whatever you want

    Conditions
    {
        // Here you add your code (the script does everything every frame)
    };
    Actions
    {
        // Here you add your code (the script does everything instantly)
    };
};

Base();
```

- If you're using conditions you need to remember that you don't use while, you use if, and in Actions you can use if and while.

# 3. If, ElseIf, Else and while

- For making if something doesn't happen something happens we use !
```
if(!cPlayer1.GetVehicle()){}; // *ONLY IN CONDITIONS!*
```

- Examples of using if, elseif and while
```
if(cPlayer1.GetVehicle()){};
elseif(cPlayer1.GetVehicle()){};
while(!cPlayer1.GetVehicle()){};
```

# 4. Worldlevels

- Worldlevel is an function to make the game know what WorldLevels are used in the script
```
WorldLevel wlCity("Lego_City"); // If you're using something that mentions wlCity you need to use that. It's an function, so you use it on the top

while(!wlCity.IsLoaded()){}; // Use this in actions
if(wlCity.IsLoaded()){}; // Use this in conditions

// If you want the game to check if the city isn't loaded use

if(!wlCity.IsLoaded()){}; // Use this in conditions
```

- Verify if its safe to interrupt the gameplay
```
if(SafeToInterruptGameplay()){}; // Use this in conditions
```

# 5. Creating a Character or a Vehicle
```
Character Guard;

Vehicle car;

Position GuardSpawnPos(0, 0, 0);
Position carPos(0, 0, 0);

Number gRot(1);
Number carRot(1);

Guard = CreateAiCharacter("PrisonGuard02", "Security", GuardSpawnPos, gRot);
car = CreateAiVehicle("Buzzer", "MotorCycle", carPos, carRot);
```

- Some things for getting characters, vehicles, models or audio to be set as something, etc.
```
Guard.SetInvulnerable(true/false);
Guard.SetPushable(true/false);
Guard.SetNoCollision(true/false);
Guard.SetNoTerrainCollision(true/false);
Guard.SetArrestable(true/false);
Guard.Kill();
Guard.PlayContextAnimation("PoliceStation_StairSweep", -1); // 1 means it plays once, -1 means it's infinite
Guard.Teleport( position, direction );
Guard.Attack(cPlayer1);
Guard.EnterVehicle(car, #DRIVER);
Guard.ExitVehicle();
Guard.SetAiOverride(true/false); // Lock a NPC in place.
Guard.LockInPlace(true, "idle"); // You can use this
Guard.Flee(cPlayer1);
Guard.SetAvoidance(true); // I dont really know what this does

car.Destroy(); 

gStairBlockage1.SetVisible(true);
gStairBlockage1.SetActive(true);
gStairBlockage1.Reset();

audio.Start(); // Starts an audio
audio.Stop(); // Stops an audio
```

- Other things car and vehicle related
```
car.TurnOnSirene(true);
if(cPlayer1.IsSkydiving()){};
if(!cPlayer1.IsSkydiving()){}; // checks if the player isnt skydiving
if(cPlayer1.EndSkydive()){};
if(cPlayer1.GetVehicle()){};
```

- Get the position of the player
```
Position playerpos(cPlayer1.GetPosition());
```

- Set Character Flags: make the character unpushable, ignoregravity and make it not render
```
SetCharacterFlags(Character=C, #DontPush, #NoTerrain, #IgnoreGravity, #DontRender); // Change the C to your character name
```

- Make the player face an character
```
cPlayer1.FaceCharacter(character); // change character to the name of your character
```

- Award an character to a player.
```
AwardCharacter("Character"); // Change the character to your character name
```

- Show a speech icon
```
Character.ShowSpeechIcon(true/false); // change Character to your character name
```

- Make a character follow the player
```
Character.FollowCharacter(cPlayer1, 0.3, 1.6);
```

- Spawn studs in player's position
```
SpawnStuds(cPlayer1.GetPosition(), 50000, 1);
```

- Checks if player is in any of these contexts
```
// Useful
if(cPlayer1.InContext("DeathContext")){};
if(cPlayer1.InContext("Swimming")){};
if(cPlayer1.InContext("Wall Run")){};
if(cPlayer1.InContext("flatten")){};
if(cPlayer1.InContext("Falling")){};
if(cPlayer1.InContext("Jumping")){};
if(cPlayer1.InContext("RideObject")){};
if(cPlayer1.InContext("Hang")){};
if(cPlayer1.InContext("Falling")){};
if(cPlayer1.InContext("Default")){};
if(cPlayer1.InContext("Throw")){};
if(cPlayer1.InContext("LandJump")){};
if(cPlayer1.InContext("HandCuffed")){};
if(cPlayer1.InContext("UnlockDisguise")){};

// Not really useful 
if(cPlayer1.InContext("Mech Jump In")){};
if(cPlayer1.InContext("AnimationTask")){};
if(cPlayer1.InContext("MechBigJump")){};
if(cPlayer1.InContext("PDAScanner")){};
if(cPlayer1.InContext("BouncePadJump")){};
if(cPlayer1.InContext("PutDown")){};
if(cPlayer1.InContext("GrappleRope")){};
if(cPlayer1.InContext("Grapple")){};
if(cPlayer1.InContext("DrainPipes")){};
if(cPlayer1.InContext("DJDeck")){};
if(cPlayer1.InContext("DropPoint")){};
if(cPlayer1.InContext("MechWallJumpWait")){};
```

# 6. Commenting something in the script
```
// My comment

/*
My comment
*/
```

# 7. Other Useful SF thingies.

- Make GUI visible/invisible
```
UI_ShowHUD(true/false); // Other GUIs
UI_ShowPlayerHUD(false); // Player GUI
```

- Set an Hint and cancel it
```
SetHint("HINT_STORY_HINT", true, false);

CancelHint();
```

- If Player pressed the button a something happens, if player holds the button L2 something happens
```
if(PlayerPressedButton("A")){};
if(PlayerHeldButton("L2")){};
```

- Shows an message on the screen
```
UI_SetMissionMessage("MOD_MESSAGE", 4); // The number is the number of seconds the message is showed on the screen.
```

- Shows an end mission message on the screen
```
UI_EndMission("MOD_MISSION", true);
```

- Shows the character on the map
```
Guard.UI_Map_SetCharacterActive(true);
```

- Making the screen fade in and out
```
Fadescreen(true);

wait(1);

Fadescreen(true);
```

- This sets and clears an Objective Marker for the 1 player
```
Position Pos(0, 0, 0);

SetSatNavDestination(Pos);
SetObjectiveMarker(Pos, 0.5, true, true);
ShowObjectiveMarker(true):

// This sets up an objective marker

SetSatNavDestination();
SetObjectiveMarker(cPlayer1, 0, false, false);
ShowObjectiveMarker(false);

// This clears the marker
```

- Stop rendering the character
```
SetCharacterFlags(Character=cPlayer1, #DontRender);
```

- How to play music and stop it
```
TrackBank tbankActionMusic("CHASE_Foot");
SetTrackBank(tbankActionMusic);

PlayActionMusic(true);

PlayActionMusic(false);

ClearTrackBank();
```

- Play a SFX
```
PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");
```

- Set time of day to DUSK, NOON or DAWN (you can also do nothing which will look like a night)
```
SetTimeOfDay(“Dusk”);
SetTimeOfDay(“Dawn”);
SetTimeOfDay(“Noon”);
SetTimeOfDay(“Night”);
```

- The game checks if the player is next to a position
```
While(cPlayer1.DistanceTo(position) > 5){}; // actions
if(cPlayer1.DistanceTo(position) > 5){}; // conditions
```

- The game spawns studs in a position
```
SpawnStuds(position, 50000, 1); // change the position to your position name
```

# 8. Wait

- The script waits before doing something
```
wait(1); // waits 1 second
wait(0.5); // waits 500 milliseconds before doing something
```









