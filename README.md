# OctoPrint-OctoRant

OctoRant is a plugin allowing Octoprint to send notifications to a Discord channel via a webhook URL. When necessary it can directly send a snapshot to Discord (without needing third-party services)

Licence : MIT 


**TODO** : Change placeholder images by screenshots

![Screeshot of the Discord messages](assets/img/discord.jpg)

![Screesho of the settings panel](assets/img/settings.jpg)


## Setup

### Install the plugin

Install via the bundled [Plugin Manager](https://github.com/foosel/OctoPrint/wiki/Plugin:-Plugin-Manager)
or manually using this URL:

    https://github.com/bchanudet/OctoPrint-Octorant/archive/master.zip

### Create the WebHook in Discord

*Note : you need to have the permission "Manage WebHooks" to create or edit a WebHook in Discord.*

**TODO** : Change placeholder images by screenshots

![Go to the channel settings](assets/docs/discord_setup_2.jpg)

![Under "Webhooks", click "Create Webhook"](assets/docs/discord_setup_2.jpg)

![Enter the details, and copy the URL at the bottom](assets/docs/discord_setup_2.jpg)

Once you got the WebHook URL, head over to the plugin configuration to finish the setup.

## Configuration

The plugin can be configured in the configuration panel, under the "Octorant" panel.

### Discord Settings

- WebHook URL : please follow the Setup procedure to retrieve the URL of the WebHook.
- Bot name : You can override the name you put on the WebHook description in Discord by a name. Useful if the webhook is not specific to Octorant and also used for other things.
- Bot Avatar URL : You can also override the avatar us put in Discord for the WebHook. The URL needs to be globally accessible (it will be retrieved by Discord's servers).

In order for you to be sure these settings work, every time you change one of them, a test message will be sent to the corresponding Discord Channel. If you don't receive it, something is most likely wrong!

### Message Settings

Here you can customize every message handled by Octorant.

- **Toggle the message** : by unchecking the checkbox in front of the message title, you can disable the message. It won't be sent to Discord.
- **Message** : you can change the default content here. See the section [Message format](#message-format) for more information.
- **Include snapshot** : if you have a snapshot URL defined in the Octoprint settings, you can choose to upload a snapshot with the message to Discord. 
- **Notify every `XX`%** : specific to the `printing progress` message, this settings allows you to change the frequency of the notification : 
    - `10%` means you'll receive a message at 10%, 20%, 30%, 40% ... 80%, 90% of the printing process.
    - `5%` means you'll receive a message at 5%, 10%, 15%, 20% ... 80%, 85%, 90%, 95% of the printing process.


## Message format

Messages are regular Discord messages, which means you can use :
- `**markdown**` format 
- `:emoji:` shortcuts to display emojis
- `@mentions` to notify someone

Some events support variables, here is a basic list : 

**Printing process : started event** :
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location

**Printing process : failed event** :
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location

**Printing process : done event** : 
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location
- `{time}`: time needed for the print (in seconds)

**Printing process : failed event** :
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location
- `{time}`: time needed for the print (in seconds)
- `{position}`: position of the hotend

**Printing process : paused event** :
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location
- `{time}`: time needed for the print (in seconds)
- `{position}`: position of the hotend

**Printing process : resumed event** :
- `{name}` : file's name that's being printed
- `{path}` : file's path within its origin location
- `{origin}` : the origin storage location
- `{time}`: time needed for the print (in seconds)
- `{position}`: position of the hotend

**Printing progress event** :
- `{progress}` : progress in % of the print.

**Printer state : error**
- `{error}` : The error received 
