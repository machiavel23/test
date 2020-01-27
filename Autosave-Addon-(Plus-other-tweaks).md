A guide on how to: Modify the game to write the save files to your computer and add an autosave feature (Plus other tweaks). [Offline users only]

Prerequisite: 

First, familiarize yourself with the following two sections of the code. I'll need to refer to them frequently

================================================================

>[help texts]

Begins with:

    def instructions():

This is what gets printed when you type 'help'. Not essential but probably still a good idea to modify.

================================================================

>[command block]

The section starting with

    if action == "restart":
        rating = input("Please rate the story quality from 1-10: ")
        rating_float = float(rating)
        story_manager.story.rating = rating_float
        break

this is the section that handles the actual input command logics.

================================================================

### To add autosaving to local directory:

1. In your AIDungeon directory, create a new directory named "saves"

2. Open "./story/story_manager.py" and add
    
    import copy

to the top of the file.

Then replace:

        def save_to_storage(self):
            self.uuid = str(uuid.uuid1())
    
    
            story_json = self.to_json()
            file_name = "story" + str(self.uuid) + ".json"
            f = open(file_name, "w")
            f.write(story_json)
            f.close()
    
            FNULL = open(os.devnull, 'w')
            p = Popen(['gsutil', 'cp', file_name, 'gs://aidungeonstories'], stdout=FNULL, stderr=subprocess.STDOUT)
            return self.uuid
    
        def load_from_storage(self, story_id):
    
            file_name = "story" + story_id + ".json"
            cmd = "gsutil cp gs://aidungeonstories/" + file_name + " ."
            os.system(cmd)
            exists = os.path.isfile(file_name)
    
            if exists:
                with open(file_name, 'r') as fp:
                    game = json.load(fp)
                self.init_from_dict(game)
                return str(self)
            else:
                return "Error save not found."
    
with

        def save_to_storage(self, overwrite=False):
            ref = self if overwrite else copy.copy(self)
    
            if overwrite == False:
                ref.uuid = str(uuid.uuid1())
    
            story_json = ref.to_json()
            file_name = "saves\\" + str(ref.uuid) + ".json"
            f = open(file_name, "w")
            f.write(story_json)
            f.close()
    
            return ref.uuid
    
        def load_from_storage(self, story_id):
    
            file_name = "saves\\" + story_id + ".json"
            with open(file_name, 'r') as fp:
                game = json.load(fp)
            self.init_from_dict(game)
            return str(self)
    
Then replace:

        def load_new_story(self, story_id):
            file_name = "story" + story_id + ".json"
            cmd = "gsutil cp gs://aidungeonstories/" + file_name + " ."
            os.system(cmd)
            exists = os.path.isfile(file_name)
    
            if exists:
                with open(file_name, 'r') as fp:
                    game = json.load(fp)
                self.story = Story("")
                self.story.init_from_dict(game)
                return str(self.story)
            else:
                return "Error: save not found."
    
with

        def load_new_story(self, story_id):
            file_name = "saves\\" + story_id + ".json"
            with open(file_name, 'r') as fp:
                game = json.load(fp)
            self.story = Story("")
            self.story.init_from_dict(game)
            return str(self.story)
    
3. In "./play.py", go to the [help texts] section and add

        text += '\n  "autosave"     Toggle autosave on and off. Default is off'

4. In [command block], replace the following:

                elif action == "save":
                    if upload_story:
                        id = story_manager.story.save_to_storage()
                        console_print("Game saved.")
                        console_print("To load the game, type 'load' and enter the following ID: " + id)
                    else:
                        console_print("Saving has been turned off. Cannot save.")

with

                elif action == "autosave":
                    autosave = not autosave
                    console_print("Autosaving is now turned " + ("on" if autosave else "off"))
    
                elif action == "save":
                    if upload_story:
                        print("Save to new file, or overwrite the current file?")
                        print("0) Save as new\n1) Save to current file\n")
                        choice = get_num_options(2)
                        id = story_manager.story.save_to_storage(overwrite=(choice == 1))
                        console_print("Game saved.")
                        console_print(
                            "To load the game, type 'load' and enter the following ID: "
                            + id
                        )
                    else:
                        console_print("Saving has been turned off. Cannot save.")
    
5. Below the line:

        upload_story = True

add

        autosave = False

6. Below

        while True:
            if story_manager.story != None:
                del story_manager.story

add in

            if autosave:
                story_manager.story.save_to_storage(overwrite=True)

================================================================

Change 'temperature' and 'top_k' while in progress
!! Warning: Requires a lot of RAM, make sure you have ~6GB of free memory !!

1. In [help texts], add

        text += '\n  "settemp"      Changes the generator temperature'
        text += '\n  "settopk"      Changes the generator top_k'

2. In [command block] add in
            
                elif action == "settemp":
                    temp = float(input("Set a new temperature\n> "))
                    story_manager.generator = GPT2Generator(temperature=temp, top_k=top_k)
    
                elif action == "settopk":
                    top_k = int(input("Set a new top_k\n>"))
                    story_manager.generator = GPT2Generator(temperature=temp, top_k=top_k)

================================================================

Change 'memory' while in progress, this is how much of the current story you want to feed to the generator

1. In [help texts], add

        text += '\n  "setmem"       

Changes the memory value. Default is 20, try lowering it if your game crashes after playing for a while'

2. In [command block] add

                elif action == "setmem":
                    new_mem = input("Enter a new memory value\n> ")
                    story_manager.story.memory = int(new_mem)
    
================================================================

Print out the current settings

1. In [help texts]

    text += '\n  "showsetting"  Display current settings and generator parameters'

2. In [command block]

                elif action == "showsetting":
                    text = "nosaving is set to:    " + str(not upload_story)
                    text += "\nautosave is set to:    " + str(autosave)
                    text += "\nmemory is set to:      " + str(story_manager.story.memory)
                    text += "\ntemperature is set to: " + str(temp)
                    text += "\ntop_k is set to:       " + str(top_k)
                    print(text)



(English is not my primary language and this is my first time writing a guide, so if you feel that any part of this document is confusing or poorly worded, feel free to rewrite it and redistribute your own version).