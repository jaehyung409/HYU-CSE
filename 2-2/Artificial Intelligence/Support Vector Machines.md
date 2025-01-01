#machine_learning #artificial_intelligence 
### SVM (Suuport Vector Machines)
- Construct <font color="#e36c09">a maximum margin separator.</font>
	- A decision boundary with the largest possible distance to example points
	- The margin is the width of the area bounded by dashed lines in the figure
		- twich the distance from the separator to the nearest example point.
		- ![](https://i.imgur.com/O0nBoB6.png)
- Have the ability yo embed the data into a higher-dimensional space (<font color="#e36c09">kernal trick</font>)
	- ![](https://i.imgur.com/rv2ZrB7.png)
- Nonparametric : the separating hyperplane is difined by <font color="#e36c09">a set of example points</font>, not by a collection of parameter values.
	- Logistic regression would find some separating line ; the exact location of the line depends on ***all*** the example points.
	- The key insights of SVMs is that some examples are more important than others (i.e., <font color="#e36c09">support vectors</font>), and that paying attention to them can lead to better generalization.
	- ![](https://i.imgur.com/mieUd9c.png)
