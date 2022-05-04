---
<!-- section: ml -->
title: "Черновик учебника"
---


## ML0 Основные понятия машинного обучения


## ML1 Регрессия


## ML2 Класификация


## ML3 Методы обучения с учителем

### K ближайших соседей

### Метод опорных векторов

### Наивная байесовская модель

### Деревья решений

### Гауссовский процесс

### Перцептрон


## ML4 Диагностика систем машинного обучения

### Метрики эффективности для регрессии

#### Коэффициент детерминации (r-квадрат)

#### Доля объясненной дисперсии

#### Средняя абсолютная ошибка (MAE)

#### Средний квадрат ошибки (MSE)

#### Среднеквадратичная ошибка (MRSE)

#### Среднеквадратичная логарифмическая ошибка (MSLE)

### Метрики эффективности для классификации

#### Доля правильных ответов (accuracy)

#### Метрики классификации для неравных классов (precision, recall, F1)

#### Метрики для множественной классификации

#### Отчет о классификации

#### ROC_AUC

#### PR-AUC

### Проблема пере- и недообучения

#### Обобщающая способность модели

#### Кривые обучения

#### Связь со сложностью модели

### Регуляризация (ridge, lasso, elastic net)

#### Ridge

#### Lasso

#### Elastic net

### Методы повышения эффективности моделей

#### Анализ ошибок

#### Методы борьбы с недообучением

#### Методы борьбы с переобучением

### Выбор модели

#### Кросс-валидация

#### Гиперпараметры модели

#### Поиск по сетке

#### Сравнение эффективности моделей (валидационный набор)


## ML5 Предварительный анализ и обработка данных

### Требования к набору данных для обучения

#### Реляционная форма - объекты, атрибуты и признаки

#### Понятие чистых данных

#### Оценка источников и объемов данных

#### Интеграция данных

### Описательный анализ данных (EDA)

#### Количественные параметры датасета

#### Цели и задачи EDA

#### Основные методы EDA

### Очистка и преобразование данных

#### Заполнение отсутствующих значений

#### Шкалы измерения данных

#### Преобразование категориальных атрибутов

#### Преобразование численных атрибутов в категориальные

#### Нормализация и решкалирование признаков

### Работа с нестандартными типами данных

#### Методы работы с изображениями

#### Методы векторизации текстов

#### Работа с временными рядами

#### Векторизация аудиоданных

#### Методы работы с видеоданными


## ML6 Задачи обучения без учителя

### Кластеризация

### Обнаружение аномалий

### Понижение размерности


## ML7 Практическое использование моделей обучения с учителем

### Стохастический и пакетный градиентный спуск

### Отбор признаков

### Частичное обучение с учителем

### Ансамблирование моделей

#### Случайный лес

#### Беггинг

#### Бустинг

### Конвейеризация моделей

### Основные этапы проекта по машинному обучению






## !!!!!!!!!!!!!Регуляризация


#### Проблема переобучения

Регуляризация предназначена для решения проблемы переобучения.

Недообучение - это проблема выбора гипотезы, когда форма нашей функции h плохо отражает тренд данных. Обычно это вызвано слишком простой функцией или использует слишком мало функций. например. если взять 

<p id="gdcalert89" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image89.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert90">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image89.png "image_tooltip")
, то мы делаем первоначальное предположение о том, что линейная модель хорошо подгоняет учебные данные и сможет обобщить, но это может быть не так.

С другой стороны, чрезмерная или высокая дисперсия или переобучение вызвано функцией гипотезы, которая подходит к имеющимся данным, но не позволяет хорошо обобщать предсказание новых данных. Обычно это вызвано сложной функцией, которая создает много ненужных кривых и углов, не связанных с данными.

Эта терминология применяется как к линейной, так и к логистической регрессии. Существует два основных варианта решения проблемы переобучения:

1) Уменьшить количество признаков:

a) Вручную выберите, какие признаки сохранить.

b) Использовать алгоритм выбора модели.

2) Регуляризация

Сохраните все признаки, но уменьшите параметры b<sub>j</sub>.

Регуляризация работает хорошо, когда у нас много полезных признаков.


#### Функция ошибки

Если мы переобучаем нашу функцию гипотезы, мы можем уменьшить вес, который привносят некоторые члены в нашей функции, увеличивая их вклад в функцию ошибки.

Скажем, мы хотели сделать следующую функцию более квадратичной:



<p id="gdcalert90" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image90.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert91">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image90.png "image_tooltip")


Мы хотим устранить влияние b<sub>3</sub> и b<sub>4</sub>. Если мы не избавимся от этих признаков и не изменим форму нашей гипотезы, мы можем вместо этого изменить нашу функцию стоимости:



<p id="gdcalert91" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image91.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert92">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image91.png "image_tooltip")


В конце мы добавили два дополнительных термина, чтобы раздуть стоимость b<sub>3</sub> и b<sub>4</sub>. Теперь, чтобы функция ошибки приблизилась к нулю, нам нужно будет уменьшить значения b<sub>3</sub> и b<sub>4</sub> до нуля. Это в свою очередь значительно уменьшит значения b<sub>3</sub>x<sup>3</sup> и b<sub>4</sub>x<sup>4</sup> в нашей функции.

Мы могли бы также регуляризовать все наши параметры в одном суммировании:



<p id="gdcalert92" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image92.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert93">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image92.png "image_tooltip")


где λ или лямбда - параметр регуляризации. Он определяет, насколько сильно штрафуются высокие значения параметров регрессии. 

Используя вышеприведенную функцию стоимости с дополнительным суммированием, мы можем сгладить выход нашей функции гипотез, чтобы уменьшить переобучение. Если лямбда выбрана слишком большой, она может слишком сильно сгладить функцию и вызвать недооценку.


#### Регулярная линейная регрессия

Мы можем применить регуляризацию как к линейной регрессии, так и к логистической регрессии. Сначала рассмотрим случай линейной регрессии.

Градиентный спуск

Мы изменим нашу функцию градиентного спуска, чтобы отделить b<sub>0</sub> от остальных параметров, потому что мы не хотим штрафовать b<sub>0</sub>:



<p id="gdcalert93" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image93.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert94">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image93.png "image_tooltip")


Множитель 

<p id="gdcalert94" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image94.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert95">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image94.png "image_tooltip")
 выполняет регуляризацию.

С некоторыми манипуляциями наше правило обновления также может быть представлено как:



<p id="gdcalert95" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image95.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert96">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image95.png "image_tooltip")


Первый член в приведенном выше уравнении, 

<p id="gdcalert96" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image96.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert97">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image96.png "image_tooltip")
 всегда будет меньше 1. Интуитивно вы можете видеть его как уменьшение значения b<sub>j</sub> на некоторую величину при каждом обновлении.

Обратите внимание, что второй член теперь точно такой же, как и раньше.


#### Нормальное уравнение

Теперь давайте подходим к регуляризации с использованием альтернативного метода неитеративного нормального уравнения.

Чтобы добавить в регуляризацию, уравнение совпадает с нашим оригиналом, за исключением того, что мы добавляем еще один член в круглые скобки:



<p id="gdcalert97" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image97.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert98">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image97.png "image_tooltip")


L - матрица с 0 в левом верхнем углу и 1 вниз по диагонали, 0 - везде вне диагонали. Она должна иметь размерность (n + 1) × (n + 1). Интуитивно это - единичная матрица (хотя мы не включаем x<sub>0</sub>), умноженная на одно действительное число λ.

Напомним, что если m ≤ n, то матрица 

<p id="gdcalert98" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image98.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert99">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image98.png "image_tooltip")
 необратима. Однако, когда мы добавляем член λ⋅L, то 

<p id="gdcalert99" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image99.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert100">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image99.png "image_tooltip")
 становится обратимой матрицей.


#### Регулярная логистическая регрессия

Мы можем регуляризовать логическую регрессию так же, как мы регуляризируем линейную регрессию. Начнем с функции ошибки. Можно регуляризовать функцию ошибки, добавив к концу дополнительное слагаемое:



<p id="gdcalert100" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image100.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert101">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image100.png "image_tooltip")


Как и при линейной регрессии, мы захотим отдельно обновить b<sub>0</sub> и остальные параметры, потому что мы не хотим регуляризовать b<sub>0</sub>.



<p id="gdcalert101" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image101.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert102">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image101.png "image_tooltip")


Это идентично алгоритму градиентного спуска, представленному для линейной регрессии.


#### Единичный вектор постоянного признака

Как оказалось, очень важно добавить постоянный признак в свой обучающий набор, прежде чем начинать обучение модели. Обычно этот признак - всего лишь набор из единиц для всех ваших учебных примеров. Конкретно, если X - матрица признаков, то X<sub>0</sub> является вектором с единицами.

Предположим, вы проектируете модель, которая предсказывает цену дома на основе некоторых признаков. В этом случае чем помогает этот единичный вектор? Предположим, что простая модель включает признаки, которые прямо пропорциональны ожидаемой цене, то есть если признак X<sub>i</sub> увеличивается, ожидаемая цена y также будет увеличиваться. Так, например, мы могли бы иметь два признака: размер дома в м<sup>2</sup> и количество комнат.

Когда вы обучаете свою модель, вы начнете с добавления одного вектора X<sub>0</sub>. Затем вы можете после обучения узнать, что вес для вашей первоначальной функции - это некоторое значение b<sub>0</sub>. Но что это значит на практике? Давайте предположим, что кто-то знает, что у вас есть рабочая модель для цен на жилье. Оказывается, что для этого примера, если они спросят, сколько денег они могут ожидать, продавая дом, вы можете сказать, что как минимум b<sub>0</sub> долларов (или рандов), прежде чем вы даже используете свою обученную модель. Как и вышеприведенная аналогия, постоянная b<sub>0</sub> несколько устойчива, когда все ваши входы являются нулями. Конкретно, это цена дома без комнат, который не занимает никакую площадь.

Однако это объяснение имеет некоторые недостатки, потому что, если у вас есть некоторые функции, которые снижают цену, например возраст дома, то b<sub>0</sub> не может быть абсолютным минимумом цены. Это связано с тем, что возраст может снизить цену. Более простой и грубый способ выразить это состоит в том, что компонент b<sub>0</sub> вашей модели представляет собой неотъемлемое смещение модели. Другие функции затем выражают импульс, чтобы отойти от этой позиции смещения.

Признак «смещения» (bias feature) - это просто способ переместить вектор наилучшего соответствия, чтобы лучше соответствовать данным. Например, рассмотрим проблему обучения с помощью одного признака X<sub>1</sub>. Формула без функции X<sub>0</sub> - это просто b<sub>1</sub> * X<sub>1</sub> = y. Это показано как линия, которая всегда проходит через начало координат с наклоном y / theta. слагаемое x<sub>0</sub> позволяет линии проходить через другую точку на оси y. Это почти всегда будет лучше соответствовать. Не все же наилучшие подходящие линии проходят через начало координат (0,0)?


### Диагностика систем машинного обучения

Ошибки в ваших прогнозах можно устранить с помощью следующих способов:



1. Получение дополнительных примеров в обучающую выборку;
2. Попытка использования меньших наборов признаков;
3. Попытка использования дополнительных признаков;
4. Попытки использования полиномиальных признаков;
5. Увеличение или уменьшение λ.

Не следует просто выбирать один из этих путей наугад. Мы рассмотрим диагностические методы для выбора одного из вышеуказанных решений путем тщательного исследования процесса обучения модели.


#### Оценка качества модели

Гипотеза может иметь низкую ошибку для примеров из обучающей выборки, но все же быть неточной (из-за переобучения). Используя набор обучающих примеров, мы можем разбить данные на два набора: набор для обучения и набор для тестов.

Новая процедура с использованием этих двух наборов:



1. Обучите b и минимизируйте 

<p id="gdcalert102" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image102.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert103">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image102.png "image_tooltip")
 с помощью обучающего набора;
2. Вычислите ошибку тестового набора 

<p id="gdcalert103" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image103.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert104">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image103.png "image_tooltip")


Ошибка тестового набора

для регрессии: 



<p id="gdcalert104" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image104.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert105">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image104.png "image_tooltip")


для классификации:



<p id="gdcalert105" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image105.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert106">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image105.png "image_tooltip")
. где



<p id="gdcalert106" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image106.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert107">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image106.png "image_tooltip")


Ошибка классификации дает нам долю тестового набора, которая была ошибочно классифицирована.


#### Выбор модели (model selection)

Просто потому, что алгоритм обучения хорошо подходит для тренировочного набора, это не значит, что это хорошая гипотеза. Ошибка вашей гипотезы, измеренная в наборе данных, с которым вы подготовили параметры, будет ниже, чем на любом другом наборе данных.

Чтобы выбрать модель вашей гипотезы, вы можете проверить каждую степень полинома и посмотреть на результат ошибки. Метод без использования третьего, валидационного набора (обратите внимание: это плохой метод - не используйте его) выглядел бы следующим образом:



1. Оптимизируйте параметры b, используя обучающий набор для каждой степени полинома.
2. Найдите степень полинома d с наименьшей ошибкой, используя тестовый набор.
3. Оцените ошибку обобщения, также используя тестовый набор с 

<p id="gdcalert107" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image107.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert108">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image107.png "image_tooltip")
 , (d = theta от полинома с более низкой ошибкой);

В этом случае мы обучили одну переменную d или степень полинома, используя тестовый набор. Это приведет к тому, что наше значение ошибки будет больше для любого другого набора данных.

Подобные переменные, не являющиеся параметрами гипотезы, но так или иначе влияющие на точность нашей модели называются гиперпараметрами модели. Обучение гиперпараметров - более сложный и долгий путь и он требует проведения специальной процедуры.


#### Использование валидационного набора 

Чтобы решить эту проблему, мы можем ввести третий набор, валидационный набор, чтобы использовать его как промежуточный набор для обучения гиперпараметров. Тогда наш тестовый набор даст нам точную, не оптимистичную ошибку.

Один из возможных примеров разбивки нашего набора данных на три набора:



1. Обучающий набор (train set): первые 60%;
2. Валидационный набор (validation set): следующие 20%;
3. Тестовый набор (test set): последние 20%.

Этот лишь одна из самых простых схем разбиения набора данных. С помощью специальной техники - кросс-валидации или перекрестной проверки - процесс разбиения набора автоматизируется и становится более робастным. Пока не будем рассматривать эту продвинутую технику выбора модели.

Теперь мы можем вычислить три отдельных значения ошибки для трех разных наборов.

Метод выбора гипотезы с помощью валидационного набора (обратите внимание: этот метод предполагает, что мы не используем регуляризацию и на валидационном наборе)



1. Оптимизируйте параметры b, используя набор тренировок для каждой степени полинома.
2. Найдите степень полинома d с наименьшей ошибкой, используя валидационный набор.
3. Оцените ошибку обобщения, используя тестовый набор с 

<p id="gdcalert108" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image108.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert109">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image108.png "image_tooltip")
(где  b - параметры от полинома с более низкой ошибкой);

Таким образом, степень полинома d не была обучена с использованием тестового набора.

Имейте в виду, что использование валидационного набора для выбора d означает, что мы также не можем использовать его для процесса проверки правильности установки значения лямбда.


#### Диагностика недо- и переобучения



<p id="gdcalert109" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image109.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert110">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image109.png "image_tooltip")


В этом разделе мы рассмотрим взаимосвязь между степенью полинома d и недо- или переообучением нашей гипотезы. Нам нужно различать, является ли проблемой, которая способствует плохим предсказаниям, смещение (bias) или дисперсия (variance) функции гипотезы. Высокое смещение чаще недообучается, а высокая дисперсия чаще переобучается. Нам нужно найти золотую середину между этими двумя крайностями. 

Ошибка обучения будет уменьшаться по мере увеличения степени d многочлена. В то же время ошибка перекрестной проверки будет уменьшаться по мере увеличения d до точки, а затем она увеличивается с увеличением d, образуя выпуклую кривую.



*   Высокое смещение (недообучение): как 

<p id="gdcalert110" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image110.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert111">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image110.png "image_tooltip")
, так и 

<p id="gdcalert111" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image111.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert112">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image111.png "image_tooltip")
 будут высокими. Кроме того, 

<p id="gdcalert112" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image112.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert113">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image112.png "image_tooltip")
.
*   Высокая дисперсия (переобучение):

<p id="gdcalert113" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image113.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert114">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image113.png "image_tooltip")
 будет низкой, а 

<p id="gdcalert114" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image114.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert115">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image114.png "image_tooltip")
 будет намного больше, чем 

<p id="gdcalert115" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image115.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert116">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image115.png "image_tooltip")
.

При выборе из многих значений d можно построить зависимость ошибок на обучающем и валидационных наборах на графике зависимости от d. Такой график наглядно показывает области недо- и переобучения и выглядит подобно следующему:



<p id="gdcalert116" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image116.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert117">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image116.png "image_tooltip")



#### Регуляризация и переобучение

Вместо того, чтобы смотреть на степень d, способствующую смещению / дисперсии, теперь мы рассмотрим параметр регуляризации λ.



*   Большой λ: высокое смещение (недообучение);
*   Малый λ: высокая дисперсия (переобучение).

Большая лямбда сильно штрафует все параметры b, что значительно упрощает линию нашей результирующей функции, поэтому вызывает недообучение.

Отношение λ к набору тренировок и набору дисперсий выглядит следующим образом:



*   Низкий λ: 

<p id="gdcalert117" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image117.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert118">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image117.png "image_tooltip")
 низкий, а 

<p id="gdcalert118" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image118.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert119">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image118.png "image_tooltip")
 высокий (высокая дисперсия / переобучение);
*   Оптимальное значение λ: 

<p id="gdcalert119" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image119.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert120">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image119.png "image_tooltip")
 и 

<p id="gdcalert120" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image120.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert121">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image120.png "image_tooltip")
 низки и 

<p id="gdcalert121" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image121.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert122">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image121.png "image_tooltip")
;
*   Большой λ: оба 

<p id="gdcalert122" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image122.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert123">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image122.png "image_tooltip")
 и 

<p id="gdcalert123" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image123.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert124">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image123.png "image_tooltip")
 будут высокими (недообучение / высокое смещение).

Опять же, можно построить зависимость ошибок от параметра регуляризации для наглядного поиска оптимального значения λ:



<p id="gdcalert124" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image124.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert125">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image124.png "image_tooltip")


Чтобы выбрать вид  модели и параметр регуляризации λ одновременно, нам нужно:



1. Создайте список возможных значения λ (например, λ∈ {0, 0.01, 0.02, 0.04, 0.08, 0.16, 0.32, 0.64, 1.28, 2.56 ,5.12, 10.24});
2. Создайте набор моделей с разной степенью или любыми другими вариантами;
3. Начните итерировать по λ и для каждого λ итерировать по всем моделям, чтобы обучать параметры b;
4. Вычислите ошибку валидационного набора, используя обученные b (вычисленные с λ) на 

<p id="gdcalert125" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image125.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert126">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image125.png "image_tooltip")
 без регуляризации или λ = 0;
5. Выберите лучшую комбинацию, которая дает самую низкую ошибку на валидационном  наборе;
6. Используя наилучшую комбинацию b и λ, примените ее на 

<p id="gdcalert126" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image126.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert127">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image126.png "image_tooltip")
, чтобы увидеть, дает ли она хорошее обобщение задачи.


#### Кривые обучения

Тренировка квадратичной функции на трех примерах легко даст нулевую  ошибку, потому что мы всегда можем найти квадратичную кривую, которая точно касается 3 точек. По мере увеличения обучающего набора ошибка для квадратичной функции будет возрастать. Значение ошибки будет стабилизироваться после определенного значения m или размера набора тренировок.


<table>
  <tr>
   <td>

<p id="gdcalert127" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image127.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert128">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image127.png" width="" alt="alt_text" title="image_tooltip">

   </td>
   <td>

<p id="gdcalert128" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image128.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert129">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


<img src="images/image128.png" width="" alt="alt_text" title="image_tooltip">

   </td>
  </tr>
</table>


Если алгоритм обучения страдает от высокого смещения, получение большего количества данных по обучению не может (само по себе) существенно улучшить эффективность. Если алгоритм обучения страдает от большой дисперсии, скорее всего, получение большего количества данных по обучению повысит общую эффективность обучения.

Типичным правилом при выполнении диагностики является:



*   Дополнительные примеры в обучающей выборке устраняют высокую дисперсию, но не помогают при высоком смещении;
*   Меньшие функции устраняют высокую дисперсию, но помогают пир высоком смещении;
*   Дополнительные признаки устраняют высокое смещение, но не высокую дисперсию;
*   Добавление полиномиальных признаков устраняют высокое смещение, но не высокую дисперсию;
*   При использовании градиентного спуска уменьшение лямбда может исправить высокое смещение, и увеличение лямбда может исправить высокую дисперсию;
*   При использовании нейронных сетей небольшие нейронные сети более подвержены недобучению, а большие - переобучению. Перекрестная проверка размера сети - это хороший способ выбора архитектуры нейронной сети.

Рекомендуемый подход к решению проблем машинного обучения:



*   Начните с простого алгоритма, быстро реализуйте его и проверьте его на ранней стадии.
*   Стройте кривые обучения, чтобы решить, поможет ли добавление данных, признаков или что-то другое
*   Анализ ошибок: вручную проверьте ошибки на примерах в валидационном наборе и попытайтесь определить общие зависимости.

Важно, чтобы результаты проверки качества модели были выражены как одно интегральное числовое значение. В противном случае сложно оценить производительность вашего алгоритма.


#### Метрики ошибок для смещенных классов

Иногда трудно сказать, является ли уменьшение ошибки на самом деле улучшением алгоритма.

Например: при прогнозировании диагнозов рака на обучающей выборке, где у 0,5% примеров есть рак, мы обнаруживаем, что наш алгоритм после обучения имеет ошибку в 1%. Однако, если бы мы просто классифицировали каждый отдельный пример как 0, то наша ошибка уменьшилась бы до 0,5%, хотя мы не улучшили алгоритм.

Обычно такая ситуация происходит при использовании наборов данных со смещенными классами; то есть, когда один из классов очень редок во всем наборе данных. Или, по-другому говоря, когда у нас есть больше примеров из одного класса, чем из другого класса.

Для этого мы можем использовать метрики, связанные с понятиями полноты и точности(precision/recall).

Рассмотрим возможные варианты классификации обучающих примеров в задаче бинарной классификации:



*   Прогнозируемый: 1, Фактический: 1 - Истинный положительный (true positive, TP);
*   Прогнозируемый: 0, Фактический: 0 - Истинный отрицательный (true negative);
*   Прогнозируемый: 0, Фактический, 1 - Ложноотрицательный (false negative);
*   Прогнозируемый: 1, Фактический: 0 - Ложноположительный (false positive).

Классическая метрика точности (accuracy) показывает следующее: из всех пациентов, какую долю мы предсказали правильно, то есть 

<p id="gdcalert129" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image129.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert130">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image129.png "image_tooltip")
.

Тем не менее, у этой метрики есть одна особенность которую необходимо учитывать. Она присваивает всем примерам одинаковый вес, что может быть некорректно в случае если распределение документов в обучающей выборке сильно смещено в сторону какого-то одного или нескольких классов. В этом случае у классификатора есть больше информации по этим классам и соответственно в рамках этих классов он будет принимать более адекватные решения. На практике это приводит к тому, что вы имеете точность, скажем, 80%, но при этом в рамках какого-то конкретного класса классификатор работает из рук вон плохо не определяя правильно даже треть документов.

Точность (precision): из всех пациентов, у которых мы предсказали y=1, какая доля действительно имеет рак?



<p id="gdcalert130" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image130.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert131">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image130.png "image_tooltip")


Полнота (recall): из всех пациентов, у которых действительно рак, у какой доли мы его распознали?



<p id="gdcalert131" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image131.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert132">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image131.png "image_tooltip")


Эти две метрики дают нам лучшее представление о том, как работает наш классификатор. Мы хотим, чтобы точность и отзыв были высокими.

В примере в начале раздела, если мы классифицируем всех пациентов как 0, тогда наш отзыв будет 

<p id="gdcalert132" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image132.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert133">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image132.png "image_tooltip")
, поэтому, несмотря на более низкий процент ошибок, мы можем быстро увидеть, что этот алгоритм хуже.

Обратите внимание: если алгоритм предсказывает только один класс, как в одном из примеров, точность не определена, так как невозможно делить на 0. 

Нам может потребоваться уверенное предсказание двух классов с использованием логистической регрессии. Один из способов - увеличить наш порог предсказания:



*   Прогнозировать 1, если: 

<p id="gdcalert133" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image133.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert134">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image133.png "image_tooltip")

*   Прогнозировать 0, если: 

<p id="gdcalert134" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image134.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert135">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image134.png "image_tooltip")


Таким образом, мы прогнозируем рак, только если у пациента есть вероятность как минимум 70%. Выполняя это, мы будем иметь более высокую точность, но более низкую полноту.

В противоположном примере мы можем снизить наш порог:



*   Прогнозировать 1, если: 

<p id="gdcalert135" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image135.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert136">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image135.png "image_tooltip")

*   Прогнозировать 0, если: 

<p id="gdcalert136" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image136.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert137">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image136.png "image_tooltip")


Таким образом, мы получаем очень безопасное предсказание. Это приведет к более высокой полноте, но более низкой точности. Чем выше пороговое значение, тем больше точность и тем ниже полнота. Чем ниже порог, тем больше полнота и тем ниже точность. Чтобы превратить эти две метрики в одно число, мы можем взять значение F.

Один из способов - взять среднее: 

<p id="gdcalert137" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image137.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert138">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image137.png "image_tooltip")
. Это не работает. Если мы прогнозируем все y = 0, то это приведет к среднему показателю, несмотря на то, что полнота такого алгоритма равна 0. Если мы прогнозируем все примеры как y = 1, то очень высокая полнота вызовет среднее значение, несмотря на точность 0.

Лучше всего вычислить оценку F1 (F-Score) - среднее геометрическое из этих двух показателей:



<p id="gdcalert138" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image138.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert139">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image138.png "image_tooltip")


Чтобы показатель F был высоким, как точность, так и отзыв должны быть высокими.


#### Данные для машинного обучения

В некоторых случаях «неполный алгоритм» при наличии достаточных данных может превосходить превосходный алгоритм с меньшим количеством данных.

Мы должны выбрать наши признаки таким образом, чтобы иметь достаточно информации для построения адекватной модели. Полезным эмпирическим тестом для проверки достаточности набора признаков  является следующее правило: учитывая вход x, сможет ли эксперт-человек уверенно предсказать y?

Если у нас есть алгоритм с низким смещением, то чем больше мы используем обучающий набор, тем меньше мы будем переообучаться и тем точнее алгоритм будет работать на тестовой выборке. Таким образом можно сформулировать золотое правило машинного обучения: нужно взять как можно больше данных и как можно более вариативный алгоритм.


### Обучение с помощью больших наборов данных

В некоторых областях существует возможность использовать для машинного обучения весьма большие наборы данных. Наборы данных часто могут приближаться к таким размерам, как m = 100 000 000. В этом случае наш шаг градиентного спуска должен будет суммировать все сто миллионов примеров. Мы хотим попытаться избежать этого - подходы для этого описаны ниже.


#### Стохастический градиентный спуск

Стохастический градиентный спуск (stochastic gradient decsent, SGD) является альтернативой классическому (или пакетному, batch gradient descent, BGD) градиентному спуску, более эффективен и масштабируется для больших наборов данных.

Стохастический градиентный спуск формализуетсяя другим, но схожим образом:



<p id="gdcalert139" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image139.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert140">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image139.png "image_tooltip")


Единственная разница в вышеперечисленной функции затрат заключается в устранении константы m в $$ \dfrac{1}{2} $$



<p id="gdcalert140" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image140.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert141">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image140.png "image_tooltip")


Алгоритм выглядит следующим образом

Случайно «перетасовать» набор данных

Для i = 1 ... m



<p id="gdcalert141" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image141.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert142">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image141.png "image_tooltip")


Этот алгоритм будет пытаться одновременно подгонять один пример обучения. Таким образом, мы можем добиться прогресса в градиентном спуске без необходимости сначала сканировать все примеры обучения. Стохастический градиентный спуск вряд ли сходится на глобальном минимуме и вместо этого будет беспорядочно перемещаться вокруг него, но обычно дает результат, достаточно близкий. Стохастический градиентный спуск обычно занимает 1-10 проходов через набор данных, чтобы приблизиться к глобальному минимуму.


#### Мини-пакетный градиентный спуск

Мини-пакетный градиентный спуск иногда может быть даже быстрее, чем стохастический градиентный спуск. Вместо использования всех m-примеров, как при пакетном градиентном спуске, и вместо использования только одного примера, как при стохастическом градиентном спуске, мы будем использовать некоторое промежуточное число примеров b.

Типичные значения для b варьируются от 2 до 100 или около того.

Например, при b = 10 и m = 1000:

Повторение:

Для i = 1,11,21,31, ..., 991



<p id="gdcalert142" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image142.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert143">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image142.png "image_tooltip")


Мы просто суммируем более десяти примеров за раз. Преимущество вычисления более чем одного примера за раз заключается в том, что мы можем использовать векторизованные реализации над примерами b.


#### Стохастическая градиентная сходимость

Как выбрать скорость обучения α для стохастического градиентного спуска? Кроме того, как мы отлаживаем стохастический градиентный спуск, чтобы убедиться, что он приближается к глобальному оптимуму?

Одна из стратегий заключается в построении средней стоимости гипотезы, применяемой к кажущимся 1000 примерам обучения. Мы можем вычислить и сохранить эти затраты во время итераций спуска градиента.

С меньшей скоростью обучения возможно, что вы можете получить немного лучшее решение со стохастическим градиентным спуском. Это связано с тем, что стохастический градиентный спуск будет колебаться и скакать по глобальному минимуму, и он будет делать небольшие случайные скачки с меньшей скоростью обучения.

Если вы увеличите количество примеров, в среднем превышающих производительность вашего алгоритма, линия графика станет более плавной. При очень небольшом числе примеров для среднего, линия будет слишком шумной, и будет трудно найти тренд.

Одна из стратегий, позволяющих фактически сходиться на глобальном минимуме, заключается в медленном уменьшении α по времени. Однако это не часто делается, потому что люди не хотят возиться с еще большим количеством гиперпараметров.


#### Онлайн обучение

При непрерывном потоке пользователей на веб-сайт мы можем запустить бесконечный цикл, который получает (x, y), где мы собираем некоторые действия пользователя для функций в x, чтобы предсказать некоторое поведение y.

Вы можете обновлять b для каждой отдельной пары (x, y) по мере их сбора. Таким образом, вы можете адаптироваться к новым действиям пользователей, так как вы постоянно обновляете параметры модели.


### Кластеризация

Обучение без учителя является противоположностью обучению с учителем, потому что оно использует немаркированный набор тренировок, а не размеченный. Другими словами, у нас нет вектора y ожидаемых результатов, у нас есть только набор данных, в которых мы можем найти структуру.

Кластеризация (или кластерный анализ) — это задача разбиения множества объектов на группы, называемые кластерами. Внутри каждой группы должны оказаться «похожие» объекты, а объекты разных группы должны быть как можно более отличны. Главное отличие кластеризации от классификации состоит в том, что перечень групп четко не задан и определяется в процессе работы алгоритма.

Кластеризация хороша для:



*   Сегментация рынка
*   Анализ социальной сети
*   Организация компьютерных кластеров
*   Астрономический анализ данных


#### Представление модели

Пусть X — множество объектов, Y — множество номеров (имён, меток) кластеров. Задана функция расстояния между объектами 

<p id="gdcalert143" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image143.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert144">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image143.png "image_tooltip")
. Имеется конечная обучающая выборка объектов 

<p id="gdcalert144" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image144.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert145">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image144.png "image_tooltip")
. Требуется разбить выборку на непересекающиеся подмножества, называемые кластерами, так, чтобы каждый кластер состоял из объектов, близких по метрике 

<p id="gdcalert145" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image145.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert146">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image145.png "image_tooltip")
, а объекты разных кластеров существенно отличались. При этом каждому объекту 

<p id="gdcalert146" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image146.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert147">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image146.png "image_tooltip")
 приписывается номер кластера 

<p id="gdcalert147" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image147.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert148">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image147.png "image_tooltip")
.

Алгоритм кластеризации — это функция 

<p id="gdcalert148" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image148.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert149">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image148.png "image_tooltip")
, которая любому объекту 

<p id="gdcalert149" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image149.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert150">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image149.png "image_tooltip")
 ставит в соответствие номер кластера 

<p id="gdcalert150" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image150.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert151">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image150.png "image_tooltip")
. Множество Y в некоторых случаях известно заранее, однако чаще ставится задача определить оптимальное число кластеров, с точки зрения того или иного критерия качества кластеризации.

Наши основные переменные:



*   K (количество кластеров)
*   Тренировочный набор 

<p id="gdcalert151" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image151.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert152">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image151.png "image_tooltip")

*   Где 

<p id="gdcalert152" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image152.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert153">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image152.png "image_tooltip")
 


#### Алгоритм K средних

Алгоритм k-средних (K-Means) является самым популярным и широко используемым алгоритмом для автоматической группировки данных в когерентные подмножества.

Основная идея алгоритма выражена в следующих шагах:



1. Случайно инициализируйте две точки в наборе данных, называемые центроидами кластера.
2. Назначение кластера: назначьте все примеры в одну из двух групп на основе того, какой кластер-центроид ближе всего к примеру.
3. Переместите центроид: вычислите средние значения для всех точек внутри каждой из двух групп кластеров кластеров, а затем переместите точки центроида кластера на эти средние.
4. Повторно запустите (2) и (3), пока мы не найдем наши кластеры.

Обратите внимание, что мы не будем использовать соглашение x<sub>0</sub> = 1.

Первый цикл алгоритма - это назначение центроидов кластеров. Мы создаем вектор c, где c<sup>(i)</sup> представляет центроид, назначенный примеру x<sup>(i)</sup>. Мы можем написать операцию шага назначения кластеров математически следующим образом:



<p id="gdcalert153" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image153.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert154">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image153.png "image_tooltip")


Каждый элемент 

<p id="gdcalert154" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image154.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert155">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image154.png "image_tooltip")
 содержит индекс центроида, который имеет минимальное расстояние до 

<p id="gdcalert155" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image155.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert156">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image155.png "image_tooltip")
.

По соглашению мы возводим правую сторону в квадрат, что делает функцию, которую мы пытаемся свести к минимуму, более быстро возрастающей. Это в основном просто удобное соглашение. Но соглашение, которое помогает уменьшить количество вычислений, потому что евклидово расстояние требует квадратного корня, но отменяется.

Второй цикл алгоритма - это перемещение центроидов, где мы перемещаем каждый центроид в среднем по своей группе. Более формально уравнение для этого цикла выглядит следующим образом:



<p id="gdcalert156" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image156.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert157">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image156.png "image_tooltip")


Где каждый из 

<p id="gdcalert157" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image157.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert158">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image157.png "image_tooltip")
 - примеры обучения, назначенные группе 

<p id="gdcalert158" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image158.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert159">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image158.png "image_tooltip")
.

Если у вас есть центроид кластера, которому соответствуют 0 точек, вы можете случайно повторно инициализировать этот центроид для новой точки. Вы также можете просто исключить эту группу кластеров.

После ряда итераций алгоритм сходится, и новые итерации не влияют существенно на положение центроидов кластеров.

Некоторые наборы данных не имеют реального внутреннего разделения или естественной структуры. Алгоритмы типа К-средних могут равномерно сегментировать такие данные в подмножества, поэтому даже в этом случае могут быть полезны.


#### Функция ошибки

Вспомним некоторые параметры, которые мы использовали в нашем алгоритме:



<p id="gdcalert159" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image159.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert160">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image159.png "image_tooltip")
 - индекс кластера (1,2, ..., K), к которому в настоящее время назначается пример x (i)



<p id="gdcalert160" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image160.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert161">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image160.png "image_tooltip")
 - кластеризованный центроид k (μ<sub>k</sub>∈ℝ<sup>n</sup>)



<p id="gdcalert161" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image161.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert162">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image161.png "image_tooltip")
 - кластерный кластер кластера, которому присвоен пример x<sup>(i)</sup>;

Используя эти переменные, мы можем определить нашу функцию стоимости:



<p id="gdcalert162" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image162.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert163">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image162.png "image_tooltip")


Наша цель оптимизации состоит в том, чтобы свести к минимуму все наши параметры, используя указанную выше функцию стоимости:



<p id="gdcalert163" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image163.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert164">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image163.png "image_tooltip")


То есть мы находим все значения в наборах _c_, представляющие все наши кластеры, и μ, представляющие все наши центроиды, которые минимизируют среднее значение расстояний каждого примера обучающей выборки до его соответствующего кластерного центра.

На этапе назначения кластеров наша цель заключается в следующем:

Минимизируйте J(...) с 

<p id="gdcalert164" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image164.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert165">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image164.png "image_tooltip")
 (удерживая 

<p id="gdcalert165" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image165.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert166">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image165.png "image_tooltip")
 фиксированным)

В шаге централизованного шага наша цель:

Минимизируйте J (...) с помощью 

<p id="gdcalert166" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image166.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert167">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image166.png "image_tooltip")


В ходе работы алгоритма k-средних общая ошибка модели не может увеличиваться. При нормальном ходе обучения она всегда должна уменьшаться.

Существует рекомендуемый метод изначального задания центроидов кластеров -  случайная инициализация. Причем:



1. Убедитесь, что количество ваших кластеров меньше числа ваших учебных примеров.
2. Случайно выберите примеры обучения K.
3. Установите 

<p id="gdcalert167" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image167.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert168">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image167.png "image_tooltip")
, равный этим примерам K.

Алгоритм K-средних может застревать в локальных оптимумах. Чтобы уменьшить вероятность этого, вы можете запустить алгоритм для многих различных случайных инициализаций. В случаях, когда K &lt;10, настоятельно рекомендуется запускать цикл случайных инициализаций.


#### Выбор количества кластеров

Выбор K может быть довольно произвольным и неоднозначным. Метод локтя: отслеживайте стоимость J и количество кластеров K. Функция стоимости должна уменьшаться по мере увеличения количества кластеров, а затем выходить на плато. Выберите K в точке, где функция ошибки начинает выравниваться (точка локтя, elbow point). Однако довольно часто кривая очень постепенная, поэтому нет четкого локтя.

J всегда будет уменьшаться по мере увеличения K. Единственное исключение - если k-средства застревают в плохом локальном оптимуме.

Другой способ выбора K - наблюдать, насколько хорошо k-означает выполнение в нисходящей цели. Другими словами, вы выбираете K, который окажется наиболее полезным для какой-то цели, которую вы пытаетесь достичь от использования этих кластеров.


#### Обзор методов кластеризации

Существует большое количество алгоритмов кластеризации. Среди них выделяют линейные и нелинейные алгоритмы. К линейным алгоритмам относятся:



1. линейный алгоритм k-средних;
2. нечеткий алгоритм кластеризации c-mean;
3. иерархический алгоритм кластеризации;
4. алгоритм кластеризации Гаусса (EM);
5. алгоритм кластеризации пороговых значений качества;

Некоторые алгоритмы нелинейной кластеризации:



*   алгоритм кластеризации на основе MST;
*   алгоритмы кластеризации ядра k-mean;
*   алгоритм кластеризации на основе плотности;


### Понижение размерности


#### Постановка задачи

Вы когда-нибудь работали над набором данных с более чем тысячей функций? Как насчет более 50 000 функций? Это очень сложная задача, особенно если вы не знаете, с чего начать. Наличие большого числа переменных является одновременно благом и проклятием. Замечательно, что у нас есть масса данных для анализа, но проводить его одновременно сложно из-за размера.

Невозможно проанализировать каждую переменную на микроскопическом уровне. Может потребоваться несколько дней или месяцев для проведения значимого анализа. Не говоря уже о количестве вычислительной мощности, которое это займет. Нам нужен лучший способ справиться с большими размерными данными, чтобы мы могли быстро извлечь из него шаблоны и идеи. 

Мы можем существенно уменьшить количество имеющихся признаков, если у нас много избыточных данных. Для этого мы найдем две сильно коррелированные признаки, на их основе создадим новый признак, который точно описывает оба. 

Выполнение уменьшения размерности уменьшит общие данные, которые мы должны хранить в памяти компьютера, и ускорит алгоритм обучения.

При уменьшении размерности мы уменьшаем количество признаков, а не наше количество примеров. Наша переменная m останется прежнего размера; n, число признаков, каждый из которых переносится из 

<p id="gdcalert168" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image168.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert169">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image168.png "image_tooltip")
 в 

<p id="gdcalert169" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image169.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert170">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image169.png "image_tooltip")
, будет уменьшено.

Нелегко визуализировать данные более трех измерений. Мы можем уменьшить размер наших данных до 3 или менее, чтобы можно было построить визуализацию, облегчающую понимание зависимостей в данных.

Нам нужно найти новые функции z<sub>1</sub>, z<sub>2</sub> (и, возможно, z<sub>3</sub>), которые могут эффективно суммировать все остальные функции.Пример: сотни признаков, связанных с экономической системой страны, могут быть объединены в один, которую можно охарактеризовать «Экономическая деятельность».

По мере того, как объем генерации и сбор аданных все больше возрастает, визуализация и выведение умозаключений становятся все более сложными. Одним из наиболее распространенных способов визуализации является использование диаграмм. Предположим, что у нас есть 2 переменные: возраст и высота. 

Теперь рассмотрим случай, в котором мы имеем, скажем, 100 переменных (p = 100). В этом случае мы можем иметь 100 (100-1) / 2 = 5000 разных графиков. Не имеет смысла визуализировать каждый из них отдельно, не так ли? В таких случаях, когда мы имеем большое количество переменных, лучше выбрать подмножество этих переменных (p &lt;< 100), которое фиксирует столько информации, сколько исходный набор переменных.

Поясним это на простом примере. Рассмотрим приведенное ниже изображение:



<p id="gdcalert170" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image170.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert171">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image170.png "image_tooltip")


Здесь мы имеем веса подобных объектов в Kg (X1) и Pound (X2). Если мы будем использовать обе эти переменные, они будут передавать аналогичную информацию. Таким образом, имеет смысл использовать только одну переменную. Мы можем преобразовать данные из 2D (X1 и X2) в 1D (Y1), как показано ниже:



<p id="gdcalert171" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image171.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert172">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image171.png "image_tooltip")


Аналогично, мы можем уменьшить p размерности данных в подмножество k размерностей (k &lt;< n). Это называется уменьшением размерности.


#### Метод главных компонент

Наиболее популярным алгоритмом сокращения размерности является метод главных компонент (principal component analysis, PCA). В этом методе переменные преобразуются в новый набор переменных, которые являются линейной комбинацией исходных переменных. Эти новые переменные известны как основные или главные компоненты. Они получаются таким образом, что первый компонент учитывает большую часть возможного изменения исходных данных, после чего каждый последующий компонент имеет максимально возможную дисперсию.

Второй главный компонент должен быть ортогонален первому главному компоненту. Другими словами, он делает все возможное, чтобы зафиксировать дисперсию данных, которые не были захвачены первым основным компонентом. Для двумерного набора данных могут быть только два главных компонента. 

Учитывая две функции: x<sub>1</sub> и x<sub>2</sub>, мы хотим найти одну такую переменную, которая эффективно описывает обе функции одновременно. Затем мы сопоставляем наши старые функции с этой новой строкой, чтобы получить новую отдельную функцию. То же самое можно сделать с тремя функциями, где мы сопоставляем их с плоскостью.

Цель PCA - уменьшить среднее значение всех расстояний каждой функции до линии проецирования. Это называется ошибка проецирования. Уменьшите от 2d до 1d: найдите направление (вектор 

<p id="gdcalert172" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image172.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert173">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image172.png "image_tooltip")
, на который нужно проецировать данные, чтобы минимизировать ошибку проецирования.

Более общий случай таков:

Понижение от n-мерности до k-размерности: найдите k векторов 

<p id="gdcalert173" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image173.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert174">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image173.png "image_tooltip")
 на которые нужно проецировать данные, чтобы свести к минимуму ошибка проектирования.

Если мы перейдем от 3d к 2d, мы будем проектировать наши данные на два направления (плоскость), поэтому k будет равно 2.

PCA не является линейной регрессией. В линейной регрессии мы минимизируем квадрат ошибки от каждой точки до нашей линии предиктора. Это вертикальные расстояния. В PCA мы минимизируем кратчайшее расстояние или кратчайшие ортогональные расстояния до наших точек данных. В более общем плане, в линейной регрессии, мы берем все наши примеры в x и применяем параметры в Θ для предсказания y. В PCA мы берем ряд функций 

<p id="gdcalert174" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image174.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert175">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image174.png "image_tooltip")
 и находим среди них наиболее близкий общий набор данных. Мы не пытаемся предсказать какой-либо результат, и мы не применяем к ним тета-веса.


#### Алгоритм анализа основных компонентов

Основные компоненты чувствительны к шкале измерения, теперь, чтобы исправить эту проблему, мы должны всегда стандартизировать переменные перед применением PCA. Прежде чем мы сможем применить PCA, необходимо выполнить предварительную обработку данных. Данный набор тренировок: x<sup>(1)</sup>, x<sup>(2)</sup>, ..., x<sup>(m)</sup>, необходимо привести к одной шкале соответствующими методами (масштабирование признаков/ нормализация по среднему):



<p id="gdcalert175" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image175.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert176">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image175.png "image_tooltip")


1. Вычислить ковариационную матрицу



<p id="gdcalert176" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image176.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert177">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image176.png "image_tooltip")


2. Вычислить собственные векторы ковариационной матрицы Σ

3. Взять первые k столбцов матрицы U и вычислить z.

Мы будем назначать первые k столбцов U переменной, называемой «Ur». Это будет n × k матрица. Мы вычисляем z так:



<p id="gdcalert177" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image177.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert178">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image177.png "image_tooltip")



#### Выбор количества основных компонентов

Как выбрать k, также называемое числом главных компонентов? Напомним, что k - размерность, которую мы уменьшаем до.

Один из способов выбора k состоит в следующем:



1. Учитывая среднюю квадратную ошибку проекции: 

<p id="gdcalert178" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image178.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert179">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image178.png "image_tooltip")
,
2. Также дано полное изменение данных:  

<p id="gdcalert179" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image179.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert180">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image179.png "image_tooltip")
,
3. Выберите k как наименьшее значение, такое, что: 

<p id="gdcalert180" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image180.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert181">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image180.png "image_tooltip")
.

Другими словами, квадратная ошибка проекции, деленная на общее изменение, должна быть меньше одного процента, так что 99% дисперсии сохраняется.



1. Алгоритм выбора k
2. Попробуйте PCA с k = 1,2, ...
3. Вычислить U_{r}, z, x

Проверьте приведенную выше формулу, что 99% дисперсии сохраняется. Если нет, перейдите к шагу 1 и увеличьте k. Это дает нам матрицу S. Мы можем проверить 99% сохраняемой дисперсии с использованием матрицы S следующим образом:



<p id="gdcalert181" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image181.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert182">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image181.png "image_tooltip")



#### Рекомендации по применению PCA

Наиболее распространенным применением PCA является ускорение обучения с учителем.

Учитывая набор тренировок с большим количеством функций (например, 

<p id="gdcalert182" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image182.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert183">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image182.png "image_tooltip")
), мы можем использовать PCA для уменьшения числа признаков в каждом примере обучающего набора (например, 

<p id="gdcalert183" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image183.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert184">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image183.png "image_tooltip")
).

Обратите внимание, что мы должны определить сокращение PCA от 

<p id="gdcalert184" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image184.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert185">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image184.png "image_tooltip")
 только на обучающем наборе, а не на валидационных или тестовых наборах. Вы можете применить отображение z<sup>(i)</sup> к вашим наборам перекрестной проверки и тестирования после того, как они определены в наборе обучения.

Вот некоторые из преимуществ применения уменьшения размерности к набору данных:



*   Пространство, необходимое для хранения данных, уменьшается по мере уменьшения количества измерений
*   Меньшие размеры приводят к меньшему времени вычисления / обучения
*   Некоторые алгоритмы не работают хорошо, когда в данных присутствует большая размерность. Поэтому необходимо уменьшить размерность, чтобы алгоритм был полезным
*   Он решает проблему мультиколлинеарности, удаляя избыточные признаки. Например, у вас есть две переменные - «время, затрачиваемое на беговую дорожку в считанные минуты» и «сжигаемые калории». Эти переменные сильно коррелируют, поскольку чем больше времени вы проводите на беговой дорожке, тем больше калорий вы будете сжигать. Следовательно, нет смысла хранить оба значения, поскольку только один из них делает то, что вам нужно
*   Это помогает визуализировать данные. Как обсуждалось ранее, очень сложно визуализировать данные в более высоких измерениях, поэтому сокращение нашего пространства до 2D или 3D может позволить нам более четко строить и наблюдать рисунки

Не следует использовать PCA в качестве попытки предотвратить переобучение. Мы могли бы подумать, что сокращение количества признаков с помощью PCA было бы эффективным способом решения проблемы переобучения. Это может работать, но не рекомендуется, поскольку он не учитывает значения наших результатов y. Использование только регуляризации будет по крайней мере столь же эффективным.

Не предполагайте заранее, что вам необходимо использовать PCA. Сначала попробуйте выполнить полный алгоритм машинного обучения без PCA. Затем используйте PCA, если это необходимо.


#### Обзор других методов понижения размерности

Метод главных компонент далеко не единственный метод, использующийся для понижения размерности в данных. В статье [(Sharma 2018)](https://paperpile.com/c/jyUyF3/3KBg) приводится обзор следующих широко распространенных алгоритмов:



1. Удаление отсутствующих значений (Missing Value Ratio): если в наборе данных слишком много отсутствующих значений, мы используем этот подход для уменьшения числа переменных. Мы можем отбросить переменные с большим количеством недостающих значений в них;
2. Фильтр с низкой дисперсией (Low Variance filter): мы применяем этот подход для определения и отбрасывания постоянных переменных из набора данных. Целевая переменная не подвержена чрезмерному воздействию переменных с низкой дисперсией, и, следовательно, эти переменные можно безопасно удалить;
3. Фильтр с высокой корреляцией (High Correlation filter): пара переменных с высокой корреляцией увеличивает мультиколлинеарность в наборе данных. Таким образом, мы можем использовать эту технику, чтобы найти высококоррелированные признаки и соответственно отбросить их;
4. Случайный лес: это один из наиболее часто используемых методов, который говорит о важности каждого признака, присутствующего в наборе данных. Мы можем найти важность каждого признака и сохранить самые лучшие признаки, что приведет к уменьшению размерности;
5. Методы последовательного исключения признаков и последовательного включения признаков требуют большого вычислительного времени и поэтому обычно используются для небольших наборов данных;
6. Факторный анализ: этот метод лучше всего подходит для ситуаций, когда мы имеем сильно коррелированный набор переменных. Он делит переменные на основе их корреляции в разные группы и представляет каждую группу с коэффициентом;
7. Анализ главных компонент: это один из наиболее широко используемых методов обработки линейных данных. Он делит данные на набор компонентов, которые стараются объяснить как можно большую дисперсию;
8. Анализ независимых компонент (ICA): мы можем использовать ICA для преобразования данных в независимые компоненты, которые описывают данные с использованием меньшего количества компонентов;
9. ISOMAP: Мы используем этот метод, когда данные сильно нелинейны;
10. t-SNE: Этот метод также хорошо работает, когда данные сильно нелинейны. Он отлично работает для визуализации;
11. UMAP: Этот метод хорошо работает для данных с высокой размерностью. Его время работы короче по сравнению с t-SNE.