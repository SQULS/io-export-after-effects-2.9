#IO Export To After Effects

This is a version of https://developer.blender.org/diffusion/BAC/browse/master/io_export_after_effects.py updated to work with Blender 2.9. I fixed this before discovering a more robust update on [Blender.org](https://developer.blender.org/diffusion/BAC/browse/master/io_export_after_effects.py) Have still created this repo for people asking the same questions as I was.

NB. Not currently an add-on and will need to be run from script page of Blender.

## Usage

Select the objects and camera etc that you wish to export, and go to File>Export>Adobe After Effect (.jsx)

Save the file.

Open After Effects (Version > CS3)

File>Scripts>Run Script File and select your file. It will ask you to name the comp. Any name will work

Next, after it is done, go into the Project panel and open up your comp. Nulls objects and a camera should be there, matching the motion of the ones in blender.

## Updating from Blender 2.6 to 2.9

Several changes to the Blender API occurred between these versions. This repo/script contains simple fixes in order to run in newer versions of Blender.

### Fixes

#### Matrix multiplication

Blender has adjusted its mathutils module, replacing the asterisk * with the at symbol @, aka the PEP 465 binary operator, for multiplying matrices with vectors.

```
384 matrix = Matrix.Translation(cam.matrix_basis.copy() @ track.bundle)
```

More information here:https://blender.stackexchange.com/questions/129473/typeerror-element-wise-multiplication-not-supported-between-matrix-and-vect/129474

#### Cannot specify unnamed parameters

Named parameters must be passed with argument name.

```
737 box.label(text='Animation:')
```

More information here: https://b3d.interplanety.org/en/porting-add-on-from-blender-2-7-to-blender-2-8/

#### Renaming of INFO_MT

Blender now longer uses ```INFO_MT``` to refer to top level menu but instead now uses ```TOPBAR_MT```

```
 765 bpy.types.TOPBAR_MT_file_export.remove(menu_func)
```
