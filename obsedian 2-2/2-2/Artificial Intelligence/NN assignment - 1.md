Project : 신경망 모델을 이용하여 10개의 Test Sentences 에 대한 sentiment-analysis를 수행하기. (70% 이상의 정확도를 가진 신경망 모델 구현하기)

이름 : 주재형

학번 : 2021032188

소속 : 한양대학교, 컴퓨터소프트웨어학부

1. 사용 모델 : CNN (from torch.nn, nn.Conv1d)
수업시간에 다루었던 CNN, FFNN, RNN, Transformer 중에 모델을 고려하였습니다. 

그 중 자연어 처리에 효율적이라고 알려진 RNN의 한 종류인 LSTM을 사용하였으나, 모델의 복잡성이 너무 커 67349개의 데이터 예제를 학습하는 데에 걸리는 시간이 길었습니다. 또한 10개의 Test Set만 평가할 예정이기에, 신경망 모델의 성능이 낮아도 된다고 생각하였습니다. 

따라서 FFNN을 고려하였으나, LSTM과는 반대로 단순한 구조로 인하여 감정 분석과 같은 자연어 처리 작업에서 에러가 크게 나타났기에 CNN을 선택하였습니다.

CNN 모델은 지역적 특징을 추출하고 데이터의 패턴을 학습하는 데 강점을 보이는 모델입니다. 수업 시간에 다루었듯, Convolution과 Pooling 작업을 통해 데이터의 차원을 줄리는 방식으로 동작합니다. (데이터의 중요한 정보를 강조)

2. 데이터셋(SST2)와 전처리 과정
- Datasets : [stanfordnlp/sst2 · Datasets at Hugging Face](https://huggingface.co/datasets/stanfordnlp/sst2)
	- Fully labeled 된 67349개의 예제 제공 (`ds[train]`)
	- Strucutre 
```python
{'idx': 0,
 'sentence' : 'hide new secretions from the parental units'
 'label' : 0}
```
- Test sets 을 앞선 Datasets과 같은 구조로 만들기 위하여 test_sentence와 label을  list 형태로 입력하고 `pandas.DataFrame` 과 `Dataset.from_pandas`를 이용하여 앞선 SST2 데이터셋 형태로 재가공하였습니다.
- 전처리 과정 (데이터를 모델이 사용할 수 있도록 바꾸는 과정)
- `tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")` 사용
- CNN 모델은 고정 길이 모델이므로 padding 및 truncation과정을 진행합니다. (또한 배치의 크기를 동일하게 맞춰 효율성을 높일 수 있습니다.)
- 이후 `map` 함수를 사용하여 각각의 데이터 셋을 토큰화하고 `set_format` 함수로 데이터셋을 PyTorch 텐서 형식으로 설정합니다.
- 이 과정에서 train 모델에서 label이 0과 1을 넘어가는 데이터 (-1의 라벨을 가진 test set이 섞였을 것으로 추정)가 존재하여 filter를 사용하였습니다.
```python
# 배치사이즈 32, numworkser 4
train_dl = DataLoader(train_ds, batch_size=32, shuffle=True, num_workers=4)  
test_dl = DataLoader(test_ds, batch_size=32, num_workers=4)
```

3. CNN 모델 (`torch.nn.Conv1d`)
- `self.embedding = nn.Embedding(tokenizer.vocab_size, 64)  `
	- 입력 데이터를 64차원의 임베딩 벡터로 변환
- `self.conv1 = nn.Conv1d(64, 8, 3)`  
	- 입력 채널 64, 출력 채널 8, 커널(필터) 크기 3으로 convolution 연산 수행
- `self.pool = nn.MaxPool1d(2)`
	- pooling 연산 수행 
- `self.fc = nn.Linear(8, 2)`  
	- 8차원 벡터를 긍정과 부정 (1, 0)으로 분류 (fully-connected)
```python
def forward(self, x):  
        x = self.embedding(x)  
        x = x.permute(0, 2, 1)  # 텐서의 차원을 레이어에 맞게 조정
        x = self.conv1(x)  
        x = x.pool(x)
        x = x.max(2)[0]         # 각 채널에서 최대값 선택
        x = self.fc(x)  
        return x
```

4. train_loop와 test_loop
- Loss function 과 Optimizer 선택
	- `loss_fn = nn.CrossEntropyLoss()` 
		- binary classification이므로 사용 (ref, FFNN error func class)
	- `optimizer = torch.optim.Adam(model.parameters(), lr=0.001)`
		- 방향과 스탭사이즈 모두 적절히 이동(ref, Programming class)
- 이외 코드는 Programming class 참조

5. 테스트 결과
- Epoch 1 : Test Accuracy : 90.0%, Avg loss : 0.033744
	- ![|400](https://i.imgur.com/7ba3v9Z.png)
- Epoch 2 : Test Accuracy : 90.0%, Avg loss : 0.016478
	- ![|400](https://i.imgur.com/YOku3Qq.png)
- Epoch 3 : Test Accuracy : 100.0%, Avg loss : 0.010886
	- ![|400](https://i.imgur.com/XYJI3Lm.png)
- Epoch 4 : Test Accuracy : 100.0%, Avg loss : 0.007592
	- ![|400](https://i.imgur.com/R4fHHbv.png)
- Epoch 5 : Test Accuracy : 100.0%, Avg loss : 0.006931
	- ![|400](https://i.imgur.com/m7eqJfY.png)
