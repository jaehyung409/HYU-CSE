Project : Large Language Models을 이용하여 10개의 Test Sentences에 대한 sentiment-analysis를 평가하기 (In-context-learning)

이름 : 주재형

학번 : 2021032188

소속 : 한양대학교, 컴퓨터소프트웨어학부

1. 사용 AI 모델 : ChatGPT 4o mini 
2. In-Context Learning
	1. Zero-Shot
		- Full dialog
			- ![|400](https://i.imgur.com/toyrd85.png)
			- Accuracy : 100%
		- 아무런 사전 지식 없이 긍정과 부정을 판단해달라는 질문에 100% 정확도를 보여주었습니다.
	2. Few-Shot
		- Full dialog
			- ![|270](https://i.imgur.com/7UDGQHJ.png)
			- Accuracy : 100%
		- 설명없이, SST2 예제를 이용하여 5개의 예시 문장을 제시하였습니다.
	3. Chain of Thought Prompting
		- 학습 과정
			- ![|300](https://i.imgur.com/KzuyMsE.png)
		- 테스트 과정
			- ![|350](https://i.imgur.com/svvahou.png)
			- Accuracy : 100%
		- 학습 과정에서 문제 풀이과정으로 제시한 방법을 그대로 적용하여, 앞선 예시와 달리 풀이과정을 함께 제시하고 있습니다.
3. 결론
 - Open AI의 Chat GPT 4o mini 의 성능이 자연어 처리에 탁월해서 zero-shot에도 100%의 정확도를 보여주었습니다. 그러나 모델이 어떠한 방법을 사용해서 문제를 해결하였는 지는 알 수 없었습니다. Few-shot 역시 모델의 정확도를 개선시켜줄 지는 모르나, 여전히 비슷한 맥락의 답을 제시하였습니다. 
 
 - Chain of Thought Prompting은 학습에 사용한 풀이과정을 그대로 답습하여 풀이과정과 함께 답을 제시하기 때문에, 학습시킬 때의 방법이 정확하다면 더 높은 수준의 정답률을 보여줄 것으로 기대됩니다. 비록 앞선 예시에서도 정확도가 100%라 이에 대한 검증을 하지는 못하였으나, 답변에 풀이과정을 제시한 점에서 긍정적으로 평가할 수 있습니다.

- 따라서 Chat GPT와 같은 Large Language Model을 통해 답을 구하려할 때, 모델의 답변이 마음에 들지않는다면 예시 문항을 풀이과정과 함께 제시하면 더 좋은 결과를 얻을 수 있다는 사실을 확인할 수 있었습니다.