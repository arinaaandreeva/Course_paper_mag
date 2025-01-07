## Notebook describtions
### Models
 1. **js24-preprocessing-catboost.ipynb** - Подготовка данных, добавление лагов responder и обучение catboost
    Другие скрипты с обучением и валидацией моделей используют выходные данные из данного ноутбука с предобработкой
 3. **jane-street-ridge-xgb-nn.ipynb**  - Ансамбль моделей xgb+ridge. score = 0.0058. Модели обучены другими участниками и это публичный ноутбук. Сейчас лучший score (0.008) у ноутбука (https://www.kaggle.com/code/harutokotou/js-nnx5-xgbx5-weighted-blend-lb-0-0078)
 4. **ae-mlp.ipynb** AE MLP model. Score пока не знаю Submission выдает ошибку, хотя в логах ее нет. Что-то не так с group by symbol_id.
 5. cluster-based regression. Кластеризация происходит с помощью GMM на 3 кластера. Также есть feature_10, которая является категориальной переменной с 9 уникальными значениями. В обсуждениях выдвигалось мнение, что это сектор или т.п., а значит может попробовать использовать данный признак как обозначения кластера. Далее рассмотрели обычную линейную регрессию и нейронную сеть( с RobustScaler, LeakyReLU, dropout). для каждого объекта, принадлежащего определенному кластеру, используется модель, обученная на этом кластере. При делении на 3 кластера и линейные регрессии качество хорошее и можно использовать как одну из моделей в ансамбле.
  Аналогично, можно обучить для каждого symbol_id (инструмента), но не все инструменты есть во всех временных промежутках + на тестовых данных может появится новый инструмент.
 8. 

### Notebooks for submitions
1. **predicting-js-boosting.ipynb** для бустинга
2. **submission-ae-mlp.ipynb** для AE MLP. <ins>Не работает</ins>


