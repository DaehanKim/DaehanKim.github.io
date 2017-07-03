---
layout: post
title: Neural Network(1)
---

* 이 포스트는 사이토 고키의 "Deep Learning from Scratch"의 내용을 바탕으로 한 것입니다.

### Activation Function(활성 함수)

앞서 살펴 봤던 Perceptron은 ```w1*x1+w2*x2+b```를 계산한 후 이 값을 계단 함수(Step Function)에 넣어 1 또는 0의 값을 출력했습니다. 이와 같이 이전 층에서의 신호의 총합이 활성화를 일으키는지 여부를 결정하는 함수를 활성 함수라고 합니다. 

### Neural Network(신경망)

신경망에서는 multi-layer perceptron과 마찬가지의 구조를 가지지만, 활성화 함수가 달라집니다. 그 주된 이유는 인간이 직접 가중치를 설정해 줘야 했던 perceptron과 달리 신경망에서는 Gradient Descent(경사 하강법)과 같은 방법을 이용하여 Data에서 직접 가중치를 학습하는 것이 가능한데, 이 과정은 activation function이 미분 가능해야 용이해지기 때문입니다.(엄밀하게 말하자면 Almost everywhere에서 도함수의 절대값이 0이 아니어야 하기 때문입니다.) 퍼셉트론에서 사용되었던 계단함수는 0에서 미분이 되지 않고 도함수의 절댓값이 모두 0입니다. 따라서 계단함수로는 gradient descent를 이용한 weight update가 불가능합니다.

### Sigmoid, ReLu

Sigmoid 함수는 \\(1/(e^{-1}+1)\\) 와 같은 함수입니다. 0과 1 사이의 값을 가지고 모든 \\(x\\)에 대해 미분 가능한 것을 확인 할 수 있습니다.  

![sigmoid](http://tikalon.com/blog/2011/sigmoid.gif)

ReLu 함수는 2012년 Imagenet challenge에서 우승한 모델인 Alex-net에서 처음 사용한 방식입니다. Sigmoid 활성함수를 사용한 레이어를 여러 층 쌓게 되면 절댓값이 1보다 작은 gradient가 계속 곱해져 사라지는 gradient-vanishing 문제가 발생하게 되는데요.  ReLu를 사용하면 gradient를 줄이지 않고 전달해 그 문제를 다소 완화시킬 수 있습니다. 수식은 아주 간단합니다.  

  \(ReLu(x)=max(0,x)\)

![ReLu](https://i.stack.imgur.com/8CGlM.png)

### 출력층의 activation function

출력층은 신경망이 답안을 내놓는 층입니다. 예를 들어 아버지의 키에서 자녀의 키를 추론하는 회귀(regression)문제라면 예측된 아들의 키인 (100,250)안의 실수를 내놓을 것이고, 주어진 손 글씨가 어떤 숫자인지를 분류(classify)하는 문제라면 일반적으로 크기가 10인 one-hot vector를 내놓을 것입니다. (one-hot vector란 정답의 위치에만 1이 표시되고 나머지는 모두 0으로 표시된 형태의 벡터를 말합니다.)  

보통 regression 문제에서는 항등함수를 사용합니다. 항등함수는 \\(f(x)=x\\)이므로 아무 처리도 하지 않고 내놓는다는 것이죠. classify 문제에서는 softmax 함수를 사용합니다. 이것은 argmax함수의 '부드러운' 버전이라고 생각하시면 되는데요. 가장 큰 번호에 1을 주는 argmax와 달리 어느 정도 비중을 차지하는 번호에도 일부를 주게 됩니다.   

softmax를 씌워서 모든 레이블의 합이 1이 되게 만들 수는 있지만 우리는 확률보다는 레이블에 관심이 있기 때문에 실제 구현에서는 궂이 softmax를 씌우지 않고 그냥 가장 큰 값을 가진 레이블을 정답으로 반환하도록 구현하면 됩니다.  


