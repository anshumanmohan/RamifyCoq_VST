#### Overview

This repository simply contains the latest version of RamifyCoq (commit 97572a) and VST (commit cb633f) thrown together into one directory. Having these directories as siblings with these names is not essential, but it simplifies things ever so slightly and allows a one-commmand build.


#### Prerequisite
Please make sure you have Coq version 8.9.1, which is the latest at the time of writing.


#### Download
Download this repository as a .zip and unpack it.


#### Build (warning, lengthy step)
Change to the RamifyCoq folder and then run either  `make vstandme7`  or  `make vstandme3`, depending on whether you would like to dedicate 7 or 3 cores to this task. You will see two warnings at the very top, but these can be safely ignored. The rest of the script will be a series of  “COQC filename” commands. You will see three ignorable warnings from VST when building the file “veric/mpred.v”.


#### Try it out!
For a quick taste, let us examine `find` from Figure 1 of the paper. The hyperlinks that follow lead back into this GitHub repository. The mathematical graph (§4) for `find` is built using a PreGraph, a suitable LabeledGraph atop the PreGraph, and a suitable GeneralGraph atop that LabeledGraph. The spatial representation (§5) of this graph is here. Finally, you can explore the C code of union-find, the Coq-readable AST of that code generated  using VST’s clightgen tool, and the Coq verification of that AST.
