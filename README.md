### 선형 회귀분석(Linear Regression) 노동시간과 수입



![](C:\Users\User\Pictures\선형회기그래프.png)

일반적으로 어떠한 값을 예측할때 몇가지 고려요소(독립변수:노동시간)를 기준으로 결과(종속변수:수입)를 예측하기 위해 가설(Hypothesis)를 세워야한다. 고려요소를 x, 결과를 y로 두고 식을 세워보면 직선 모양의 1차방정식이 만들어진다. 독립변수가 여러가지라고 해도 직선모양의 1차방정식이다.

회기식은 H(x)=Wx+b 라고하자.

실제 데이터들을 점으로 표시를 하면 위 그래프처럼 나타날 것이다. 점이 모여 어림잡아 회귀선을 그릴수는 있다. 하지만, 우리가 그리는 회귀선의 기울기에 따라 예측의 정확도가 차이가 날것이다. 이러한 예측의 정확도를 높여주기 위해 최소제곱법을 이용해 비용/손실 함수(cost/loss function)을 구해준다.

예측값(H(x))에서 실제값(y)를 빼주고 제곱을하여 다 더한 후 모수로 나눠준 값이 cost function이다.

결론적으로 cost function을 0에 가깝게 만들어 주면, 회귀선에 대한 예측 결과값의 정확도가 높아진다는 것이다.제곱을 해주는 이유는 음수든 양수든 차이를 통일화 시켜주고, 차이가 많이 날수록 페널티를 더 부여하기 위해 사용한다.

위의 식을 정리하면 아래와 같다.

![](C:\Users\User\Pictures\회기식 2.png)

**1.가설**

 가설을 세우자. X, Y에 주어진 데이터를 넣어줄것이고, W, b는 텐서플로우를 통해서 받아낼것이다.지금은 독립변수가 하나여서 배열로 값을 받지만 독립변수가 많아지면 메트릭스(Matrix)를 사용하여 코드를 작성한다.

---

x_data = [1, 2, 3]
y_data = [10000, 20000, 30000]

X = tf.placeholder(tf.float32, shape=None)
Y = tf.placeholder(tf.float32, shape=None)

W = tf.Variable(tf.random_normal([1]), 'weight')
b = tf.Variable(tf.random_normal([1]), 'bias')

hypothesis = X * W + b//가설

---





#### 2. cost function(비용 함수)

cost function을 구하기 위해 식을 세운다.

tensorflow모듈에 reduce_mean과 square 함수를 사용해준다.

reduce_mean : 모수로 나눠주는 작업

square : 제곱을 해주는 작업

---

cost = tf.reduce_mean(tf.square(hypothesis - Y))

---



#### 3. cost function 최소화

cost function을 최소화 해주기 위해 GradientDescent 알고리즘을 사용한다

---

optimizer = tf.train.GradientDescentOptimizer(learning_rate=1e-2)
train = optimizer.minimize(cost)

---

**4. 결과**

![](C:\Users\User\Pictures\기말1.png)

![](C:\Users\User\Pictures\기말 2.png)



20번 학습마다 출력이 되게끔 하여 값을 확인해보자.

처음 시작의 Cost값을 확인해보면 0과는 거리가 멀고 W와 b값은 뒤죽박죽 변경이 되는것이 확인된다