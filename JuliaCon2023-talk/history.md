# History

  * March 2021: a three page text, [Towards Practical Use of Dataflow Matrix Machines](https://www.cs.brandeis.edu/~bukatin/towards-practical-dmms.pdf), calling for use of modern differentiable programming engines such as Zygote.jl (Julia Flux) and JAX to solve problems of DMM synthesis is published.

  * July 2021: an open source project to synthesize an equivalent of the handcrafted DMM from Section 3 of https://arxiv.org/abs/1606.09470 starts and immediately encounters difficulties in taking gradients with respect to dictionaries.

  * April 2022: I open source a JAX-based example of taking gradients with respect to dictionaries: https://github.com/anhinga/jax-pytree-example

  * April 2022: I obtain and open source a Zygote.jl (Julia Flux) example of taking gradients with respect to dictionaries: https://github.com/anhinga/julia-flux-drafts/tree/main/arxiv-1606-09470-section3

  * May 2022: First gradients with respect to tree-based sparse connectivity matrix of a DMM using Zygote.jl.

  * June 2022: First successful training of a DMM using Zygote.jl.

  * June 2022: First successful synthesis of sparse DMMs via a sparsifying training procedure. The synthesized DMMs have impressive generalization properties.

  * July 2022-August 2022: Some follow-up expreriments (everything is done using Zygote.jl).

  * September 2022: I open source the May-August work: https://github.com/anhinga/julia-flux-drafts/tree/main/arxiv-1606-09470-section3/May-August-2022
  
  * July 2023: Double-checking that things work in Julia 1.9.2: https://github.com/anhinga/2023-julia-drafts/tree/main/reproduce-in-Julia-1.9.2/DMM-lite