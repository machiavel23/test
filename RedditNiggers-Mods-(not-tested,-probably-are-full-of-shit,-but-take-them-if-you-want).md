Some mods for you [(original link)](https://www.reddit.com/r/AIDungeon/comments/e92ft2/some_mods_for_you/).

Here are some mods (patches) I created for the game that you might want to install on your installation or colab file.

- [Hang detection](https://gist.github.com/MightyAlex200/f640fbca963788d096c2505d30cb4665).
Stops the model and returns control to the user if inference takes over 30 seconds (the time is configurable using the infto command

- [Custom prompt is final](https://gist.github.com/MightyAlex200/528804ea07905d6b29e060c14b6c617c).
I find it somewhat annoying that the game adds stuff to your custom prompt after you have finished writing it, so this removes that feature (for custom prompts only)

- ["Unrestricted mode"](https://gist.github.com/MightyAlex200/424faa2b3fd5fdf7ffb5b92ec57feeb4).
I couldn't think of a good name for this one, but if you prepend your command with '!', it will inject what you write directly into the story, without having it go through automatic conversion into an action. (e.g. typing "The dragon flies off" is converted to "> You the dragon files off." by default, but with this patch, typing "!The dragon flies off" will insert that sentence directly into the story) (You can use the print command to check out what I mean)

- [Retry command](https://gist.github.com/MightyAlex200/973018426ee126e2783b0f13ec07dca2).
Adds a command retry that allows you to get a different outcome using the same action.
You may run into some warnings about whitespace errors if you apply this with hang detection, but as long as it says "Patch applied", it should work fine

================================================================

How to install:

(If you are using colab, you must create a copy in your google drive to modify it)

>1) The first thing you need to do to install these mods is to make sure you have the full git repo downloaded. If you are using colab, you need to change the first line of the first code cell from !git clone --depth 1 --branch master https://github.com/AIDungeon/AIDungeon/ to !git clone https://github.com/AIDungeon/AIDungeon/ (remove the --depth 1 and --branch master)
>2) Next you can copy the code from any of the mods and place it into its own code cell (you can create new code cells with the button labelled "+ Code" in the top left). You must run these after running the first cell, and every time you play the game, otherwise they will not apply correctly. After they run you should see the last line saying "Patch applied!" if it worked.
>3) If you have a local installation of the game, simply enter the directory you have the game installed in, open a bash shell and paste the code of the patches in to install (excluding the first line %%bash, which only works in Colab and jupyter). Patches installed on a local installation do not have to be applied again, unless you update to a newer version and do not merge your current branch with the new updates.

Disclaimer:

>Due to the fast paced development of the game, there is a very high chance these will run in to some sort of merge conflict at some point and no longer be usable on the latest version. 