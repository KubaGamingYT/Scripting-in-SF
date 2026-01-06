In this document i'll show you how to script in .SF.

# SF Scripting

Starting your code:
```
State Base() {

    Conditions
    {
        // Here you add your code (the script does everything every frame)
    };
    Actions
    {
        // Here you add your code (the script does everything instantly)
    };
}

Base();
```

Verify if the city is loaded
```
WorldLevel wlCity("Lego_City"); // Make the game know that code is executing in LEGO_CITY

while(!wlCity.IsLoaded()){} // For actions
```

Verify if its safe to interrupt the gameplay
```
if( SafeToInterruptGameplay() ) {};
```

Getting player characters for the script
```
Global Character cPlayer1;
Global Character cPlayer2; // cPlayer1 is the first player and cPlayer2 is the second player
```

Variable types in LCU
```
Character NPC;

Vehicle PrisonerTransport;

Job fFlowMutex("Flow_Setup");

Number nDirection(lFrankLobbySpawn.GetDirection() );

Text tLightsOn("Light_On_");

Sound sMainIntro_01_40_Mayor("MainIntro_01_40_Mayor");

Gizmo gBankMCut("M03_BankMinicut");

Locator lFrankMove("Story_02_FrankMove", wlTheCity);

Timer scriptTimer(0);

Bool bPlayer1(false);

Position startPos(-179.5, 3.36, -220);
```

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

If we want to make the game to do something when this and this happen we use OR
```
if (  cPlayer1.GetVehicle() OR cPlayer2.GetVehicle()  )
{
				
goto SetLCPDSatNav();
```

Make an character enter/leave the vehicle
```
NPC.EnterVehicle(car, #DRIVER);
NPC.ExitVehicle()
```

Creating the AI Character and a AI vehicle
```
Guard = CreateAiCharacter("PrisonGuard02", "Security", GuardSpawnPos, (200 / 360) * 65535);
Vehicle = CreateAIVehicle(tVehicleType, "Enforcer", lCar02, nDirection );
```

Some things for getting characters, vehicles, models or audio to do something
```
Guard.SetInvulnerable(true/false); // Makes him invincible
Guard.SetPushable(true/false); // Makes him pushable
Guard.SetNoCollision(true/false); // Makes him have no collision
Guard.SetNoTerrainCollision(true/false); // Makes him have no Terrain collision
Guard.SetArrestable(true/false); // Makes him arrestable
Guard.Kill(); // Destroys him
Guard.PlayContextAnimation("PoliceStation_StairSweep", -1) // Makes him play some kind of animation (-1 means it plays forever, 1 means it plays once)
Guard.Teleport( position, direction ); // Makes him teleport somewhere

cTrooper.Destroy(); // Destroys a vehicle

gStairBlockage1.SetVisible(true); // Makes a model visible
gStairBlockage1.SetActive(true); // Makes a model active
gDoors.Reset(); // Resets it

sFranKTalk1.Start(); // Starts an audio
sFranKTalk1.Stop(); // Stops an audio
```

How to play music and stop it
```
TrackBank tbankActionMusic("myEpicFight");
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

Make an character attack the player
```
Gangmember1.Attack(cPlayer1);
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
//this sets up an objective marker
SetSatNavDestination();
SetObjectiveMarker(cPlayer1, 0, false, false);
ShowObjectiveMarker(false);
//this clears the marker
```

Lock the player in place
```
cPlayer1.SetAiOverride(true); // lock

cPlayer1.SetAiOverride(false); // unlock

cPlayer1.LockInPlace(true, "idle"); // you can also use this
```

If Player pressed the button a something happens, if player holds the button L2 something happens
```
if ( PlayerPressedButton("A") )
if (PlayerHeldButton("L2") )
```

The script changes the State Base to another one (For example State SpawnRobber)
```
goto SpawnRobber();
```

Play a SFX
```
PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");
```

Commenting something in the script
```
// My comment

/*
My comment
*/
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

SetTimeOfDay(“You can put whatever you want here for the night effect”);
```

Check if player is skydiving, isnt skydiving or make the player end a skydive
```
if (cPlayer1.IsSkydiving())
if (!cPlayer1.IsSkydiving())
if (!cPlayer1.EndSkydive());
```

Make the player face another character
```
cPlayer1.FaceCharacter(vinnie);
```







