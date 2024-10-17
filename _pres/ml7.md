---
# section: ml
title: "Практическое использование моделей обучения с учителем"
---

### Трансфер обучения

![](https://i.ytimg.com/vi/LAaLSdp8Q90/maxresdefault.jpg){: .align-center style="width: 60%;"}

![Заморозка слоев](https://sysblok.ru/wp-content/uploads/2023/03/image1.jpg){: .align-center style="width: 60%;"}

![](https://www.researchgate.net/profile/Joao-Tavares-23/publication/351085550/figure/fig3/AS:1016156517310464@1619282001253/The-transfer-learning-and-fine-tuning-techniques-used-in-the-development-of-the-proposed_W640.jpg){: .align-center style="width: 60%;"}

![](https://skyengine.ai/se/images/blog/transfer_learning.jpeg){: .align-center style="width: 60%;"}

![](https://habrastorage.org/webt/pz/zk/xy/pzzkxyzmqf21r5rik00228zntwm.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Дообучение (fine-tuning) позволяет использовать общие модели для решения специфических задач.
1. Трансфер обучения (трансферное обучение) - это техника использования и дообучения предобученных моделей.
1. Позволяет существенно сэкономить ресурсы на обучение моделей.
1. Чаще всего применяется для нейросетей, но дообучать можно любые модели.
1. При трансфере обучения часть параметров модели может быть зафиксирована (freeze).
1. Позволяет использовать малые специфические датасеты.
1. Эффективность трансфера зависит от схожести задач.
1. Модель может быть обучена надругой задаче, припомощи обучения без учителя или другими произвольными техниками.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Векторизация данных

![Извлечение аудиопризнаков](https://www.mdpi.com/sensors/sensors-21-03434/article_deploy/html/images/sensors-21-03434-g001.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Для подачи данных на вход модели машинного обучения они должны быть представлены как вектор действительных чисел.
1. Векторизация - процесс преобразования данных из исходного формата в числовой вектор.
1. Существует много различных методов векторизации. Для разных задач могут подойти разные.
1. Методы векториации зависят от модальности входных данных.
1. Векторизация должна как можно более явно представлять значимую информацию из данных.
1. Эквивалентно извлечению признаков из данных.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Векторизация естественного текста

![Кодировка символов](https://res.cloudinary.com/practicaldev/image/fetch/s--LIPiEtU2--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_800/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rjngem130a8cqbgmn46u.jpg){: .align-center style="width: 60%;"}

![Азбука Морзе](https://www.dogsbody.com/wp-content/uploads/2019-11-27_11h32_06.png){: .align-center style="width: 60%;"}

![Мешок слов](https://i.postimg.cc/pLvhy7zs/basicbow.png){: .align-center style="width: 60%;"}

![Матрица мешка слов](https://i.postimg.cc/LsBRs9js/binarybow.jpg){: .align-center style="width: 60%;"}

![Косинусное расстояние](https://i.postimg.cc/DzSnKShk/cosine-similarity-vectors-original.jpg){: .align-center style="width: 60%;"}

![N-граммы](https://i.postimg.cc/ZncZPgp4/8ARA1.png){: .align-center style="width: 60%;"}

![Формула TF-IDF](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQoTUJIiJJPO7rKZCWDB-YI0dibskN9K9zZHtP7ARH9Ow&s){: .align-center style="width: 60%;"}

![Матрица TF-IDF](https://media.licdn.com/dms/image/D4D12AQF8sI1V68UsIQ/article-cover_image-shrink_600_2000/0/1677509695129?e=2147483647&v=beta&t=pDHLFUdBEFMD3q6K0eNgg_C_zPYYYxikomIN00cfTuo){: .align-center style="width: 60%;"}

```py
vectorizer = CountVectorizer()
bow = vectorizer.fit_transform(corpus)
vectorizer.vocabulary_
bow.toarray()
```

```
array([[0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1],
       [0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 1, 0],
       [0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1],
       [1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0]])
```

{% capture notice %}
Выводы:
1. Есть много разных способов представить текст в виде чисел.
1. Мешок слов (bag of words) представляет документ в виде вектора слов. 
1. Извлекает информацию о частотеслов в тексте. Позволяет сравнивать тематику текста.
1. Словарь составляется по обучающей выборке.
1. Для учета контекста часто используются N-граммы. Глубину контекста нужно подбирать.
1. На практике вместо слов используются токены.
1. Минусы - расход памяти, ортогональность токенов, нет учета схожести смысла слов.
1. TF-IDF используется для выделения специфических токенов документа, отличающихся от других документов корпуса.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Текстовые эмбеддинги

![Идея эмбеддингов](https://corpling.hypotheses.org/files/2018/04/3dplot-500x381.jpg){: .align-center style="width: 60%;"}

![Пространство латентных признаков](https://i.postimg.cc/zv5V5FWJ/embed.webp){: .align-center style="width: 60%;"}

![Отношения в Word2vec](https://i.postimg.cc/fLGfqNnV/word2vec.png){: .align-center style="width: 60%;"}

![Вектора Word2vec в пониженной размерности](https://www.kaggleusercontent.com/kf/119787565/eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0JDLUhTMjU2In0..gPdZNtpS523_qf02fcYzxQ.KynYAD_V7j-GXwyiWpyggCW9n6lY2358CduzhIz09SdaoOsnAU-E9AwA0bHtMUh1dtal1rmO8ahuh8MBJa2-Nn3YMPaQzgOIBN87wazVjt7xYmUnF8VCsGxLuvYjm0PfL0OByFn-fgCi-YHOH_uWN5WqkLyp-4Xo-ShbN_AtYlnrOam2r2x-Fts2t67JMZ2QB8eB9Y7qXUSpDItgJ6VPNE4utD7GymhQkk5Kb7fCoBmv_MyPYAZydQomgK4wyfUoUnsLFF8J9kzLan0wjKRP5FKr0R7e6CigXh1TOvFRG5oSqhRG55fowBFMSWa9Kekzaj6o6EJNFKCZa4q2nlAZ4ZlMb8NY8PbmL-gIam_yLJdfF_zNJDHVnTcNO9uyQTPf-FA0nnk8bytMUqpRJHy3nKFYjAFLm5I3VbQXdlqCQHDHrqQT1lNnw3BJtsMD-Ot-deIv6YBALjiVIu7tRvgrBOnFV-nQY7qZ1MiHEuen24Z-3twZSsgBF1kjKd5W3vI1hpuo1IVCiaM84tWOLc7AnZc9PxCXYd_7rh0FN2hlLP_fYiHaORVaWFzo8DYsi1wb9mvoectHNKWUuGFOFPybxKAh97Nmr7toWM1RdpBb4CpATsu9v_9AVDd52JNZAEVkgibYlzs0Ast1kUeztbrJsg.DJh7kHz4tRC10TRfg_s-ZA/__results___files/__results___16_0.png){: .align-center style="width: 60%;"}

![Обучение Word2vec](https://i.postimg.cc/PfZQNzqb/cbow.png){: .align-center style="width: 60%;"}

![Обучение Word2vec](https://i.postimg.cc/ydNHPN2T/skipgram.png){: .align-center style="width: 60%;"}

![Использование Word2vec](https://habrastorage.org/getpro/habr/post_images/85d/ad8/627/85dad8627ae6845b62f5bb965c291b19.png){: .align-center style="width: 60%;"}

![BERT](https://images.prismic.io/turing/65a53f447a5e8b1120d5891f_BERT_NLP_model_architecture_d285530efe.webp?auto=format,compress){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Текстовый эмбеддинг - это короткое и плотное векторное представление токенов, которое стремится учесть семантику.
1. Основываются на гипотезе о том, что семантически схожие слова употребляются в схожих контекстах.
1. Используют пространство латентных признаков. Размерность варьируется от 50 до 1000.
1. Модель Word2vec (2013) использует предобученную нейросеть, чтобы получать эмбеддинги с семантическими операциями суммы и разности.
1. Word2vec обучается на двух задачах частичного обучения с учителем. Используется для векторизации текстов.
1. Текстовые эмбеддинги позволяют существенно повысить эффективность моделей анализа естественных текстов.
1. Модель BERT (2018) более сложна и использует нейросеть сложной архитектуры. Контекстно-зависимая. Размерность - 768 или 1024.
1. 
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Векторизация графических данных

### Ансамблирование моделей

![Ансамбль](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/627d12343ba5be3ca8ceb31c_61f7bbd4e90cce440b88ea32_ensemble-learning.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Ансамблевое обучение - техника обучения нескольких моделей на одной и той же задаче с целью повышения предсказательной эффективности.
1. Ансамбль - набор нескольких моделей машинного обучения и способ их комбинирования и обучения. 
1. Ансамблирование - способ повысить эффективность за счет повышения вычислительной сложности.
1. Используется как в обучении с учителем, так и без него.
1. Ансамбль выступает как единая модель с входом и выходом. Техника обучения аналогичная.
1. Ансамбли также могут переобучаться и недообучаться.
1. Работает закон убывания отдачи в построении ансамбля.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Беггинг

![Беггинг](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61a4414d28946a3ac3e69ed9_q-FrlRMLk-5nSxZ_3ONlFpu5hQ61PsuAxkusTD1vEX5NqkdH2Ie0u_75rIySTZKXVI4VBxM-AIw3APQvRboG3kv-3l3cA5c5qyMwwTMe2OLXzoAgA051Dqbx7XVfdJaDyNwrSLUf.png){: .align-center style="width: 60%;"}

```py

clf1 = LogisticRegression(random_state=1)
clf2 = RandomForestClassifier(n_estimators=50, random_state=1)
clf3 = GaussianNB()

eclf = VotingClassifier(
    estimators=[('lr', clf1), ('rf', clf2), ('gnb', clf3)],
    voting='hard')
```

```py
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier

tree = DecisionTreeClassifier()
bagging_clf = BaggingClassifier(base_estimator=tree, 
                                n_estimators=1500, 
                                random_state=42)
bagging_clf.fit(X_train, y_train)
```

{% capture notice %}
Выводы:
1. Беггинг (Bagging, bootstrap aggregating) - метод обучения нескольких моделей на подвыборках обучающей выборки.
1. Обучающая выборка разделяется на подмножества с повторениями. На каждом подмножестве обучается своя модель.
1. Комбинирование предикторов осуществляется усреднением либо голосованием.
1. Беггинг без ресемплинга - это простой голосующий ансамбль.
1. Голосование может быть жестким или мягким.
1. Существенно уменьшает вариативность моделей. ТАким образом борется с переобучением (ошибки усредняются).
1. Итоговая модель менее чувствительна к аномалиям и ошибкам в данных.
1. Обучение предикторов можно распараллелить.
1. Минусы - потеря интерпретируемости, вычислительная сложность.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Стекинг

![Стакинг](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61a4414dba9e9f94d7b31368_RhQ6ctlYepNo3J-yChyk_jLM_siHT9eGIJTpcI0NEPhADEcGic31JW4TWwLLzWv0LvqyDjFx9yQ8m16kKENTtPZeW-fY-9z6k7m-rsmPseGIeHhB-IiI0V5t4hImEPZRnEWPChAo.png){: .align-center style="width: 60%;"}

```py
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.ensemble import StackingRegressor
final_estimator = GradientBoostingRegressor(
    n_estimators=25, subsample=0.5, 
    min_samples_leaf=25, max_features=1,
    random_state=42)
reg = StackingRegressor(
    estimators=estimators,
    final_estimator=final_estimator)
```

{% capture notice %}
Выводы:
1. Стакинг (стекинг, stacking, Stacked generalization) - аналогично беггингу, но с добавлением метапредиктора (модель второго порядка).
1. Метапредиктор использует выходы ансамблевых предикторов как входные данные.
1. При стекинге используется разбиение обучающего набора на K фолдов, как при кросс-валидации.
1. Из-за комбинации преимуществ разных моделей способен существенно повысить точность.
1. Обучается дольше из-за органиченности параллелизации.
1. Склонен к переобучению из-за наличия модели второго порядка.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Бустинг

![Бустинг](https://i0.wp.com/neptune.ai/wp-content/uploads/2022/10/When-to-Choose-CatBoost-Over-XGBoost-or-LightGBM-Practical-Guide_13.png?resize=771%2C431&ssl=1){: .align-center style="width: 60%;"}

![Бустинг](https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61a4414d5e568a661fb7896c_mji7xyiAlyQAdxQde14HY1OVvAVzDyyKhDOo4a4bg53_m2OHUvHhMGexaHuHCfKGRVQQlfFlihuodX7LD5hugPgGw8ZzJV4bHjHc648Zr0LyVr2I0i6ciJvJri_OFCuQpOf81xcn.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Идея бустинга - в последовательном анализе данных моделями из ансамбля.
1. Первая модель ансамбля обучается на всей выборке.
1. Следующая модель получает лишь те данные, на которых предыдущая модель ошиблась.
1. Последующие модели могут исправлять ошибки предыдущих. 
1. Моделям присваиваются веса в зависимостиот их эффективности. 
1. Может понижать смещение моделей.
1. В качестве предикторов обычно берутся простые модели с высоким смещением и низкой вариацией.
1. Из-за последовательной обработки данных, вычислительно сложен.
1. Чувствителен к выбросам и аномалиям.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Случайный лес

![Случайный лес](https://vitalflux.com/wp-content/uploads/2022/03/random-forest-classifier-1-640x471.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Случайные лес - это беггинг над набором деревьев решений.
1. Деревья решения имеют высокую вариацию, которую может снизить беггинг.
1. В случайном лесе обычно используется семплирование как по строкам, так и по столбцам.
1. Используется как для классификации, так и для регрессии.
1. Менее подвержены переобучению.
1. Чем больше количество дереьев, тем больше регуляризационный эффект.
1. Можно настраивать максимальное количество признаков для индивидуальных деревьев.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### Градиентный бустинг

![Адаптивный бустинг](https://almablog-media.s3.ap-south-1.amazonaws.com/image_28_7cf514b000.png){: .align-center style="width: 60%;"}

![Градиентный бустинг](https://almablog-media.s3.ap-south-1.amazonaws.com/image_43_deeb0633cc.png){: .align-center style="width: 60%;"}

{% capture notice %}
Выводы:
1. Адаптивный бустинг (AdaBoost) присваивает веса точкам обучающей выборки в зависимости от того, правильно ли они были распознаны первыми классификаторами.
1. Последующие классификаторы фокусируются на "сложных" случаях пропорционально весам.
1. Адаптивный бустинг зачастую применяется для задач бинарной классификации.
1. Граиентный бустинг (GBM) передает в последующие модели величину отклонения предыдущих моделей.
1. Градиентный бустинг использует деревья решений в качестве индивидуальных предикторов.
1. XGBoost - это параллелизуемая высокоэффективная реализация градиентного бустинга.
1. XGBoost может обрабатываеть большие объемы данных. 
1. XGBoost склонен к переобучению, но использует регуляризацию.
1. XGBoost достаточно требователен к объему оперативной памяти. 
1. Другие ивестные реалиации - LightGBM, CatBoost
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

#### CatBoost

### Конвейеризация моделей

![](https://onnx.ai/sklearn-onnx/_images/blockdiag-0e2bbe287bfc020181cb7981832f234c906f12a6.png{: .align-center style="width: 60%;"}

```py
from sklearn.pipeline import Pipeline
from sklearn.svm import SVC
from sklearn.decomposition import PCA
pipe = Pipeline([('reduce_dim', PCA()), 
                 ('clf', SVC())])
pipe.fit(iris.data, iris.target)
```

```py
numeric_features = [0, 1, 2] # ["vA", "vB", "vC"]
categorical_features = [3, 4] # ["vcat", "vcat2"]

classifier = LogisticRegression(C=0.01, ...)

numeric_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ('onehot', OneHotEncoder(sparse_output=True, handle_unknown='ignore')),
    ('tsvd', TruncatedSVD(n_components=1, algorithm='arpack', tol=1e-4))
])

preprocessor = ColumnTransformer(
    transformers=[
        ('num', numeric_transformer, numeric_features),
        ('cat', categorical_transformer, categorical_features)
    ])

model = Pipeline(steps=[
    ('precprocessor', preprocessor),
    ('classifier', classifier)
])
```

```py
simple_imputer = SimpleImputer(strategy='median')
std_scaler = StandardScaler()

pipe_num = Pipeline([('imputer', simple_imputer), ('scaler', std_scaler)])

s_imputer = SimpleImputer(strategy='constant', fill_value='unknown')
ohe_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
pipe_cat = Pipeline([('imputer', s_imputer), ('encoder', ohe_encoder)])

col_transformer = ColumnTransformer([
    ('num_preproc', pipe_num, 
        [x for x in features.columns if features[x].dtype!='object']),
    ('cat_preproc', pipe_cat, 
        [x for x in features.columns if features[x].dtype=='object'])])

final_pipe = Pipeline([('preproc', col_transformer),
                       ('model', model)])

final_pipe.fit(features_train, target_train)
preds = final_pipe.predict(features_test)
```

```py
from numpy.random import randint
from sklearn.base import BaseEstimator, TransformerMixin


class CustomTransformer(BaseEstimator, TransformerMixin):
    def fit(self, X, y=None):
        return self

    def transform(self, X, y=None):
        # Perform arbitary transformation
        X["random_int"] = randint(0, 10, X.shape[0])
        return X
```

```py
import pandas as pd
from sklearn.pipeline import Pipeline


df = pd.DataFrame({"a": [1, 2, 3], "b": [4, 5, 6], "c": [7, 8, 9]})

pipe = Pipeline(
    steps=[
        ("use_custom_transformer", CustomTransformer())
    ]
)
transformed_df = pipe.fit_transform(df)
```

{% capture notice %}
Выводы:
1. Конвейер (pipeline) - это цепочка объектов sklearn, которая выступает единым объектом.
1. Конвейеры нужня для автоматизации обработки данных и машинного обучения и построения простого воспроизводимого кода.
1. Конвейер имеет единый интерфейс и может одной инструкцией применяться к разным данным.
1. В конвейер обычно объединяют операции предварительной обработки, преобразования и векторизации данных, предиктивную модель.
1. Модель обычно является последним этапом в конвейере.
1. Конвейеры удобны для тестирования гипотез.
{% endcapture %}
<div class="notice--info">{{ notice | markdownify }}</div>

### Основные этапы проекта по машинному обучению

