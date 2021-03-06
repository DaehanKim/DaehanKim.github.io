---
layout: post
title: Perceptron
---

* 이 포스트는 사이토 고키의 "Deep Learning from Scratch"의 내용을 바탕으로 한 것입니다.

### Perceptron

퍼셉트론이란 인간의 신경이나 전류와 같이 신호가 흐르는 구조를 모방한 것입니다. 일반적인 신호와의 차이점은 0 또는 1의 상태밖에 없다는 것이죠. 입력이 두 개인 퍼셉트론을 생각해 보겠습니다.  

각각의 신호에는 중요도가 있습니다. 더 중요한 신호는 결과에 많은 영향을 미칠 것이고, 덜 중요한 신호는 그렇지 않을 것입니다. 퍼셉트론에서는 이것을 가중치로 표현합니다. w1,w2는 각각 첫번째, 두번째 신호의 가중치입니다.  

또 동일한 가중치라고 하더라도 기본적인 환경의 영향이 있을 것입니다. 우리는 이것을 b로 표현하고 편향이라고 하겠습니다. 이렇게 셋팅을 마치고 나서 x1*w1+x2*w2+b의 값이 양수이면 1을(신호가 흐름), 그렇지 않으면 0(신호가 흐르지 않음)을 출력하도록 해보겠습니다.

이런 설정을 하고 나면 가중치와 편향을 조정하여 많은 게이트를 표현할 수 있습니다.

예를 들어 and gate는 (w1,w2,b)=(0.5,0.5,-0.7)로 표현할 수 있습니다. 그 이유는 

```
and(0,0) : 0*0.5+0*0.5-0.7 < 0 --> 0
and(0,1) : 0*0.5+1*0.5-0.7 < 0 --> 0
and(1,0) : 1*0.5+0*0.5-0.7 < 0 --> 0
and(1,1) : 1*0.5+1*0.5-0.7 > 0 --> 1
```

다음은 각 게이트의 파이썬 코드입니다.   

```python
import numpy as np

def AND(x1,x2):
    w = np.array([0.5,0.5])
    x = np.array([x1,x2])
    b = -0.7
    ret = np.sum(w*x)+b
    if ret > 0:
    	return 1
    else:
    	return 0

def OR(x1,x2):
    w = np.array([0.5,0.5])
    x = np.array([x1,x2])
    b = -0.3
    ret = np.sum(w*x)+b
    if ret > 0:
    	return 1
    else:
    	return 0

def NAND(x1,x2):
    x = np.array([x1,x2])
    w = np.array([-0.5,-0.5])
    b = 0.7
    ret = np.sum(x*w)+b
    if ret > 0:
        return 1
    else:
        return 0
```

### XOR gate

퍼셉트론을 하나만 사용하면 XOR gate를 만들 수 없는 단점이 있습니다. XOR은 직선 하나로 나눌 수 없기 때문입니다. 
따라서 두 개의 퍼셉트론을 쌓습니다.  


```python
def XOR(x1,x2):

	s1 = P.NAND(x1,x2)
	s2 = OR(x1,x2)
	return AND(s1,s2)
```


