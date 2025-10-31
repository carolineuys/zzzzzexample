---
title: "Milling a PCB board"
date: 2025-10-30 08:30:00 -0400
categories: 
  - blog
  - in-class assignment
tags:
  - update
---

Setting up the toolpath:
Before milling, you must create a tool path for the PCB board in MakeraCam so that the CNC machine will know what path to take while milling. This process started with uploading the design into MakeraCam and selecting the area that would be used for a 2D pocket toolpath which is when the CNC machine only takes off a layer (in this case it was 0.05mm deep) of the copper rather than cutting all the way through. The purpose of the pocket is to ensure that there is only copper for current to flow through in the areas where the electronics will be soldered on. The 0.8mm corn and 0.2mm 30º engraving bits were used for the 2D pocket. Next, I selected all of the holes that would be for the 2D drilling toolpath which means the bit chosen (in this case it was the 0.8mm corn) will just drill a hole straight through the board (1.7mm deep). Lastly, I selected the outer edge of the design for the 2D contour cut which is a straight line cut all the way through the board (1.7mm deep). For this I also used to 0.8mm corn bit and I added tabs to the path so that the PCB board would not fall down after being cut all the way around. Something I had to keep in mind throughout this entire process was that there was a design flaw with the outer edge - there were two lines very close together that was tricky to see, so I always had to make sure I only had the inner edge selected. Any files that I used and created during this process can be found under the "PCB project files folder" linked here:

Workflow for preparing design:
1. Open new 3D project
2. Set material to PCB: Edit→Material→PCB
3. Set dimensions
    a. X = 127mm
    b. Y = 101mm
    c. Z = 1.7mm
4. Download files from Fab drive: (blue folder named Dubick)
    a. Resistance1-F_Cu.gbr
    b. Resistance1-PTH.drl
    c. Resistance1-Edge_Cuts.gbr
5. Import each of these files in MakeraCAM:
    a. File→Import PCB→Downloads→Resistance1-Edge_Cuts.gbr→Open
    b. File→Import PCB→Downloads→Resistance1-PTH.drl→Open
    c. File→Import PCB→Downloads→Resistance1-F_Cu.gbr→Open
6. Anchor lower left corner:
    a. Select whole design (highlight over everything)
    b. Click “m” key
    c. Select lower left corner in “Anchor” diagram at the top of new pop up (in top right corner of screen)
    d. Under “Location” in pop up, set X to 6 and Y to 6 (offsets design from very edge of material)
    e. Design should have moved to align with axes given
7. Path:
    a. Under “2D Layers” menu, hide (eye with red cross through):
        i. Resistance1-F_Cu.gbr_pad
        ii. Resistance1-PTH.drl_0.900 mm
        iii. Resistance1-PTH.drl_1.400 mm
    b. Select 2D Path (in tool bar)→2D Pocket
    c. Select whole (visible) design
    d. Set “End Depth” to .05mm
    e. Add tool x2
        i. 8mm Corn
        ii. 0.2mm*30Engraving(Metal)
    f. Calculate
8. Drilling holes:
    a. 2D Path→2D drilling
    b. Under “2D Layers” menu, hide (eye with red cross through) all but file with holes to drill (
    c. End Depth: 1.7mm
    d. Add tool: 8mm Corn
    e. Calculate
9. Outside cut:
    a. 2D Path→2D Contour
    b. Under “2D Layers” menu, hide (eye with red cross through) all but file with outside cut (Resistance1-Edge_Cuts.gbr)
    c. End Depth: 1.7mm
    d. Strategy: Outside
    e. Tabs: Custom
        i. Tab Shape: Triangle
        ii. Select “Add”
        iii. Click 3 places on outer edge (spaced fairly evenly apart)
    f. Add tool: 8mm Corn
    g. Calculate
10. Path→Export→Export OR if you want to edit file on milling machine’s computer, File→Save As, save file in downloads with .mkc format (file-type)
11. Upload file to your folder in Fab google drive

Workflow for the CNC Machine:
  Setting up the PCB board:
1. Orient the PCB board so that its bottom left corner is pressed flush against the metal blocks
2. Then put the jigs over the edge of the PCB board so that the little ledge on the jig is pressing down on the PCB board when you tighten the screws
  Setting up Cavera Controller:
1. Check project file is .mkc in order to open in Makeracam
2. In order to open in Cavera Controller the file format must be gcode.nc format
3. Open gcode.nc file in Cavera Controller
    a. Make sure to press “Upload & Select”
4. Make sure the com port is connected 
5. Home the CNC drill so it knows where the PCB board is
    a. To do this, press the icon in the top right corner that are three lines stacked on top of each other
    b. Then press the icon with the four arrows in a cross shape labeled “Switch to display manual interface”
    c. Finally, press the icon labeled “Home” in the middle of the screen
6. Switch back to the preview interface which is also under the icon with the three lines
7. Click on the icon  in the bottom left corner that looks like a gear that is labeled “Start running gcode test”
8. Turn on the vacuum
9. Turn on auto leveling
    a. In the bottom left corner of the screen where it is showing the design, there should be 25 yellow dots showing where the CNC machine can adjust its software to discrepancies in the level of the board
10. Hit close
11. Home the CNC again
12. Check voltage under tool status (WP - voltage for wireless pro)
    a. Should be about 3.6V
13. Click the gear icon again
14. Press “on”
15. Then click origin 
16. Hit run

Setback today:
We were given the wrong dimensions when creating the original design, so we had to recalculate the gcode for the design before milling. To do this we opened the design in Makeracam and changed the dimensions there. The correct dimensions were supposed to be 127.0mm x 101.0mm x 1.7mm. After fixing the dimensions we just recalculated the gcode so that the toolpaths would direct the machine to mill in the correct places. Another setback we had was that the software was confused because there was a bit that it was not expecting to be there after restarting due to the dimensions being wrong so when we hit “run” an error message popped up that the machine was locked.

Image of milled PCB board:
<img width="3264" height="2448" alt="IMG_1292" src="https://github.com/user-attachments/assets/38b8cc5b-e343-49dd-9ac0-5f37e078fa8e" />
