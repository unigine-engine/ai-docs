# Unigine::Plugins::Steam Class (USC)

> **Warning:** The scope of applications for UnigineScript is limited to implementing materials-related logic (material expressions, scriptable materials, brush materials). Do not use UnigineScript as a language for application logic, please consider C#/C++ instead, as these APIs are the preferred ones. Availability of new Engine features in UnigineScript (beyond its scope of applications) is not guaranteed, as the current level of support assumes only fixing critical issues.

> **Notice:** This class is a singleton.


## Steam Class

### Members

## int getMyState () const

Returns the current friend status of the current user. One of the [PERSONA_STATE_*](#PERSONA_STATE_OFFLINE) values.
### Return value

Current friend status of the current user
## const char * getMyName () const

Returns the current persona (display) name of the current user. This is the same name that is displayed on the user's community profile page.
### Return value

Current persona (display) name of the current user
## long getMyUserID () const

Returns the current ID of the current user.
### Return value

Current ID of the current user
## int isOverlayShown () const

Returns the current value indicating if the Steam Overlay is running and the user can access it.
### Return value

Current the Steam Overlay is running and the user can access it
## const char * getUserDataFolder () const

Returns the current name of the user data folder.
### Return value

Current name of the user data folder
## const char * getAvailableGameLanguages () const

Returns the current comma-separated list of languages.
### Return value

Current comma-separated list of languages
## const char * getCurrentGameLanguage () const

Returns the current language that the user has set.
### Return value

Current language that the user has set
## int isVACBanned () const

Returns the current value indicating if the user has a VAC ban on their account.
### Return value

Current the user has a VAC ban on their account
## int isCybercafe () const

Returns the current value specifying if the current app is for cyber cafes.
### Return value

Current the current app is for cyber cafes
## int isLowViolence () const

Returns the current value indicating if the license owned by the user provides low violence depots.
### Return value

Current the license owned by the user provides low violence depots
## int isSubscribed () const

Returns the current value indicating if the user is allowed to run the current app.
### Return value

Current the user is allowed to run the current app
## getAppID () const

Returns the current Steam AppID.
### Return value

Current Steam AppID
---

## void steam. showOverlay ( string dialog )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: *"friends", "community", "players", "settings", "officialgamegroup", "stats", "achievements"*.

## void steam. showOverlayToWebPage ( string url , int mode )

Activates *Steam Overlay* web browser directly to the specified URL.
### Arguments

- *string* **url** - The webpage to open (a fully qualified address with the protocol is required).
- *int* **mode** - Overlay mode to be set. One of the *[OVERLAY_TO_WEB_PAGE_MODE_*](#OVERLAY_TO_WEB_PAGE_MODE_DEFAULT)* values.

## void steam. showOverlayToUser ( string dialog , long steam_id )

Opens the *Steam Overlay* to the specified dialog.
### Arguments

- *string* **dialog** - The dialog to open. Valid options are: *"steamid", "chat", "jointrade", "stats", "achievements", "friendadd", "friendremove", "friendrequestaccept", "friendrequestignore"*.
- *long* **steam_id** - The Steam ID of the context to open this dialog to.

## void steam. showOverlayToStore ( int app_id , int store_flag )

Activates the *Steam Overlay* to the Steam store page for the provided app.
### Arguments

- *int* **app_id** - The app ID to show the store page of.
- *int* **store_flag** - Flag to modify the behavior when the page opens, one of the [STEAM_OVERLAY_TO_STORE_*](#OVERLAY_TO_STORE_FLAG_NONE) values.

## void steam. showOverlayInviteDialog ( long steam_id_lobby )

Activates the *Steam Overlay* to open the invite dialog. Invitations sent from this dialog will be for the provided lobby.
### Arguments

- *long* **steam_id_lobby** - The Steam ID of the lobby that selected users will be invited to.

## void steam. setOverlayNotificationPosition ( int position )

Sets which corner the *Steam Overlay* notification popup should display itself in.
### Arguments

- *int* **position** - The overlay notification popup position, one of the [STEAM_OVERLAY_POSITION_*](#OVERLAY_POSITION_TOP_LEFT) values.

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

Returns the Steam ID of the friend at the specified index in the list of users that meet the given criteria.
### Arguments

- *int* **ifriend** - Index of the friend, in the range from 0 to the value returned by [getNumFriends()](#getNumFriends_int_int) for the same flags.
- *int* **ifriend_flags** - A combined union (binary "or") of one or more [STEAM_FRIEND_FLAG_*](#FRIEND_FLAG_NONE) values, matching the flags passed to [getNumFriends()](#getNumFriends_int_int).

### Return value

The Steam ID of the friend at the given index.
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
## void steam. setCallback ( int num , Variable name )

Sets a callback function of the specified type.
### Arguments

- *int* **num** - Callback type. One of the [STEAM_CALLBACK_*](#CALLBACK_OVERLAY_SHOWN) values.
- *Variable* **name** - Callback function to be set. There are two ways you can specify a callback function:

  - **by name** - when you call a function declared globally.
  - **by ID** - when you call a member function of a certain class. > **Notice:** An ID can be obtained via [functionid()](../../../../api/library/common/class.system_usc.md#functionid_variable_int).

## Variable steam. getCallback ( int num )

Returns the callback function set for the specified type.
### Arguments

- *int* **num** - Callback type. One of the [STEAM_CALLBACK_*](#CALLBACK_OVERLAY_SHOWN) values.

### Return value

Callback function set for the specified type.
