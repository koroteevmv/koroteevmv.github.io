---
section: ml
title: "Методы обучения с учителем"
---

### Линейные модели

![Регрессия и классификация](https://www.researchgate.net/profile/Christian-Bauckhage/publication/330760775/figure/fig3/AS:721129559822338@1548942093486/binary-linear-classification-in-3D.png "Регрессия и классификация"){: .align-center style="width: 50%;"}
Источник: [ResearchGate](https://www.researchgate.net/publication/330760775_Lecture_Notes_on_Machine_Learning_Binary_Linear_Classifiers/figures?lo=1&utm_source=google&utm_medium=organic).
{: style="text-align: center; font-size:0.7em;"}

```py
from sklearn.linear_model import LogisticRegression
clf = LogisticRegression()
plot_model(clf)
```

![Линейная классификация](/assets/images/ml_text/ml3-11.png "Линейная классификация"){: .align-center style="width: 50%;"}

```python
from sklearn.linear_model import LinearRegression
clf = LinearRegression()
plot_regression(clf)
```

![Линейная регрессия](/assets/images/ml_text/ml3-12.png "Линейная регрессия"){: .align-center style="width: 50%;"}

{% capture notice %}
Выводы:
1. Линейные модели могут служить как моделями классификации, так и моделями регрессии.
1. По сути, это одна модель, которую приспосабливают для решения разных задач.
1. Линейная модель - это результат вычисления линейной комбинации признаков и параметров: $ h_b (x) = X \cdot \vec{b} $
1. Для задач регрессии мы сравниваем результат $ X \cdot \vec{b} $ с $ y $.
1. Для задач классификации мы строим разделяющее множество $ X \cdot \vec{b} = 0 $.
1. Эффективность линейных моделей зависит от структуры данных (для регрессии это должна быть линейная корреляция, для классификации - линейная разделимость).
1. Линейные модели эквивалентны одному нейрону нейронной сети.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Полиномиальные модели

![Линейная граница](/assets/images/ml_text/ml2-9.png "Линейная граница"){: .align-center style="width: 50%;"}

{% capture block %}
$$ h_b (x) = g(b_0 + b_1 x_1 + b_2 x_2) $$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>

![Нелинейная граница](/assets/images/ml_text/ml2-10.png "Нелинейная граница"){: .align-center style="width: 50%;"}

{% capture block %}
$$ h_b(x) = g(b_0 + b_1 x_1 + b_2 x_2 + b_3 x_1^2 + b_4 x_2^2) $$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>

![Полиномиальная классификация](https://i.stack.imgur.com/OV3Fp.png "Полиномиальная классификация"){: .align-center style="width: 800px;"}
Источник: [Data Science Stack exchange](https://datascience.stackexchange.com/questions/85441/non-linear-decision-boundary-in-logistic-regression-algorithm-with-polynomial-fe).
{: style="text-align: center; font-size:0.7em;"}

![Полиномиальная классификация](/assets/images/ml_text/ml3-13.png "Полиномиальная классификация"){: .align-center style="width: 50%;"}

![Полиномиальная классификация](/assets/images/ml_text/ml3-14.png "Полиномиальная классификация"){: .align-center style="width: 50%;"}

![Полиномиальная регрессия](/assets/images/ml_text/ml3-15.png "Полиномиальная регрессия"){: .align-center style="width: 50%;"}

![Полиномиальная регрессия](/assets/images/ml_text/ml3-16.png "Полиномиальная регрессия"){: .align-center style="width: 50%;"}

{% capture notice %}
Выводы:
1. Добавление полиномиальных признаков возможно как к регрессионным, так и к классификационным моделям.
1. Полиномиальная регрессия позволяет охватывать нелинейные зависимости атрибутов и целевой переменной.
1. Полиномиальная классификация позволяет очерчивать нелинейные границы принятия решений.
1. Здесь и далее: атрибуты - характеристики объектов, данные в датасете; признаки - компоненты вектора, подающегося на вход модели машинного обучения.
1. Полиномиальные модели универсальны, но очень дороги при высоких порядках полинома.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Метод опорных векторов

В случае линейно разделимых данных логистическая регрессия ищет какую-нибудь разделяющую гиперплоскость. Можно поставить задачу нахождения разделяющей гиперплоскости максимального зазора.

![Оптимальная граница](https://upload.wikimedia.org/wikipedia/commons/thumb/9/97/Classifier.svg/1280px-Classifier.svg.png "Оптимальная граница"){: .align-center style="width: 50%;"}
Источник: [Wikipedia](https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%BE%D0%BF%D0%BE%D1%80%D0%BD%D1%8B%D1%85_%D0%B2%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D0%BE%D0%B2).
{: style="text-align: center; font-size:0.7em;"}

Для этого мы модифицируем функцию ошибки таким образом, чтобы

{% capture block %}
$$ y = 1 \rightarrow X \cdot \vec{b} \ge 1 $$

$$ y = 0 \rightarrow X \cdot \vec{b} \le -1 $$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>

![Функция ошибки](/assets/images/ml_text/ml2-5.png "Функция ошибки"){: .align-center style="width: 800px;"}

Такая ошибка позволяет максимизировать зазор между разделяющей гиперплоскостью и крайними точками выборки:

![Ошибка в опорных векторах](/assets/images/ml_text/ml3-10.png "Ошибка в опорных векторах"){: .align-center style="width: 50%;"}

Эти крайние точки и называются опорными векторами.

Мы опустим полную математическую формализацию метода опорных векторов и оптимизации параметров метода опорных векторов.

Скажем лишь, что разделяющая гиперплоскость определяется теперь именно как функция от опорных векторов.

![Опорные вектора](https://upload.wikimedia.org/wikipedia/commons/thumb/2/20/SVM_margins.svg/1280px-SVM_margins.svg.png "Опорные вектора"){: .align-center style="width: 50%;"}
Источник: [Wikipedia](https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%BE%D0%BF%D0%BE%D1%80%D0%BD%D1%8B%D1%85_%D0%B2%D0%B5%D0%BA%D1%82%D0%BE%D1%80%D0%BE%D0%B2).
{: style="text-align: center; font-size:0.7em;"}

```python
class SVM:
    def __init__(self, learning_rate=0.001, lambda_param=0.01, n_iters=1000):
        self.lr = learning_rate
        self.lambda_param = lambda_param
        self.n_iters = n_iters
        self.w = None
        self.b = None

    def fit(self, X, y):
        n_samples, n_features = X.shape        
        y_ = np.where(y <= 0, -1, 1)        
        self.w = np.zeros(n_features)
        self.b = 0
        for _ in range(self.n_iters):
            for idx, x_i in enumerate(X):
                condition = y_[idx] * (np.dot(x_i, self.w) - self.b) >= 1
                if condition:
                    self.w -= self.lr * (2 * self.lambda_param * self.w)
                else:
                    self.w -= self.lr * (2 * self.lambda_param * self.w - np.dot(x_i, y_[idx]))
                    self.b -= self.lr * y_[idx]

    def predict(self, X):
        approx = np.dot(X, self.w) - self.b
        return np.sign(approx)
```

![Классификация методом SVM без ядра](/assets/images/ml_text/ml3-17.png "Классификация методом SVM без ядра"){: .align-center style="width: 50%;"}

![Регрессия методом SVM без ядра](/assets/images/ml_text/ml3-18.png "Регрессия методом SVM без ядра"){: .align-center style="width: 50%;"}

В таком виде метод опорных векторов просуществовал с начала 60-х до начала 90-х годов. В это время исследователи догадались, что такая постановка задачи позволяет совершить один трюк, который сильно расширяет применение и вариативность метода опорных векторов.

![Нелинейная граница](/assets/images/ml_text/ml3-1.png "Нелинейная граница"){: .align-center style="width: 50%;"}

Можно ли более эффективно задать признаки для модели линейной классификации? Например, если признаком сделать расстояние от данной точки до выбранных "центров кластеров"? Тогда данная проблема станет линейно разделимой. Хотя граница принятия решения будет сложной формы.

На практике в качестве опорных векторов для начала берут сами точки обучающей выборки. А затем, в процессе обучения, быстро становится понятно, что не все точки "одинаково полезны".

![Опорные вектора](/assets/images/ml_text/ml3-3.png "Опорные вектора"){: .align-center style="width: 50%;"}

![Классификация методом SVM с гауссовым ядром](/assets/images/ml_text/ml3-19.png "Классификация методом SVM с гауссовым ядром"){: .align-center style="width: 50%;"}

![Классификация методом SVM с гауссовым ядром](/assets/images/ml_text/ml3-20.png "Классификация методом SVM с гауссовым ядром"){: .align-center style="width: 50%;"}

В качестве функции расстояния можно брать разные метрики (они должны удовлетворять сложным условиям).

{% capture block %}
Наиболее распространенные ядерные функции:
1. Линейное (SVM без ядра): $ (x \cdot x') $
1. Полиномиальное: $ (x \cdot x' + 1)^d $
1. Радиальная базисная функция: $ e^{-\gamma \| x - x'\|^2} $
1. Сигмоида: $ tanh(k x \cdot x' + c) $
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>

![Классификация методом SVM с полиномиальным ядром](/assets/images/ml_text/ml3-21.png "Классификация методом SVM с полиномиальным ядром"){: .align-center style="width: 50%;"}

![Классификация методом SVM с полиномиальным ядром](/assets/images/ml_text/ml3-22.png "Классификация методом SVM с полиномиальным ядром"){: .align-center style="width: 50%;"}

{% capture notice %}
Выводы:
1. Метод опорных векторов находит оптимальную разделяющую гиперплоскость, а значит приводит к более уверенной классификации.
1. SVM может реализовывать нелинейные модели за счет применения функций ядер.
1. Метод опорных векторов может использоваться как для регрессии (SVR), так и для классификации (SVC).
1. SVM эффективны, когда количество атрибутов больше количества объектов.
1. SVM очень чувствителен к шуму, выбросам в данных.
1. SVM не дают прямых оценок вероятности принадлежности. 
1. Метод опорных векторов эквивалентен однослойной нейронной сети с количеством нейронов на скрытом слое равном количеству опорных векторов.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Перцептрон

![Нейрон](/assets/images/ml_text/ml3-5.png "Нейрон"){: .align-center style="width: 50%;"}

![Нейрон подробно](/assets/images/ml_text/ml3-42.png "Нейрон подробно"){: .align-center style="width: 50%;"}

![Ступенчатая активация](/assets/images/ml_text/ml3-44.png "Ступенчатая активация"){: .align-center style="width: 50%;"}

![Функции активации](/assets/images/ml_text/ml3-45.png "Функции активации"){: .align-center style="width: 50%;"}

![ReLU](/assets/images/ml_text/ml3-46.png "ReLU"){: .align-center style="width: 50%;"}

![Нейрон подробно](/assets/images/ml_text/ml3-42.png "Нейрон подробно"){: .align-center style="width: 50%;"}

![Нейрон как признаки](/assets/images/ml_text/ml3-7.png "Нейрон как признаки"){: .align-center style="width: 50%;"}

![Перцептрон](/assets/images/ml_text/ml3-6.png "Перцептрон"){: .align-center style="width: 50%;"}

```python
class Perceptron:
    def __init__(self, learning_rate=0.01, n_iters=1000):
        self.lr = learning_rate
        self.n_iters = n_iters
        self.activation_func = self._unit_step_func
        self.weights = None
        self.bias = None

    def fit(self, X, y):
        n_samples, n_features = X.shape
        self.weights = np.zeros(n_features)
        self.bias = 0
        y_ = np.array([1 if i > 0 else 0 for i in y])
        for _ in range(self.n_iters):            
            for idx, x_i in enumerate(X):
                linear_output = np.dot(x_i, self.weights) + self.bias
                y_predicted = self.activation_func(linear_output)
                update = self.lr * (y_[idx] - y_predicted)
                self.weights += update * x_i
                self.bias += update

    def predict(self, X):
        linear_output = np.dot(X, self.weights) + self.bias
        y_predicted = self.activation_func(linear_output)
        return y_predicted

    def _unit_step_func(self, x):
        return np.where(x>=0, 1, 0)
```

![Нейросеть по умолчанию](/assets/images/ml_text/ml3-23.png "Нейросеть по умолчанию"){: .align-center style="width: 50%;"}

![Нейросеть на другом наборе данных](/assets/images/ml_text/ml3-24.png "Нейросеть на другом наборе данных"){: .align-center style="width: 50%;"}

![Многослойный перцептрон](/assets/images/ml_text/ml3-8.png "Многослойный перцептрон"){: .align-center style="width: 50%;"}

![Глубокая сеть](/assets/images/ml_text/ml3-9.png "Глубокая сеть"){: .align-center style="width: 50%;"}

![Нейросеть глубокая](/assets/images/ml_text/ml3-25.png "Нейросеть глубокая"){: .align-center style="width: 50%;"}

![Нейросеть на третьем наборе](/assets/images/ml_text/ml3-26.png "Нейросеть на третьем наборе"){: .align-center style="width: 50%;"}

![Нейросеть глубокая для регрессии](/assets/images/ml_text/ml3-27.png "Нейросеть глубокая для регрессии"){: .align-center style="width: 50%;"}

### Деревья решений

![Дерево решений глубиной 1](/assets/images/ml_text/ml3-28.png "Дерево решений глубиной 1"){: .align-center style="width: 50%;"}

![Дерево решений глубиной 2](/assets/images/ml_text/ml3-29.png "Дерево решений глубиной 2"){: .align-center style="width: 50%;"}

![Дерево решений глубиной 3](/assets/images/ml_text/ml3-30.png "Дерево решений глубиной 3"){: .align-center style="width: 50%;"}

![Дерево решений глубиной 4](/assets/images/ml_text/ml3-31.png "Дерево решений глубиной 4"){: .align-center style="width: 50%;"}

![Дерево решений глубиной 5](/assets/images/ml_text/ml3-32.png "Дерево решений глубиной 5"){: .align-center style="width: 50%;"}

![Дерево решений глубиной 21](/assets/images/ml_text/ml3-33.png "Дерево решений глубиной 21"){: .align-center style="width: 50%;"}

![Дерево решений для регрессии](/assets/images/ml_text/ml3-34.png "Дерево решений для регрессии"){: .align-center style="width: 50%;"}

### K ближайших соседей

```py
import numpy as np
from collections import Counter

def euclidean_distance(x1, x2): return np.sqrt(np.sum((x1 - x2)**2))

class KNN:
    def __init__(self, k=3):
        self.k = k
    def fit(self, X, y):
        self.X_train = X
        self.y_train = y
    def predict(self, X):
        y_pred = [self._predict(x) for x in X]
        return np.array(y_pred)
    def _predict(self, x):
        distances = [euclidean_distance(x, x_train) for x_train in self.X_train]
        k_idx = np.argsort(distances)[:self.k]
        k_neighbor_labels = [self.y_train[i] for i in k_idx]
        most_common = Counter(k_neighbor_labels).most_common(1)
        return most_common[0][0]
```

![Классификация по 1 ближайшему соседу](/assets/images/ml_text/ml3-35.png "Классификация по 1 ближайшему соседу"){: .align-center style="width: 50%;"}

![Классификация по 5 ближайшему соседу](/assets/images/ml_text/ml3-36.png "Классификация по 5 ближайшему соседу"){: .align-center style="width: 50%;"}

![Классификация по 20 ближайшему соседу](/assets/images/ml_text/ml3-37.png "Классификация по 20 ближайшему соседу"){: .align-center style="width: 50%;"}

![Регрессия методом ближайших соседей](/assets/images/ml_text/ml3-38.png "Регрессия методом ближайших соседей"){: .align-center style="width: 50%;"}

### Наивная байесовская модель

```python
class NaiveBayes:
    def fit(self, X, y):
        n_samples, n_features = X.shape
        self._classes = np.unique(y)
        n_classes = len(self._classes)

        self._mean = np.zeros((n_classes, n_features), dtype=np.float64)
        self._var = np.zeros((n_classes, n_features), dtype=np.float64)
        self._priors =  np.zeros(n_classes, dtype=np.float64)

        for idx, c in enumerate(self._classes):
            X_c = X[y==c]
            self._mean[idx, :] = X_c.mean(axis=0)
            self._var[idx, :] = X_c.var(axis=0)
            self._priors[idx] = X_c.shape[0] / float(n_samples)

    def predict(self, X):
        y_pred = [self._predict(x) for x in X]
        return np.array(y_pred)

    def _predict(self, x):
        posteriors = []
        for idx, c in enumerate(self._classes):
            prior = np.log(self._priors[idx])
            posterior = np.sum(np.log(self._pdf(idx, x)))
            posterior = prior + posterior
            posteriors.append(posterior)
        return self._classes[np.argmax(posteriors)]

    def _pdf(self, class_idx, x):
        mean = self._mean[class_idx]
        var = self._var[class_idx]
        numerator = np.exp(- (x-mean)**2 / (2 * var))
        denominator = np.sqrt(2 * np.pi * var)
        return numerator / denominator
```

![Классификация методом наивного Байеса](/assets/images/ml_text/ml3-39.png "Классификация методом наивного Байеса"){: .align-center style="width: 50%;"}

### Гауссовский процесс

![Классификация методом Гауссовых процессов](/assets/images/ml_text/ml3-40.png "Классификация методом Гауссовых процессов"){: .align-center style="width: 50%;"}

![Регрессия методом Гауссовых процессов](/assets/images/ml_text/ml3-41.png "Регрессия методом Гауссовых процессов"){: .align-center style="width: 50%;"}