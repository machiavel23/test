**READ THIS FIRST!**

This offline version contains only the original AI Dungeon 2 base game, with only being uncensored by default as an addon.

There are 2 ways of installing this (both using the same torrent), the first one bellow is simpler and comes with batch files that automates most things. The second one is the manual version where you will have to do everything yourself, it's at the end of the page. Both versions are the same, it just changes how you install them.

Bellow that, there is information on how to easily update the game with whatever GitHub fork you desire, beware that there is a modded version that requires extra steps to get it going so read the instructions for it BEFORE doing anything else if you intend on using it.

Also, near the end of the page there is a supposed fix that improves performance of the game, try it if you want but it is not necessary.

================================================================

**Requirements**: 64-bit Windows, either 16+ GB of RAM to run this on your CPU or have a CUDA enabled GPU with more than 12GB of VRAM (lower specs will run the game slower, you have been warned).

================================================================

<details>
<summary> Automatic install </summary>

#
1) If you have "Python" installed, **uninstall** it.

2) Download the Windows version of the game from this torrent (don't be a leecher and keep seeding): 

- magnet:?xt=urn:btih:dcff0d93ab2b1cad2823360e31d3668b93a81510&dn=AIDun2EASY.zip

  * This contains batch files and the correct Python installer included for dead-simple installing.

3) Just **FOLLOW** the instructions.

4) **CHECK** the box that say "Add Python 3.7 to PATH" in the Python installer.

5) **DON'T TOUCH** the pip installs until it says "Press any key to continue...".

6) "RunAIDungeon.bat", is like a shortcut to launch the game after it's installed.
</details>

***

<details>
<summary> Updating your local install to use a modded version </summary>

#
The are 2 GitHub forks (modded version) you can use: by [thadunge2](https://github.com/thadunge2/AIDungeon) and by [CloverAnon](https://github.com/cloveranon/Clover-Edition).

It is possible to use a modded version developed by Anons by simply downloading the ".zip" of whatever GitHub fork you wanted to use. Then, simply take those files and overwrite with them in the root folder of your local version (to revert to the base/original version, I advise to have a copy elsewhere of the base game that came with the torrent, then you would only need to delete the modded version folder and copy back the base game one to restore the base game).

Beware that it's very likely that, when you use a modded version, it will give you an error when trying to play. So you will have to edit the "AUTO INSTALL FOR BRAINDEAD COOMERS" batch so that it also installs whatever thing you are lacking, and then run it (if you installed manually, the process is similar, you just need to type the commands in "cmd").

Current fix:

    !pip install regex
    !pip install profanityfilter
    !pip install playsound
    !pip install func_timeout
    !pip install tracery
    !pip install pyjarowinkler
    !pip install transformers
    !pip install torch

**VERY IMPORTANT**

**About Clover Edition:**

**Requirements**: 64-bit Windows, either 8+ GB of RAM to run this on your CPU or have a CUDA enabled GPU with more than 6GB of VRAM (lower specs will run the game slower, you have been warned).

Clover Edition recently started to use PyTorch, that's the main reason why the game requirements are so much lower. The installation process is a bit more complicated than what was depicted above, but is still doable.

To see more info on how to do it, **click [here](https://github.com/cloveranon/Clover-Edition) and follow the instructions**.
</details>

***

<details>
<summary> Performance Fix </summary>

#
If your CPU was made in the last decade it probably supports AVX2. If you run tensorflow with AVX2 support, you will have potentially slightly faster calculations. This tensorflow build has those CPU optimizations, try it if you want but it is not necessary.

1) Download this guy's pre-compiled tensorflow: https://github.com/fo40225/tensorflow-windows-wheel/tree/master/1.14.0/py37/CPU/avx2

- (you just do pip install "name of the whl" from the folder where it's saved, don't fucking change the name or it will break) (or, go to the folder where you downloaded the file and type cmd in the path thingy).

Then:

2) Run the command "pip uninstall tensorflow"

3) Run the command "pip uninstall tensorboard"

4) Run the command "pip uninstall tensorflow_estimator"

5) Run the command "pip install tensorflow-1.14.0-cp37-cp37m-win_amd64.whl"
</details>

***

<details>
<summary> Quick troubleshooting </summary>

#
>#### pip not recognized
>Python wasn't added to PATH. Rerun the python installer, select modify, enable pip, hit next, enable "Add Python to environment variables," and hit install.

***

>#### ERROR: Could not find a version that satisfies the requirement tensorflow (from versions: none)
>You either have Python 32-bit or version v3.8. Uninstall and get the right download.

***

>#### If you have problems installing python on Windows 10:
>Windows 10 makes a stupid fucking alias to help you install python, but if you already installed it. It doesn't recognize it.
>
>Basically running python from command prompt will open windows store if you didn't install it from windows store. To solve it just go into "manage app execution aliases" and disable python in there, you may need to restart your computer.

***

>#### How fast does the Local offline version run on only the CPU?
>Local response time depends on number of CPU cores, amount of RAM, Bus size on CPUs, Mobo/Bus speeds, and Tensorflow's version. You can try to downgrade to Tensorflow 1.14 or 1.13 to speed up the AI.

***

>#### Help! I'm seeing censored words, what can I do to disable this function?
>Just replace "return pf.censor(text)" with "return text" in story/utils.py line 71.
>
>Or just use a modded version (like the one in the torrent or the other featured versions) that has it disabled by default.

***

>#### Is there a way to tell the AI Dungeon to use my CPU over GPU and vice versa?
>It will switch to CPU if it sees your GPU is up to no good (or at least if you miss some CUDA stuff). You can also install tensorflow 1.14, which is a CPU only version so it won't even try. Newer versions than 1.14 are for both CPU and GPU, it will probably try running it through GPU first but should switch to cpu after throwing some errors on startup.
>    
>Or you can try this in cmd: "pip uninstall tensorflow-gpu"

***

>#### How can I use a background image in cmd like I see people using?
>Windows and Linux shells lets you use background images for your terminal (only if using Powershell). End result should look [something like this](https://i.ibb.co/RD7ZShf/1576562191889.jpg).

***

>#### How do I stop AI Dungeon from allocating 125MB of VRAM on every GPU it finds? I don't want to make the other people using this server suspicious.
>This is a bug with Tensorflow 1. There's supposedly a "max_devices" GPU option you can set to make it only run on 1 GPU.
>
>Add these lines at the top of play.py (put this after "import os", obviously):

    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument('--gpus', nargs="+", default=["0"])
    args = parser.parse_args()
    visible_devices = ",".join(args.gpus)
    os.environ["CUDA_VISIBLE_DEVICES"] = visible_devices
    print("running on gpus", visible_devices)

>Then you can run play.py --gpus <gpu1> <gpu2>... to explicitly tell it which GPUs to run on. Or you can leave out the argument and it will just run on GPU 0.

***

>#### While I played the game I get an OOM (out of memory) error."
>You ran out of memory, probably because you played it in GPU mode. To force CPU mode, go to where your CUDA bin folder is and delete the "cudnn64_7.dll" file.

***

>#### Upon launching the game I get "encoder.json is missing".
>Your model files are missing, make sure they are located inside your AI Dungeon folder in "\generator\gpt2\models\model_v5".

***

>#### When I try to run AIDungeon, I get the error "ImportError: DLL load failed: A dynamic link library (DLL) initialization routine failed".
>Your CPU doesn't support the "Performance Fix" (AVX2). The only solution is to upgrade your CPU or run the command "pip uninstall tensorflow-1.14.0-cp37-cp37m-win_amd64.whl" and install the default version of tensorflow again.
</details>

***

<details>
<summary> Manual install </summary>

#
1) If you have "Python" installed, **uninstall** it. Then install Python 3.7.5, 64-bit. **Make sure** you enable adding Python to PATH when installing.

- If you plan to use the GPU, also install CUDA Toolkit (latest release should be fine, but it's recommended to use CUDA 10.0) and cuDNN (make sure this version matches your CUDA Toolkit version, it's v7.6.5 for CUDA 10.0).

2) Download the Windows version of the game from this torrent (in this instance, only download the "AIDungeon" folder, ignore the rest, although you can use the Python installer over there if you didn't install Python yet) (don't be a leecher and keep seeding):

- magnet:?xt=urn:btih:dcff0d93ab2b1cad2823360e31d3668b93a81510

3) Open a command prompt ("cmd") in whatever folder you extracted the game into (just type "cmd" into the folder's url and hit enter).

4) Run the command "pip install tensorflow" for the CPU version or "pip install tensorflow-gpu" for the GPU version.

- If you have tensorflow issues later on, try "pip install tensorflow==1.14".

5) Run the command "pip install pyyaml"

6) Run the command "pip install -r requirements.txt"

7) Run the command "python play.py" and it should start the game

#### To run the game easily after a manual install, do this:
>1) Make ".txt" file in the main folder.
>
>2) Type the command you use to run the game into the ".txt" file (python play.py) and save it.
>
>3) Rename the file from "whatever.txt" to "whatever.bat".
>
>The inside of ".bat" should look something like this:
>
    python play.py
    pause
>
>And done, you have a working program that will automatically open "cmd" and run that command for you, starting the game in one easy click.