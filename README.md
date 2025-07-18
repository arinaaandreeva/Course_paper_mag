## Описание задачи
Цель [соревнования ]([url](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/overview))— построить модель, которая на основе рыночных признаков (features) и индикаторов (responders) будет принимать решение о совершении сделки (buy/sell/hold). Финальная метрика качества — utility score, приближённая к реальным показателям доходности в алгоритмической торговле.

### Ссылка на данные:
[Данные соревнования (Kaggle)](https://www.kaggle.com/competitions/jane-street-real-time-market-data-forecasting/data)

**Данные включают:**
* Более 100 признаков (feature_00, ..., feature_79, + производные)
* 9 целевых переменных (resp, resp_1, ..., resp_8)
* Временные и символьные идентификаторы (date, ts_id, symbol_id)
* Веса сделок для оценки качества (weight)

В файлах задаются пути к данным:
В предобработка задается путь к данным соревнования(parquet), далее обработанные данные сохраняются в parquet, к которым в дальнейшем обращаются модели
Сами модели подгружаются с помощью библиотек kagglehub и joblib

      ├── training/
      |   ├── hypothesis-1-train-size.ipynb
      │   ├── Preprocessing.ipynb 
      │   ├── boosting-as-baseline.ipynb
      │   ├── Ridge+XGB+NN.ipynb
      │   ├── ae-mlp.ipynb
      │   ├── cluster-based-regressions.ipynb
      │   ├── garch-lstm.ipynb
      │   └── 
      ├── data-analysis.ipynb
      ├── README.md


### Анализ даннных
**data-analysis.ipynb**
Описание и анализ данных

### Предобработка
**Preprocessing.ipynb** 
Выделяем достаточную для нас часть данных, делим на обучающую и валидационную выборку


### Модели
**hypothesis-1-train-size.ipynb**
Гипотеза: Для обучения достаточно 200 последних дат, увеличение тренировочной выборки не дает значительного улучшения качества моделей.
Содержание: Сравнение качества моделей при разном размере обучающей выборки (150, 200, 250, 300 временных точек) с использованием метрик R² и стандартного отклонения.

**boosting-as-baseline.ipynb**
Гипотеза: Бустинговые модели (CatBoost, LightGBM, XGBoost) могут служить эффективным бейзлайном.
Содержание: Тестирование и сравнение производительности различных бустинговых алгоритмов на финансовых данных, анализ их способности предсказывать волатильность.


**Ridge+XGB+NN.ipynb**
Гипотеза: ансамлю из моделей бустинга, ridge и mlp превосходит в качестве модели, так как моделируют разные зависимости и дополняют друг друга
Модели: 
* https://www.kaggle.com/models/peach785/js-with-lags-trained-xgb
* https://www.kaggle.com/models/peach785/bayes_ridge

**ae-mlp.ipynb**
Гипотеза: Использование автоэнкодера для предварительного выделения признаков в сочетании с MLP улучшает качество прогнозирования.
Содержание: Реализация и оценка гибридной модели AE-MLP, сравнение с традиционными методами, анализ влияния снижения размерности на качество прогноза.
Модели:
* scaler for data preprocess https://www.kaggle.com/models/peach785/scaler_new/Other/scaler_new/1
* https://www.kaggle.com/models/peach785/ae_mlp_js24_v2

**cluster-based-regressions.ipynb**
Гипотеза: Кластеризация временных рядов по схожести финансовых показателей улучшает результаты прогнозирования.
Содержание: Применение методов кластеризации (GMM, feature-based) и построение отдельных регрессионных моделей для каждого кластера, оценка эффективности подхода.
Модели: 
* https://www.kaggle.com/models/peach785/clustering_6groups_js24_v2
* https://www.kaggle.com/models/peach785/clustering_3groups_js24
* https://www.kaggle.com/models/peach785/cluster_based_linear


**garch-lstm.ipynb**
Гипотеза: Комбинация GARCH-модели волатильности с LSTM улучшает прогнозирование финансовых временных рядов.
Содержание: Реализация гибридной модели GARCH-LSTM, анализ ее способности учитывать изменчивость данных по сравнению с чистой LSTM.


      Модели скачиваются с помощью
      import kagglehub
      path = kagglehub.model_download("path")
      joblib.load(f'{path}/name.pkl')


### Notebooks for submitions
1. **predicting-js-boosting.ipynb** для бустинга
2. **submission-ae-mlp.ipynb** для AE MLP.
3. **xgb-nn-tabm-ridge-ae-mlp.ipynb**. Ансамбль xgb+nn+tabm+ridge+ae-mlp. (xgb+nn+tabm+ridge) модель с самым высоким score.
4. **boost-nn-online-retraining.ipynb; online-retrain-ae-mlp.ipynb** При тесте поступает много новых данных, поэтому во время сабмита модели можно дообучать, дообучение было включено в сабмит для бустинга и для ae mlp.




