---
section: ml
title: "Диагностика систем машинного обучения"
---

### Что такое метрики эффективности?

{% capture notice %}
Выводы:
1. Метрики эффективности - это способ показать, насколько точно модель отражает реальный мир.
1. Метрики эффективность должны выбираться исходя из задачи, которую решает модель.
1. Функция ошибки и метрика эффективности - это разные вещи, к ним предъявляются разные требования.
1. В задаче можно (и, зачастую, нужно) применять несколько метрик эффективности.
1. Наряду с метриками эффективности есть и другие характеристики моделей - скорость обучения, скорость работы, надежность, робастность, интерпретируемость.
1. Метрики эффективности вычисляются как правило из двух векторов - предсказанных (теоретических) значений целевой переменной и эмпирических (реальных) значений.
1. Обычно метрики устроены таким образом, что чем выше значение, тем модель лучше.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Метрики эффективности для регрессии

{% capture notice %}
Выводы:
1. Метрики эффективности для регрессий обычно анализируют отклонения предсказанных значений от реальных.
1. Большинство метрик пришло в машинное обучение из математической статистики.
1. Результаты работы модели можно исследовать более продвинутыми статистическими методами.
1. Обычно метрики сравнивают данную модель с тривиальной - моделью, которая всегда предсказывает среднее реальное значение целевой переменной.
1. Модель могут быть точны на 100%, но плохи они могут быть без ограничений.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Коэффициент детерминации (r-квадрат)

{% capture block %}
$$
R^2(y, \hat{y}) = 1 - \frac
{\sum_{i=1}^n (y_i - \hat{y_i})^2}
{\sum_{i=1}^n (y_i - \bar{y_i})^2}
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import r2_score
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> r2_score(y_true, y_pred)
0.948...
```

{% capture notice %}
Выводы:
1. Коэффициент детерминации показывает силу связи между двумя случайными величинами.
1. Если модель всегда предсказывает точно, метрика равна 1. Для тривиальной модели - 0.
1. Значение метрики может быть отрицательно, если модель предсказывает хуже, чем тривиальная.
1. Это одна из немногих несимметричных метрик эффективности.
1. Эта метрика не определена, если $y=const$. Надо следить, чтобы в выборке присутствовали разные значения целевой переменной.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

<!-- #### Доля объясненной дисперсии

```py
>>> from sklearn.metrics import explained_variance_score
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> explained_variance_score(y_true, y_pred)
0.957...
``` -->

#### Средняя абсолютная ошибка (MAE)

{% capture block %}
$$
MAE(y, _\hat{y}) = \frac{1}{n} \sum_{i=0}^{n-1} |y_i - \hat{y_i}|
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import mean_absolute_error
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> mean_absolute_error(y_true, y_pred)
0.5
```

{% capture notice %}
Выводы:
1. MAE показывает среднее абсолютное отклонение предсказанных значений от реальных.
1. Чем выше значение MAE, тем модель хуже. У идеальной модели $MAE=0$
1. MAE очень легко интерпретировать - на сколько в среднем ошибается модель.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Средний квадрат ошибки (MSE)

{% capture block %}
$$
MSE(y, _\hat{y}) = \frac{1}{n} \sum_{i=0}^{n-1} (y_i - \hat{y_i})^2
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import mean_squared_error
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> mean_squared_error(y_true, y_pred, squared=False)
0.612...
```

{% capture notice %}
Выводы:
1. MAE показывает средний квадрат отклонений предсказанных значений от реальных.
1. Чем выше значение MSE, тем модель хуже. У идеальной модели $MSE=0$
1. MSE больше учитывает сильные отклонения, но хуже интерпретируется, чем MAE.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Среднеквадратичная ошибка (RMSE)

{% capture block %}
$$
RMSE(y, _\hat{y}) = \sqrt{\frac{1}{n} \sum_{i=0}^{n-1} (y_i - \hat{y_i})^2}
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import mean_squared_error
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> mean_squared_error(y_true, y_pred)
0.375
```

{% capture notice %}
Выводы:
1. RMSE - это по сути корень из MSE. Выражается в тех же единицах, что и целевая переменная.
1. Чаще применяется при статистическом анализа данных.
1. Данная метрика очень чувствительна к аномалиям и выбросам.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Среднеквадратичная логарифмическая ошибка (MSLE)

{% capture block %}
$$
MSLE(y, _\hat{y}) = \frac{1}{n} \sum_{i=0}^{n-1} (
ln(1 + y_i) - ln(1 + \hat{y_i})
)^2
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import mean_squared_log_error
>>> y_true = [3, 5, 2.5, 7]
>>> y_pred = [2.5, 5, 4, 8]
>>> mean_squared_log_error(y_true, y_pred)
0.039...
```

{% capture notice %}
Выводы:
1. MSLE это среднее отклонение логарифмов реальных и предсказанных данных.
1. Так же, идеальная модель имеет $MSLE = 0$.
1. Данная метрика используется, когда целевая переменная простирается на несколько порядков величины.
1. Еще эта метрика может быть полезна, если моделируется процесс в экспоненциальным ростом.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Среднее процентное отклонение (MAPE)

{% capture block %}
$$
MAPE(y, _\hat{y}) = \frac{1}{n} \sum_{i=0}^{n-1}
\frac{|y_i - \hat{y_i}|}{max(\epsilon, |y_i|)}
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import mean_absolute_percentage_error
>>> y_true = [1, 10, 1e6]
>>> y_pred = [0.9, 15, 1.2e6]
>>> mean_absolute_percentage_error(y_true, y_pred)
0.2666...
```

{% capture notice %}
Выводы:
1. Идея этой метрики - это чувствительность к относительным отклонениям.
1. Данная модель выражается в процентах и имеет хорошую интерпретируемость.
1. Идеальная модель имеет $MAPE = 0$. Верхний предел - не ограничен.
1. Данная метрика отдает предпочтение предсказанию меньших значений.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Абсолютная медианная ошибка

{% capture block %}
$$
MedAE(y, _\hat{y}) = \frac{1}{n} median_{i=0}^{n-1}
|y_i - \hat{y_i}|
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import median_absolute_error
>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]
>>> median_absolute_error(y_true, y_pred)
0.5
```

{% capture notice %}
Выводы:
1. медианная абсолютная ошибка похожа на среднюю абсолютную, но более устойчива к аномалиям.
1. Применяется в задачах, когда известно, что в данных присутствуют выбросы, аномальные , непоказательные значения.
1. Эта метрика более робастная, нежели MAE. 
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Максимальная ошибка

{% capture block %}
$$
ME(y, _\hat{y}) = max_{i=0}^{n-1}
|y_i - \hat{y_i}|
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> from sklearn.metrics import max_error
>>> y_true = [3, 2, 7, 1]
>>> y_pred = [9, 2, 7, 1]
>>> max_error(y_true, y_pred)
6
```

{% capture notice %}
Выводы:
1. Максимальная ошибка показывает наихудший случай предсказания модели.
1. В некоторых задачах важно, чтобы модель не ошибалась сильно, а небольшие отклонения не критичны.
1. Зачастую эта метрика используется как вспомогательная совместно с другими.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Метрики эффективности для классификации

{% capture notice %}
Выводы:
1. Метрики эффективности классификации подсчитывают количество правильно распознанных объектов.
1. В задачах классификации почти всегда надо применять несколько метрик одновременно.
1. Некоторые метрики работают с метрическими методами, другие - со всеми.
1. Качество бинарной классификации при прочих равных почти всегда будет сильно выше, чем для множественной.
1. Вообще, чем больше в задаче классов, тем ниже ожидаемые значения эффективности.
1. Тривиальной моделью в задачах классификации считается та, которая предсказывает случайный класс, либо самый популярный класс.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Доля правильных ответов (accuracy)

{% capture block %}
$$ 
acc(y, \hat{y}) = \frac{1}{n} \sum_{i=0}^{n} 1(\hat{y_i} = y_i) 
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> import numpy as np
>>> from sklearn.metrics import accuracy_score
>>> y_pred = [0, 2, 1, 3]
>>> y_true = [0, 1, 2, 3]
>>> accuracy_score(y_true, y_pred)
0.5
```

{% capture notice %}
Выводы:
1. Точность (accuracy) - самая простая метрика качества классификации, доля правильных ответов.
1. Может быть выражена в процентах и в долях единицы.
1. Идеальная модель дает точность 1.0, тривиальная - 0.5, самая худшая - 0.0.
1. Тривиальная модель в множественой сбалансированной задаче классификации дает точность 1/m.
1. Метрика точности очень чувствительная к несбалансированности классов.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Топ k классов

{% capture block %}
$$ 
tka(y, \hat{f}) = \frac{1}{n} \sum_{i=0}^{n-1} 
\sum_{j=1}^{k} 1(\hat{f_{ij}} = y_i) 
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>


```py
>>> import numpy as np
>>> from sklearn.metrics import top_k_accuracy_score
>>> y_true = np.array([0, 1, 2, 2])
>>> y_score = np.array([[0.5, 0.2, 0.2],
...                     [0.3, 0.4, 0.2],
...                     [0.2, 0.4, 0.3],
...                     [0.7, 0.2, 0.1]])
>>> top_k_accuracy_score(y_true, y_score, k=2)
0.75
```

{% capture notice %}
Выводы:
1. Эта метрика - обобщение точности для случая, когда модель выдает вероятности отнесения к каждому классу.
1. Вычисляется как доля объектов, для которых правильный класс попадает в список k лучших предсказанных классов.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Метрики классификации для неравных классов (precision, recall, F1)

{% capture block %}
$$
P = \frac{TP}{TP + FP} \\
R = \frac{TP}{TP + FN} \\
S = \frac{TN}{TN + FP}
$$
{% endcapture %}
<div class="presentation">{{ block | markdownify }}</div>

![PR_F1](/assets/images/ml_text/ml4-1.png "PR_F1"){: .align-center style="width: 800px;"}

```py
>>> from sklearn import metrics
>>> y_pred = [0, 1, 0, 0]
>>> y_true = [0, 1, 0, 1]
>>> metrics.precision_score(y_true, y_pred)
1.0
>>> metrics.recall_score(y_true, y_pred)
0.5
>>> metrics.f1_score(y_true, y_pred)
0.66...
```

{% capture notice %}
Выводы:
1. Если классы в задаче не сбалансированы, то метрика точности не дает полного представления о качестве работы моделей.
1. Для бинарной классификации подсчитывается количество истинно положительных, истинно отрицательных, ложно положительных и ложно отрицательных объектов.
1. Прецизионность (precision) - доля истинно положительных объектов во всех, распознанных как положительные.
1. Прецизионность характеризует способность модели не помечать положительные объекты как отрицательные (не делать ложно положительных прогнозов).
1. Правильность (recall) - для истинно положительных объектов во всех положительных.
1. Правильность характеризует способность модели выявлять все положительные объекты (не делать ложно отрицательных прогнозов).
1. Специфичность (specificity) - доля истинно отрицательных объектов во всех отрицательных.
1. F1 - среднее гармоническое между этими двумя метриками. F1 - это частный случай. Вообще, семейство F-метрик - это взвешенное среднее гармоническое.
1. Часто используют все вместе для более полной характеристики модели.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### PR-AUC

![PR_AUC](https://scikit-learn.org/stable/_images/sphx_glr_plot_precision_recall_001.png "PR_AUC"){: .align-center style="width: 800px;"}
Источник: [sklearn](https://scikit-learn.org/stable/modules/model_evaluation.html).
{: style="text-align: center; font-size:0.7em;"}

{% capture notice %}
Выводы:
1. Кривая precision-recall используется для методов метрической классификации, которые выдают вероятность принадлежности объекта данному классу.
1. Дискретная классификации производится при помощи порогового значения.
1. Чем больше порог, тем больше объектов модель будет относить к отрицательному классу.
1. Повышение порога в среднем увеличивает прецизионность модели, но понижает правильность.
1. PR-кривая используется чтобы выбрать оптимальное значение порога.
1. PR-кривая нужна для того, чтобы сравнивать и оценивать модели вне зависимости от выбранного уровня порога.
1. PR-AUC - площадь под PR-кривой, у лучшей модели - 1.0б у тривиальной - 0.5, у худшей - 0.0.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Метрики для множественной классификации

```py
>>> from sklearn import metrics
>>> y_true = [0, 1, 2, 0, 1, 2]
>>> y_pred = [0, 2, 1, 0, 0, 1]
>>> metrics.precision_score(y_true, y_pred, average='macro')
0.22...
>>> metrics.recall_score(y_true, y_pred, average='micro')
0.33...
>>> metrics.f1_score(y_true, y_pred, average='weighted')
0.26...
>>> metrics.fbeta_score(y_true, y_pred, average='macro', beta=0.5)
0.23...
```

![MultiPR](https://scikit-learn.org/0.15/_images/plot_precision_recall_0011.png "MultiPR"){: .align-center style="width: 800px;"}
Источник: [sklearn](https://www.google.com/url?sa=i&url=https%3A%2F%2Fscikit-learn.org%2F0.15%2Fauto_examples%2Fplot_precision_recall.html&psig=AOvVaw15eJNKyR29Xy4Zqjn9s-jS&ust=1653408447730000&source=images&cd=vfe&ved=0CAwQjRxqFwoTCND5hs2A9vcCFQAAAAAdAAAAABAI).
{: style="text-align: center; font-size:0.7em;"}

{% capture notice %}
Выводы:
1. Для множественной классификации точность считается традиционно, а все остальные метрики - отдельно для каждого класса.
1. Каждую метрику можно усреднить арифметически или взвешенно по классам. Весами выступают объемы классов.
1. В модуле sklearn реализовано несколько алгоритмов усреднения они выбираются исходя их задачи.
1. В случае средневзвешенного, F1-метрика может получиться не между P и R. 
1. PR-кривая тоже может строиться для каждого класса отдельно, либо кривая средних значений P и R. 
1. Метрика PR_AUC считается по кривой средних значений.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Матрица классификации

```py
>>> from sklearn.metrics import confusion_matrix
>>> y_true = [2, 0, 2, 2, 0, 1]
>>> y_pred = [0, 0, 2, 2, 0, 2]
>>> confusion_matrix(y_true, y_pred)
array([[2, 0, 0],
       [0, 0, 1],
       [1, 0, 2]])
```

![Classification matrix](https://scikit-learn.org/stable/_images/sphx_glr_plot_confusion_matrix_001.png "Classification matrix"){: .align-center style="width: 800px;"}
Источник: [sklearn](https://scikit-learn.org/stable/modules/model_evaluation.html).
{: style="text-align: center; font-size:0.7em;"}

{% capture notice %}
Выводы:
1. Матрица классификации, или матрица ошибок представляет собой количество объектов по двум осям - истинный класс и предсказанный класс.
1. Обычно, истинный класс располагается по строкам, а предсказанный - по столбцам.
1. Для идеальной модели матрица должна содержать ненулевые элементы только на главной диагонали.
1. Матрица позволяет наглядно представить результаты классификации и увидеть, в каких случаях модель делает ошибки.
1. Матрица незаменима при анализе ошибок, когда исследуется, какие объекты были мисклассфицированы.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>


#### Отчет о классификации

```py
>>> from sklearn.metrics import classification_report
>>> y_true = [0, 1, 2, 2, 0]
>>> y_pred = [0, 0, 2, 1, 0]
>>> target_names = ['class 0', 'class 1', 'class 2']
>>> print(classification_report(y_true, y_pred, target_names=target_names))
#              precision    recall  f1-score   support
#
#     class 0       0.67      1.00      0.80         2
#     class 1       0.00      0.00      0.00         1
#     class 2       1.00      0.50      0.67         2
#
#    accuracy                           0.60         5
#   macro avg       0.56      0.50      0.49         5
#weighted avg       0.67      0.60      0.59         5
```

{% capture notice %}
Выводы:
1. Отчет о классификации содержит всю необходимую информацию в стандартной форме.
1. Отчет показывает метрики для каждого класса, а так же объем каждого класса.
1. Также отчет показывает средние и средневзвешенные метрики для всей модели.
1. Отчет предполагает, что порог уже выбран.
1. Отчет о классификации - обязательный элемент представления результатов моделирования.
1. По отчету можно понять сбалансированность задачи, какие классы определяются лучше, какие - хуже.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### ROC_AUC

$$
TPR = \frac{TP}{TP + FN} = R \\
FRP = \frac{FP}{TN + FP} = 1 - S
$$

```py
>>> import numpy as np
>>> from sklearn.metrics import roc_curve
>>> y = np.array([1, 1, 2, 2])
>>> scores = np.array([0.1, 0.4, 0.35, 0.8])
>>> fpr, tpr, thresholds = roc_curve(y, scores, pos_label=2)
>>> fpr
array([0. , 0. , 0.5, 0.5, 1. ])
>>> tpr
array([0. , 0.5, 0.5, 1. , 1. ])
>>> thresholds
array([1.8 , 0.8 , 0.4 , 0.35, 0.1 ])
```

![ROC_AUC](https://scikit-learn.org/stable/_images/sphx_glr_plot_roc_001.png "ROC_AUC"){: .align-center style="width: 800px;"}
Источник: [sklearn](https://scikit-learn.org/stable/_images/sphx_glr_plot_roc_001.png).
{: style="text-align: center; font-size:0.7em;"}

{% capture notice %}
Выводы:
1. ROC-кривая показывает качество бинарной классификации при разных значениях порога.
1. В отличие от PR-кривой, ROC-кривая монотонна.
1. Площадь под графиком ROC-кривой, ROC_AUC - одна из основных метрик качества классификационных моделей. 
1. ROC_AUC можно использовать для сравнения качества разных моделей, обученных на разных данных.
1. Для множественной классификации также есть несколько алгоритмов усредения (но они устроены немного иначе).
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Проблема пере- и недообучения

#### Проблема Bias/Variance

![Bias-variance](/assets/images/ml_text/ml4-11.png "Bias-variance"){: .align-center style="width: 800px;"}

![Bias-variance](/assets/images/ml_text/ml4-3.png "Bias-variance"){: .align-center style="width: 800px;"}

{% capture notice %}
Выводы:
1. Прежде чем обучать модель, нужно выбрать ее вид (параметрическое семейство функций).
1. Разные модели при своих оптимальных параметрах будут давать разный результат.
1. Чем сложнее и вариативнее модель, тем больше у нее параметров.
1. Простые модели быстрые, но им недостает вариативности, изменчивости, у них высокое смещение (bias).
1. Сложные модели могут описывать больше зависимостей, но вычислительно более трудоемкие и имеют большую дисперсию (variance).
1. Слишком вариативные (сложные) модели алгоритм может подстраиваться под случайный шум в данных - переобучение.
1. Слишком смещенные (простые) модели алгоритм может пропустить связь признака и целевой переменной - недообучение.
1. Не всегда модель, которая лучше подстраивается под данные (имеет более высокие метрики эффективности) лучше.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Обобщающая способность модели, тестовый набор

![Test set](/assets/images/ml_text/ml4-12.png "Test set"){: .align-center style="width: 800px;"}

{% capture notice %}
Выводы:
1. Цель разработки моделей машинного обучения - не описывать обучающий набор (мы уже знаем ответы), а на его примере описывать другие объекты реального мира.
1. Главное качество модели - описывать объекты, которых она не видела при обучении - обобщающая способность.
1. Для того, чтобы оценить обобщающую способность модели нужно вычислить метрики эффективности на новых данных.
1. Для этого исходный датасет разбивают на обучающую и тестовую выборки. Делить можно в любой пропорции, обычно 80-20.
1. Обучающая выборки используется для подбора параметров модели (обучения), а тестовая - для оценки ее эффективности.
1. Никогда не оценивайте эффективность модели на тех же данных, на которых она училась - оценка получится слишком оптимистичная.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Кривые обучения

![Learning curve](/assets/images/ml_text/ml4-6.png "Learning curve"){: .align-center style="width: 800px;"}

{% capture notice %}
Выводы:
1. Кривая обучения - это зависимость эффективности модели от размера обучающей выборки.
1. Для построения кривых обучения модель обучают много раз, каждый раз с другим размером обучающей выборки (от одного элемента до всех, что есть).
1. При малых объемах обучающая эффективность будет очень большой, а тестовая - очень маленькой.
1. При увеличении объема обучающей выборки они будут сходиться, но обычно тестовая эффективность всегда ниже обучающей.
1. Кривые обучения позволяют увидеть, как быстро модель учится, хватает ли ей данных, а также обнаруживать пере- и недообучение.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Обнаружение пере- и недообучения

![Learning curve](/assets/images/ml_text/ml4-7.png "Learning curve"){: .align-center style="width: 800px;"}

![Learning curve](/assets/images/ml_text/ml4-8.png "Learning curve"){: .align-center style="width: 800px;"}

![Learning curve](/assets/images/ml_text/ml4-13.png "Learning curve"){: .align-center style="width: 800px;"}

{% capture notice %}
Выводы:
1. При недообучении тестовая и обучающая эффективности будут достаточно близкими, но недостаточными.
1. При переобучении тестовая и обучающая эффективности будут сильно различаться - тестовая будет значительно ниже.
1. Пере- и недообучение - это относительные понятия.
1. Более простые модели склонны к недообучению, более сложные - к переобучению.
1. Диагностика пере- и недообучения очень важна, так как для повышения эффективности предпринимаются противоположные меры.
1. Для построения можно использовать функцию ошибки, метрику эффективности или метрику ошибки, важна только динамика этих показателей.
1. Диагностика моделей машинного обучения - это не точная наука, здесь нужно принимать в расчет и задачу, и выбор признаков и многие другие факторы.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Регуляризация (ridge, lasso, elastic net)

![Bias vs complexity](/assets/images/ml_text/ml4-14.png "Bias vs complexity"){: .align-center style="width: 800px;"}

![Bias vs regularization](/assets/images/ml_text/ml4-4.png "Bias vs regularization"){: .align-center style="width: 800px;"}

#### Ridge

#### Lasso

#### Elastic net

### Методы повышения эффективности моделей

#### Анализ ошибок

#### Методы борьбы с недообучением

#### Методы борьбы с переобучением

### Выбор модели

#### Кросс-валидация

![CV](https://miro.medium.com/max/1400/1*AAwIlHM8TpAVe4l2FihNUQ.png "CV"){: .align-center style="width: 800px;"}
Источник: [Towards Data Science](https://towardsdatascience.com/cross-validation-k-fold-vs-monte-carlo-e54df2fc179b).
{: style="text-align: center; font-size:0.7em;"}

#### Гиперпараметры модели

#### Поиск по сетке

#### Случайный поиск

#### Сравнение эффективности моделей (валидационный набор)

```py
>>> from sklearn.model_selection import cross_validate
>>> from sklearn.metrics import recall_score

>>> scoring = ['precision_macro','recall_macro']
>>> clf = 
svm.SVC(kernel='linear', C=1, random_state=0)

>>> scores = 
cross_validate(clf, X, y, scoring=scoring)

>>> sorted(scores.keys())
['fit_time', 'score_time', 
'test_precision_macro', 'test_recall_macro']

>>> scores['test_recall_macro']
array([0.96..., 1.  ..., 0.96..., 0.96..., 1. ])

```

![CV](/assets/images/ml_text/ml4-9.png "CV"){: .align-center style="width: 800px;"}