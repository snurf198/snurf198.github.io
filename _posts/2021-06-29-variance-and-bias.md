---
layout: single
title: "Bias와 Variance"
categories:
  - machine learning
tags:
  - 
use_math: true
comments: true
---
## Bias와 Variance란?

머신러닝 모델을 학습할 때 모델이 train data에 대해서는 괜찮은 accuracy가 나오는 한편 test data에 대해서는 accuracy가 형편없는 경우가 있습니다. 이것은 모델이 train data에 overfitting 되었기 때문입니다. 다른말로 하면 variance가 높기 때문입니다. 반면 모델의 학습에 어떤 알고리즘을 사용할 때 train data와 test data에 대해서 둘 다 나쁜 accuracy가 나오는 경우가 있습니다. 가령 linear regression에서 예측값과 데이터의 feature가 선형적인 추세를 보이지 않는다면 accuracy가 낮게 나올 것입니다. 이 경우 모델은 train data에 대해 underfitting 되어있습니다. 다른말로 하면 bias가 높습니다.

위에서 variance가 높다, bias가 높다와 같은 말을 사용했습니다. 그럼 variance와 bias는 도대체 뭘 의미하는 것일까요?

Variance와 bias에 대해 풀어쓰자면 다음과 같습니다.

- Variance: 모델을 학습시키는 알고리즘이 train data에 대해 얼마나 민감하게 반응하느냐를 나타낸 값
- Bias: Train data가 무한적으로 주어졌을 때에도 어쩔 수 없이 생기는 모델 학습 알고리즘에 내재적으로 포함된 오류를 나타낸 값

풀어쓰기는 했지만 뭐라는지 이해가 잘 안됩니다. 그럼 좀 더 풀어서 설명을 하도록 하겠습니다.

Variance가 크다는 것은 특정 알고리즘(ex. linear regression)을 사용할 때 학습에 사용되는 데이터가 달라짐에 따라 얼마나 민감하게 모델이 달라지느냐를 나타낸 값입니다. 위에서 말한 overfitting의 경우 train data에 대해서는 모델의 성능이 좋았지만 test data에 대해서는 성능이 좋지 않았습니다. 이는 만약 test data로 알고리즘을 학습하는 경우 모델이 크게 달라질 수 있음을 의미합니다. 즉, 모델을 학습시키는 데이터에 따라 모델의 변화가 크기 때문에 이 variance가 높은 것 입니다. 이 모델은 새로운 학습 데이터가 들어온다면 모델이 민감하게 반응하여 큰 변화가 생길 것입니다.

Bias가 크다는 것은 평균적으로 모델이 얼마나 값을 잘 예측하는가를 나타내는 값입니다. 예를 들어 아래의 그림을 봅시다.

[![img](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Normdist_regression.png/300px-Normdist_regression.png)](https://commons.wikimedia.org/wiki/File:Normdist_regression.png)

데이터가 위 그림의 점으로 주어지고 linear regression을 사용해 모델을 만들었습니다. 이 때 어떤 train data를 사용해도 데이터가 저런 분포라면 linear model은 어쩔 수 없지 error를 발생시킬 수 밖에 없습니다. 이는 애초에 linear 함수 자체가 내재적으로 가지는 특성으로 인해 생기는 오류값입니다. 위에서 말한 underfitting의 경우 train과 test data에 대해서 모두 성능이 좋지 않았기 때문에 이 경우 bias가 높은 것 입니다.



## Bias와 Variance에 대한 엄밀한 설명

이때까지 bias와 variance에 대해 예시와 함께 말로 풀어서 설명해봤습니다.

지금부터는 위의 설명으로는 내용이 부족하다! 나는 좀 더 엄밀하고 수학적인 정의와 설명이 필요하다! 하시는 분들을 위해 아래의 링크의 내용을 제가 공부하고 이해하여 재구성한 글입니다. 위의 설명으로도 충분하신 분들은 굳이 이 부분은 읽지 않으셔도 됩니다.

https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/lecturenote12.html

그럼 시작하겠습니다.

머신모델을 학습하기 이전에 dataset이 필요합니다. 이 때 dataset을 $D$라고 하겠습니다. 이 dataset은 분포 $P(X,Y)$로 부터 추출되었다고 합시다. 우리는 일반적인 regression 모델에 대해서 살펴볼 것이기 때문에 $y\in \R$입니다.
$$
D  = \{(\bold x_1, y_1),\space...\space,(\bold x_n, y_n)\}\space from\space distribution\space P(X, Y)\\
D: dataset\\
\bold x_n: feature\\
y_n: target\space y_n\in\R
$$

$$
E_{x, y, D}[(h_D(x)-y)^2]\\
$$
