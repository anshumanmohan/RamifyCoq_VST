#### Overview

This repository simply contains the latest version of RamifyCoq (commit 97572a) and VST (commit cb633f) thrown together into one directory. Having these directories as siblings with these names is not essential, but it simplifies things ever so slightly and allows a one-commmand build.


#### Prerequisite
Please make sure you have Coq version 8.9.1, which is the latest at the time of writing.


#### Download
Download this repository as a .zip and unpack it.


#### Build (warning, lengthy step)
Change to the RamifyCoq folder and then run either  `make vstandme7`  or  `make vstandme3`, depending on whether you would like to dedicate 7 or 3 cores to this task. You will see two warnings at the very top, but these can be safely ignored. The rest of the script will be a series of  “COQC filename” commands. You will see three ignorable warnings from VST when building the file “veric/mpred.v”.


#### Try it out!
For a quick taste, let us examine `find` from Figure 1 of the paper. The hyperlinks that follow lead back into this GitHub repository. The mathematical graph (§4) for `find` is built using a generic [PreGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/graph/graph_model.v#L18-L23), a suitable [LabeledGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/msl_application/UnionFindGraph.v#L35) atop the PreGraph, and a suitable [GeneralGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/msl_application/UnionFindGraph.v#L26-L36) atop that LabeledGraph. The spatial representation (§5) of this graph is built incrementally over several steps to improve code reusability, but it comes together [here](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/sample_mark/verif_unionfind.v#L21-L25) in our code. Finally, you can explore the [C code](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/unionfind.c) of union-find, the [Coq-readable AST](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/unionfind.v) of that code generated using VST’s clightgen tool, and the [Coq verification](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/verif_unionfind.v) of that AST.
