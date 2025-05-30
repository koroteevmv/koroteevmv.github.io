---
title: "Обзор MLOps"
classes: None
categories:
  - scipop
  - translation
  - article
tags:
  - MLOps
toc: true
excerpt: "Эксперт попытался дать общую характеристику MLOps. Что это такое, зачем нужно и какие инструменты существуют?"
---

[Оригинал](https://www.kdnuggets.com/2021/03/overview-mlops.html)

Создание модели машинного обучения - это здорово, но чтобы обеспечить реальную ценность для бизнеса, эту модель нужно сделать полезной и поддерживать так, чтобы она оставалась полезной с течением времени. Рассматриваемые здесь операции машинного обучения (MLOps) - это быстрорастущая отрасль, которая включает в себя все необходимое для развертывания модели машинного обучения в производственной среде и является важным аспектом для обеспечения этой востребованной ценности.

Для создания набора данных и построения модели для конкретного приложения обычно требуется значительный опыт в области науки о данных. Но построить хорошую модель обычно недостаточно. На самом деле этого совсем недостаточно. Как показано ниже, разработка и тестирование модели - это только первый шаг.


![Жизненный цикл модели машинного обучения](/assets/images/2021-05-06/image1.jpg "Жизненный цикл модели машинного обучения")


Операции машинного обучения (MLOps) - это все, что необходимо для того, чтобы эта модель стала полезной, включая возможности для автоматизированного конвейера разработки и развертывания, мониторинга, управления жизненным циклом и руководства, как показано выше. Давайте посмотрим на каждый из них.


### Конвейер автоматизации

Создание производственной системы машинного обучения требует нескольких шагов: во-первых, данные должны пройти серию преобразований. Затем обучается модель. Обычно это требует экспериментов с различными архитектурами нейросетей и гиперпараметрами. Часто необходимо вернуться к данным и попробовать другие преобразования. Затем модель необходимо проверить с помощью модульных и интеграционных тестов. Она должна пройти тесты на предмет репрезентативности и интерпретируемости  данных и модели. Наконец, она развертывается в общедоступном облаке, локальной или гибридной среде. Кроме того, для некоторых этапов процесса может потребоваться специальный процесс согласования.

Если каждый из этих шагов выполняется вручную, процесс разработки будет медленным и нестабильным. К счастью, существует множество инструментов MLOps для автоматизации этих шагов от преобразования данных до сквозного развертывания. Когда необходимо повторение обучения, это будет полнностью автоматизированный, надежный и воспроизводимый процесс.


### Мониторинг 

Модели машинного обучения обычно работают хорошо при первом развертывании, а затем со временем работают хуже. Как [сказал](https://go.forrester.com/blogs/no-deploy-no-joy-leverage-modelops-to-operationalize-ai-and-machine-learning/) аналитик Forrester, доктор Кьелл Карлсон[:](https://go.forrester.com/blogs/no-deploy-no-joy-leverage-modelops-to-operationalize-ai-and-machine-learning/) «модель AI, как шестилетние дети во время карантина: они нуждаются в постоянном внимании... иначе что-нибудь сломается».

Крайне важно, чтобы процесс развертывания включал различные типы мониторинга, чтобы рабочие группы были предупреждены, когда снижение производительности начинает происходить. Производительность может снизиться из-за проблем с инфраструктурой, таких как неадекватный ЦП или память. Производительность также может ухудшиться, когда реальные данные, составляющие независимые переменные, вводимые в модель, начинают приобретать характеристики, отличные от характеристик обучающих данных - явление, известное как **дрейф данных**.

Точно так же модель может стать менее применимой из-за изменения условий реального мира - явления, известного как **дрейф концепций**. Например, COVID-19 отправил в небытие многие прогнозные модели поведения клиентов и поставщиков.

Некоторые компании также отслеживают альтернативные модели (например, разные архитектуры нейросетей или разные гиперпараметры), чтобы увидеть, начинает ли какая-либо из этих «претендентов» работать лучше, чем основная, продуктовая, модель.

Часто имеет смысл поставить “ограждения” вокруг решений или предсказаний, производимых моделью. Эти ограждения представляют собой простые правила, которые либо вызывают предупреждение, либо предотвращают принятие решения, либо перемещают решение в процесс, курируемый человеком.


### Управление жизненным циклом

Когда производительность модели начинает ухудшаться из-за смещения данных или модели, требуется повторное обучение модели и, возможно, реорганизация модели. Однако команде по анализу данных не следует начинать с нуля. При разработке исходной модели и, возможно, в предыдущих реконструкциях они, вероятно, протестировали множество архитектур, гиперпараметров и функций. Очень важно, чтобы все эти предыдущие эксперименты (и результаты) были записаны, чтобы команде специалистов по анализу данных не приходилось возвращаться к исходной точке. Это также важно для общения и сотрудничества между членами команды по анализу данных.


### Управление 

Модели машинного обучения используются во многих приложениях, влияющих на людей, таких как решение о предоставлении кредита, медицинский диагноз и решения о найме/увольнении. Использование моделей машинного обучения при принятии решений подвергается критике по двум причинам: во-первых, эти модели подвержены предвзятости, особенно если обучающие данные имеют проблемы с репрезентативностью по расе, цвету кожи, этнической принадлежности, национальному происхождению, религии, полу, сексуальной ориентации или другим социальным категориям. Во-вторых, эти модели часто представляют собой черные ящики, не объясняющие принимаемые ей решения.

В результате организации, использующие процесс принятия решений на основе машинного обучения, вынуждены следить за тем, чтобы их модели никого не дискриминировали и могли объяснить свои решения. Многие поставщики MLOps-решений включают инструменты, основанные на академических исследованиях (например, [SHAP](https://arxiv.org/pdf/1705.07874.pdf) и [Grad-CAM](https://arxiv.org/pdf/1610.02391.pdf)), которые помогают объяснить решения по модели, и используют различные методы, чтобы гарантировать, что данные и модели не являются предвзятыми. Кроме того, они включают тесты на предвзятость и объяснимость в свои протоколы мониторинга, потому что со временем модели могут стать предвзятыми или потерять объясняющую способность.

Организациям также необходимо постепенно формировать доверие и начинать следить за тем, чтобы текущая производительность, отсутствие предвзятости и объяснимость поддавались аудиту. Для этого требуются каталоги моделей, которые не только документируют все решения по данным, параметрам и архитектуре, но также регистрируют каждое решение и обеспечивают прослеживаемость, чтобы можно было определить, какие данные, модель и параметры использовались для каждого решения, когда модель была переобучена или иным образом изменено и кто внес каждое изменение. Для аудиторов также важно иметь возможность повторять исторические транзакции и проверять границы модели принятия решений с помощью сценариев «что, если».

Безопасность и конфиденциальность данных также являются ключевыми проблемами для организаций, использующих машинное обучение. Необходимо позаботиться о том, чтобы личная информация была защищена, а возможности доступа к данным на основе ролей необходимы, особенно для регулируемых отраслей.

Правительства по всему миру также стремятся регулировать процесс принятия решений на основе обученных моделей, затрагивающих людей. Европейский Союз первым ввел свои правила GDPR и CRD IV в этой сфере. В США несколько регулирующих агентств, в том числе Федеральный резервный банк США и FDA, создали правила, регулирующие принятие финансовых и медицинских решений на основе машинного обучения. Более всеобъемлющий нормативный акт, недавно предложенный “Закон об отчетности и прозрачности данных” 2020 года, намечен на рассмотрение Конгресса США в 2021 году. Правила, скорее всего, доработают до такой степени, что генеральному директору потребуется подтвердить объяснимость и отсутствие предвзятости в своих моделях машинного обучения.


### Ландшафт MLOps

В 2021 году, рынок MLOps стремительно растет. По данным аналитической компании Cognilytica,ожидается, что объем [рынка составит 4 миллиарда долларов](https://www.cognilytica.com/2020/04/02/infographic-the-rapid-growth-of-mlops/) к 2025 году.

В сфере MLOps есть как крупные, так и мелкие игроки. Основные поставщики платформ машинного обучения, такие как Amazon, Google, Microsoft, IBM, Cloudera, Domino, DataRobot и H2O, включают возможности MLOps в свои платформы. По данным Crunchbase, в сфере MLOps есть 35 частных компаний, которые привлекли от 1,8 до 1 млрд долларов финансирования и имеют от 3 до 2800 сотрудников в LinkedIn:


<table>
  <tr>
   <td>
   </td>
   <td>Финансирование ( млн.долл.)
   </td>
   <td>Кол-во сотрудников
   </td>
   <td>Описание
   </td>
  </tr>
  <tr>
   <td>Cloudera
   </td>
   <td>1000
   </td>
   <td>2803
   </td>
   <td>Cloudera предоставляет корпоративное облако данных для любых данных в любом месте.
   </td>
  </tr>
  <tr>
   <td>Databricks
   </td>
   <td>897
   </td>
   <td>1757
   </td>
   <td>Databricks - это программная платформа, которая помогает своим клиентам унифицировать аналитику для бизнеса, науки о данных и инженерии данных.
   </td>
  </tr>
  <tr>
   <td>DataRobot
   </td>
   <td>750
   </td>
   <td>1105
   </td>
   <td>DataRobot предлагает глобальным предприятиям технологии искусственного интеллекта и услуги по повышению рентабельности инвестиций.
   </td>
  </tr>
  <tr>
   <td>Dataiku
   </td>
   <td>246
   </td>
   <td>556
   </td>
   <td>Dataiku работает как корпоративная платформа искусственного интеллекта и машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Alteryx
   </td>
   <td>163
   </td>
   <td>1623
   </td>
   <td>Alteryx ускоряет цифровую трансформацию за счет объединения аналитики, обработки данных и автоматизированных процессов.
   </td>
  </tr>
  <tr>
   <td>H2O
   </td>
   <td>151
   </td>
   <td>257
   </td>
   <td>H2O.ai - лидер в области ИИ и автоматического машинного обучения с открытым исходным кодом, цель которого - демократизировать ИИ для всех.
   </td>
  </tr>
  <tr>
   <td>Domino
   </td>
   <td>124
   </td>
   <td>232
   </td>
   <td>Domino - это ведущая в мире корпоративная платформа для анализа данных, обеспечивающая более 20% компаний из списка Fortune 100.
   </td>
  </tr>
  <tr>
   <td>Iguazio
   </td>
   <td>72
   </td>
   <td>83
   </td>
   <td>Платформа Iguazio Data Science Platform позволяет разрабатывать, развертывать и управлять приложениями искусственного интеллекта в масштабе и в режиме реального времени.
   </td>
  </tr>
  <tr>
   <td>Explorium.ai
   </td>
   <td>50
   </td>
   <td>96
   </td>
   <td>Explorium предлагает платформу для анализа данных, основанную на расширенном обнаружении данных и разработке функций.
   </td>
  </tr>
  <tr>
   <td>Algorithmia
   </td>
   <td>38
   </td>
   <td>63
   </td>
   <td>Algorithmia - это решение для развертывания и управления моделями машинного обучения, которое автоматизирует MLOps для организации.
   </td>
  </tr>
  <tr>
   <td>Paperspace
   </td>
   <td>23
   </td>
   <td>37
   </td>
   <td>Paperspace поддерживает приложения следующего поколения, созданные на основе графических процессоров.
   </td>
  </tr>
  <tr>
   <td>Pachyderm
   </td>
   <td>21
   </td>
   <td>32
   </td>
   <td>Pachyderm - это платформа для анализа данных корпоративного уровня, которая делает реальностью объяснимый, воспроизводимый и масштабируемый AI/ML.
   </td>
  </tr>
  <tr>
   <td>Weights and Biases
   </td>
   <td>20
   </td>
   <td>58
   </td>
   <td>Инструменты для отслеживания экспериментов, повышения производительности моделей и совместной работы с результатами
   </td>
  </tr>
  <tr>
   <td>OctoML
   </td>
   <td>19
   </td>
   <td>37
   </td>
   <td>OctoML меняет способы оптимизации и развертывания моделей машинного обучения разработчиками для своих нужд ИИ.
   </td>
  </tr>
  <tr>
   <td>Arthur AI
   </td>
   <td>18
   </td>
   <td>28
   </td>
   <td>Arthur AI - это платформа, которая отслеживает продуктивность моделей машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Truera
   </td>
   <td>17
   </td>
   <td>26
   </td>
   <td>Truera предоставляет предприятиям платформу Model Intelligence для анализа машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Snorkel AI
   </td>
   <td>15
   </td>
   <td>39
   </td>
   <td>Snorkel AI нацелен на практическое применение ИИ с помощью Snorkel Flow: платформы данных прежде всего для ИИ предприятия
   </td>
  </tr>
  <tr>
   <td>Seldon.io
   </td>
   <td>14
   </td>
   <td>48
   </td>
   <td>Платформа развертывания машинного обучения
   </td>
  </tr>
  <tr>
   <td>Fiddler Labs
   </td>
   <td>13
   </td>
   <td>46
   </td>
   <td>Fiddler позволяет пользователям создавать прозрачные, объяснимые решения ИИ.
   </td>
  </tr>
  <tr>
   <td>run.ai
   </td>
   <td>13
   </td>
   <td>26
   </td>
   <td>Run:AI разрабатывает автоматизированную технологию распределенного обучения, которая виртуализирует и ускоряет глубокое обучение.
   </td>
  </tr>
  <tr>
   <td>ClearML (Allegro)
   </td>
   <td>11
   </td>
   <td>29
   </td>
   <td>Экспериментальный менеджер ML/DL и решение с открытым исходным кодом MLOps-решение для управления жизненным циклом продукта 
   </td>
  </tr>
  <tr>
   <td>Verta
   </td>
   <td>10
   </td>
   <td>15
   </td>
   <td>Verta создает программную инфраструктуру, чтобы помочь группам корпоративного анализа данных и машинного обучения (ML) разрабатывать и развертывать модели машинного обучения.
   </td>
  </tr>
  <tr>
   <td>cnvrg.io
   </td>
   <td>8
   </td>
   <td>38
   </td>
   <td>cnvrg.io - это платформа для анализа данных с полным стеком, которая помогает командам управлять моделями и строить конвейеры машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Datatron
   </td>
   <td>8
   </td>
   <td>19
   </td>
   <td>Datatron предоставляет единую платформу управления моделями для машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Comet
   </td>
   <td>7
   </td>
   <td>19
   </td>
   <td>Comet.ml - это платформа машинного обучения, разработанная, чтобы помочь специалистам-практикам и командам ИИ создавать надежные модели машинного обучения.
   </td>
  </tr>
  <tr>
   <td>ModelOp
   </td>
   <td>6
   </td>
   <td>39
   </td>
   <td>Управление, мониторинг и управление всеми моделями предприятия
   </td>
  </tr>
  <tr>
   <td>WhyLabs
   </td>
   <td>4
   </td>
   <td>15
   </td>
   <td>WhyLabs - это компания, занимающаяся наблюдением и мониторингом ИИ.
   </td>
  </tr>
  <tr>
   <td>Arize AI
   </td>
   <td>4
   </td>
   <td>14
   </td>
   <td>Arize AI предлагает платформу, которая объясняет и устраняет неполадки производственного ИИ.
   </td>
  </tr>
  <tr>
   <td>DarwinAI
   </td>
   <td>4
   </td>
   <td>31
   </td>
   <td>Технология генеративного синтеза DarwinAI «ИИ, создающая ИИ» обеспечивает оптимизированное и понятное глубокое обучение.
   </td>
  </tr>
  <tr>
   <td>Mona
   </td>
   <td>4
   </td>
   <td>11
   </td>
   <td>Mona - это платформа мониторинга SaaS для систем, управляемых данными и искусственным интеллектом.
   </td>
  </tr>
  <tr>
   <td>Valohai
   </td>
   <td>2
   </td>
   <td>13
   </td>
   <td>Управляемая платформа машинного обучения, которая позволяет специалистам по обработке данных создавать, развертывать и отслеживать модели машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Modzy
   </td>
   <td>0
   </td>
   <td>31
   </td>
   <td>Безопасная платформа ModelOps для обнаружения, развертывания, управления и управления машинным обучением в любом масштабе - более быстрое получение прибыли.
   </td>
  </tr>
  <tr>
   <td>Algomox
   </td>
   <td>0
   </td>
   <td>17
   </td>
   <td>Трансформация, основанная на искусственном интеллекте
   </td>
  </tr>
  <tr>
   <td>Monitaur
   </td>
   <td>0
   </td>
   <td>8
   </td>
   <td>Monitaur - это компания-разработчик программного обеспечения, которая обеспечивает возможности аудита, прозрачности и управления для компаний, использующих программное обеспечение для машинного обучения.
   </td>
  </tr>
  <tr>
   <td>Hydrosphere.io
   </td>
   <td>0
   </td>
   <td>3
   </td>
   <td>Hydrosphere.io - платформа для автоматизации операций AI/ML.
   </td>
  </tr>
</table>


 

Многие из этих компаний сосредоточены только на одном сегменте MLOps, таком как конвейер автоматизации, мониторинг, управление жизненным циклом или руководство.  [Некоторые утверждают,](https://www.oreilly.com/radar/why-best-of-breed-is-a-better-choice-than-all-in-one-platforms-for-data-science/) что использование нескольких лучших в своем классе продуктов MLOps лучше для проектов в области науки о данных, чем монолитные платформы. А некоторые компании создают продукты MLOps для вертикальной интеграции. Например, [Monitaur](https://monitaur.ai/) позиционирует себя как лучшее в своем классе решение для управления, которое может работать с любой платформой. Monitaur также создает специализированные решения по управлению MLOps для регулируемых отраслей, таких как страхование. (Полное раскрытие информации: я инвестор в Monitaur).

Есть также целый ряд MLOps проектов в открытым исходным кодом, в том числе:

*   **MLFlow** управляет жизненным циклом ML, в том числе эксперименты, воспроизводимость и развертывание, включает в себя реестр моделей;
*   **DVC** управляет контролем версий для проектов Ml, чтобы сделать их общедоступными и воспроизводимыми;
*   **Polyaxon** имеет возможности для экспериментирования, автоматизации жизненного цикла, командной разработки и развертывания, а также реестр моделей
*   **Metaflow** - это бывший проект Netflix по управлению конвейером автоматизации и развертыванием.
*   **Kubeflow** имеет возможности для автоматизации рабочих процессов и развертывания в контейнерах Kubernetes.

2021 год обещает стать интересным годом для MLOps. Скорее всего, мы увидим быстрый рост, колоссальную конкуренцию и, скорее всего, некоторую консолидацию.
