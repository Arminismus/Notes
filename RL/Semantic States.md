Similar to [[Semantic Experience Replay]] and [[Semantic Exploration]], we can use sematic relationships to find states that we are in. This means, given an observation $O$, we turn this observation into a menaingful, standard and reproducible type of sentence that includes some abstract information about the environment. 


Then, when other states that are "abstractly" similar to this one are seen, we can easily find them using their semantic similarity, and this allows us to easily have generalization, and only maybe store a few hundred (depending on the problem of course, this varies) abstract states that are then evlauated using tabular methods.

As [[Vector Data Base|VDB]] embeddings are not only for text, but also for all other datatypes, other uses can be thought of, like image similarity. We could train the embeddings to see similarities that are relevant to the task, and then use them later with the [[Vector Data Base|VDB]].