https://docs.godotengine.org/en/stable/index.html

*Goal*: complete all tutorials on godot docs relevant to my project.

### **9/20/2020:** Setting Up

https://docs.godotengine.org/en/stable/getting_started/step_by_step/index.html
 
- Got my setup ready for research, but it's late now.  Will dive in tomorrow.

### **9/28/2020:** Starting

- **Nodes**
  - **Properties** Can be edited in the inspector on the right (default)
  - Emit **Signals** that can be received by other nodes via scripting
  - Can be put into **Groups** to organize
  - Can receive a callback per frame
  - Can have parents and children in a tree
  - **Node types** (as I walk through tutorial)
    - `Node2D:` Superclass for 2D objects
        - Has position, rotation, scale, and Z index
        - `RigidBody2D` for mobile, physics objects and `StaticBody2D` for immobile objects.
    - `Control:` Superclass for UI
        - Has anchors and margins adapt position relative to parent
        - `Label` Displays plain text.

- **Scenes**
  - Tree of nodes
  - Always has 1 root
  - Can be saved to disk (`.tscn`), called **"packed scenes"**
  - The runnable portions of a game
  - Can set main scene in **Project Settings**
  - You can **instance** a scene as if it were a node (drop its root node and tree into another scene)
    - Link-shaped button at top of scene editor

- **Scripts**
  - Can be attached to nodes
  - Can be registered into classes via `class_name` keyword:
  ```
  class_name ScriptName, "res://path/to/optional/icon.svg"
  ```
  - The scroll icon next to a node represents the script
  - Signals are received via functions e.g. `func _on_[node name]_[signal name]`
    - can be connected via `get_node("[receiving node]").connect("[signal name]", self, "[function]")`
  - `get_node()` searches immediate children; you must have full path, delimited by slashes.  e.g. `get_node("Panel/Options/Button")` or something.
  - **Processing**
    - `_process(delta)` (idle processing) is called every frame (which can vary by device).  Happens AFTER physics step.
      - `delta` is a `float`: time elapsed since last call to `_process`
    - `_physics_process()` (physics processing) is called with regularity (usually 60hz)
    - `set_process(bool)` can turn `_process()` on and off for the node
  - `SceneTree` is a class that contains functions that can interact with the entire tree.  Get the current scene tree using `get_tree()`
  - **Groups**
    - `add_to_group("[group name]")` adds to a group
    - `get_tree().call_group("[group name]", "[function]")` calls a function on all members of the group
    - `get_tree().get_nodes_in_group`
  -  There is a low-level system of `notifications` that can be sent between Classes.  Shouldn't need to use them
  - **Lifecycle** Instead of using notifications, override lifecycle functions
    - `_enter_tree()` Called when entering tree
    - `_ready()` Called after children have entered tree
    - `_exit_tree` Called after exiting tree
    - `_process(delta)` Called every frame
    - `_physics_process(delta)` Called every physics frame
  - **Creating/Deleting Nodes**
    - `add_child([Node Class].new())`
    - `node.free()` where `node` is a node object.  Deletes all subnodes too.  CAN CRASH GAME THOUGH!
    - `node.queue_free()` waits for processing to finish THEN deletes node.
  - **Instancing Scenes** 
    - `load("res://path/to/scene.tscn")`
    - `preload("res://path/to/scene.tscn")` these create a PackedScene object.
    - `scene.instance()` turns a PackedScene object into a Node object.
- **Project**
  - Project settings are saved in `project.godot` 
  - *"The project root is res:// which means "resource path". This means that files can only be saved inside the project. For the future, when doing file operations in Godot, remember that res:// is the resource path, and no matter the platform or install location, it is the way to locate where resource files are from inside the game."* 


  **FOR NEXT TIME:** https://docs.godotengine.org/en/stable/getting_started/step_by_step/signals.html

  ### **Next time:**
