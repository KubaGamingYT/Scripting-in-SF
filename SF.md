In this document i'll show you how to script in .SF.

# Basics

Hello, welcome to this guide. I'm still working on it if you have any questions add me on discord: jakub8413_.

Here are some basics and how to make good scripts.

1. Always first use variables such as
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
Position startPos(-179.5, 3.36, -220);
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

2. States. 

- We use them after variables. You can name the State whatever you want.

- To change states from one to another we use:
```
goto MainB();
```

- And that's how States look:
```
State MainB() {

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

3. If, ElseIf, Else and while

- For making if something doesn't happen something happens we use !
```
if(!cPlayer1.GetVehicle()){};
```

- Examples of using if, elseif, else and while
```
if(cPlayer1.GetVehicle()){};
elseif(cPlayer1.GetVehicle()){};
else(cPlayer1.GetVehicle()){};
while(!cPlayer1.GetVehicle()){};
```

4. Worldlevels

- Worldlevel is an function to make the game know what WorldLevels are used in the script
```
WorldLevel wlCity("Lego_City"); // Make the game know that code is executing in LEGO_CITY

while(!wlCity.IsLoaded()){}; // Use this in actions
if(wlCity.IsLoaded()){}; // Use this in conditions

// If you want the game to check if the city isn't loaded use

if(!wlCity.IsLoaded()){}; // Use this in conditions
```

- Verify if its safe to interrupt the gameplay
```
if(SafeToInterruptGameplay()){}; // Use this in conditions
```

5. Creating a Character or a Vehicle
```
Character Guard;

Vehicle Vehicle;

Position GuardSpawnPos(0, 0, 0);
Position carPos(0, 0, 0);

Number gRot(1);
Number carRot(1);

Guard = CreateAiCharacter("PrisonGuard02", "Security", GuardSpawnPos, gRot);
Vehicle = CreateAIVehicle(tVehicleType, "Enforcer", carPos, carRot);
```

- Some things for getting characters, vehicles, models or audio to be set as something, etc.
```
Guard.SetInvulnerable(true/false);
Guard.SetPushable(true/false);
Guard.SetNoCollision(true/false);
Guard.SetNoTerrainCollision(true/false);
Guard.SetArrestable(true/false);
Guard.Kill();
Guard.PlayContextAnimation("PoliceStation_StairSweep", -1) // 1 means it plays once, -1 means it's infinite
Guard.Teleport( position, direction );
Guard.Attack(cPlayer1);

cTrooper.Destroy(); // Destroys a vehicle

gStairBlockage1.SetVisible(true);
gStairBlockage1.SetActive(true);
gDoors.Reset();

sFranKTalk1.Start(); // Starts an audio
sFranKTalk1.Stop(); // Stops an audio
```

- Other things car and vehicle related
```
CopCar4.TurnOnSirene(true);
```

6. Commenting something in the script
```
// My comment

/*
My comment
*/
```

# Other Functions, Variables etc.

Make GUI visible/invisible
```
UI_ShowHUD(true/false); // Other GUIs
UI_ShowPlayerHUD(false); // Player GUI
```

Stop rendering the character
```
SetCharacterFlags(Character=cPlayer1, #DontRender);
```

Get the position of the player
```
Position playerpos(cPlayer1.GetPosition());
```

Make an character enter/leave the vehicle
```
NPC.EnterVehicle(car, #DRIVER);
NPC.ExitVehicle();
```

How to play music and stop it
```
TrackBank tbankActionMusic("CHASE_Foot");
SetTrackBank(tbankActionMusic);

PlayActionMusic(true);

PlayActionMusic(false);

ClearTrackBank();
```

Make Something happen when you enter or leave the vehicle
```
if(cPlayer1.GetVehicle()) {}
elseIf(!cPlayer1.GetVehicle()) {}
```

The script waits before doing something
```
wait(1); // waits 1 second
wait(0.5); // waits 500 milliseconds before doing something
```

Shows an message on the screen
```
UI_SetMissionMessage("MOD_MESSAGE", 4);
```

This sets and clears an Objective Marker for the 1 player
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

Lock the player in place
```
cPlayer1.SetAiOverride(true); // lock

cPlayer1.SetAiOverride(false); // unlock

cPlayer1.LockInPlace(true, "idle"); // you can also use this
```

If Player pressed the button a something happens, if player holds the button L2 something happens
```
if(PlayerPressedButton("A")){};
if(PlayerHeldButton("L2")){};
```

Play a SFX
```
PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");
```

Making the screen black and normal again
```
Fadescreen(true);

wait(1);

Fadescreen(true);
```

Set time of day to DUSK, NOON or DAWN (you can also do nothing which will look like a night)
```
SetTimeOfDay(“Dusk”);
SetTimeOfDay(“Dawn”);
SetTimeOfDay(“Noon”);
SetTimeOfDay(“Night”);
```

Check if player is skydiving, isnt skydiving or check if the player has stopped the skydive
```
if (cPlayer1.IsSkydiving())
if (!cPlayer1.IsSkydiving())
if (cPlayer1.EndSkydive());
```







