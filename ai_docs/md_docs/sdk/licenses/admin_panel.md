# Managing Company Accounts and Licenses


## Admin Panel Overview


The company admin has the access to the Admin Panel available on the UNIGINE developer portal, that allows managing company accounts and licenses. To open the Admin Panel, do the following:


1. Go to *[developer.unigine.com](https://developer.unigine.com/)* and click the *Sign In* button in the top-right corner. ![](sign_in_button.png)
2. On the page that opens, sign in using your credentials. ![](developer_login.png)
3. As you are logged in, more options are available to you. ![](logged_top_menu.jpg)
4. Select the *[MY COMPANY](https://developer.unigine.com/my-company)* section. ![](company_info.png)


In the menu on the left side, the following sections are available:


- *COMPANY INFO* - provides the overall information on the total user amount, maximum upload capacity for the files uploaded to supplement support tickets. You can also edit such company information as website and phone there using the *Edit* button and manage the files uploaded to supplement support tickets via the *Manage files* button.
- *[USERS](#users)* - allows managing the company users: adding, deleting, editing, enabling, and disabling their profiles and modifying their roles.
- *MANAGE FILES* - the interface for managing the files uploaded to supplement support tickets.
- *SUPPORT TICKETS* - displays all support tickets created by the company users, allows viewing and editing them.
- *[LICENSE MANAGER](#license_manager)* - the interface for managing licenses and allocated seats.
- *[ACCESS CONTROL](#access_control)* - allows controlling access to various products for various groups of users according to their roles.


## USERS


This section allows managing the company users.


### Creating a New User


To create a new user, click the *Add User* button.


![](add_new_user.png)


The form will open:


![](add_user_form.png)


This form requires the following data to be filled in:


| EMAIL | User email that is used for logging in to [UNIGINE SDK Browser](../../sdk/index.md). |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FIRST NAME | The user's first name. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| LAST NAME | The user's last name. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| POSITION | The user's position in the company. This field is optional. |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| USER ROLE | The role assigned to the user to regulate the [access](#access_control) to SDKs and their materials. The following roles are available: \| User Role \| Developer \| Company Admin \| \|---\|---\|---\| \| Access to SDKs \| ![](yes.png) \| ![](yes.png) \| \| Create support tickets (if support is included) \| ![](yes.png) \| ![](yes.png) \| \| Manage own uploaded files (download, delete) \| ![](yes.png) \| ![](yes.png) \| \| Manage company files, including files uploaded via Support (download, delete) \| ![](no.png) \| ![](yes.png) \| \| Access to *My Company* interface \| ![](no.png) \| ![](yes.png) \| \| Manage user accounts (add, modify, delete, block) \| ![](no.png) \| ![](yes.png) \| \| Manage licenses (release seats, activate *Fixed* seats) \| ![](no.png) \| ![](yes.png) \| \| Control user access to products \| ![](no.png) \| ![](yes.png) \| | User Role | Developer | Company Admin | Access to SDKs | ![](yes.png) | ![](yes.png) | Create support tickets (if support is included) | ![](yes.png) | ![](yes.png) | Manage own uploaded files (download, delete) | ![](yes.png) | ![](yes.png) | Manage company files, including files uploaded via Support (download, delete) | ![](no.png) | ![](yes.png) | Access to *My Company* interface | ![](no.png) | ![](yes.png) | Manage user accounts (add, modify, delete, block) | ![](no.png) | ![](yes.png) | Manage licenses (release seats, activate *Fixed* seats) | ![](no.png) | ![](yes.png) | Control user access to products | ![](no.png) | ![](yes.png) |
| User Role | Developer | Company Admin |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Access to SDKs | ![](yes.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Create support tickets (if support is included) | ![](yes.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Manage own uploaded files (download, delete) | ![](yes.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Manage company files, including files uploaded via Support (download, delete) | ![](no.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Access to *My Company* interface | ![](no.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Manage user accounts (add, modify, delete, block) | ![](no.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Manage licenses (release seats, activate *Fixed* seats) | ![](no.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| Control user access to products | ![](no.png) | ![](yes.png) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |


### Managing Users


The Company Admin can manage the existing users. Click on the nickname of the user you want to modify. The *USER PROFILE* page will open.


![](user_profile.jpg)


To modify the user profile, click the *Edit* button.


![](edit_user.jpg)


In addition to the data set when [adding the user](#create_user), the following details are available for editing:


| NICKNAME | User nickname to be used on the UNIGINE forums. In can be changed on a semiannual basis only. |
|---|---|
| PASSWORD | User password. You can either type or generate a new password for the user. |
| SITE LANGUAGE | The language in which the website is displayed by default. Users can switch the website language on their own. |
| CDN | Content Delivery Network from which SDK will be downloaded. |


## LICENSE MANAGER


The ***License Manager*** section contains the information on available licenses and the users who currently use these licenses and allows managing the license allocation.


![](license_manager.jpg)


The details on the license are viewed by clicking on the corresponding product:


![](license_table.png)


1. Name of the product for which the license is purchased
2. Number of [seats](#seats) available (not allocated to anyone) out of the total number of [seats](#seats) purchased with the license
3. Date up to which you can download SDK updates
4. Date up to which you can use the engine runtime
5. Methods of [activating the license](../../sdk/licenses/index.md) available with this license
6. List of [allocated seats](#seats)


### Allocated Seats


The *Seat* is a kind of workplace for a developer or an artist involved in project development. It can be taken by any member of the team at a certain moment, then [released manually](#seat_deallocation) by the [Admin](#roles) via the Admin Panel and taken by another member.


![](allocated_seats.png)


The list of allocated seats contains information on who has taken the seat and which type of [activation method](../../sdk/licenses/index.md) has been used


### Seat Deallocation


To release the seat, click the ![](release_seat_button.png) button next to the corresponding allocated seat. This would allow disconnecting the license from the current user and making it available to another user.


> **Notice:** Only two deletions per day are allowed for the **Fixed** license activation.


### Generating Activation Code for Fixed License


To generate the activation code for the **Fixed** license that requires offline activation, you should have the [request code](../../sdk/licenses/activation.md#fixed_offline) generated on the PC where the SDK is going to run.


1. In the *License Manager* section of the [Admin Panel](#admin_panel), click the ***Get Code For Fixed License*** button. ![](get_code_button.png)
2. To generate an activation code for the SDK installed on a single PC, in the form that opens, choose the **ACTIVATION TYPE** *Single*. > **Notice:** Choose **Licensing Server** to generate a key for the [Licensing Server](../../sdk/licenses/licensing_server.md), a tool that serves seats or channels to all machines on a local network. In this case you select the product and the license to take the seats or channels from, and their number, instead of a user account. For complete step-by-step instructions, see the [Licensing Server](../../sdk/licenses/licensing_server.md#scenarios) article. Then choose the **LICENSE TYPE** (*Seats* or *Channels*), paste or type in the request code obtained in **[Step 5](../../sdk/licenses/activation.md#fixed_offline)**, write a note (optional), and click **Get code**. ![](get_activation_code.png) The activation code will be generated. > **Notice:** If the user changes the PC itself or some of the hardware components, a new activation code must be generated, and the seat should be reassigned.
3. Copy the activation code to the clipboard or download it as a `*.key` text file on the local disk by clicking the corresponding button. ![](activation_code_for_offline.jpg) > **Notice:** Depending on your web browser settings, the file can be automatically saved in the folder used by the web browser to store downloaded files. Usually, it is the `Downloads` folder.
4. Provide the activation code to the PC where the SDK that needs to be activated is installed in order to complete activation (**[Steps 7-9](../../sdk/licenses/activation.md#fixed_offline)**).


## ACCESS CONTROL


The *Access Control* section allows restricting users access to each of the available products.


![](access_control.png)


By default, when a new user is added, all SDKs licensed to the company automatically become available to them (the box is checked for all available products).


You can check and uncheck every box individually.


It is also possible to **select a user or users** by checking a box near their name and use the ***Grant All / Revoke All*** buttons to grant (or revoke) access to all products for selected user(s).
