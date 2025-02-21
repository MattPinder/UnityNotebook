# Implementing data persistence between scenes and sessions
Note: the code block and details below are derived from Unity Learn's tutorial (see [here](https://learn.unity.com/tutorial/676202a9edbc2a019fcfe5bc?uv=6&pathwayId=5f7e17e1edbc2a5ec21a20af&missionId=5f751af7edbc2a0022cdbbb6) and two subsequent pathway steps), but organised here to aid my own memory in future

**Transferring data between scenes** requires the use of an object and script that aren't destroyed when the new scene is loaded, using `DontDestroyOnLoad`.

**Transferring data between sessions** requires saving/loading data to/from a JSON file, using `JsonUtility`.

## Example script
**Context**: a menu screen where the user selects a colour which will be passed to another scene in the game, as well as be saved between sessions
* The script is attached to an empty MainManager object in the Menu scene
* Another script in the subsequent Game scene contains reference to `MainManager.Instance.TeamColor`, enabling it to use the `TeamColor` variable that has been passed from the Menu scene via MainManager

```
using UnityEngine;
using System.IO;

public class MainManager : MonoBehaviour
{
	// All values stored in the MainManager class will be shared across all instances of MainManager
	public static MainManager Instance;

	// This is a variable that we want to persist between scenes
	public Color TeamColor;

	// When the MainManager object is created...
	private void Awake()
	{
		// ... it is destroyed instantly if another already exists...
		if (Instance != null)
		{
			Destroy(gameObject);
			return;
		}

		// ... otherwise, it is put into the special 'DontDestroyOnLoad' scene...
		Instance = this;
		DontDestroyOnLoad(gameObject);

		// ... and does whatever it's intended to do (in this case, load a colour from file)
		LoadColor();
	}

	// Conversion to/from JSON can only be performed on 'serialisable' data types,
	// and must be tagged with the [System.Serializable] attribute
	[System.Serializable]
	class SaveData
	{
		public Color TeamColor;
	}

	// Save the selected colour to file for next session
	public void SaveColor()
	{
		// A new SaveData instance is created, and its TeamColor class member is set
		SaveData data = new SaveData();
		data.TeamColor = TeamColor;

		// The new SaveData instance is converted to JSON format, and written to file
		string json = JsonUtility.ToJson(data);
		File.WriteAllText(Application.persistentDataPath + "/savefile.json", json);
	}

	// Load the selected colour from the previous session from a file
	public void LoadColor()
	{
		string path = Application.persistentDataPath + "/savefile.json";	// Define the filepath
		if (File.Exists(path))	// If the file exists...
		{
			// ... read its contents, and convert from JSON into a SaveData instance
			string json = File.ReadAllText(path);
			SaveData data = JsonUtility.FromJson<SaveData>(json);

			// Set the TeamColor variable of MainManager to the TeamColor class member of the new SaveData instance
			TeamColor = data.TeamColor;
		}
	}
}

```