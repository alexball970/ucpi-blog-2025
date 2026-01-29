# Why Computational Notebooks Are Great (and Why They Can Be a Mess)

If you have taken a data science, machine learning, or research-oriented computer science course, chances are that you have worked with a computational notebook. Tools like Jupyter Notebook have become the default environment for programming and data analysis, largely because they allow code, explanations, and results to coexist in a single place [2]. For many students (myself included), notebooks are also the first setting in which programming feels genuinely interactive rather than constrained by rigid structure.

That said, anyone who has spent time on a larger notebook project is likely familiar with how quickly this flexibility can become a source of problems. Cells may be executed out of order, variables can appear with unclear origins, and restarting the kernel can cause code that “worked five minutes ago” to fail entirely. It is tempting to attribute these issues to careless use. However, recent research suggests that many of these difficulties come from how notebook interfaces represent execution, state, and narrative, rather than from user error alone.

## Why Notebooks Feel So Natural to Use

A key strength of computational notebooks lies in their support for *computational narratives*: the interleaving of code, output, and explanatory text to communicate the progression of an analysis. This approach is closely related to Knuth’s notion of *literate programming*, which frames programs as artifacts written primarily for human readers, with machines as a secondary concern [1].

In practice, however, notebooks succeeded where literate programming did not. One reason is their lightweight nature. A user can write a few lines of code, execute them immediately, inspect the output, and move on. Jupyter, in particular, further lowered the barrier by requiring minimal setup and enabling interactive execution directly in the browser [2].

What is easy to miss is how strongly this design encourages exploration. Users are implicitly invited to try ideas, backtrack when needed, and iterate freely, without having to commit to a polished structure early on.

## The Notebook Execution Model (and Why It Causes Problems)

At the core of this experience is the cell-based execution model. Code is divided into cells, each of which can be executed independently and in arbitrary order. While this flexibility is essential for exploratory work, it also introduces a fundamental tension: the *visual structure* of a notebook often diverges from the actual execution history that produced its current state.

Ramasamy et al. provide empirical evidence for this mismatch by analyzing hundreds of real-world Jupyter notebooks. They show that most notebooks follow non-linear workflows, involving forks, alternative paths, and dead ends during development [4]. Yet, when notebooks are later cleaned up or shared, these decision points are typically collapsed into a single linear sequence of cells.

As a result, a notebook may appear orderly and linear, even though the analysis that led to it involved many branching decisions that are no longer visible to the reader.

## Why This Becomes a Real Issue in Practice

This hidden non-linearity becomes particularly problematic when notebooks are read by someone other than their original author. Ramasamy et al. demonstrate that third-party readers often struggle to reconstruct the intent and reasoning behind a notebook because exploratory decisions, abandoned directions, and intermediate rationale are rarely documented explicitly [4]. Their controlled user study further shows that visualizing workflow structure, such as forks and dead ends, can significantly improve comprehension.

Executability presents another recurring concern. Earlier studies reported that a large proportion of public notebooks fail to execute from top to bottom, which has contributed to the perception that notebooks are fundamentally unreliable. Nguyen et al. revisit this claim and argue that such a binary notion of executability is poorly suited to interactive notebook environments [6].

By examining more than 42,000 popular notebooks, they find that only a minority are *pathologically non-executable*. In most cases, failures arise from missing files, missing libraries, or implicit execution order. Importantly, their analysis shows that partial executability, the ability to successfully run a prefix of cells, can still offer meaningful value for comprehension and reuse, even when full execution is not possible [6].

## How Research Tries to Improve Notebooks

Instead of trying to limit how people explore, recent research has focused on making notebook structure and state easier to reason about.

Ramasamy et al. propose visual representations of data science workflows that explicitly surface forks, dead ends, and intermediate analysis steps, allowing readers to reconstruct the author’s reasoning process instead of seeing only the final outcome [4].

Another line of research targets the reliance on global state in notebooks. Pagebreaks addresses this issue by introducing *multi-cell scopes*, which allow variables to be shared within a limited region of the notebook rather than across the entire document [5]. Notably, the design of Pagebreaks is motivated by the observation that traditional function scopes often interfere with common exploratory practices, such as using cells as alternatives or interleaving code with output [5].

Instead of organizing notebooks around functions, Pagebreaks represents a compromise: it introduces structure while preserving the interactive behaviors that notebook users rely on.

Other systems, such as *mage*, explore how users move fluidly between writing code and directly manipulating visual elements. This work further reinforces the idea that notebooks function not only as programming environments, but also as interaction spaces for thinking through problems [3].

Finally, Nguyen et al. point towards a more flexible view of notebook quality by showing that lightweight restoration techniques, including LLM-based fixes for missing inputs or dependencies, can substantially improve notebook executability without requiring a complete rewrite of the analysis [6].

## Why This Matters Going Forward

Computational notebooks are no longer limited to educational settings. They now play an important role in modern data science workflows and increasingly serve as interfaces for AI-assisted programming. As their use expands, the limitations of current notebook interfaces become harder to ignore.

Across recent work, a common theme emerges: notebooks should not be evaluated as traditional software artifacts. Their value lies in exploration, iteration, and partial results. Therefore, The challenge here is to design interfaces that preserve this flexibility while making execution state, workflow structure, and author intent more explicit.

## Looking Ahead: Rethinking the Notebook as an Interface

It is easy to see the limitations of computational notebooks as a set of isolated usability problems. In practice, recent research suggests something broader: these issues reflect how notebooks are designed as programming interfaces. Rather than treating notebooks as static documents that sometimes fail, it may be more useful to think of them as interactive systems meant to support exploration.

One possible direction is to make execution history and user intent more explicit. Instead of only recording code and outputs, notebooks could surface which cells represent exploratory branches, which ones contribute to the final result, and which assumptions were made along the way. This would build on work that highlights non-linear workflows and hidden state as well as making notebooks easier to understand for others.

There is also growing interest in how notebooks might interact with AI systems. Beyond generating code, future interfaces could help users reason about partial executability, missing context, or implicit execution order. In this sense, AI would not replace exploration but serve as a reflective layer that helps users understand the consequences of their actions.

Overall, these directions suggest that notebooks should not be evaluated solely as traditional software artifacts. Their value often lies in iteration and revision. If notebooks are meant to support thinking as much as programming, then making the evolution of an analysis visible may be just as important as whether it runs end-to-end.

## Final Thoughts

Computational notebooks have reshaped how many of us learn and practice programming. They lower the barrier to entry and make experimentation feel more natural. At the same time, they hide important information about execution order, state, and decision-making.

Recent research reframes these shortcomings as interface design problems rather than user failures. By making workflows, scopes, and executability more visible without constraining exploration, it becomes possible to retain what makes notebooks powerful while mitigating many of their most annoying issues.

## References

[1] Knuth, D. E. (1984). *Literate programming*. The Computer Journal, 27(2), 97–111.  
[2] Kluyver, T., et al. (2016). *Jupyter Notebooks – a publishing format for reproducible computational workflows*. Proceedings of the 20th International Conference on Electronic Publishing.  
[3] Kery, M. B., Ren, D., Hohman, F., Moritz, D., Wongsuphasawat, K., & Patel, K. (2020). *mage: Fluid moves between code and graphical work in computational notebooks*. Proceedings of the 33rd ACM Symposium on User Interface Software and Technology.  
[4] Ramasamy, D., Sarasua, C., Bacchelli, A., & Bernstein, A. (2023). *Visualising data science workflows to support third-party notebook comprehension*. Empirical Software Engineering, 28(58).  
[5] Rawn, E., & Chasins, S. E. (2025). *Pagebreaks: Multi-cell scopes in computational notebooks*. Proceedings of the 2025 CHI Conference on Human Factors in Computing Systems.  
[6] Nguyen, T., Gill, W., & Gulzar, M. A. (2025). *Are the majority of public computational notebooks pathologically non-executable?* Proceedings of the IEEE/ACM International Conference on Mining Software Repositories.
