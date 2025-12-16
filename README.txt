# TruckDetector

Disclaimer
This is personal, hobbyist software provided for free and with no guarantees. 
It may contain bugs, may break, and may not be suitable for any particular purpose.
You use this software entirely at your own risk. The author(s) are not responsible for any loss, damage, or issues that result from using, modifying, or distributing this software.
Automates finding trucks on the map, checking their inventory for a specific item, and pausing on the first truck that has **3+** of that item.

Expected files/folders:

TruckDetector/			   # main folder
  main.exe                 # main bot script
  calibrate.exe            # layout calibration tool
  layout_config.json       # auto-generated layout data (DO NOT EDIT by hand)
  refresh_button.png       # template image of the refresh button

  templates/               # truck templates (map view)
    truck_gold_1.png
    truck_gold_2.png
    truck_purple_1.png
    ...

  inventory_templates/     # ONE item template (inventory icon)
    item.png

  README.md
  
  Walkthrough:
  
1. Set up the game resolution and templates ---------------------------------------------------------------------------------------------------------
	1.1 Choose the game resolution

		Set the game to the window size you want

		Important:

		Templates and calibration are resolution/scale-specific.

		If you later change the game window size THE CURRENT CONFIGURATION WILL BREAK!!!
		
		If you do this: 

		Re-capture templates

		Re-run calibrate.py

		Keep the game running while you do the next steps.

	1.2 Capture the refresh button template

		With the game running at the chosen size:

		Take a screenshot (e.g. PrtScn, Windows+Shift+S, etc.) of ONLY the refresh button! Refer to the folder called "references" to see an example.

		Save the image as:

		refresh_button.png

		in the main folder (TruckDetector folder).

	1.3 Capture truck templates (templates/)

		The bot uses these to detect trucks on the map.

		Create (or clean) the folder:

		TruckDetector\templates\

		In-game, find each truck variant you care about:

		Gold truck

		Gold-on-fire

		Purple truck

		Purple-on-fire

		etc.

		For each variant:

		Take a screenshot with that truck visible on the map.

		Crop around the stable part of the truck:

		Include body/bed/cabin

		Avoid as much of the moving fire / extreme bobbing as possible

		Save each cropped truck as a .png into templates/.

		Examples (names can be anything, they’re just labels):

		templates/
		  gold_1.png
		  gold_2.png
		  purple_1.png
		  purple_fire_1.png

		You can add multiple frames/variants for the same truck type; the bot will treat each PNG as a template.

	1.4 Capture the item template (inventory_templates/)

		The bot checks if a truck has 3+ copies of a specific item in its inventory.

		Open a truck in-game that has the target item in its inventory.

		Take a screenshot with the inventory visible.

		Crop just the item icon as it appears in the inventory.

		Save as a .png inside:

		TruckDetector\inventory_templates\

		For example:

		inventory_templates\
		  item.png

		Currently the code just uses the first PNG in inventory_templates/, so only put the item you care about in this folder.

2. Calibrate the layout (calibrate.py) ---------------------------------------------------------------------------------------------------------

	Once templates are ready and the game is running at the final layout (resolution & scale), calibrate the positions.

	From the project folder in PowerShell run the command:

	Double click clibrate.exe

	You’ll see step-by-step prompts like:

	Hover over refresh button center, then press Enter in the PowerShell window.

	Hover over search region TOP-LEFT corner (where trucks appear).

	Hover over search region BOTTOM-RIGHT corner.

	Hover over inventory region TOP-LEFT corner (where inventory items show up for a selected truck).

	Hover over inventory region BOTTOM-RIGHT corner.

	For each prompt:

	Move mouse to the requested spot in the game

	Then focus back on PowerShell and press Enter

	When it finishes, it will create/update:

	layout_config.json

	This file stores all the calibrated coordinates and derived offsets used by main.py. You do not need to edit it manually.

	If you later change in-game resolution or UI scale:

	Re-capture templates (refresh / trucks / item)

	Run calibrate.exe again

3. Running the bot (main.py) ---------------------------------------------------------------------------------------------------------

	With:

	Templates in place

	layout_config.json created by calibrate.py

	You’re ready to run the bot.

	Double click main.exe

	Behavior:

	The bot starts PAUSED. The bot should ONLY be run on the truck screen!

	Press F5 to toggle:

	F5 → ENABLED (starts scanning trucks)

	F5 → PAUSED (stop all actions, but keep the script running)

	If a truck has 3+ items:

	Prints a message in the console.

	Leaves that truck selected.

	Automatically pauses the bot

	You can manually inspect the truck.

	Press F5 to resume scanning if you want to continue.

	If no trucks pass the inventory check:

	The bot clicks the refresh button

	Repeats the process.

	To stop the program completely, press:

	Ctrl + C in the the window
