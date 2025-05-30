---
title: "MLOps: основы мониторинга моделей машинного обучения"
classes: None
categories:
  - scipop
  - translation
  - article
tags:
  - MLOps
toc: true
excerpt: "От общего описания, к конкретике: по каким принципам и метрикам должен быть организован мониторинг моделей машинного обучения в производственном окружении?"
---

[Оригинал](https://www.kdnuggets.com/2021/01/mlops-model-monitoring-101.html)

Мониторинг моделей при помощи набора показателей эффективности необходим для создания цикла обратной связи от развернутой модели до процесса построения модели, чтобы они могли постоянно улучшаться при различных сценариях.


![alt_text](/assets/images/2021-05-07/image4.jpg "image_tooltip")


Рис 1: ML Workflow (Изображение из [martinfowler.com,](https://martinfowler.com/articles/cd4ml.html)2019)


## Введение

Модели машинного обучения определяют наиболее важные решения для бизнеса. По существу, важно, чтобы эти модели оставались актуальными в контексте самых последних данных после их внедрения в производство. Модель может выйти из контекста, если есть перекос данных, т.е. распределение данных могло измениться в производственной среде по сравнению с тем, что использовалось во время обучения. Также может случиться так, что функция становится недоступной в производственных данных или что модель больше не актуальна, поскольку реальная среда могла измениться (например, Covid19), или, что проще, поведение пользователя могло измениться. Таким образом, мониторинг изменений в поведении модели и характеристик самых последних данных, используемых при выводе, имеет первостепенное значение. Это гарантирует, что модель останется актуальной и верной с желаемым уровнем производительности, как и было обещано на этапе обучения модели.

Пример такого фреймворка мониторинга моделей показан на рисунке 2 ниже. Цель состоит в том, чтобы отслеживать модели по различным метрикам, подробности которых мы рассмотрим в следующих разделах. Но сначала давайте разберемся с задачами фреймворка мониторинга.


![alt_text](/assets/images/2021-05-07/image3.png "image_tooltip")


![alt_text](/assets/images/2021-05-07/image2.jpg "image_tooltip")


Рис. 2: Иллюстрированная структура фреймворка мониторинга моделей (изображение автора)


## Мотивация

Петли обратной связи играют важную роль во всех аспектах жизни, а также в бизнесе. Циклы обратной связи просты для понимания: вы что-то производите, измеряете информацию о производстве и используете эту информацию для улучшения производства. Это постоянный цикл мониторинга и улучшения. Все, что содержит измеримую информацию и возможности для улучшения, может включать в себя цикл обратной связи, и модели машинного обучения, безусловно, могут извлечь из этого пользу.

Типичный рабочий процесс машинного обучения включает в себя такие шаги, как прием данных, предварительная обработка, построение и оценка модели и, наконец, развертывание. Однако здесь отсутствует один ключевой аспект - обратная связь. Таким образом, основной мотивацией любой системы «мониторинга моделей» является создание этой важнейшей петли обратной связи после развертывания, возвращающейся к фазе построения модели (как показано на рис. 1). Это помогает модели машинного обучения постоянно улучшаться, принимая решение либо обновить модель, либо продолжить работу с существующей моделью. Чтобы реализовать это решение, платформа должна отслеживать и сообщать различные метрики модели (подробности в разделе «Метрики» ниже) в двух возможных сценариях, описанных ниже.



1. Сценарий I. Обучающие данные доступны, и фреймворк вычисляет указанные метрики модели как на обучающих данных, так и на производственных (логических) данных после развертывания и сравнивает их для принятия решения.
2. Сценарий II: Обучающие данные недоступны, и платформа вычисляет указанные метрики модели на основе только данных, доступных после развертывания.

В следующей таблице перечислены входные данные, необходимые для системы мониторинга моделей для отслеживания указанных показателей в двух сценариях.


![alt_text](/assets/images/2021-05-07/image5.jpg "image_tooltip")


В зависимости от того, какой из двух сценариев применим, показатели, выделенные в следующем разделе, вычисляются, чтобы решить, нуждается ли развернутая модель в обновлении или каких-либо других вмешательствах.


## Метрики

Предлагаемый перечень показателей мониторинга моделей представлен на рисунке 3 ниже. Он определяет три широких типа метрик, основанных на зависимости метрики от данных и/или модели машинного обучения. В идеале структура мониторинга должна состоять из одной или двух метрик из всех трех категорий, но если нужен компромисс, то можно строить систему показателей начиная снизу, то есть начать с операционных метрик, а затем наращивать по мере зрелости модели. Кроме того, операционные показатели должны отслеживаться в реальном времени или, по крайней мере, ежедневно, тогда как метрики стабильности и производительности могут отслеживаться на еженедельных или даже более длительных временных рамках, в зависимости от предметной области и бизнес-сценария.


![alt_text](/assets/images/2021-05-07/image1.png "image_tooltip")


Рис. 3. Стек показателей мониторинга модели (изображение автора)



1. Метрики стабильности - эти метрики помогают нам фиксировать два типа сдвигов распределения данных:
    1. Смещение априорной вероятности - фиксирует сдвиг распределения предсказанных выходных данных и/или зависимой переменной между данными обучения и производственными данными (сценарий I) или различные временные рамки производственных данных (сценарий II). Примеры этих показателей включают индекс стабильности популяции (PSI), индекс дивергенции (концептуальный сдвиг), статистику ошибок;
    2. Ковариационный сдвиг фиксирует сдвиг - распределения каждой независимой переменной между обучающие данные и производственные данные (сценарий I) или различные временные рамки производственных данных (сценарий II), если применимо. Примеры этих показателей включают в себя индекс стабильности характеристик (CSI) и индекс новизны.
2. Показатели эффективности - эти показатели помогают нам обнаружить концептуальный сдвиг в данных, т.е. определить, изменилось ли соотношение между независимыми и зависимыми переменными (например, после COVID могло измениться то, как пользователи совершают покупки во время фестивалей). Они делают это, исследуя, насколько хорошо или плохо существующая развернутая модель работает визуально, когда она была обучена (сценарий I) или в течение предыдущего периода времени после развертывания (сценарий II). Соответственно, может быть принято решение доработать развернутую модель или нет. Примеры этих показателей включают:
    3. Проектные метрики, такие как RMSE, R-Square и т. д. для регрессии и точность, AUC-ROC и т. д. для классификации;
    4. Статистики Gini и KS: статистические меры того, насколько хорошо предсказанные вероятности/классы разделены (только для моделей классификации).
3. Операционные метрики - эти метрики помогают нам определить, как развернутая модель работает с точки зрения использования. Как таковые, они не зависят от типа модели, данных и не требуют каких-либо входных данных, как в случае с двумя вышеупомянутыми метриками. Примеры этих показателей включают:
    5. Количество вызовов конечных точек ML API;
    6. Задержка при вызове конечных точек ML API;
    7. Использование ввода-вывода/памяти/процессора при выполнении прогнозирования;
    8. Время безотказной работы системы;
    9. Использование диска.


## Заключение

Мониторинг моделей в сфере MLOps стал необходимостью для зрелых систем ML. На практике необходима реализация такой системы для обеспечения согласованности и надежности системы машинного обучения, поскольку без нее системы машинного обучения могут потерять «доверие» конечного пользователя, что может быть фатальным. Таким образом, включение и планирование такого решения в общую архитектуру использования машинного обучения имеет первостепенное значение.

В следующих блогах этой серии мы более подробно рассмотрим две наиболее важные метрики мониторинга модели, т.е. метрики стабильности и производительности, и увидим, как мы можем использовать их для построения нашей инфраструктуры мониторинга моделей.


## Источники



1. Д. Сато, А. Уидер, К. Виндхойзер, [Непрерывная доставка для машинного обучения](https://martinfowler.com/articles/cd4ml.html#IntroductionAndDefinition) (2019), [martinflower.com](http://martinflower.com/)
2. М. Стюарт, [Понимание сдвига набора данных](https://towardsdatascience.com/understanding-dataset-shift-f2a5a262a766) (2019), [todatascience.com](http://towardsdatascience.com/)