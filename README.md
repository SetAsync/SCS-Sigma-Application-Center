# SCS-Sigma-Application-Center
The SCS-Sigma-Application-Center is a closed source commission.
https://www.roblox.com/groups/6961215/SCA-Sigma#!/about

This repository hosts the explanation and documentation for it.

## All Scripts
**PlayerHandler.lua**
Handles the player as soon as they join, asserts whether they have permission for the CenterLimits - sets ReplicatedStorage.Closed.Value to true if you do not have access.

**Networking.lua**
Handles SubmitApplication OnServerInvoke
Takes: ApplicationID, ApplicationResponse
Fetches Application with ApplicatedionID.
Checks the amount of questions and responses are equal - iterates through each response and uses SharedModule.GetResponseApplicable to ensure the response may be sent through Discord. Sends the Post request to your URL and handles any errors - returning them to the client to be displayed through NotificationService.

**SharedModule.lua**
Hosts the two important functions used by both Client and Server, EvaluateTerms and GetResponseApplicable. These are used by the Client to verify it has access to the application - the server then double checks that these checks have not been circumvented and the networking has been artifically invoked before posting to Discord.

**Main.lua**
Initializes the home screen, iterates through applications, uses SharedModule.EvaluateTerms to see if the player may use the application then styles the button accordingly. It then binds an event to each button - check if they may use it, if not throw an error through NotificationService, if they have permission access `script.Application` and call it.

**Application.lua**
Sets up all the events for each button, when next is clicked it checks if the response is applicable via SharedModule, if it's the last question it will change "Next" to "Submit" and InvokeServer in a safe enviorment, should an error be thrown upon Invokation it will be shown via NotificationService - if everything worked it will check the `Status` and `Data` returned from the server, if a controlled error occured during the server's oninvoke then this would have been returned as a `False` status.


## Settings
```lua
--[[

Welcome to the --]] configuration --[[ script.

  

DM me if you need any assistance.

  

____ _ _

/ ___| ___| |_ / \ ___ _ _ _ __ ___

\___ \ / _ \ __| / _ \ / __| | | | '_ \ / __|

___) | __/ |_ / ___ \\__ \ |_| | | | | (__

|____/ \___|\__/_/ \_\___/\__, |_| |_|\___| #7868

|___/

www.tinyurl.com/setasync-home

  

* Thank you! *

--]]

={}

-- Emergency Notice.

--[[

This is a notice that will be shown to users, if it is enabled.

Use this to get announcements out.

It will not impede the player's experience in any way.

--]]

configuration.EmergencyNotice = {

Active = false;

Title = "Warning - Delayed Response.";

Description = "Our application team are working hard to meet the amount of new applications, please bare with us during this hard time. Thank you."

}

  

-- Application Center Limits.

--[[

These are limits for players to meet. You can add limits like this:

{"GroupRank", 123123123, 255}

{"Group", 123123123}

--]]

configuration.CenterLimits = {

{"Group", 6961215}

}

configuration.CenterLimitsNotice = {

Title = "Access Denied.";

Description = "You do not meet the requirements for this application center."

}

  

  

-- Response Limits

--[[

These are limits for the responses.

--]]

configuration.MaximumLength = 1000

configuration.MinimumLength = 5

configuration.ResponseLimitNotice = {

Title = "Invalid Response",

Description = "Please make sure your response is 5-50 characters, thank you."

}

  

  

  

  

-- DONE ! --

configuration.Self = script

  

return configuration
```

## Application Template
```lua
--[[

Job Name: General Job Name

--]]

  

local ApplicationDisplay = {

Title = "Security Clearance-1";

Description = "Apply for a career further in the foundation!";

ButtonText = "Apply.";

Requirements = {

{"GroupRank", 6961215, 249}

};

}

  

local Application = {

"What would you do if High Ranking Personnel, like SC-4, wants you to break the rule? 3 sentences at least.";

"Describe SCP-999. 3 sentences at least.";

"Describe SCP-527. 3 sentences at least.";

"Name all departments.";

"Explain 1 department of your choice in detail. 3 sentences at least.";

}

  

return {ApplicationDisplay, Application}
```
