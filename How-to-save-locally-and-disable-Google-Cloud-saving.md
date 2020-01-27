This will fix the local saving and loading, based off the torrent local version.
 
Create a folder called "stories" in the AIDungeon root. (If you don't want to do this, remove stories\ from the path in the two functions below, but it clutters your root folder)
 
Go into story\story_manager.py and replace the following two functions with this code:
 
    def save_to_storage(self):
    self.uuid = str(uuid.uuid1())
     
     
    story_json = self.to_json()
    file_name = "stories\story" + str(self.uuid) + ".json"
    f = open(file_name, "w")
    f.write(story_json)
    f.close()
     
    return self.uuid
     
     
    def load_from_storage(self, story_id):
     
    file_name = "stories\story" + story_id + ".json"
    with open(file_name, 'r') as fp:
    game = json.load(fp)
    self.init_from_dict(game)
    return str(self)
     
That's it. Local saving and no upload to the Cloud bullshit.
For the visually retarded, your file should look [like this](https://i.ibb.co/C93pDJp/Should-look-like-this-save.png).