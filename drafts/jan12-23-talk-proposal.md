# Exploring synthesis of flexible neural machines with Zygote.jl

---

We were able to successfully synthesize simple compact high-level neural machines via a novel algorithm for neural architecture search using flexible differentiable programming capabilities of Zygote.jl.

---

We are studying an interesting class of flexible neural machines where single neurons process streams of vectors with tree-shaped indices rather than streams of numbers (see https://anhinga.github.io/ and https://arxiv.org/abs/1712.07447, "Dataflow Matrix Machines and V-values: a Bridge between Programs and Neural Nets"). These machines are expressive enough to be used for general-purpose stream-oriented programming (dataflow or functional reactive programs). They are also expressive enough to flexibly and compositionally modify their own weight-connectivity matrices on the fly. They can be thought of as flexible attention machines, with neuron inputs computing linear combinations of vectors with tree-shaped indices and thus working as attention devices.

We would like to explore a variety of machine learning experiments using this class of neural machines. In particular, it would be nice to be able to use differentiable programming and gradient methods in those experiments. Traditional machine learning frameworks would necessitate difficult engineering work reshaping those flexible tree-shaped vectors into flat tensors. 

Zygote.jl provides flexible differentiable programming facilities and, in particular, allows users to take gradients with respect to variables aggregated inside a tree. That makes it a perfect fit for our machine learning experiments with flexible neural machines.

We consider the following novel algorithm for neural architecture search. Consider neural architectures where connections between neural modules are gated with scalar multipliers. Start with a sufficiently large network and perform sparsifying training of this network on a set of test problems using sparsifying regularization and gradually pruning inter-module connections with low gating weights.

In our case, the neural modules are powerful "super-neurons" of dataflow matrix machines. In our exploratory set of experiments we consider a duplicate character detector problem (a hand-crafted compact neural machine solving this problem is described in Section 3 of https://arxiv.org/abs/1606.09470, "Programming Patterns in Dataflow Matrix Machines and Generalized Recurrent Neural Nets").

The history of our preliminary experiments is documented at https://github.com/anhinga/DMM-synthesis-lab-journal/blob/main/history.md

These are moderate scale experiments successfully performed on a home laptop CPU.

Zygote.jl is quite awesome, but using it is still not without some difficulties. In particular, while "backpropagation theorem" promises us reverse-mode gradients at cost of the corresponding forward computation multiplied by a small constant, in practice we often observe larger slowdowns (presumably this happens when the forward computation is friendly to compiler optimizations, while the induced gradient computation is not). When this slowdown is still moderate one can successfully use Zygote.jl. When the slowdown starts to exceed two-three orders of magnitude, it makes sense to switch to the stochastic approximation of gradient computations via OpenAI flavor of evolution strategies even if one is computing sequentially and not on a cluster (see https://arxiv.org/abs/1712.06564, "On the Relationship Between the OpenAI Evolution Strategy and Stochastic Gradient Descent" by Xingwen Zhang, Jeff Clune, and Kenneth O. Stanley).

In our case, we have initially bumped into heavy slowdowns and memory swaps when trying to perform this neural synthesis in the most ambitious prior-free manner starting with a fully-connected recurrent machine with long backpropagation through time. 

Because we have been aiming to synthesize feedforward circuits with local recurrences, we decided to scale our ambition down and rely on some priors and start with fully connected feedforward machines with skip connections and local recurrences.

Then we have obtained acceptable performance and have been able to synthesize very compact, human-readable neural machines with rather remarkable generalization properties using a tiny training set.

These are very exciting preliminary results where nice-looking compact, human-readable neural circuits approximating a hand-written neural program have been automatically synthesized for the first time.

We hope that this line of exploration will be continued, by ourselves and by other people. (The speaker is looking for collaboration opportunities.)
