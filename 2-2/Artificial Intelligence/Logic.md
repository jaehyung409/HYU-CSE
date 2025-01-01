#artificial_intelligence #discrete_mathmatics #math 

### Concepts of Logical Representations
- syntax
- semantics
- $m$ : model ("possible world")
### Logical Entailment
- $\alpha\vDash\beta$ : sentence $\alpha$ entails the sentence $\beta$, $M(\alpha)\subseteq M(\beta)$
### Formal Definition of Inference
- $KB\vdash_i\alpha$ : "$\alpha$ is derived from $KB$ by $i$" or "$i$ derives $\alpha$ from $KB$"

### Propositional Logic
![](https://i.imgur.com/6ncqfIx.jpeg)
>In propositional logic, a model simply sets the<font color="#fac08f"> truth value</font> for every proposition symbol

- The semantics for propositional logic must specify how to compute the truth value of any sentence, given a model.
	- This is done recursively.
	- All sentences are constructed from atomic sentences and the five connectives.
	- Therefore, we need to specify how to compute the truth of atomic sentences and how to compute the truth of sentences formed with each of the five connectives

| $P$ | $Q$ | $\neg P$ | $P\wedge Q$ | $P\vee Q$ | $P\rightarrow Q$ | $P\Leftrightarrow Q$ |
| --- | --- | -------- | ----------- | --------- | ---------------- | -------------------- |
| F   | F   | T        | F           | F         | T                | T                    |
| F   | T   | T        | F           | T         | T                | F                    |
| T   | F   | F        | F           | T         | F                | F                    |
| T   | T   | F        | T           | T         | T                | T                    |

- A Simple Inference Procedure
	- Model checking with KB
		- Enumerate the models, and check that $\alpha$ is true in every model where $KB$ is true.
		- Models are assignments of _true_ of _false_ to every proposition symbol
	- theorem proving

### Theorem proving
> Finding a proof <font color="#fac08f">can be more efficient</font> (compared to building a truth table or model checking) because the proof can <font color="#fac08f">ignore irrelevant propositions.</font>
- #### Base
	- Logical Equivalences
		- $(\alpha\Rightarrow\beta)\equiv(\neg\alpha\vee\beta)$ : implication elimination
	- Modus Ponens $$\frac{\alpha\Rightarrow\beta,\ \alpha}{\beta}$$
	- And-Elimination (Simplification) $$\frac{\alpha\wedge\beta}{\alpha}$$
- #### Proof by Resolution $$\frac{l_1\vee\cdots\vee l_k,\quad\quad\quad m_1\vee\cdots\vee m_n}{l_1\vee\cdots\vee l_{i-1}\vee l_{i+1}\vee\cdots\vee l_k\vee m_1\vee\cdots\vee m_{j-1}\vee m_{j+1}\vee\cdots\vee m_n}$$
	- where $l_i$ and $m_j$ are complemnetary literals
- #### Conjunctive Normal Form (CNF)
    > A sentence expressed as a conjunction of clauses is said to be in <font color="#fac08f">conjunctivenormal form (CNF)</font>.

	1. Eliminate $\Leftrightarrow$
	2. Eliminate $\Rightarrow$
	3. $\neg$ to appear only in literals : Using double-negation and De Morgan's law
- #### [[Resolution Algorithm]]

### First-Order Logic