#artificial_intelligence #probability #machine_learning 
## Naïve Bayes
- ref : [나이브 베이즈 분류기 - GeeksforGeeks](https://www.geeksforgeeks.org/naive-bayes-classifiers/?ref=gcse_outind)
- Naïve Bayes models assume that the value of a particular feature (or random variable) is <font color="#d99694">(conditionally) independent</font> of the value of any other feature, given the class variable. 
	- In practice, naïve Bayes systems often work very well, even when the conditional independence assumpion is not strictly true. 
- The naïve Bayes model consists of
	- <font color="#b2a2c7">the prior probabilities P </font>
	- <font color="#e36c09">the conditional probabilities P</font>
- The posterior probability is proportional to the multiplication of the prior and conditional probabilities (likelihood) $$\Pi_iP(conditional\ probabilities)P(prior\ probability)$$

- Naïve Bayes models are widely used for language determination, document 
retrieval, spam filtering, and other classification tasks. 
- For tasks such as medical diagnosis, where the actual values of the posterior 
probabilities really matter, one would usually prefer to use more sophisticated 
models such as neural networks.