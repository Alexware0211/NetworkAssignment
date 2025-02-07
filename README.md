# NetworkAssignment

## Health Packs
[MedKit.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Props/HealthKit.cs) / [ObjectSpawner.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Props/ObjectSpawner.cs) / [RandomPointUtility.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Common/RandomPointUtility.cs)

Similar to the mine mechanics, a simple trigger detects if a player is positioned on a health pack. Upon usage, the med kit spawns a new one randomly while healing the player if their health is not already full. Notably, server-side logic governs the med kit functionality.

I also re-made the way the object spawn happens. It now uses the ObjectSpawner class to spawn all props (mines, healthkits) on the screen with the help of a utility script I wrote to get a random point inside of the camera.

## Shield Power-up
[Shield.cs](https://github.com/Alexware0211/NetworkAssignment//blob/main/Assets/Scripts/Player/Shield.cs) / [ShieldProp](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Props/ShieldProp.cs)

A shield power-up is added to the game, functioning similarly to health packs and mines. When picked up, it grants the player a shield that absorbs 2 hits. The shield status is synchronized across all clients. If the shield depletes, it's removed until the player picks up another. Damage first affects the shield, then the player's health. This can be seen in [Health.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Health.cs).

## Sprite Renderer
[PlayerController.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/PlayerController.cs)

Incorporating a sprite list for movement animation, a coroutine cycles through these sprites as the player moves, managed by the SpriteRenderer component. Client-side animation handling is preferred over server-side due to the non-secure nature of the animation logic.

## Shooting Cooldown
[FiringAction.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/FiringAction.cs)

Added a cooldown when shooting, I am un-sure if this system works, but based on my testing it seems to be fully functional.

## Overhead Names
[Name.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Name.cs), [NameUI.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/UI/CommonUI/NameUI.cs)

To display player names, the server utilizes SavedClientInformationManager to retrieve UserData containing each player's name. By referencing the NetworkObject's OwnerClientID, the server obtains the corresponding name, which is synchronized across all clients via a NetworkVariable. The NameUI class binds the player's name to a method that updates the UI text accordingly.

## Player Death
[Health.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Health.cs)

When a player's health reaches zero or below, their NetworkObject is despawned. This process is straightforward as the server already manages health-related operations.

## Limited Respawns
[Health.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Health.cs)

Players are assigned three lives, tracked through a NetworkVariable. Upon death, the lives decrement by one, and respawning involves resetting health and teleporting the player to a random position in the screen. Transitioning from server to owner methods for setting transform and health is facilitated via Remote Procedure Calls (RPCs). Once a player exhausts their lives, they are permanently despawned.

## Shield Power-up
[Shield.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Shield.cs) / [ShieldProp](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Props/ShieldProp.cs)

A shield power-up is added to the game, functioning similarly to health packs and mines. When picked up, it grants the player a shield that absorbs 2 hits. The shield status is synchronized across all clients. If the shield depletes, it's removed until the player picks up another. Damage first affects the shield, then the player's health. This can be seen in [Health.cs](https://github.com/Alexware0211/NetworkAssignment/blob/main/Assets/Scripts/Player/Health.cs).
