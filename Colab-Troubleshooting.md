AI Dungeon 2 Cloveranon/Thadunge Colab Troubleshooting Advice

First of all **this page is for the Colab only**. I don't know anything about playing it offline. If you want a guide on how to play cloveranon's version offline just go [here](https://github.com/cloveranon/Clover-Edition/blob/master/README.md) and watch the video.

#### If you prefer pastebin to github you can read the same information here: https://pastebin.com/whBty9rQ

Now then, let's go through some common errors and how to fix them.
***
>#### 1. "I tried using the colab but it gives a fatal error saying model_v5 is missing!" This is a bug for Thadunge's version, cloveranon uses a completely different model now but I'll get to that later.
> 
> Alright so open up your google drive. Now search model_v5 and see if anything comes up. Do you have model_v5? If you do, check the folder location by right clicking and select show folder location. It should be located in AI Dungeon>generator>gpt2>models Make absolute sure it's located in that folder. If it's not in the models folder, drag and drop it there one folder at a time until it's in the right spot.

***    
>#### 1b. "I don't have the model_v5 folder, do I have to upload it after torrenting it?" 
>    
> No, not at all. Getting the folder takes like 5 seconds. Go to this link: https://drive.google.com/drive/folders/1XiDD2BD8vLZaJxZpCrNYjscpvnD3EYrP
    Now right click where it says model_v5 up top and click on add to my drive. After you do that, just drag it into 
    AI Dungeon>generator>gpt2>models after you do that you should be golden.
***
>#### 2. "The colab is giving me an error that says model-550.data-00000-of-00001; No such file or directory!"
>    
> Okay I ran into this error myself like twice. This is really easy to fix. If you already have model_v5, go check the folder and see if it has the file model-550.data-00000-of-00001 if it doesn't have that file then you need to get that file. Go to https://drive.google.com/drive/folders/1XiDD2BD8vLZaJxZpCrNYjscpvnD3EYrP and right click on the file model-550.data-00000-of-00001 and add to my drive. After that drag that file into your model_v5 folder which again should be located in AI Dungeon>generator>gpt2>models after you put it in that folder it should run just fine.
***
>#### 3. "I want to run cloveranon's version but for some reason the model_v5 isn't working!"
>    
> Okay cloveranon's version uses a completely different model now, you need to get that model. Now normally you would need to torrent it and upload it to your google drive. That can take over an hour to do. Luckily I made an easy skip where you can just copy it to your drive. Go to https://drive.google.com/drive/folders/1yVKnbwiIp5I5xZw7sr_zlamgw14algYh and right click on pytorch-gpt2-xl-aid2-v5 and add to my drive. After you add it to your drive you need to put the model folder in My Drive/Clover-Edition/models This should make cloveranon's version run now.
***
#### 4. If you get this error:
    > Traceback (most recent call last):
    > File "play.py", line 43, in <module>
    > is_notebook = _is_notebook()
    > File "play.py", line 34, in _is_notebook
    > if 'IPKernelApp' not in get_ipython().config: # pragma: no cover
    > AttributeError: 'NoneType' object has no attribute 'config'
    Do this:
    > If you're on the Colab change [is_notebook = _is_notebook()] to [is_notebook = True]
    > If you're on Desktop change [is_notebook = _is_notebook()] to [is_notebook = False]
>
***
>#### 5. "The AI just keeps repeating itself over and over and it won't listen to anything I tell it to do anymore!" (This one is extremely common and isn't really an error)
>    
>    Okay so the AI keeps repeating words like it's super cursed or something. It's okay this is really easy to fix but doesn't always work. What you should do is /revert multiple times in a row I'd say about 3 or 4 times and then do something completely different. As an example if you were fighting a dragon and suddenly looping occured when you tried to kill it /revert a few times and then just type: You leave the dragon and head into the forest. To prevent this more in the first place don't ignore what the AI is telling you. If a character is telling you something and you don't care about what they said just start your prompt with: Ignore the person talking and do x. If you want more advice on how to stop the AI from doing stuff like this check out https://github.com/VBPXKSMI/Open-CYOAI-Project/wiki/How-to-save-your-AI-from-becoming-retarded it has plenty of advice on the matter.
***
#### 6. "I keep disconnecting every x minutes! The colab didn't do this before, how do I make it stop?"
    
 The absolute best thing you can do is fill out the form at the bottom of the pastebin and post it in the thread. While there is no known fix any and all information helps.
    
 There is no fix known currently for this bug. The devs believe it's on Google's side completely and there is nothing we can do about it. It shouldn't actually make a difference but 1.0 is stable for some people. If you have all the files already downloaded in your google drive you can just switch to the 1.0 branch by following these steps:
    
    1. Go to https://colab.research.google.com/github/VBPXKSMI/Open-CYOAI-Project/blob/master/Old_Open_CYOAI.ipynb
    2. Make a copy of the colab like you usually would.
    3. Run CELL 1 : Installing dependencies and mounting GDrive
    4. Run CELL 1 : Play
    
    After that it might run without disconnecting. Once again though it's all on Google so nothing we can do if it does.
>
#### 7. "The 1.0 colab is giving me strange errors and isn't working even though I have all the files I should need in my google drive already!" (This is purely connected to step *6 ignore this if you aren't using 1.0 of the colab) 
    
    NOTICE I can only give advice on fixing Thadunge version that I've been playing, I don't know how you would fix 
    cloveranon's version on 1.0 but maybe the steps are similar, nothing is confirmed though, delete files in your google 
    drive at your own risk!
    
    Okay I ran into this error a lot myself. 
    The fastest way to fix this that is unconfirmed but worked for me personally is to follow these steps:
    
    1. Delete your AI Dungeon folder in your google drive.
    2. Delete your copy of the 1.0 colab inside of your Colab Notebooks folder. 
    (I'm not sure if this step is necessary but I do it every time I change versions.)
    3. Go to the 1.22 colab version and follow the steps you normally would when using it for the first time. 
    As in try to run it like normal.
    4. After it starts running Thadunge's version properly(just test if it starts a story without breaking) 
    you can stop the cell and close out of the copy after that.
    5. Check your google drive to see if AI Dungeon folder is there again. 
    If it is, delete your copy of the colab in Colab Notebooks.
    6. Go back to step *6 where I detail how to run the 1.0 version. 
    With the new AI Dungeon folder you have it SHOULD run properly now without breaking.
    
    If this doesn't work say so in the thread so I can confirm it only worked on my end and take this part out of the page.
***
>#### Some general tips:
>
> Make sure you do exactly as the instructions say on the collab. If it says to save a copy to your drive and run that, then do it.
>   
> If you run into any errors that aren't shown here or just don't line up with anything in this page try ctrl+f and copy paste the error and search to see if anyone else mentioned it. 
They may already have a reply with the fix you need. If that fails, then go ahead and post a screenshot of your error in the thread for help.
>    
>    Always be specific with what your error is and try to provide a screenshot in the thread when you want help. 
    If you just show up and say "The collab is broken it won't run I got an error and it disconnected!" no one can do anything to help you because we don't know what went wrong or even have any idea if the error was on your end or something else entirely. Context is always helpful.
>
***
#### Do you want to help test the newest version of the colab and help errors get fixed sooner rather than later? Please fill out this form whenever you run the newest colab version and post it in the thread after you use it:

    Open CYOAI v1.21(the number here will change depending on the version, check the top of the page for what version you have)
    Had random disconnect: Yes / No
    Managed to play for: "X" minutes
    Had good internet connection while playing (the entire time): Yes / No
    Switched from the Colab tab (frequently or not): Yes / No
    Left the Colab tab iddle without disconnecting for: "X" minutes
    Played with: “X” browser
    Noticed a difference in response time: Yes / No
    Average time per response was: "X" seconds
    Played with code: 8 / 16 / 32 / 64 / print("Program Completed!")

#### If you want me to specifically add an error and solution to this page please submit an issue and I'll try to add it in as soon as possible.