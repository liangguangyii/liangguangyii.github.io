---
layout: post
title: Notes for vmd
tags: [vmd, "Visualisation"]
categories: code
toc: true
math: true
---
## molecule_number and rep_number
molecule_number is the index of the molecule in the molecule list, and it is not reusued after the molecule is deleted. **Thus it's truely inconvenient when using command line, and we could use `top` to represent the molID in the bottom of the current molecule list.**

rep_number is the index of the representation in the representation list, with respect to the molecule_number. 


## `mol` command
[mol introduction](https://www.ks.uiuc.edu/Research/vmd/current/ug/node140.html), and [molinfo command](https://www.ks.uiuc.edu/Research/vmd/current/ug/node142.html#ug:topic:molinfo)

subcommands:

- `new`: add new molecule from a file, if it's blank, then it will create with no atoms.
- `addfile`: similar with `add`, except it will bind the new file and former file together, they will share with the same molID, and by using the command like `mol modcolor rep_ID mol_ID volume 1`, we could map the values of the latter file to the isosurface of the former file(where `1` is the index, start by 0, of the binding files in the molID).
- `delete` molecule_number: Delete molecule(s).
- `modcolor` rep_number molecule_number coloring_method: Change the current coloring method for the given representation in the specified molecule.
- `modmaterial` rep_number molecule_number material_name: Change the current material for the given representation in the specified molecule.
- `modstyle` rep_number molecule_number rep_style: Change the current rendering method (style) for the given representation in the specified molecule.
- `modselect` rep_number molecule_number select_method: Change the current selection for the given representation in the specified molecule.

- `scaleminmax` molecule_number rep_number [min max / auto]: Get/set the color scale range for this rep. Normally the color scale is automatically scaled to the minimum and maximum of the corresponding range of data. This command overrides the autoscaled values with the values you specify. Omit the min and max arguments to get the current values. Use ``auto" instead of a min and max to rescale the color scale to the maximum range again.

code to delete all molID in vmd:
```tcl
foreach i [molinfo list] {
mol delete $i
}
```


## Custom colormap

The colormap could be customized by `color change rgb[$i] $r $g $b`, and the `$i` is the index of the color in the colormap, and the `$r`, `$g`, `$b` are the RGB values of the color.

```tcl
proc mycolor_scale {} {
  set color_start [colorinfo num]
  display update off

  set colors(0) [list 1.0 1.0 1.0]  
  set colors(256) [list 0.0 0.0 1.0]  
  set colors(512) [list 1.0 0.0 0.0]  
  set colors(768) [list 0.0 1.0 0.0]  
    
  

  for {set i 0} {$i < 1024} {incr i} {
    if {$i < 256} {
      set ratio [expr double($i) / 256.0]
      set r [expr (1.0 - $ratio) * [lindex $colors(0) 0] + $ratio * [lindex $colors(256) 0]]
      set g [expr (1.0 - $ratio) * [lindex $colors(0) 1] + $ratio * [lindex $colors(256) 1]]
      set b [expr (1.0 - $ratio) * [lindex $colors(0) 2] + $ratio * [lindex $colors(256) 2]]
    } elseif {$i < 512} {
      set ratio [expr double($i - 256) / 256.0]
      set r [expr (1.0 - $ratio) * [lindex $colors(256) 0] + $ratio * [lindex $colors(512) 0]]
      set g [expr (1.0 - $ratio) * [lindex $colors(256) 1] + $ratio * [lindex $colors(512) 1]]
      set b [expr (1.0 - $ratio) * [lindex $colors(256) 2] + $ratio * [lindex $colors(512) 2]]
    } elseif {$i < 768} {
      set ratio [expr double($i - 512) / 256.0]
      set r [expr (1.0 - $ratio) * [lindex $colors(512) 0] + $ratio * [lindex $colors(768) 0]]
      set g [expr (1.0 - $ratio) * [lindex $colors(512) 1] + $ratio * [lindex $colors(768) 1]]
      set b [expr (1.0 - $ratio) * [lindex $colors(512) 2] + $ratio * [lindex $colors(768) 2]]
    } else {
      set ratio [expr double($i - 768) / 255.0]
      set r [expr (1.0 - $ratio) * [lindex $colors(768) 0] + $ratio * [lindex $colors(0) 0]]
      set g [expr (1.0 - $ratio) * [lindex $colors(768) 1] + $ratio * [lindex $colors(0) 1]]
      set b [expr (1.0 - $ratio) * [lindex $colors(768) 2] + $ratio * [lindex $colors(0) 2]]
    }

  color change rgb [expr $i + $color_start     ] $r $g $b
  }
  display update on
}
```

It will be activated by using the colormap command such as `mol scaleminmax molID repID min max` once again.