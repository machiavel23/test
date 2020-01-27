================================================================

         Evolution of the GitHub repos that have been used by Anons in the threads so far

================================================================

>nickwalton/AIDungeon (original/vanilla, changed to AIDungeon/AIDungeon around 9/12/19 and added a censor toggle around 11/12/19)

>PolarManne/AIDungeon (uncensored, Tarumath was the same repo but a different collab) [7/12/19]

>WAUthethird/AIDungeon-Uncensored (second uncensored version) [10/12/19]

>original Drive method stops working

>Akababa/AIDungeon (censored) [10/12/19]

>Telain/AIDungeon and asazary/AIDungeon (uncensored) [10/12/19]

>aidungeon99999/AIDungeon-Uncensored (fork of WAUthethird, created because people were wary of the previous forks, then received temperature tweaks and eventually let you pick temp and top_k before starting) [11/12/19]

>Sojournophile/AIDungeon-Uncensored (fork of aidungeon99999, to circumvent anon99999's drama whoring) [11/12/19]

>Tarumath/Thadunge2-Fork-Working-Colab (repo with Colab that let you play directly with thadunge2 fork) [12/12/19]


================================================================

                      Current most used forks (all are active in development)

================================================================

>[Kornilov1/Open CYOAI Project](https://github.com/Kornilov1/AI-Dungeon-2-Anons-modded-Versions-Colab) (Colab frontend that lets you use the different modded versions of the game, added a bunch of cells, guides and functionalities that makes the installing and playing experiences smother and easier) 
>
>(After some false flagging attacks, the related GitHub account got flagged, i.e. not available to the public. But the account was successfully unflagged and a change of account name was put in place, but no files or repository got changed.) Current account: [VBPXKSMI/Open CYOAI Project](https://github.com/VBPXKSMI/Open-CYOAI-Project) [13/12/19] 

>[thadunge2/AIDungeon](https://github.com/thadunge2/AIDungeon) (not a proper fork of vanilla, merged a bunch of mods and added new functions, see bellow and [this addon](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Context-Variable-Addon) for changes) [12/12/19]

Changelog (as of writing this) of thadunge2 version:
- Commented out cloud saving phone-home shit, only saves locally
- Moved saves to a dedicated save folder
- Censor off by default
- Added "retry" command that reverts and resubmits the last command.
- You can objectively influence the story by prefacing your command with "!" (e.g. "!A dragon swoops in and eats Sir Theo.")
- Made the game parse your commands into second person a little better
- Eliminated index crash when the story goes on for too long
- Added timeout to return control to you when the AI gets stuck generating a response
- You can now adjust AI temperature on the fly
- Added a command to permanently add things to the AI's memory for that story
- Tried to make the AI a little more descriptive and less likely to just repeat your prompt back to you
- Tried to make conversations a little more fleshed out
- Fixed a bug that made the AI suggest actions for you.
- Improved the editing on the action and response text so you should get fewer incomplete sentences and stuff.
- Improved the part of the code that prefixes sentences with "You"
- AI should be way more coherent now and no longer suggest (as many) actions for you
- The game will no longer strip the final period off what the AI returns, which will confuse it less over long periods and give better results
- Your own submitted action is now removed from the result if it shows up there so it doesn't just parrot you.
- Prompt inputs sanitized now to confuse the AI less
- Made a change to how blank inputs are handled to make them less confusing to the AI
- ! inputs also properly sent to the AI
- Bad and naughty AIs get sent back to generate another response
There might be an increase in hang timeouts as the AI's response gets rejected and it has to regenerate more.

>[CloverAnon/Clover-Edition](https://github.com/cloveranon/Clover-Edition) (not a proper fork of vanilla, more of a re-write of the game than a mod) [16/12/19]

Changelog (as of writing this) of CloverAnon version:
- Complete rewrite of the user interface
- Color text output
- Console Bell when AI finishes
- Much improved prompt selection
- A much larger library of fan made starting prompts
- Better config file
- Eventually hope to improve the AI itself, but this will take some time


================================================================

To access any of this GitHubs, you just have to add https://github.com/ (before any of those accounts) to get the link. 
Remember that you can use the forks both for the Colab (online) and the Local (offline) versions, for instructions on how to do that: it's already included in the Colab version and for the Local one just go [here](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/How-To-Install-AI-Dungeon-2-Locally-On-Windows-(Manual-and-Automatic-installations)) and read the instructions.