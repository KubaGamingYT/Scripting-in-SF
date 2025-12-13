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

Make the game know that code is executing in LEGO_CITY (or other places)
```
WorldLevel wlCity("Lego_City"); // Make the game know that code is executing in LEGO_CITY

if( wlCity.IsLoaded() ) {}; // Make the game verify if the City is loaded
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

Spawning the character in some kind of position
```
Position GuardSpawnPos(0, 0, 0); // replace the Guard with the name of the character for example Gangmember1
```

Creating the AI Character
```
Guard = CreateAiCharacter("PrisonGuard02", "Security", GuardSpawnPos, (200 / 360) * 65535);
```

Can the character be killed, can it be pushed or can it be arrested.
```
Guard.SetInvulnerable(true/false);
Guard.SetPushable(true/false)
Guard.SetArrestable(true/false);
```

How to play music and stop it
```
TrackBank tbankActionMusic("myEpicFight");
SetTrackBank(tbankActionMusic);

PlayActionMusic(true);

PlayActionMusic(false);

ClearTrackBank();
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
UI_SetMissionMessage("MOD_MISSION_FAILED_TEXT", 4);
```

This sets an Objective Marker for the 1 player
```
SetObjectiveMarker(cPlayer1, 0, true/false, true/false);
ShowObjectiveMarker(true/false);
```





