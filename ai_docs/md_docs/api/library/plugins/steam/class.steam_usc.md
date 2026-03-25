# Unigine::Plugins::Steam Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## Steam Class

### Members

---

## int steam. getAppID ( )

Returns Steam AppID.
### Return value

Steam AppID.
## int steam. isSubscribed ( )

Checks if the user is allowed to run the current app.
### Return value

**1** if the user is allowed to run the current app; otherwise **0**.
## int steam. isLowViolence ( )

Checks if the license owned by the user provides low violence depots.
### Return value

**1** if the license owned by the user provides low violence depots; otherwise **0**.
## int steam. isCybercafe ( )

Returns the value specifying if the current app is for Cyber Cafes.
### Return value

**1** if the current app is for Cyber Cafes; otherwise **0**.
## int steam. isVACBanned ( )

Checks if the user has a VAC ban on their account.
### Return value

**1** if the user has a VAC ban on their account; otherwise, **0**.
## string steam. getCurrentGameLanguage ( )

Returns the current language that the user has set.
### Return value

Language set by the user.
## string steam. getAvailableGameLanguages ( )

Returns a comma-separated list of languages.
### Return value

Comma-separated list of languages.
## string steam. getUserDataFolder ( )

Returns the name of the user data folder.
### Return value

Name of the user data folder.
## void steam. showOverlay ( string dialog )

Opens the Steam overlay to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: "friends", "community", "players", "settings", "officialgamegroup", "stats", "achievements".

## void steam. showOverlayToWebPage ( string url , int mode )

Activates Steam Overlay web browser directly to the specified URL.
### Arguments

- *string* **url** - The webpage to open (a fully qualified address with the protocol is required).
- *int* **mode** - Overlay mode to be set. One of the *[OVERLAY_TO_WEB_PAGE_MODE_*](#OVERLAY_TO_WEB_PAGE_MODE_DEFAULT)* values.

## void steam. showOverlayToUser ( string dialog , long steam_id )

Opens the Steam overlay to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: "steamid", "chat", "jointrade", "stats", "achievements", "friendadd", "friendremove", "friendrequestaccept", "friendrequestignore".
- *long* **steam_id** - The Steam ID of the context to open this dialog to.

## void steam. showOverlayToStore ( int app_id , int store_flag )

Activates the Steam Overlay to the Steam store page for the provided app.
### Arguments

- *int* **app_id** - The app ID to show the store page of.
- *int* **store_flag** - Flag to modify the behavior when the page opens, one of the [STEAM_OVERLAY_TO_STORE_*](#OVERLAY_TO_STORE_FLAG_NONE) values.

## void steam. showOverlayInviteDialog ( long steam_id_lobby )

Activates the Steam Overlay to open the invite dialog. Invitations sent from this dialog will be for the provided lobby.
### Arguments

- *long* **steam_id_lobby** - The Steam ID of the lobby that selected users will be invited to.

## void steam. setOverlayNotificationPosition ( int position )

Sets which corner the Steam overlay notification popup should display itself in.
### Arguments

- *int* **position** - The overlay notification popup position, one of the [STEAM_OVERLAY_POSITION_*](#OVERLAY_POSITION_TOP_LEFT) values.

## int steam. isOverlayShown ( )

Checks if the Steam Overlay is running and the user can access it.
### Return value

**1** if the overlay is running and the user can access it; otherwise **0**.
## long steam. getMyUserID ( )

Gets the current user's ID.
### Return value

The current user's ID.
## string steam. getMyName ( )

Gets the current user's persona (display) name. This is the same name that is displayed on the user's community profile page.
### Return value

The current user's persona (display) name.
## int steam. getMyState ( )

Returns the friend status of the current user.
### Return value

The friend state of the current user, one of the [STEAM_PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
## string steam. getUserName ( long steam_id_friend )

Returns the specified user's persona (display) name.
### Arguments

- *long* **steam_id_friend** - The Steam ID of the user.

### Return value

The current users persona name in UTF-8 format. Guaranteed to not be NULL. Returns an empty string (""), or "[unknown]" if the Steam ID is invalid or not known to the caller.
## int steam. getNumFriends ( int friend_flags )

Returns the number of users the client knows about who meet a specified criteria (friends, blocked, users on the same server, etc.).
### Arguments

- *int* **friend_flags** - A combined union (binary "or") of one or more [STEAM_FRIEND_FLAG_*](#FRIEND_FLAG_NONE) values.

### Return value

The number of users that meet the specified criteria. Returns -1 if the current user is not logged on.
## long steam. getFriendByIndex ( int ifriend , int ifriend_flags )

### Arguments

- *int* **ifriend** - An index between 0 and GetFriendCountFromSource.
- *int* **ifriend_flags** - .

### Return value

.
## int steam. getUserRelationship ( long steam_id_friend )

Returns a relationship to a specified user.
### Arguments

- *long* **steam_id_friend** - The Steam ID of the other user.

### Return value

Relationship to a specified user, one of the [STEAM_FRIEND_RELATIONSHIP_*](#FRIEND_RELATIONSHIP_NONE) values.
## int steam. getUserPersonaState ( long steam_id_friend )

Returns the status of the friend.
### Arguments

- *long* **steam_id_friend** - Steam ID of the user.

### Return value

Status of the friend, one of the [STEAM_PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
## Variable steam. getUserAvatarSmall ( long id )

Returns a handle to the small avatar for the specified user.
### Arguments

- *long* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (32*32 px) image. Returns 0 if no avatar is set for the user.
## Variable steam. getUserAvatarMedium ( long id )

Returns a handle to the medium avatar for the specified user.
### Arguments

- *long* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (64x64 px) image. Returns 0 if no avatar is set for the user.
## Variable steam. getUserAvatarLarge ( long id )

Returns a handle to the large avatar for the specified user.
### Arguments

- *long* **id** - Steam ID of the user.

### Return value

A Steam handle to the large (128*128 px) image. Returns 0 if no avatar is set for the user.
## SteamLeaderboard steam. createLeaderboard ( string name )

Returns the leaderboard interface.
### Arguments

- *string* **name** - Name of the leaderboard to be created.

### Return value

Leaderboard interface.
## SteamLeaderboard steam. getLeaderboard ( int id )

Returns the leaderboard interface.
### Arguments

- *int* **id** - ID of the leaderboard to view.

### Return value

Leaderboard interface.
## void steam. deleteLeaderboard ( SteamLeaderboard * OUT_leaderboard )

Deletes the leaderboard.
### Arguments

- *[SteamLeaderboard](../../../../api/library/plugins/steam/class.steamleaderboard_usc.md) ** **OUT_leaderboard** - Leaderboard interface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.
