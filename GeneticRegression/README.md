# Linear Regression using Genetic Algorithm

유전 알고리즘은 여러 개의 해를 임의로 생성하여 초기 후보해를 생성한 뒤, 선택, 교차, 돌연변이 연산을 통해 최적해 또는 최적해에 근접한 해를 구하는 알고리즘이다. 유전 알고리즘을 사용한 선형 회귀는 적합도 평가를 MSE로 진행하며, 회귀 계수를 유전 알고리즘에서의 염색체라 가정한 뒤 진행하였다.

다양한 데이터에 적용하여 구현한 코드를 테스트하기 위해 클래스를 정의하였다. 전체 코드는 [여기](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/GeneticRegression.ipynb)에서 확인할 수 있다.

```python
class GeneticRegression():
    def __init__(self, num_population, mutation_rate, data_x, data_y):
    def fit(self, stop_count):
    def next_generation(self):
    def selection(self):
    def crossover(self):
    def mutation(self):
    def query(self, idx):
    def MSE(self, y, t):
    def find_best(self):
    def debugging(self, index):
```

_**\_\_init\_\_**_에서는 후보해의 수, 돌연변이율, 독립변수, 종속변수 등 초기 값들을 설정한다.

**_selection_**, **_crossover_**, **_mutation_**을 통해 선택 연산, 교차 연산, 돌연변이 연산이 진행된다.

_**next\_generation**_은 **_selection_**, **_crossover_**, **_mutation_**을 통해 다음 세대의 후보해를 선택한다.

_**fit**_는 최적해 또는 최적해에 근접한 해를 찾을 때까지 세대 교체를 진행한다.

_**query**_는 입력 값에 대해 후보해의 선형회귀 예측값을 반환한다. 후보해는 초기 _**\_\_init\_\_**_에서 설정해 준 만큼의 수가 있으므로, _idx_를 통해 어떤 후보해를 사용할 지 지정한다.

_**MSE**_는 각 후보해의 오차를 측정한다.

_**find_best**_는 현재 세대에서 가장 적합한 후보해를 찾아낸 뒤 추후 시각화를 위해 회귀 계수를 저장한다.

_**debugging**_은 디버깅을 위해 정의하였다. 시각화 및 회귀에는 사용되지 않는다. _DEBUG_DATA_를 True로 지정할 경우 각 세대의 후보해 목록을 보여준다.



> ## Genetic Regression #1
> Randomly created train dataset for linear regression
> https://www.kaggle.com/andonians/random-linear-regression

첫 번째 실험은 선형회귀를 검증하기 위해 생성된 데이터를 사용하였다.

해당 데이터는 예측 모델 및 분석 대회 플랫폼인 Kaggle에서 가져왔으며,
선형 회귀만을 위해 생성된 데이터이므로 실제 데이터와 다르게 Outlier가 존재하지 않는다.

데이터는 [여기](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/input/RandomlyCreatedDatasetTrain.csv)에서 확인할 수 있다.

![GeneticRegression 1](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/Result/GeneticRegression1.gif?raw=true)

초기에 무작위로 생성된 후보해는 전혀 데이터를 예측하지 못하고 있다.

하지만 세대 교체에 따라 점점 선형 모델이 데이터에 적합되어가는 것을 확인할 수 있다.

<br>

> ## Genetic Regression #2
> Randomly created test dataset for linear regression
> https://www.kaggle.com/andonians/random-linear-regression

두 번째 실험 역시 선형회귀를 검증하기 위해 생성된 데이터를 사용하였다.

해당 데이터 역시 선형 회귀만을 위해 생성된 데이터이므로 실제 데이터와 다르게 Outlier가 존재하지 않는다.

데이터는 [여기](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/input/RandomlyCreatedDatasetTest.csv)에서 확인할 수 있다.

![GeneticRegression 2](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/Result/GeneticRegression2.gif?raw=true)

1번 실험과 마찬가지로 초기에 무작위로 생성된 후보해는 전혀 데이터를 예측하지 못하고 있지만

세대 교체에 따라 점점 선형 모델이 데이터에 적합되어가는 것을 확인할 수 있다.

<br>

> ## Genetic Regression #3
> 부산 금정구 어린이집 Dataset
> https://www.data.go.kr/data/15007684/fileData.do

앞선 두 번의 실험에서 회귀가 잘 동작하는 것을 확인하였기 때문에,
이번에는 실제 데이터에도 제대로 동작하는지 확인하기 위해 부산 금정구 어린이집 데이터를 사용하였다.

해당 데이터는 [공공데이터포탈](http://data.go.kr/)에서 가져왔으며, 어린이집 코드, 어린이집 이름, 유형 구분, 우편번호 등 다양한 데이터를 제공한다.

본 실험에서는 보육실 면적에 대해 현원수를 예측하는 선형회귀 모델을 만들었다.

데이터는 [여기](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/input/BusanDaycareCenter.csv)에서 확인할 수 있다.

![GeneticRegression 3](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/Result/GeneticRegression3.gif?raw=true)

선형회귀를 위해 생성된 데이터가 아닌 실제 데이터이기 때문에 선형 모델로 예측하기에는 한계가 있지만, 데이터의 추세를 가장 잘 예측하는 방향으로 선형 모델이 적합된 것을 확인할 수 있다.

<br>

> ## Genetic Regression #4
> 육군 신체측정정보 Dataset
> https://www.data.go.kr/data/3034732/fileData.do

마지막으로 진행한 실험에서 사용한 데이터는 육군 신체측정정보 데이터이다.

해당 데이터는 육군 신병 신체치수 측정정보를 공공데이터포탈을 통해 국방부가 제공하고 있다.

제공되는 데이터를 사용하여 키에 대해 발 크기를 예측하는 선형회귀 모델을 만들었다.

데이터는 [여기](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/input/KoreanArmy.csv)에서 확인할 수 있지만, sample 수가 많아 웹 상으로는 데이터를 확인할 수 없다.
데이터를 확인하기 위해서는 파일을 다운로드 받아야 한다.

![GeneticRegression 4](https://github.com/kusakina0608/Python/blob/master/GeneticRegression/Result/GeneticRegression4.gif?raw=true)

두 번째 실제 데이터인 신체측정정보 데이터 역시 선형회귀 모델이 잘 동작하는 것을 확인하였다.

x축과 y축의 눈금 단위가 다르기 때문에 데이터가 많이 퍼져 있는 것 처럼 보이지만, 실제 데이터는 거의 선형적인 분포를 가지고 있다.

<br>