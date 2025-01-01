### Ref : [Knowledge based agents in AI - GeeksforGeeks](https://www.geeksforgeeks.org/knowledge-based-agents-in-ai/?ref=gcse_outind)

### Knowledge base(KB) 
> is a set of sentence
>	- Each sentence is expressed in a language called a <font color="#fac08f">knowledge representation language</font> and represents some assertion about the world
>	- When the sentence is taken as being given without being derived from other sentences, we call it an <font color="#fac08f">axiom</font>
```psuedo code
function KB-AGENT(percept) returns an action
	persistent: KB,a knowledge base
				t,a counter,initially 0,indicating time
	TELL(KB,MAKE-PERCEPT-SENTENCE(percept,t))
	action <- ASK(KB,MAKE-ACTION-QUERY(t))
	TELL(KB,MAKE-ACTION-SENTENCE(action,t))
	t <- t+1
	return action
```