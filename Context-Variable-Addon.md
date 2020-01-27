ABOUT:

Added a "context" command you can use to change the context variable.

When you type some prompt, the AI is basically fed a context that is generated at the game start and never changes + the last n actions/results tuples + your prompt. 

The problem is that as story progresses that initial prompt might be out of date (e.g.: you might have failed to kill the dragon 30 prompts ago and the king removed your knighthood and now you're a bandit robbing merchants in the road). Another issue is that when you create a custom prompt your story doesn't seem to generate any context. 

This changes the Custom choice to first ask you for a context and then for the starting prompt so that custom stories also have contexts for the AI to read. 

What this means is that when you run the game, it now asks you a context, and then your usual prompt. The context will be remembered but the prompt will be forgotten after some entries (because of the limitations of the game, not because of this Addon).

Also added some shit mods that were in the github, added a few "try: except:" to previous to deal with the most common crashes and wrote some experimental code to try and cap the amount of words feeded to the AI to avoid getting the out of bounds. I still don't know the optimal cap but for now I set it at 700 (token cap seems to be 1024 tokens, so you might want to change it). If you get out of bounds errors consider lowering it.

Also the taskbar icon flashes when the game is done processing something.

Oh and it's set to use local storage for saving/loading rather than the Google bucket. Create a "stories" folder inside the game folder.

================================================================

DOUBTS:

>So if I copied all my custom promp in the context part while ALSO putting it in the starting prompt, will the AI remember better the custom prompt because of the context?

The context is the part you want it to remember forever, the starting prompt is just how you're starting your story off, and will eventually be forgotten (a few actions down the line).

So if you typed it on the context and starting prompt, it will be probably doubled info until it forgets the starting prompt. Not sure if it will make the doubled info more relevant, but shouldn't matter because it's only temporary anyways.
You should be able to put the entire thing there in context, but be really careful because it will remember everything there forever. So stuff like needing to kill a dragon will still be your mission even after killing said dragon.

================================================================

ADDON:

It's for the Local Windows version + CPU, you can either copy the interesting bits or if you're brainlet just use the whole file I guess.

[play.py](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Context-Variable-Addon-play.py)

[story_manager.py](https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/Context-Variable-Addon-story_manager.py)