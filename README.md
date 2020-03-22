This project is intended to understand how Data Scientists compute a range of common metrics in a production context.

There are 10 prompts, all of which use the same data set. The data is described below, and a sample can be found in this folder. 

To contribute
-------------

You can assume that the data is a database or data lake of your choice.

For each prompt, we ask that you provide at least 1 and up to 5 separate ways to compute the metric from this data. Modify the file itself to include your solution.

Submit a pull request detailing:
* Which database or data lake you targeted.
* Edits to each prompt file with your script. Separate different solutions by a comment please.
* Leave any further comments in the script if you think they will help.
* Don't worry about exact syntactic correctness as long as you are using functions and syntax available in the dialect you choose.

We ask for a SQL response and for you to tell us which system you are tageting (e.g. pgSQL, sparkSQL, snowflake), though we don't care what dialect you use.


The data
--------

**Event Table**

This table records events in the application. Table name is `events`.

* EventId -- string (guid)
* SessionId -- string (guid)  Groups events into a user Session.
* UserId -- string (guid)  Groups Sessions and Events into a single user identifier. 
* EventName -- string  Event that triggered. Examples events are detailed below.
* Timestamp -- string (UTC time)  Client-side Timestamp
* ServerTime -- string (UTC time)   Server-side timestamp marked by collection mechanism.
* UserGroup -- string array   Comma-separated list of user groups that this user falls into. This is used to record which treatments in AB tests that this user falls into when the event fired.
* EventDetails -- string KVP   key-value pairs of information about the event. Assume it takes the structure "k=v&k2=v2". Assume that this is naively parsable by splitting on & then =.

**Event types**

|Event|Key|Meaning|
|---|---|---|
|impression|frompage|the source of this impression|
|impression|impressionid|guid for this impression|
|addToCart|impressionid|guid for the impression that led to add to cart|
|addToCart|item|guid for the item added|
|addToCart|frompage|the landing page that led to the add|
|addToCart|qty|quantity added for this action|
|enterCheckout|basketSize|Total basket quantity|
|completeCheckout|shippingOption|numerical code for shipping speed|
|completeCheckout|totalValue|dollar value of order.|
|removeFromCart|item|guid for item removed|
|removeFromCart|qty|quantity removed|


**User Table**

This table records user-level facts and is updated once per day. Table name is `users`.

* UserId -- string (guid) FK to the event table.
* Language -- string 
* DateCreated -- string (UTC time)  time of account creation

