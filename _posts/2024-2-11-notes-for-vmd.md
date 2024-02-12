---
layout: post
title: Notes for vmd
tags: [vmd, "Computer Science"]
categories: code
toc: true
math: true
---
## molecule_number and rep_number
molecule_number is the index of the molecule in the molecule list, and it is not reusued after the molecule is deleted.

rep_number is the index of the representation in the representation list, with respect to the molecule_number. 


## `mol` command
[mol introduction](https://www.ks.uiuc.edu/Research/vmd/current/ug/node140.html), and [molinfo command](https://www.ks.uiuc.edu/Research/vmd/current/ug/node142.html#ug:topic:molinfo)

subcommands:

- `new`: add new molecule from a file, if it's blank, then it will create with no atoms.
- `addfile`: similar with `add`, except it will add the molecule to the top of the molecule list. 
- `delete` molecule_number: Delete molecule(s).
- `modcolor` rep_number molecule_number coloring_method: Change the current coloring method for the given representation in the specified molecule.
- `modmaterial` rep_number molecule_number material_name: Change the current material for the given representation in the specified molecule.
- `modstyle` rep_number molecule_number rep_style: Change the current rendering method (style) for the given representation in the specified molecule.
- `modselect` rep_number molecule_number select_method: Change the current selection for the given representation in the specified molecule.

- `scaleminmax` molecule_number rep_number [min max | auto]: Get/set the color scale range for this rep. Normally the color scale is automatically scaled to the minimum and maximum of the corresponding range of data. This command overrides the autoscaled values with the values you specify. Omit the min and max arguments to get the current values. Use ``auto" instead of a min and max to rescale the color scale to the maximum range again.
