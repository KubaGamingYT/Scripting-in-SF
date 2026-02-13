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
Gadget gDebris01("Boulder_01_INST02", wlObservatory);
```

- If you want to use variables between scripts use Global before the variable name.

Examples
```
Global Character c;
Global Vehicle v;
Global Bool b;
Global Number n;

// etc.
```

# 2. States. 

- We use them after variables. You can name the State whatever you want.

- To change states from one to another we use
```
goto MainB();
```

- And that's how States look
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

- All Worldlevels I found
```
WorldLevel wlPoliceGarage("Police_Station_Garage");
WorldLevel wlFinalMiniCut("tFinalBrickLevel");
WorldLevel wlFinalMiniCutLD("tLDTileName");
WorldLevel wlLocalFight("tTileName_Fight");
WorldLevel wlLocalForce("tTileName_HotspotForce1");
WorldLevel wlLocalScan("tTileName_Scan");
WorldLevel wlLocal("tTileName");
WorldLevel wlLocal("tWorldLevelName");
WorldLevel wlApartment("Apartment");
WorldLevel wlArena("Scrapyard_Arena");
WorldLevel wlBankConnection("Bank_Connection");
WorldLevel wlBankLobby("Bank_Interior");
WorldLevel wlBankSewer("Bank_Sewer");
WorldLevel wlBankSewer2("Bank_Sewer_02");
WorldLevel wlBankVault("Bank_Vault");
WorldLevel wlBoathouse("Fire_Station_Boathouse");
WorldLevel wlFireInterior("Fire_Station_Interior");
WorldLevel wlFireTraining("Fire_Station_Training_Area");
WorldLevel wlIcecreamBar("Icecream_Bar");
WorldLevel wlLevelIceCreamOffice("IceCream_Office");
WorldLevel wlLevelMansion1Cave("Mansion1_Cave");
WorldLevel wlLevelMansion1CaveTunnel("Mansion1_CaveTunnel");
WorldLevel wlLevelMansion2Exterior("Mansion2_Exterior");
WorldLevel wlLevelMineCavern("Mine_Cavern");
WorldLevel wlLevelMineTunnel("Mine_Tunnel");
WorldLevel wlLevelMoonBaseFinalBattle("MoonBase_FinalBattle");
WorldLevel wlLevelMoonBaseSpaceDive("MoonBase_SpaceDive");
WorldLevel wlLevelMoonBase1Crater("MoonBase1_Crater");
WorldLevel wlLevelMuseumRoom01("Museum_Room01");
WorldLevel wlLevelMuseumRoom02("Museum_Room02");
WorldLevel wlPoliceBriefingRoom("Police_Station_BriefingRoom");
WorldLevel wlScrapyardEntrance("Scrapyard_Entrance");
WorldLevel wlLevelMoonBase3RocketLoadingBay("MoonBase3_RocketLoadingBay");
WorldLevel wlCity("Lego_City");
WorldLevel wlCityFight("Lego_City_Fight");
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
cPlayer1.SetInvulnerable(true/false);
cPlayer1.SetPushable(true/false);
cPlayer1.SetNoCollision(true/false);
cPlayer1.SetNoTerrainCollision(true/false);
cPlayer1.SetArrestable(true/false);
cPlayer1.SetNoTagRelease(true/false);
cPlayer1.SetAvoidance(false);
cPlayer1.SetIgnoreCamVolumes(true);
cPlayer1.Kill();
cPlayer1.PlayContextAnimation("PoliceStation_StairSweep", -1); // 1 means it plays once, -1 means it's infinite
cPlayer1.Teleport( position, direction );
cPlayer1.Attack(cPlayer1);
cPlayer1.EnterVehicle(car, #DRIVER);
cPlayer1.ExitVehicle();
cPlayer1.SetAiOverride(true/false); // Lock a NPC in place.
cPlayer1.LockInPlace(true, "idle"); // You can use this
cPlayer1.Flee(cPlayer1);
cPlayer1.BeenKilled();
cPlayer1.Deactivate();
cPlayer1.InVehicle(car);
cPlayer1.Takeover(car);
cPlayer1.SetHealth(#Set, plyrHp + 1);
cPlayer1.SetVehicle( car, #Driver );
cPlayer1.SetWaypointDriveSpeed(locator, speed);
cPlayer1.HasClassAbilities("Cop");

car.Destroy(); 

gStairBlockage1.SetVisible(true);
gStairBlockage1.SetActive(true);
gStairBlockage1.Reset();

audio.Start(); // Starts an audio
audio.Stop(); // Stops an audio
```

- Get position, vehicle, etc of Player
```
cPlayer1.GetSpeed();
cPlayer1.GetPosition();
cPlayer1.GetRidden();
cPlayer1.GetVehicle();
cPlayer1.GetDirection();
cPlayer1.GetHealth();
cPlayer1.GetClass();
cPlayer1.GetModelName();
cPlayer1.GetPaintColour();
```

- Other things car and vehicle related
```
car.TurnOnSirene(true);
cPlayer1.IsSkydiving();
cPlayer1.EndSkydive();
cPlayer1.DeployParachute();
cPlayer1.SkydiveRotateToHeading( 20, 30 );
cPlayer1.SetAlternateChute(true);
cPlayer1.StartSkydiveMidfall();

cPlayer1.InArea(aCheckNearBike);

cPlayer1.DistanceTo( position );
cPlayer1.DistanceToXZ( position );
cPlayer1.MakeChaseCamFollow(position);
```

- Make the vehicle drive somewhere
```
cPlayer1.DriveTo(lSpawnPursuitBuggy_01, 4);
```

- Get the position of the player
```
Position playerpos(cPlayer1.GetPosition());
```

- Set Character Flags make the character unpushable, ignoregravity and make it not render
```
SetCharacterFlags(Character=C, #DontPush, #NoTerrain, #IgnoreGravity, #DontRender); // Change the C to your character name
```

- Make the player face an character, camera or locator
```
cPlayer1.FaceCharacter(character);
cPlayer1.FaceCamera();
cPlayer1.FaceLocator(lTowerObjective);
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
if(cPlayer1.InContext("AnimationTask")){};
if(cPlayer1.InContext("Attack")){};
if(cPlayer1.InContext("BenchPress")){};
if(cPlayer1.InContext("BouncePadJump")){};
if(cPlayer1.InContext("Brick Grab")){};
if(cPlayer1.InContext("BuckingBronco")){};
if(cPlayer1.InContext("CatchCat")){};
if(cPlayer1.InContext("DeathContext")){};
if(cPlayer1.InContext("Default")){};
if(cPlayer1.InContext("DetectiveMove")){};
if(cPlayer1.InContext("DJDeck")){};
if(cPlayer1.InContext("DrainPipes")){};
if(cPlayer1.InContext("DrillShock")){};
if(cPlayer1.InContext("DropPoint")){};
if(cPlayer1.InContext("Fall")){};
if(cPlayer1.InContext("Falling")){};
if(cPlayer1.InContext("flatten")){};
if(cPlayer1.InContext("FlyHover")){};
if(cPlayer1.InContext("GizSwitch")){};
if(cPlayer1.InContext("Gliding")){};
if(cPlayer1.InContext("Grabbed")){};
if(cPlayer1.InContext("Grapple")){};
if(cPlayer1.InContext("GrappleRope")){};
if(cPlayer1.InContext("Handcuff")){};
if(cPlayer1.InContext("HandCuffed")){};
if(cPlayer1.InContext("Hang")){};
if(cPlayer1.InContext("HPole")){};
if(cPlayer1.InContext("InBarrel")){};
if(cPlayer1.InContext("Jumping")){};
if(cPlayer1.InContext("Knockdown")){};
if(cPlayer1.InContext("Knockdown_Getup")){};
if(cPlayer1.InContext("Ladder")){};
if(cPlayer1.InContext("LandingFromJump")){};
if(cPlayer1.InContext("LandJump")){};
if(cPlayer1.InContext("Ledge")){};
if(cPlayer1.InContext("LegoItem")){};
if(cPlayer1.InContext("Mech Jump In")){};
if(cPlayer1.InContext("MechBigJump")){};
if(cPlayer1.InContext("MechClimbing")){};
if(cPlayer1.InContext("MechWallJumpWait")){};
if(cPlayer1.InContext("ParkourMove")){};
if(cPlayer1.InContext("PDAScanner")){};
if(cPlayer1.InContext("PoleClimbContext")){};
if(cPlayer1.InContext("Post Hop")){};
if(cPlayer1.InContext("PutDown")){};
if(cPlayer1.InContext("RexFuryStunned")){};
if(cPlayer1.InContext("RideAlong")){};
if(cPlayer1.InContext("RideObject")){};
if(cPlayer1.InContext("RocketOutOfControl")){};
if(cPlayer1.InContext("ShootTargetting")){};
if(cPlayer1.InContext("Shrug")){};
if(cPlayer1.InContext("SuperCarry")){};
if(cPlayer1.InContext("Swimming")){};
if(cPlayer1.InContext("Takedown_Getup")){};
if(cPlayer1.InContext("TakeHit")){};
if(cPlayer1.InContext("Techno")){};
if(cPlayer1.InContext("teleport")){};
if(cPlayer1.InContext("Throw")){};
if(cPlayer1.InContext("Thrown")){};
if(cPlayer1.InContext("Treadmill")){};
if(cPlayer1.InContext("UnlockDisguise")){};
if(cPlayer1.InContext("Wall Run")){};
if(cPlayer1.InContext("Whip")){};
if(cPlayer1.InContext("Whistle")){};
```

- Registers Events
```
RegisterEvent("AllGoldBricksCollected","function");
RegisterEvent("ArrivedAtTarget","function");
RegisterEvent("ArrivedAtWaypoint","function");
RegisterEvent("ArrivedToBouncePadTarget","function");
RegisterEvent("CityObjectiveCompleted","function");
RegisterEvent("CrashmatLanding","function");
RegisterEvent("CutsceneFinished","function");
RegisterEvent("EnteredVehicle","function");
RegisterEvent("ExitedVehicle","function");
RegisterEvent("FastTravelSelected","function");
RegisterEvent("FlowExitRequest","function");
RegisterEvent("FlowRetryRequest","function");
RegisterEvent("GameObjectObjHitObj","function");
RegisterEvent("HelipadLanding","function");
RegisterEvent("MapClosed","function");
RegisterEvent("MapOpened","function");
RegisterEvent("MoonBaseBossDefeated","function");
RegisterEvent("OnDriveTrain","function");
RegisterEvent("OnFastTravel","function");
RegisterEvent("OnSummaryCancel","function");
RegisterEvent("OnSummarySelection","function");
RegisterEvent("Player2HasDroppedOut","function");
RegisterEvent("PlayerExitedVehicle","function");
RegisterEvent("PlayerJackedVehicle","function");
RegisterEvent("PlayerVehicleAndAIVehicleCollision","function");
RegisterEvent("PlayerVehicleDestroyed","function");
RegisterEvent("PlayerVehicleHitKrawlie","function");
RegisterEvent("PlayerVehicleHitProp","function");
RegisterEvent("PlayerVehicleHitTraffic","function");
RegisterEvent("PlayerVehicleJumping","function");
RegisterEvent("PlayerVehicleNearlyWrecked","function");
RegisterEvent("PlayerVehicleOnRoof","function");
RegisterEvent("PlayerVehicleWaterRespawn","function");
RegisterEvent("RampActivated","function");
RegisterEvent("SideMissionMenuQuitRequest","function");
RegisterEvent("SideMissionMenuRetryRequest","function");
RegisterEvent("SideMissionMenuStartRequest","function");
RegisterEvent("VehicleTakenDamage","function");
RegisterEvent("WasTackled","function");
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
ShowObjectiveMarker(true);

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









