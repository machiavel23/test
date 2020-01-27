    import os
    import sys
    import time
    import ctypes
    import logging
    logging.getLogger('tensorflow').disabled = True
    logging.getLogger('numpy').disabled = True
    os.environ["CUDA_VISIBLE_DEVICES"]=""
    os.environ["TF_CPP_MIN_LOG_LEVEL"] = "3"
    from generator.gpt2.gpt2_generator import *
    from story.story_manager import *
    from story.utils import *
    from func_timeout import func_timeout, FunctionTimedOut
    
    
    
    def splash():
        print("0) New Game\n1) Load Game\n")
        choice = get_num_options(2)
    
        if choice == 1:
            return "load"
        else:
            return "new"
    
    
    def select_game():
        with open(YAML_FILE, "r") as stream:
            data = yaml.safe_load(stream)
    
        print("Pick a setting.")
        settings = data["settings"].keys()
        for i, setting in enumerate(settings):
            print_str = str(i) + ") " + setting
            if setting == "fantasy":
                print_str += " (recommended)"
    
            console_print(print_str)
        console_print(str(len(settings)) + ") custom")
        choice = get_num_options(len(settings) + 1)

        if choice == len(settings):
    
            console_print(
                "\nEnter a prompt that describes who you are and what are your goals. The AI will always remember this prompt and "
                "will use it for context, ex:\n 'Your name is John Doe. You are a knight in the kingdom of Larion. You "
                "were sent by the king to track down and slay an evil dragon.'\n"
            )
            context = input("Story Context: ") + " "
            console_print(
                "\nNow enter a prompt that describes the start of your story. This comes after the Story Context and will give the AI "
                "a starting point for the story. Unlike the context, the AI will eventually forget this prompt, ex:\n 'After arriving "
                "at the forest, it turns out the evil dragon is actually a pretty cute monster girl. You decide you're going to lay "
                "this dragon instead.'"
            )
            prompt = input("Starting Prompt: ")
            return context, prompt
    
        setting_key = list(settings)[choice]
    
        print("\nPick a character")
        characters = data["settings"][setting_key]["characters"]
        for i, character in enumerate(characters):
            console_print(str(i) + ") " + character)
        character_key = list(characters)[get_num_options(len(characters))]
    
        name = input("\nWhat is your name? ")
        setting_description = data["settings"][setting_key]["description"]
        character = data["settings"][setting_key]["characters"][character_key]
    
        context = (
            "You are "
            + name
            + ", a "
            + character_key
            + " "
            + setting_description
            + "You have a "
            + character["item1"]
            + " and a "
            + character["item2"]
            + ". "
        )
        prompt_num = np.random.randint(0, len(character["prompts"]))
        prompt = character["prompts"][prompt_num]
    
        return context, prompt
    
    
    def instructions():
        text = "\nAI Dungeon 2 Instructions:"
        text += '\n Enter actions starting with a verb ex. "go to the tavern" or "attack the orc."'
        text += '\n To speak enter \'say "(thing you want to say)"\' or just "(thing you want to say)" '
        text += "\n\nThe following commands can be entered for any action: "
        text += '\n  "revert"   Reverts the last action allowing you to pick a different action.'
        text += '\n  "quit"     Quits the game and saves'
        text += '\n  "restart"  Starts a new game and saves your current one'
        text += '\n  "save"     Makes a new save of your game and gives you the save ID'
        text += '\n  "load"     Asks for a save ID and loads the game if the ID is valid'
        text += '\n  "print"    Prints a transcript of your adventure (without extra newline formatting)'
        text += '\n  "help"     Prints these instructions again'
        text += '\n  "infto"    Change the default timeout.'
        text += '\n  "retry"    Get another result from the same input.'
        text += '\n  "context"  Update the story\'s context (helps AI keep track of things in longer stories).'
        text += '\n  "censor off/on" to turn censoring off or on.'
        text += '\n  Use ! at the beginning of a sentence to process it literally.'
        return text
    
    
    def play_aidungeon_2():
    
        console_print(
            "AI Dungeon 2 will save and use your actions and game to continually improve AI Dungeon."
            + " If you would like to disable this enter 'nosaving' for any action. This will also turn off the "
            + "ability to save games."
        )
    
        upload_story = True
    
        print("\nInitializing AI Dungeon! (This might take a few minutes)\n")
        generator = GPT2Generator()
        story_manager = UnconstrainedStoryManager(generator)
        inference_timeout = 180
        def act(action):
            return func_timeout(inference_timeout, story_manager.act, (action,))
        def notify_hanged():
            console_print("That input caused the model to hang (timeout is {inference_timeout}, use infto ## command to change)")
            ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
        print("\n")
    
        with open("opening.txt", "r", encoding="utf-8") as file:
            starter = file.read()
        print(starter)
        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
    
        while True:
            if story_manager.story != None:
                del story_manager.story
    
            generated = False
            while not generated:
                print("\n\n")
                splash_choice = splash()
    
                if splash_choice == "new":
                    print("\n\n")
                    context, prompt = select_game()
                    console_print(instructions())
                    print("\nGenerating story...\n")
                    generated = story_manager.start_new_story(
                        prompt, context=context, upload_story=upload_story
                    )
                    if generated:
                        console_print(str(story_manager.story))
                        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                else:
                    load_ID = input("What is the ID of the saved game? ")
                    result = story_manager.load_new_story(load_ID)
                    print("\nLoading Game...\n")
                    print(result)
                    generated = True
    
            while True:
                sys.stdin.flush()
                action = input("> ")
                if action == "restart":
                    rating = input("Please rate the story quality from 1-10: ")
                    rating_float = float(rating)
                    story_manager.story.rating = rating_float
                    break
    
                elif action == "quit":
                    rating = input("Please rate the story quality from 1-10: ")
                    rating_float = float(rating)
                    story_manager.story.rating = rating_float
                    exit()
    
                elif action == "nosaving":
                    upload_story = False
                    story_manager.story.upload_story = False
                    console_print("Saving turned off.")
    
                elif action == "help":
                    console_print(instructions())
    
                elif action == "censor off":
                    generator.censor = False
    
                elif action == "censor on":
                    generator.censor = True
    
                elif action == "save":
                    if upload_story:
                        save_ID = input("Choose a name (ID) for the saved game:")
                        id = story_manager.story.save_to_local(save_ID)
                        console_print("Game saved.")
                        console_print(
                            "To load the game, type 'load' and enter the following ID: "
                            + save_ID
                        )
                    else:
                        console_print("Saving has been turned off. Cannot save.")
    
                elif action == "load":
                    load_ID = input("What is the ID of the saved game?")
                    result = story_manager.story.load_from_local(load_ID)
                    console_print("\nLoading Game...\n")
                    console_print(result)
    
                elif len(action.split(" ")) == 2 and action.split(" ")[0] == "load":
                    load_ID = action.split(" ")[1]
                    result = story_manager.story.load_from_local(load_ID)
                    console_print("\nLoading Game...\n")
                    console_print(result)
    
                elif action == "print":
                    print("\nPRINTING\n")
                    print(str(story_manager.story))
    
                elif action == "revert":
    
                    if len(story_manager.story.actions) is 0:
                        console_print("You can't go back any farther. ")
                        continue
    
                    story_manager.story.actions = story_manager.story.actions[:-1]
                    story_manager.story.results = story_manager.story.results[:-1]
                    console_print("Last action reverted. ")
                    if len(story_manager.story.results) > 0:
                        console_print(story_manager.story.results[-1])
                    else:
                        console_print(story_manager.story.story_start)
                    continue
                    
                elif action == "retry":
                    if len(story_manager.story.actions) is 0:
                        console_print("There is nothing to retry.")
                        continue
                    last_action = story_manager.story.actions.pop()
                    last_result = story_manager.story.results.pop()
                    try:
                        act
                    except NameError:
                        act = story_manager.act
                    try:
                        try:
                            result = act(last_action)
                            if result == "":
                                console_print("Error: The story is too long to be processed, try using a shorter input or reverting some actions.")
                                ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                            else:
                                console_print(last_action)
                                console_print(story_manager.story.results[-1])
                                ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                        except FunctionTimeOut:
                            story_manager.story.actions.append(last_action)
                            story_manager.story.results.append(last_result)
                            notify_hanged()
                            console_print("Your story progress has not been altered.")
                    except NameError:
                        pass
                    continue
    
                elif action == "context":
                    console_print("Current story context: \n" + story_manager.get_context() + "\n")
                    new_context = input("Enter a new context describing the general status of your character and story: ")
                    story_manager.set_context(new_context)
                    console_print("Story context updated.\n")
                #Fuck reddit
                elif len(action.split(" ")) == 2 and action.split(" ")[0] == 'infto':
                    try:
                        inference_timeout = int(action.split(" ")[1])
                        console_print("Set timeout to {inference_timeout}")
                    except:
                        console_print("Failed to set timeout. Example usage: infto 30")
                else:
                    if action == "":
                        action = ""
                        try:
                            result = act(action)
                        except FunctionTimedOut:
                            notify_hanged()
                            continue
                        console_print(result)
                        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
    
                    elif action[0] == '"':
                        action = "You say " + action
    
                    elif action[0] == '!':
                        action = "\n" + action[1:].replace("\\n", "\n") + "\n"
    
                    else:
                        action = action.strip()
                        action = action[0].lower() + action[1:]
                        if "You" not in action[:6] and "I" not in action[:6]:
                            action = "You " + action
                        if action[-1] not in [".", "?", "!"]:
                            action = action + "."
                        action = first_to_second_person(action)
                        action = "\n> " + action + "\n"
                    try:
                        result = "\n" + act(action)
                    except FunctionTimedOut:
                        notify_hanged()
                        continue
                    if len(story_manager.story.results) >= 2:
                        similarity = get_similarity(
                            story_manager.story.results[-1], story_manager.story.results[-2]
                        )
                        if similarity > 0.9:
                            story_manager.story.actions = story_manager.story.actions[:-1]
                            story_manager.story.results = story_manager.story.results[:-1]
                            console_print(
                                "Woops that action caused the model to start looping. Try a different action to prevent that."
                            )
                            ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                            continue
    
                    if player_won(result):
                        console_print(result + "\n CONGRATS YOU WIN")
                        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                        break
                    elif player_died(result):
                        console_print(result)
                        console_print("YOU DIED. GAME OVER")
                        console_print("\nOptions:")
                        console_print("0) Start a new game")
                        console_print(
                            "1) \"I'm not dead yet!\" (If you didn't actually die) "
                        )
                        console_print("Which do you choose? ")
                        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
                        choice = get_num_options(2)
                        if choice == 0:
                            break
                        else:
                            console_print("Sorry about that...where were we?")
                            console_print(result)
    
                    else:
                        console_print(result)
                        ctypes.windll.user32.FlashWindow(ctypes.windll.kernel32.GetConsoleWindow(), True)
    
    
    if __name__ == "__main__":
        play_aidungeon_2()