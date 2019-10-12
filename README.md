# oniom_from_vmd
A small utility to facilitate the creation of ONIOM inputs from Gaussian using VMD selections

# To run

Two files are needed. The `maskfile.txt` is where the high, medium, and low levels are set. Use VMD masks, as these will be directly passed to VMD for the selections. An example is:

```
SYSTEM='(same residue as all within 8 of protein) or (same residue as all within 20 of resid 224)'
FREEZE='resname NULL'
HIGH='( (resid 67 64 and (sidechain)) or resid 224 or (resid 65 and name C O) or (resid 66 and name N  H CA HA) or (same residue as all within 6 of resid 224))'
LOW='resname NULL'
```

Will create a 2 level system, using the entire protein. Nothing will be frozen in the optimization.

An accompanying run script could be:

```
d=~/research/active/tgokey/dna_repair/1AKZ/receptor/WT-1Cd2_placed_in_AS_186HID
get_oniom.sh \
	$d/qm/WT-1Cd2_placed_in_AS_186HID_qm.parm7 \
	$d/qm/WT-1Cd2_placed_in_AS_186HID_qm.nc \
	../input/maskfile.txt \
	107
```

And we see that we need to provide a parameter file, a trajectory, the maskfile created above, and the frame number in the trajectory. 

Many inputs are generated, but the final output is `newinput.gin`. Ideally, once link atoms are added, the file is ready to run!


# Notes

Everything is automated except writing the link atoms. This means that they will need to be inserted by hand.

Additionally, several things are hard-coded in the configuration, such as method/basis, as well as many extra options for Gaussian.

# Requirements

*	VMD
*	cpptraj
*	python
*	tleap
