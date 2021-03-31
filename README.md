In UI/ActionRemapButton.gd, insert the following at line 32 (replacing the # Input remapping goes here):
```
	InputMap.action_erase_events(action)
	InputMap.action_add_event(action, event)
```

As always, ensure you are indenting with tabs instead of spaces.

In Global.gd, replace the load_input() and save_input() methods (starting on line 24) with the following:
```
func load_input():
	var error = save_file.load(SAVE_PATH)
	if error != OK:
		print("Failed loading file")
		return
	
	for i in inputs:
		var key = save_file.get_value("Inputs", i, null)
		InputMap.action_erase_events(i)
		InputMap.action_add_event(i, key)

func save_input():
	for i in inputs:
		var actions = InputMap.get_action_list(i)
		for a in actions:
			save_file.set_value("Inputs", i, a)
	save_file.save(SAVE_PATH)
```

Play the "game" and press Escape to bring up the menu. Change the controls to the arrow keys and close the menu (by pressing escape). See that the changes have been reflected. Then quit and reload the game; the controls should have persisted into the new game.

Quit Godot. In GitHub desktop, add a summary message, commit your changes and push them back to GitHub. If you return to and refresh your GitHub repository page, you should now see your updated files with the time when they were changed.

Now edit the README.md file. When you have finished editing, commit your changes, and then turn in the URL of the main repository page (https://github.com/[username]/Exercise-05b-Input-Remap) on Canvas.

The final state of the file should be as follows (replacing the "Created by" information with your name):
```
# Exercise-05b-Input-Remap
Exercise for MSCH-C220, 29 March 2021

An example of input remapping, saved to a config file, in Godot

## Implementation
Built using Godot 3.2.3

## References
This project borrows heavily from the [input_mapping Godot Demo Project](https://github.com/godotengine/godot-demo-projects/tree/master/gui/input_mapping)

## Future Development
None

## Created by 
Jason Francis
```
