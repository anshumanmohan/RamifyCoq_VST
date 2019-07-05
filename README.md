This readme is organized into two parts: an overview for setting up the system on your computer and a deeper dive for navigating different parts of the build thereafter. We provide a command-line-only Docker machine containing a functional, compiled, and Coq-checked installation of our system, so this setup is skippable if you are only mildly curious. However, if you want to actually step through the proofs in detail, we do recommend downloading and building our system on your machine and then using a more graphic explorer such as ProofGeneral in Emacs. We explain this setup here. 

## Overview
This repository simply contains the latest version of RamifyCoq (commit 97572a) and VST (commit cb633f) thrown together into one directory. Having these directories as siblings with these names is not essential, but it simplifies things ever so slightly and allows a one-commmand build.


#### Prerequisite
Please make sure you have Coq version 8.9.1, which is the latest at the time of writing.


#### Download
Download this repository as a .zip and unpack it.


#### Build (warning, lengthy step)
Change to the RamifyCoq folder (`cd RamifyCoq/`) and then run either  `make vstandme7`  or  `make vstandme3`, depending on whether you would like to dedicate 7 or 3 cores to this task. You will see two warnings at the very top, but these can be safely ignored. The rest of the script will be a series of  “COQC filename” commands. You will see three ignorable warnings from VST when building the file “veric/mpred.v”.


#### Try it out!
For a quick taste, let us examine `find` from Figure 1 of the paper. The hyperlinks that follow lead back into this GitHub repository. The mathematical graph (§4) for `find` is built using a generic [PreGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/graph/graph_model.v#L18-L23), a suitable [LabeledGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/msl_application/UnionFindGraph.v#L35) atop the PreGraph, and a suitable [GeneralGraph](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/msl_application/UnionFindGraph.v#L26-L36) atop that LabeledGraph. The spatial representation (§5) of this graph is built incrementally over several steps to improve code reusability, but it comes together [here](https://github.com/anshumanmohan/RamifyCoq_VST/blob/f0afce0137ffdfe7635646f1398beae5224a14d8/RamifyCoq/sample_mark/verif_unionfind.v#L21-L25) in our code. Finally, you can explore the [C code](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/unionfind.c) of union-find, the [Coq-readable AST](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/unionfind.v) of that code generated using VST’s clightgen tool, and the [Coq verification](https://github.com/anshumanmohan/RamifyCoq_VST/blob/master/RamifyCoq/sample_mark/verif_unionfind.v) of that AST.

## A Deeper Dive
Just like `find` described above, we have similar developments for each of our examples. As explained in our paper, we enjoy code reuse with the mathematical and spatial graphs, but the C code, the AST, and the verification files are individually customized. 

We verified the following algorithms:
 
 
Algorithm | Code File | Verification Files
------|------ | -------------
Marking a bigraph | mark_bi.c | verif_mark_bi.v, verif_mark_bi_dag.v
Unionfind using struct Node | unionfind.c | verif_unionfind.v, verif_unionfind_rank.v, verif_unionfind_slim.v
Unionfind using an array | unionfind_arr.c | verif_unionfind_arr.v
Unionfind using iter | unionfind_iter.c | verif_unionfind_iter.v, verif_unionfind_iter_rank.v
Disposing a bigraph | dispose_bi.c | verif_dispose_bi.v
Garbage collector | gc.c | verif_garbage_collect.v

With the exception of the last row, all the .c and .v files are in the directory RamifyCoq/sample_mark/. The garbage collector algorithm was sufficiently involved that we placed its files in a separate directory, RamifyCoq/CertiGC/. 

As the table shows, we verified some C programs repeatedly, i.e. using different Coq specifications. For instance, we verified mark_bi.c by abstracting the problem to a mathematical bigraph (verif_mark_bi.v) and also by abstracting the problem to a mathematical directed acyclic graph (verif_mark_bi_dag.v).

The artifact supports the claims made in the paper in that it does actually verify six algorithms, as summarised in the table above. The mathematical graph model described in §4 of the paper is built over several files in the directory RamifyCoq/graph and the spatial graph explored in §5 is in RamifyCoq/msl_application.
