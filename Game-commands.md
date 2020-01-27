# List of Commands
Commands are inputs you can use in-game to control the AI in a wide array of ways. Think of them not much as "Settings" but more like as "Tools" you can use to tweak the AI to your liking.<br> They are very useful, and are very recommended to be used at the beggining of the game (to set the AI on track to whatever initial prompt you used) or when the AI does something you don't like. You can use them whenever you like, even after a long while passed since you first started playing.

Using them is simple, just **type the command in the "input box"** where you usually make your prompts **and press enter**. Depending on the command, different further actions may be asked of you, but they are still pretty intuitive.

Example:<br>
If you wanted to use the command "/revert" because the AI did something unexpected as a reaction to your previous input, you would just need to type in the input box "/revert" (without quatation marks) and the command will work. Typing only "revert" **WILL NOT** work as a command, because the AI will interpret that as only a normal prompt, thus carrying on with the action you inputed.

================================================================

**Do note** that all commands are separated in categories depending on which versions of the game they work on. 
* Some are shared between all versions (mostly the "Base Game Commands").
* While others function only in the modded versions (either thadunge2 or Clover Edition) and, even then, some commands may work slightly different between those modded versions.

This page contains the commands available **up to the latest version** of the game, meaning that if you are using an old version you might not be able to use the newest ones at all.

================================================================

## Base Game Commands:

#### Insert ! before any starting sentence to insert it directly into the story. 
Example: !The dragon swoops down and eats one of the orcs before flying away.

Example 2: !You look at the back of Ganondorf's hand and see a golden triangle on it. You gasp as you realize he holds the triforce of power.

#### /revert 
This takes back the last action you just did and goes back 1 turn in the story.

***

## Thadunge and Clover Commands:

#### Insert ! before any starting sentence to insert it directly into the story. 
Example: !The dragon swoops down and eats one of the orcs before flying away.

Example 2: !You look at the back of Ganondorf's hand and see a golden triangle on it. You gasp as you realize he holds the triforce of power.

#### /revert 
This takes back the last action you just did and goes back 1 turn in the story.
  
#### /retry 
This is the equivalent of you typing /revert and then typing the same thing you just did and hitting enter. The AI will just do it for you so you do the same thing you just did but want a different outcome.

#### /quit 
Quits the game and saves.

#### /restart 
Starts the same game over but your prompt and temp/top_p/top_k settings are still the same. If you're using Thadunge it will also remember whatever you told the AI to remember when using /remember.

#### /print 
Shows the story so far without including any commands you input during it. Great for taking screenshots.

#### /help 
Shows the instructions again in case you forgot them or don't want to scroll up.

#### Thadunge:/temp #.# Clover:set temp #.#
Changes the AI's temperature. The simple way of putting it is how random the AI is. 0.2 is less random and more coherent. 0.4 is normal which is usually pretty random. 0.6 and up is just pure random nonsense which can be fun but don't expect a real coherent story to occur. The default is 0.4.

#### Thadunge:/top #.# Clover:set top_p 
Changes the AI's top_p. Default is 0.9. Might as well also be how random the AI is. I'd leave this alone unless you know what you're doing. If you lower it the story will be less random but the AI might have some problems. If you raise it all hell will probably break loose and it will just be worthless random occurrences the whole way through your story.

***

## Thadunge Only Commands:

#### /alter 
This let's you change the last thing the AI said. Example: You enter the forest and see a giant tree. You begin to climb the tree and stand on one of it's branches to check on your surroundings. Okay so I just said enter the forest I did NOT say climb a tree so let's /revert and choose 1)Remove a sentence. and just remove the bits about climbing the tree. The tree can stay for all I care I just want my actions to be my own. You can also edit the starting prompt of your story with this command.

#### /reset 
Ends the current game completely while saving it and starting fresh so you can enter a new prompt/choose a new starting prompt.

#### /cloud off/on 
Turns off and on cloud saving when you use the "save" command.

#### /save 
Makes a new save of your game and gives you the save ID.

#### /load 
Asks for a save ID and loads the game if the ID is valid.

#### /encrypt 
Turns on encryption when saving and loading.

#### /showstats 
Shows you the current game settings.

#### censor off/on 
Turn censoring off or on. It's off by default so if you want to do smut/don't care just leave this command alone.

#### /infto ## 
This will let you tell the AI to respond within a certain amount of seconds. I usually do /infto 20 so it responds within 20 seconds. Mind you, you don't really need to do this unless the AI is suddenly taking forever and you think it's stuck or something.

#### /raw off/on 
Don't bother touching this command just leave it set to off.

#### /remember XXX 
Make the AI remember something for the rest of the story so it doesn't forget in 12 turns. Example: /remember My name is Johnny. Another example: /remember Lilly is my cat girl slave.

#### /context 
This let's you edit whatever you put in /remember before. Example: Earlier you put /remember I am a potato. After you type /context it will say You know I am a potato. and you can edit it just like how you would edit with /revert and the AI will remember whatever it is you changed it to.

***

## Clover Only Commands:

#### set top_keks # 
Let's you set the top_k which might as well be how random the AI is. The only reason you should bother touching this is if you really want to make things more random by turning it up. Otherwise leave it alone. The default is 20.

#### set rep-pen #.#  
Below 1 encourages repeats(no one wants this). Above 1 penalizes repeats and tells the AI stop repeating itself like a broken record. Don't ever lower this value. Raise it if you think the AI is repeating itself too often.

#### set text-wrap-width 
Maximum width of lines printed by computer. Default: 80

#### set console-bell 
Beep after AI generates text? Default: on

#### set generate-num 
How long should the longest suggested actions be? higher is slower. Default is 60.

#### set log-level 
30 will not spam you with console log message, below 30 will spam devs. Default is 30.

#### set action-d20 off
This turns off the thing that makes you attempt every action which is trying to make the game harder. If you want more freedom turn this off.

#### /set action-sugg #
This sets the number of suggested actions. The higher the number the slower the game is to respond. Set it to 0 if you want to turn it off entirely.

#### /autosave
This saves after every move so that in the case of your game crashing or something going wrong you can just load the last save made instead of having to start over from the beginning. It also makes it so you don't have to stop playing to get a save state.