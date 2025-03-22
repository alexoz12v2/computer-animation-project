# Snippets

- find all image textures path 
  ```python
  for img in bpy.data.images:
    print(img.name, ":", img.filepath)
  ```
- manipulate selected objects 
  ```python	
  for obj in bpy.context.selected_objects:
    obj.rotation_euler.x += 1.5708  # Rotate 90 degrees (π/2) on X-axis
  ```
  
# Shortcuts

## Selection & Navigation

- Ctrl + \`: Hide/Show gizmos
- Tab – Toggle between Object Mode and Edit Mode
- A – Select all
- Alt + A – Deselect all
- L – Select linked geometry (hover over a part and press L)
- Ctrl + L – Select all linked geometry (based on selection)
- B – Box select
- C – Circle select
- Shift + G – Select similar (choose criteria like area, shape, or material)
- Alt + RMB - loop select 
- Shift + RMB - ring select 

## Transformations

- G – Grab (move)
- R – Rotate
- S – Scale
- X / Y / Z – Constrain movement to an axis (e.g., G + X moves along the X-axis)
- Shift + X / Y / Z – Move along the other two axes (exclude one axis)
- Ctrl + A – Apply transformations (use in Object Mode)
- Vertex, Edge, and Face Editing
- Ctrl + Tab (or 1, 2, 3 in Blender 2.8+) – Switch between Vertex, Edge, and Face selection
- Ctrl + E – Edge menu (Bevel, Mark Seam, etc.)
- Ctrl + B – Bevel (works for edges and vertices)
- Shift + Ctrl + B – Vertex bevel
- F – Fill (creates a face between selected vertices/edges)
- Alt + Left Click – Select edge loop
- Shift + Alt + Left Click – Select multiple edge loops
- Loop Cuts & Subdivision
- Ctrl + R – Loop cut (scroll mouse wheel to increase cuts)
- K – Knife tool (click to cut, Enter to confirm)
- Shift + R – Repeat last action
- Ctrl + Shift + B – Chamfer/Bevel vertices

## Extrude, Inset & Merge

- E – Extrude
- I – Inset faces
- M – Merge vertices (choose options like "At Center" or "At Last")
- Alt + M – Older version of merge (pre-2.8)

## Proportional Editing & Smoothing

- O – Toggle Proportional Editing
- Shift + O – Change proportional falloff type
- Ctrl + Shift + B – Bevel vertices
- Shift + S – Snap menu (snap selection to grid, cursor, etc.)
- Ctrl + S – Save file (always a good habit 😆)
- UV & Shading
- U – Unwrap UV (when in UV Editing)
- Ctrl + T – Triangulate faces
- Alt + J – Convert tris to quads

## Miscellaneous

- H – Hide selection
- Alt + H – Unhide all
- Shift + H – Hide everything except selection
- P – Separate selection into a new object
- Ctrl + J – Join selected objects

# Pivot to Cursor 

Temp
Press Shift + Right Click to place the 3D Cursor manually.
Or use Shift + S → "Cursor to Selected" to place it at the selection.

Change the Pivot Point to Cursor:

In Object Mode, go to the top-center of the viewport (next to the selection mode dropdown) where the pivot point options are.
Click on the Pivot Point dropdown (it’s an icon that usually shows a circle with a dot in the center).
Select 3D Cursor from the list of pivot options.
Alternatively, you can use the shortcut:

Period key (.) to open the pivot point menu and choose 3D Cursor.
Perm 
Object ‣ Set Origin

## Edit mode UV tools 

- press U

## Edge slide tool 

in edit mode, with a vertex selected, press Grab (G) twice

## Triplanap projection 

- https://www.youtube.com/watch?v=KV_hgeQdCXk

## Baking

- https://www.youtube.com/watch?v=sOvRr_D8ZpU

# Animations: Docs Summary

These notes about animations in blender are made by summarizing The [Blender 4.3 Docs](https://docs.blender.org/manual/en/4.3/animation/introduction.html)

## Introduction 

Animation = Transforming an object or changing its shape over time. More generally, any property about a blender object can be animated.
Animation is typically achieved by employing *Keyframes* (more on that later)

Any property in the _Properties Editor_ has a *State Color* 

<img src="Y:\blender_docs_images\animation_introduction_state-colors.png" alt="State Colors" width="500"/>

|       |                                                  |
|:--------|:--------------------------------------------------------|
| **Gray**   | Not animated                                          |
| **Yellow** | Changed from the current frame                        |
| **Green**  | Keyframed on a different frame                        |
| **Orange** | Changed from the keyframed value (before it was Yellow/Green) |
| **Purple** | Controlled by a *Driver* (more on that later)         |

### Rigging

Rigging = adding controls handles to animate an object. Blender offers the following feature to rig a model

|                    |             |
|--------------------|-------------|
| **Armatures**      | A Hierarchy of Joints associated with a mesh. Each joint has a *weight* [0.0, 1.0] for each vertex of the aforementioned mesh (can be painted). Transforming a joint will influence all vertices whose weight for that particular joint is greater than 0. This technique is called *Skeletal Animation* (more later). |
| **Constraints**    | Control the kind of motion the rig is allowed to perform. They are found under _Properties Editor_, tab "Constraints" (more later). |
| **Object Modifiers** | Mesh deformation through modifiers. We are interested in [Deformations](https://docs.blender.org/manual/en/4.3/modeling/modifiers/deform/index.html) and [Physics](https://docs.blender.org/manual/en/4.3/modeling/modifiers/physics/index.html) (more later). |
| **Shape Keys**     | Commonly called *blendshape*, meaning having different copies of a mesh (same topology, same UV, same *everything*). Example: different facial expressions that blend over time with *Keyframing* (more later). |
| **Drivers**        | Mechanisms to control multiple properties at once and make some properties automatically update when others change (more later). |


## Keyframes 

### Relevant Shortcuts

<ul>
  <li>
    <span>With a property/object Selected</span>
    <table>
      <tr>
        <td><strong>I</strong></td>
        <td>Insert Keyframe (brings up keyframe menu)</td>
      </tr>
      <tr>
        <td><strong>Alt + I</strong></td>
        <td>Delete Keyframe</td>
      </tr>
      <tr>
        <td><strong>Shift + I</strong></td>
        <td>Insert Keyframe for all properties</td>
      </tr>
      <tr>
        <td><strong>Ctrl + I</strong></td>
        <td>Add keyframe to active keying set</td>
      </tr>
      <tr>
        <td><strong>Alt + S</strong></td>
        <td>Reset Scale (useful when animating transforms)</td>
      </tr>
      <tr>
        <td><strong>Alt + R</strong></td>
        <td>Reset Rotation</td>
      </tr>
      <tr>
        <td><strong>Alt + G</strong></td>
        <td>Reset Location</td>
      </tr>
    </table>
  </li>
  <li>
    <span>Inside <em>Graph Editor</em> or <em>Dope Sheet Editor</em></span>
    <table>
      <tr>
        <td><strong>G</strong></td>
        <td>Move keyframe(s)</td>
      </tr>
      <tr>
        <td><strong>S</strong></td>
        <td>Scale keyframe(s)</td>
      </tr>
      <tr>
        <td><strong>R</strong></td>
        <td>Rotate keyframe handle (in Graph Editor)</td>
      </tr>
      <tr>
        <td><strong>Shift + D</strong></td>
        <td>Duplicate keyframe(s)</td>
      </tr>
      <tr>
        <td><strong>X</strong> or <strong>Delete</strong></td>
        <td>Delete keyframe(s)</td>
      </tr>
      <tr>
        <td><strong>E</strong></td>
        <td>Extrapolate (Graph Editor)</td>
      </tr>
      <tr>
        <td><strong>T</strong></td>
        <td>Set Keyframe Interpolation (Linear, Bezier, Constant, etc.)</td>
      </tr>
      <tr>
        <td><strong>V</strong></td>
        <td>Set Keyframe Handle Type (Vector, Aligned, etc.)</td>
      </tr>
      <tr>
        <td><strong>Ctrl + C</strong></td>
        <td>Copy Keyframe</td>
      </tr>
      <tr>
        <td><strong>Ctrl + V</strong></td>
        <td>Paste Keyframe</td>
      </tr>
    </table>
  </li>
  <li>
    <span>Playback Shortcuts</span>
	<table>
      <tr>
        <td><strong>Spacebar</strong></td>
        <td>Play/Pause animation</td>
      </tr>
      <tr>
        <td><strong>Shift + Left Arrow</strong></td>
        <td>Jump to <strong>start frame</strong></td>
      </tr>
      <tr>
        <td><strong>Shift + Right Arrow</strong></td>
        <td>Jump to <strong>end frame</strong></td>
      </tr>
      <tr>
        <td><strong>Left Arrow</strong></td>
        <td>Move <strong>one frame backward</strong></td>
      </tr>
      <tr>
        <td><strong>Right Arrow</strong></td>
        <td>Move <strong>one frame forward</strong></td>
      </tr>
      <tr>
        <td><strong>Up Arrow</strong></td>
        <td>Move to <strong>next keyframe</strong></td>
      </tr>
      <tr>
        <td><strong>Down Arrow</strong></td>
        <td>Move to <strong>previous Keyframe</strong></td>
      </tr>
      <tr>
        <td><strong>Shift + Ctrl + Spacebar</strong></td>
        <td>Play animation in <strong>reverse</strong></td>
      </tr>
      <tr>
        <td><strong>Home</strong></td>
        <td>Zoom to fit all keyframes in <strong>Graph Editor/Dope Sheet</strong></td>
      </tr>
      <tr>
        <td><strong>Ctrl + Middle Mouse Scroll</strong></td>
        <td>Zoom in/out in Timeline/Graph Editor</td>
      </tr>
    </table>
  </li>
</ul>

When you set a keyframe on a simple static mesh, like a cube. (in the Viewport, object mode, Ctrl + A -> Mesh -> Cube). If 
- You press **I**, then all the transform properties are saved in the current frame as a keyframe (see in _Dope_Sheet_Editor_)
- If you want only a part of the default properties to be saved, then you can set them manually by clicking the *Animate Property* handle to 
  the right of the property in the _Properties Editor_ <br/>
  <img src="Y:\blender_docs_images\my_properties_animate_handle.png" alt="Animate Property Handle" width=40% />

### Introduction 

A *Keyframe* is a marker of time which stores the value of the selected property.
The purpose of a keyframe is to save the value of a property in a given instance of "time" (on a rendered frame. Physical elapsed time depends on the FPS of the animation).

An overview of all the existing keyframe in your animation can be seen in the _Playback Editor_. To get the full information about existing keyframes (ie. to which 
object they refer to and which property they alter/set, use the _Dope Sheet Editor_).

<img src="Y:\blender_docs_images\animation_keyframes_introduction_visualization.png" alt="Playback Keyframes" width=70% />

<div style="border: 2px solid #ccc; padding: 2px; border-radius: 1px; width: 70%; margin: 0 auto">
    <h4>Quick Experiment: KeyframeVisualiziation</h4>
	<h6>File <tt>01_Keyframes_Intro-Moving_Cube.blend</tt></h6>
    <div>
	  <ol>
	    <li>Create an empty blender scene with a cube and check FPS <br/>(<em>Properties Editor</em>/Output/Frame Rate)</li>
	    <li>Select its position from the <em>Properties Editor</em> and set a keyframe (<strong>I</strong> to keyframe the transform)</li>
	    <li>Move to another keyframe inside <em>Dope Sheet Editor</em> or <em>Playback Editor</em></li>
	    <li>
	      Freely Transform your cube and then set a keyframe. <strong>Note:</strong> It's Imperative that you first move to another place in the timeline and 
	  	then manipulate your object, otherwise it won't work!
	    </li>
	    <li>Go back to the start of the timeline (<strong>Shift+Left Arrow</strong>) and play the animation (<strong>Spacebar</strong>)</li>
	  </ol>
	  <p>Keep this example for the next on Interpolation</p>
	</div>
</div>

### Interpolation

When you set two keyframes on the same property, its value changes over the span of frames inbetween the two keyframes with *Interpolated Values*, ie values computed using 
a matematical formula. In particular, such formula is defined by an [*F-Curve*](https://docs.blender.org/manual/en/4.3/editors/graph_editor/fcurves/introduction.html), 
manipulated in the _Graph Editor_.

<img src="Y:\blender_docs_images\animation_keyframes_introduction_curves.png" alt="F-Curves Graph Editor" width=70% />

There is 1 curve for each animated property in the _Dope Sheet Editor_. The main setting is the *Interpolation* Type, which appears in the _Graph Editor_ inside the 
*F-Curve* Tab.
- *Bezier Curve*
- *Linear*
- *Constant* (Basically Bezier with the outward tangent handle fixed to horizontal direction)

<img src="Y:\blender_docs_images\my_graph_editor_interpolation_mode.png" alt="Graph Editor F-Curve Interpolation" width=90% />

**All the settings inside the F-Curve Tab affect the keyframes selected**

While what happens during the transition between a keyframe and the next one is defined by the *Interpolation* Mode, What happens outside the "Keyframed Range" 
(before the first keyframe and after the last keyframe) is defined by the *Extrapolation Mode*.<br/>
*Extrapolation Mode* is found under "_Graph Editor_/Channel/Extrapolation Mode" or <br/> with shortcut **Shift + E** (_Graph Editor_ Selected)
The following are the available *Extrapolation Modes*:

| | |
|-|-|
| *Constant* | (Default) Continue in a straight horizontal line |
| *Linear* | Continue in a straight line keeping the slope of the first/last keyframe |
| *Make Cyclic* | Repeat the curve, by adding a [*Cycles Modifier*](https://docs.blender.org/manual/en/4.3/editors/graph_editor/fcurves/modifiers.html#bpy-types-fmodifiercycles) |
| *Clear Cyclic* | Removes the *Cycles Modifier* if present in the active object |

**Extrapolation Mode affects all F-Curves Selected**

The settings to manipulate Curve Handles (placed on the F-Curve on the keyframe positions) depend on the Interpolation Type. A common setting among them all is the 
*Auto Handle Smoothing*, which can be either *None* or *Continuous Acceleration*. When not *None*, edits to a handle are propagated in the near handles (similiar to proportional editing)
to keep the F-Curve as smooth as possible. 

<img src="Y:\blender_docs_images\my_properties_cycylic_extrapolation.png" alt="F-Curve Extrapolation" width=90% />

<div style="border: 2px solid #ccc; padding: 2px; border-radius: 1px; width: 70%; margin: 0 auto">
  <h4>Quick Experiment: Interpolation and Extrapolation: "Cyclic Overshoot"</h4>
  <h6>File <tt>02_Keyframes_Interpolation-Moving_Cube_Custom_Interpolation.blend</tt></h6>
    <div>
    <ol>
      <li>Open the cube example you produced from the previous experiment</li>
      <li>Open the <em>Graph Editor</em> and select a "Location" Curve (the one with the bigger displacement in the Vertical axis)</li>
      <li>Play around with the 2 Handles freely. Example: Use the last one as "Bezier" Interpolation and create an "overshoot"</li>
      <li>Change the Extrapolation mode to Linear and then to Make Cyclic</li>
      <li>Check in the <em>Graph Editor</em>/Modifiers (Tab) that The Cycles Modifier has been added to the F-Curve</li>
      <li>Go back to the start of the timeline (<strong>Shift+Left Arrow</strong>) and play the animation (<strong>Spacebar</strong>)</li>
    </ol>
  </div>
</div>

### Keyframe Types 



# Animation: Used Editors 

## Properties Editor 

### Intro

### Rendering Tab 

### Modifiers Tab

## Playback Editor

## Dope Sheet Editor

## Graph Editor

# Animation Scenario: Camera Rig 

