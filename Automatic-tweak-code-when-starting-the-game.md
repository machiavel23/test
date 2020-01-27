# ORIGINAL CODE

    def play_aidungeon_2():
    
        console_print("AI Dungeon 2 will save and use your actions and game to continually improve AI Dungeon."
                      + " If you would like to disable this enter 'nosaving' for any action. This will also turn off the "
                      + "ability to save games.")
    
        upload_story = True
    
        print("\nInitializing AI Dungeon! (This might take a few minutes)\n")
        generator = GPT2Generator()

# NEW CODE

    def play_aidungeon_2():
    
        console_print(
            "\nAI Dungeon 2 will save and use your actions and game to continually improve AI Dungeon."
            + " If you would like to disable this enter 'nosaving' for any action. This will also turn off the "
            + "ability to save games.\n"
        )
    
        upload_story = True
    
        # "temperature" dictates randomness. A low temperature means that the AI is
        #  more likely to go with the word that best fits the context, a high
        #  temperature makes the AI more random and it may chose surprising less fitting words
        # original 0.4
        temp = 0.2
    
        # lower top_k is a hard limit of "how many fitting words should I consider",
        #  i.e. lowering this value also limits the AI in creativity
        # original 40
        top_k = 20
    
        console_print("\nBefore we start, would you like to change the default temperature (" + str(temp) + ") and top_k (" + str(top_k) + ") value?\n")
        choice = input("1) Aeeyup!\n-) Press enter to skip\n>")
    
        if choice == "1":
            temp = float(input("New temperature: "))
            top_k = int(input("New top_k: "))
    
        print("\nInitializing AI Dungeon! (This might take a few minutes)\n")
        generator = GPT2Generator(60, temp, top_k, 0.9)