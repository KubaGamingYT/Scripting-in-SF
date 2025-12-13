In this document i'll show you how to script in .SF.

# Basics

How to start your code:
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

while(!wlCity.IsLoaded()){} // Make the game verify if the City is loaded
```

Getting player characters for the script
```
Global Character cPlayer1;
Global Character cPlayer2; // cPlayer1 is the first player and cPlayer2 is the second player
```

Mentioning a character
```
Character Gangmember1;
```

Mentioning a vehicle
```
Vehicle PrisonerTransport;
```

Make an character enter/leave the vehicle
```
NPC.EnterVehicle( PrisonerTransport, #PASSENGER2 );
NPC.ClearVehicle
```

Declaring the position of a character
```
Position GuardSpawnPos(0, 0, 0); // replace the Guard with the name of the character for example Gangmember1
```

Creating the AI Character
```
Guard = CreateAiCharacter("PrisonGuard02", "Security", GuardSpawnPos, (200 / 360) * 65535);
```

Some things for getting characters to do something
```
Guard.SetInvulnerable(true/false); // Makes him invincible
Guard.SetPushable(true/false); // Makes him pushable
Guard.SetArrestable(true/false); // Makes him arrestable
Guard.Kill(); // Destroys him
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

The scripts waits before doing something
```
wait(); // add seconds to the ()
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

True and false variable
```
Bool bPlayer1(false);
```

If player pressted the button A something happens
```
if ( PlayerPressedButton("A") )
```
Stop using base and use SpawnRobber
```
goto SpawnRobber();
```

Destroy a vehicle
```
cTrooper.Destroy();
```

Play a SFX
```
PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");
```

Commenting something in the script
```
// My comment
```

Making the screen black and normal again
```
Fadescreen(true);
wait(1);
Fadescreen(true);
```








