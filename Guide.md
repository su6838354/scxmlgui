## Terminology ##
  * State/node are used interchangeably to indicate SCXML states (parallel or not, cluster or not)
  * Edge/transition are used interchangeably to indicate SCXML transitions.

## Display Legend ##
  * Nodes are filled rectangles with smoothed corners.
  * Cluster and parallel nodes are rectangles with sharp corners and empty body.
  * Transitions without targets (event handlers) are dotted.
  * Final states have a red border.
  * Initial states have a green fill.
  * Restricted states have a thicker border with color defined in the restrictedStates.xml restriction configuration file.

![http://scxmlgui.googlecode.com/svn/trunk/extra/legend.png](http://scxmlgui.googlecode.com/svn/trunk/extra/legend.png)

## Opening a file ##

If you plan to open an already existing file, first select whether you want to use the layout information possibly contained in the scxml file (e.g. in case this file was saved by this editor, and would like to maintain the saved layout) or if you want the graph layout to be automatically done (e.g. in case the file was not saved by this editor, and therefore does not contain layout information). This selection is done with the voice **"Ignore stored layout"** in the **File** menu.

A **backup** functionality is available by starting the editor with the **"-b"** option. This function saves each opened file with a time-stamp in its file name.

to initially open a specific file you can use the -i option. For example, "java -jar fsm-editor.jar -i test.scxml" will start the editor and open the file "test.scxml".

## Creating a new file ##

Click on the graph area (the largest portion of the interface) and press **Control-N** or click on **File**->**New**

## Adding a Node ##

A node (i.e. a SCXML state) can be added only as child (i.e. contained) in a cluster node. Every file has a default cluster node that contains the entire graph and that is called SCXML. To add a node, right click on the location in which you want to add the node and select **"Add node"** from the context menu. You can also add a restricted node by selecting the **"Add restricted node"** option and a restriction type from the context menu. When the cursor is over the restriction type, its documentation will appear in a tooltip field.

## Adding an Edge ##

The filled part of each node is divided into two regions:
  * **edge region**: the central region, in which the mouse cursor becomes a hand is used to create edges.
  * **move region**: the surrounding region, in which the cursor becomes the standard move "four arrows" is used to move nodes.

To connect two nodes, move the mouse in the edge region of the starting node; when the cursor becomes a hand, start the drag gesture (left-click and hold) and finish it in the edge region of the destination node (the destination node will become highlighted in green if the edge is possible).

If you want to add a target to an existing edge (i.e. create a multi-target edge): create an edge as described above. Then start a drag gesture on the terminal node of the edge while pressing **Control**, terminate the drag gesture on the edge region of the node you want to add as additional target for that edge. A dialog will open asking whether you want to create a separate edge or add a target to that edge.

If you want to make a cycle (source and destination are the same): just terminate the drag gesture in the same node it was started.

You can also add corners to existing edges by right clicking on the point along an edge in which you want to add the corner and select the appropriate voice in the context menu. To remove a corner from an edge, just repeat the same procedure (this time the context menu will show a remove corner voice instead of an add corner voice).

It's essential to add an event to an edge. You can do this in the edge editor. If the source node is restricted you can select a possible event from a list which is defined in the restriction configuration file, otherwise you can give an arbitrary event name you want. When an edge's event value is empty a warning will be displayed in the **"Validation errors"** section.

## Deleting Nodes and Edges ##

Select them with the mouse (either by selecting a region or clicking on each element you want to delete (pressing Control if you plan to click on more than one element)) and use the Delete key to remove them.

## Editing the properties of a Node/Edge ##

Right click on the element you want to edit and select **"Edit ..."** from the context menu.
Comments should be preserved. If not, please submit a bug report. Anther way to open the editor window is by selecting the element and pressing F2.

All editing functions are available through the context menu. Either directly as voices of the menu or in the editor that appears when selecting the **"Edit ..."** voice.

## Undo/Redo ##

**Control-Z**/**Control-Y**. There are multiple undo managers. One is a global manager that keeps track of changes to the entire graph. Then there are individual undo managers in each panel of each editing window associated to the states/edges that have been edited. In those panels you can undo/redo small changes to selected properties. (just practice by editing the ID of a node, if you undo when the focus is on the graph, you will undo the complete change, while if you undo when the focus is on the ID editing pane, you will undo one character at a time).

## Save ##

To save in the same file just use **Control-S**. to save in a different file use **Control-Shift-S**. Exporting in different formats is available in the **"Save as"** dialog.
When saving a file, the layout is also saved using comments and can be retrieved next time you open the file by unselecting the **"Ignore stored layout"** option in the **File** menu. If there are restricted nodes, the restrictions are also saved using comments and can be retrieved next time.

## Search ##

Press **Control-F** to open the search dialog box. Click on the help button of the search dialog to get further help on how to use that tool.

## No GUI processing ##

The software can be used to batch auto-layout and/or convert to image formats (or dot format) scxml files. To do so you must include in the command line at least the options **"-i"** and **"-o"**.
For example, the command "java -jar fsm-editor.jar -i test.scxml -o test.png -l" will open test.scxml, apply autolayout and save the result in test.png. If **"-l"** is omitted, auto-layout will not be called and the saved layout will be used. If the output file must not have an extension then use the option **"-t"** to specify the format of the output (e.g. use "-t png" to force the output to be in the png format).

## Restriction handling ##

The software can handle restrictions on states. In this case restriction means that only defined events can trigger state change from a restricted source state. In SCXML editor this means that in edge editor the user can select an event from a group of possible events if the edge’s source node is restricted. It is possible to place more than one restriction on a state with the “Toggle restricted” function. If you drag the mouse over a node, a tooltip field will be appear, which contains the list of restrictions on the state. When a state has more restrictions, its possible event list is the union of the restricted state’s possible event lists.
The restrictions and the possible events are stored in a configuration xml file (named restrictedStates.xml), which is placed next to the fsm-editor.jar. If the user doesn’t define a restriction configuration, the editor will start in normal mode, without using restrictions on nodes. The restriction configuration xml file looks like the following:

![http://scxmlgui.googlecode.com/svn/trunk/extra/sample-restriction-config.png](http://scxmlgui.googlecode.com/svn/trunk/extra/sample-restriction-config.png)

There are restrictedState tags with name, color (restricted state’s border color), and documentation (it describes the restriction) attributes, and a list of possible events. An event has got a name and documentation attributes.
You can download a sample restriction configuration file from here: http://scxmlgui.googlecode.com/svn/trunk/extra/restrictedStates.xml
If you put this file next to fsm-editor.jar, and start the application, it will handle restrictions.