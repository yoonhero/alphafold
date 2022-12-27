# Alphafold

> 과학 발표를 위해서 조사했지만 오늘 과학 수업이 끝나서 내년에..?

## Prerequisits

### 단백질

<strong>단백질</strong> 생화학에서 생물의 몸을 구성하는 고분자 유기 물질이다. 수많은 아미노산의 연결체로 20가지의 서로 다른 아미노산들이 펩타이드 결합이라고 하는 화학 결합으로 길게 연결된 것을 폴리펩타이드라고 한다. 여러 가지의 폴리펩타이드 사슬이 4차 구조를 이루어 고유한 기능을 갖게 되었을 때 비로소 단백질이라고 부른다.

![structure](http://thescienceplus.com/news/data/20220212/p1065604444086143_988_thum.jpg)

### 펩타이드 결합

아미노산은 염기성인 아미노기와 산성인 카르복시기를 모두 가지고 있는 화합물이다. 아미노산이 결합을 할 때 아미노기의 H와 카르복시기의 OH가 탈수 축합 반응이 일어나 물 분자 1개가 나오는 탈수 과정이 <strong>펩타이드 결합</strong>이다.

### ATP

세포호흡을 통해서 세포질과 미토콘드리아에서 영양소를 분해하여 얻은 에너지를 <strong>ATP</strong>로 저장한다.
ATP는 아데노신 + 인산3개란 뜻이다. 아데노신은 아데닌+리보스 당으로 아데닌은 ATCG의 A이고 리보스는 RNA를 구성하는 당이다. 인산기를 하나씩 가수분해하여 떼어낼 때마다 큰 에너지가 방출되어 이 에너지를 필요한 곳에 사용할 수 있도록 한다. 그래서 ATP는 에너지 저장 겸 사용 형태가 되는 것이다. 펩타이드 결합 과정에서도 ATP를 통해서 에너지를 공급 받는다.

## Intro

![first](./docs/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-12-27%2008.40.19.png)

> Proteins are essential to life, supporting practically all its functions. They are large complex molecules, made up of chains of amino acids, and what a protein does largely depends on its unique 3D structure.

단백질이 어떤 역할을 할지는 바로 각 단백질의 독특한 3D구조에 달려있다.

> Figuring out what shapes proteins fold into is known as the “protein folding problem”, and has stood as a grand challenge in biology for the past 50 years.

따라서 아미노산 염기 서열에 따라 단백질이 어떤 모양으로 접히는 지를 알아내면 오랫동안 해결하지 못했던 <strong>Protein Folding</strong> 문제를 해결할 수 있다.

### “protein folding problem”

단백질의 아미노산 염기 서열이 어떻게 단백질의 입체 구조를 결정하는데 영향을 주는지에 대한 질문이다.

![img](./docs/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-12-27%2008.46.54.png)

위 그림처럼 아미노산의 염기 서열이 단백질이 어떻게 접혀야 할지 정보를 가지고 있어서 최종적인 3D 구조를 만들 수 있다고 한다.

![plot](./docs/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-12-27%2009.43.29.png)

![plot](./docs/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202022-12-27%2009.43.45.png)

과거에는 데이터가 많지 않았다. 하지만 시간이 지날수록 아미노산 염기서열과 단백질 구조에 대한 데이터가 쌓였고 AlphaFold는 <strong>10만 가지</strong>의 단백질 순서와 구조를 학습하여, 아미노산 염기 서열만 안다면 단백질의 3D 구조를 비교적 정확히 예측할 수 있었다.

> In a major scientific advance, the latest version of our AI system AlphaFold has been recognised as a solution to this grand challenge by the organisers of the biennial Critical Assessment of protein Structure Prediction (CASP). This breakthrough demonstrates the impact AI can have on scientific discovery and its potential to dramatically accelerate progress in some of the most fundamental fields that explain and shape our world.

CASP(Critical Assessment of protein Structure Prediction)의 참가자들로부터 개발한 AlphaFold 기술을 통해 단백질의 3D 구조를 예측하고자 하는데요, 이는 질병 치료제 개발이나 산업 폐기물을 분해해주는 효소의 개발 등의 효과를 가져오게 된다.

## AlphaFold

![i](https://s3.ap-northeast-2.amazonaws.com/img.stibee.com/52512_1644204396.png)

![i](https://miro.medium.com/max/1400/1*kdUYLcK-m5nwqdrBxY4L2A.webp)

1. MSA Features

Multiple sequence alignment (MSA)는 알파폴드 학습에 사용되는 데이터셋이다.

Data augmentation, feature representation, auxiliary losses, cropping 및 data curation 등의 기법들이 특성 추출에 활용된다.

2. 신경망으로 구조 예측하기

AlphaFold의 input은 단백질 염기서열이다.

단백질 서열이 주어지면 이를 토대로

-   아미노산 쌍의 거리
-   아미노산을 연결하는 화학 본드 간의 각도

를 예측한다.

neural network는 기존에 학습한 데이터를 바탕으로 예측하기 때문에, 예측 전 실험으로 직접 알아낸 단백질의 R기들 간의 거리 데이터를 학습시켰다.

이 신경망에서 주목할 점은 일반적인 Convolution Layer가 아닌 dilated convolution layer을 사용하여 특정 위치의 아미노산에 대한 정보가 주변 영역으로 빠르게 확산될 수 있는 이점을 갖는다는 것이다.

3. 거리 예측 및 포텐셜 계산하기

전 단계에서, 신경망으로부터 얻어진 출력에는 곁사슬 간의 거리와 뒤틀림각에 대한 추정치가 담겨 있다. 이 추정치로 단백질 3차원 구조를 바로 생산해도 될 것 같지만 더 안정된 구조의 존재 가능성 및 불가능한 화학 결합 각도등을 포함할 가능성이 있기 때문에 단백질의 포텐셜을 수학적으로 계산한다.

4. 단백질 구조 예측하기

실제 세계의 단백질은 포텐셜이 가장 낮아지는 구조로 접히기 때문에 계산된 포텐셜을 일종의 손실 함수로 볼 수 있다. 알파폴드에서는 이 단백질의 포텐셜이 가장 낮아지도록 경사하강법을 적용하여 뒤틀림각을 조정한다. 최종적으로 가장 안정적인 단백질이 된다.
