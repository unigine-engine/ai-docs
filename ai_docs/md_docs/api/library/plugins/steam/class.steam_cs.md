# Unigine::Plugins::Steam Class (CS)

> **Notice:** This class is a singleton.


## Steam Class

### Enums

## CALLBACK_INDEX

| Name | Description |
|---|---|
| **OVERLAY_SHOWN** = 0 | Triggered when the Steam Overlay is shown or hidden. The callback receives a flag indicating whether the overlay is now active. |
| **LEADERBOARD_FOUND** = 1 | Triggered when a requested leaderboard has been found on the Steam back-end. |
| **LEADERBOARD_SCORES_UPLOADED** = 2 | Triggered when a score upload to a leaderboard has finished. The callback receives whether the upload failed and whether the stored score has changed. |
| **LEADERBOARD_SCORES_DOWNLOADED** = 3 | Triggered when a leaderboard entries download has finished. The callback receives whether the download failed and the type of the data request. |

## PERSONA_STATE

| Name | Description |
|---|---|
| **OFFLINE** = 0 | Friend is not currently logged on. |
| **ONLINE** = 1 | Friend is logged on. |
| **BUSY** = 2 | User is on, but busy. |
| **AWAY** = 3 | Auto-away feature. |
| **SNOOZE** = 4 | Auto-away for a long time. |
| **LOOKING_TO_TRADE** = 5 | Online, trading. |
| **LOOKING_TO_PLAY** = 6 | Online, wanting to play. |

## FRIEND_FLAG

| Name | Description |
|---|---|
| **NONE** = 0 | None. |
| **BLOCKED** = 1 | Users that the current user has blocked from contacting. |
| **FRIENDSHIP_REQUESTED** = 2 | Users that have sent a friend invite to the current user. |
| **IMMEDIATE** = 4 | The current user's "regular" friends. |
| **CLAN_MEMBER** = 8 | Users that are in one of the same (small) Steam groups as the current user. |
| **ON_GAME_SERVER** = 16 | Users that are on the same game server. |
| **REQUESTING_FRIENDSHIP** = 128 | Users that the current user has sent friend invites to. |
| **REQUESTING_INFO** = 256 | Users that are currently sending additional info about themselves. |
| **IGNORED** = 512 | Users that the current user has ignored from contacting them. |
| **IGNORED_FRIEND** = 1024 | Users that have ignored the current user; but the current user still knows about them. |
| **ALL** = 65535 | All friend flags. |

## FRIEND_RELATIONSHIP

| Name | Description |
|---|---|
| **NONE** = 0 | The users have no relationship. |
| **BLOCKED** = 1 | The user has just clicked Ignore on an friendship invite. This doesn't get stored. |
| **REQUEST_RECIPIENT** = 2 | The user has requested to be friends with the current user. |
| **FRIEND** = 3 | A "regular" friend. |
| **REQUEST_INITIATOR** = 4 | The current user has sent a friend invite. |
| **IGNORED** = 5 | The current user has explicit blocked this other user from comments/chat/etc. This is stored. |
| **IGNORED_FRIEND** = 6 | The user has ignored the current user. |

## OVERLAY_TO_STORE

| Name | Description |
|---|---|
| **FLAG_NONE** = 0 | No. |
| **ADD_TO_CART** = 1 | Add the specified app ID to the user's cart. |
| **ADD_TO_CART_AND_SHOW** = 2 | Add the specified app ID to the user's cart and show the store page. |

## OVERLAY_POSITION

| Name | Description |
|---|---|
| **TOP_LEFT** = 0 | Top left corner position of the overlay notification popup. |
| **TOP_RIGHT** = 1 | Top right corner position of the overlay notification popup. |
| **BOTTOM_LEFT** = 2 | Bottom left corner position of the overlay notification popup. |
| **BOTTOM_RIGHT** = 3 | Bottom right corner position of the overlay notification popup. |

## OVERLAY_TO_WEB_PAGE_MODE

Overlay mode to be used.
| Name | Description |
|---|---|
| **DEFAULT** = 0 | The web page is opened in the standard Steam Overlay browser window. |
| **MODAL** = 1 | The web page is opened in a modal Steam Overlay browser window that the user must dismiss before returning to the game. |

### Properties

## 🔒︎ Steam.PERSONA_STATE MyState

The friend status of the current user. One of the [PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
## 🔒︎ string MyName

The persona (display) name of the current user. This is the same name that is displayed on the user's community profile page.
## 🔒︎ ulong MyUserID

The ID of the current user.
## 🔒︎ bool IsOverlayShown

The value indicating if the Steam Overlay is running and the user can access it.
## 🔒︎ string UserDataFolder

The name of the user data folder.
## 🔒︎ string AvailableGameLanguages

The comma-separated list of languages.
## 🔒︎ string CurrentGameLanguage

The language that the user has set.
## 🔒︎ bool IsVACBanned

The value indicating if the user has a VAC ban on their account.
## 🔒︎ bool IsCybercafe

The value specifying if the current app is for cyber cafes.
## 🔒︎ bool IsLowViolence

The value indicating if the license owned by the user provides low violence depots.
## 🔒︎ bool IsSubscribed

The value indicating if the user is allowed to run the current app.
## 🔒︎ int AppID

The Steam AppID.
### Members

---

## void ShowOverlay ( string dialog )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: *"friends", "community", "players", "settings", "officialgamegroup", "stats", "achievements"*.

## void ShowOverlayToWebPage ( string url , Steam.OVERLAY_TO_WEB_PAGE_MODE mode )

Activates *Steam Overlay* web browser directly to the specified URL.
### Arguments

- *string* **url** - The webpage to open (a fully qualified address with the protocol is required).
- *[Steam.OVERLAY_TO_WEB_PAGE_MODE](../../../../api/library/plugins/steam/class.steam_cs.md#OVERLAY_TO_WEB_PAGE_MODE)* **mode** - Overlay mode to be set. One of the *[OVERLAY_TO_WEB_PAGE_MODE_*](#OVERLAY_TO_WEB_PAGE_MODE_DEFAULT)* values.

## void ShowOverlayToUser ( string dialog , ulong steam_id )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: *"steamid", "chat", "jointrade", "stats", "achievements", "friendadd", "friendremove", "friendrequestaccept", "friendrequestignore"*.
- *ulong* **steam_id** - The Steam ID of the context to open this dialog to.

## void ShowOverlayToStore ( int app_id , Steam.OVERLAY_TO_STORE store_flag )

Activates the *Steam Overlay* to the Steam store page for the provided app.
### Arguments

- *int* **app_id** - The app ID to show the store page of.
- *[Steam.OVERLAY_TO_STORE](../../../../api/library/plugins/steam/class.steam_cs.md#OVERLAY_TO_STORE)* **store_flag** - Flag to modify the behavior when the page opens, one of the [OVERLAY_TO_STORE.*](#OVERLAY_TO_STORE_FLAG_NONE) values.

## void ShowOverlayInviteDialog ( ulong steam_id_lobby )

Activates the *Steam Overlay* to open the invite dialog. Invitations sent from this dialog will be for the provided lobby.
### Arguments

- *ulong* **steam_id_lobby** - The Steam ID of the lobby that selected users will be invited to.

## void SetOverlayNotificationPosition ( Steam.OVERLAY_POSITION position )

Sets which corner the *Steam Overlay* notification popup should display itself in.
### Arguments

- *[Steam.OVERLAY_POSITION](../../../../api/library/plugins/steam/class.steam_cs.md#OVERLAY_POSITION)* **position** - The overlay notification popup position, one of the [OVERLAY_POSITION.*](#OVERLAY_POSITION_TOP_LEFT) values.

## string GetUserName ( ulong steam_id_friend )

Returns the specified user's persona (display) name.
### Arguments

- *ulong* **steam_id_friend** - The Steam ID of the user.

### Return value

The current users persona name in UTF-8 format. Guaranteed to not be NULL. Returns an empty string (""), or "[unknown]" if the Steam ID is invalid or not known to the caller.
## int GetNumFriends ( int friend_flags )

Returns the number of users the client knows about who meet a specified criteria (friends, blocked, users on the same server, etc.).
### Arguments

- *int* **friend_flags** - A combined union (binary "or") of one or more [FRIEND_FLAG.*](#FRIEND_FLAG_NONE) values.

### Return value

The number of users that meet the specified criteria. Returns -1 if the current user is not logged on.
## ulong GetFriendByIndex ( int ifriend , int ifriend_flags )

Returns the Steam ID of the friend at the specified index in the list of users that meet the given criteria.
### Arguments

- *int* **ifriend** - Index of the friend, in the range from 0 to the value returned by [getNumFriends()](#getNumFriends_int_int) for the same flags.
- *int* **ifriend_flags** - A combined union (binary "or") of one or more [FRIEND_FLAG.*](#FRIEND_FLAG_NONE) values, matching the flags passed to [GetNumFriends()](#getNumFriends_int_int).

### Return value

The Steam ID of the friend at the given index.
## Steam.FRIEND_RELATIONSHIP GetUserRelationship ( ulong steam_id_friend )

Returns a relationship to a specified user.
### Arguments

- *ulong* **steam_id_friend** - The Steam ID of the other user.

### Return value

Relationship to a specified user, one of the [FRIEND_RELATIONSHIP.*](#FRIEND_RELATIONSHIP_NONE) values.
## Steam.PERSONA_STATE GetUserPersonaState ( ulong steam_id_friend )

Returns the status of the friend.
### Arguments

- *ulong* **steam_id_friend** - Steam ID of the user.

### Return value

Status of the friend, one of the [PERSONA_STATE.*](#PERSONA_STATE_OFFLINE) values.
## Variable GetUserAvatarSmall ( ulong id )

Returns a handle to the small avatar for the specified user.
### Arguments

- *ulong* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (32*32 px) image. Returns 0 if no avatar is set for the user.
## Variable GetUserAvatarMedium ( ulong id )

Returns a handle to the medium avatar for the specified user.
### Arguments

- *ulong* **id** - Steam ID of the user.

### Return value

A Steam handle to the small (64x64 px) image. Returns 0 if no avatar is set for the user.
## Variable GetUserAvatarLarge ( ulong id )

Returns a handle to the large avatar for the specified user.
### Arguments

- *ulong* **id** - Steam ID of the user.

### Return value

A Steam handle to the large (128*128 px) image. Returns 0 if no avatar is set for the user.
## SteamLeaderboard CreateLeaderboard ( string name )

Returns the leaderboard interface.
### Arguments

- *string* **name** - Name of the leaderboard to be created.

### Return value

Leaderboard interface.
## SteamLeaderboard GetLeaderboard ( int id )

Returns the leaderboard interface.
### Arguments

- *int* **id** - ID of the leaderboard to view.

### Return value

Leaderboard interface.
## void DeleteLeaderboard ( SteamLeaderboard [] OUT_leaderboard )

Deletes the leaderboard.
### Arguments

- *[SteamLeaderboard](../../../../api/library/plugins/steam/class.steamleaderboard_cs.md)[]* **OUT_leaderboard** - Leaderboard interface. > **Notice:** This output buffer is to be filled by the Engine as a result of executing the method.

## IntPtr addCallback ( Steam.CALLBACK_INDEX callback , CallbackDelegate func )


Adds a callback of the specified type. The signature of the callback function depends on the callback type:


- [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN) - **void callback(unsigned char shown)**
- [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND) - **void callback(int id)**
- [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED) - **void callback(int id, int failed, unsigned char score_changed)**
- [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED) - **void callback(int id, int failed, int data_request)**


### Arguments

- *[Steam.CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cs.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
- *CallbackDelegate* **func** - Callback function.

### Return value

ID of the added callback, if the callback was added successfully; otherwise, **-1**.
## bool removeCallback ( Steam.CALLBACK_INDEX callback , IntPtr id )

Removes the callback with the given ID from the list of callbacks of the specified type.
### Arguments

- *[Steam.CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cs.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
- *IntPtr* **id** - ID of the callback to be removed (returned by [addCallback()](#addCallback_int_CallbackBase_ptr_void_ptr)).

### Return value

true if the callback with the given ID was removed successfully; otherwise, false.
## void clearCallbacks ( Steam.CALLBACK_INDEX callback )

Clears all added callbacks of the specified type.
### Arguments

- *[Steam.CALLBACK_INDEX](../../../../api/library/plugins/steam/class.steam_cs.md#CALLBACK_INDEX)* **callback** - Callback type. One of the following values:

  - [CALLBACK_OVERLAY_SHOWN](#CALLBACK_OVERLAY_SHOWN)
  - [CALLBACK_LEADERBOARD_FOUND](#CALLBACK_LEADERBOARD_FOUND)
  - [CALLBACK_LEADERBOARD_SCORES_UPLOADED](#CALLBACK_LEADERBOARD_SCORES_UPLOADED)
  - [CALLBACK_LEADERBOARD_SCORES_DOWNLOADED](#CALLBACK_LEADERBOARD_SCORES_DOWNLOADED)
