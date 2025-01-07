## Notebook describtions
### Models
 1. **js24-preprocessing-catboost.ipynb** - Подготовка данных, добавление лагов responder и обучение catboost
    Другие файлы с моделями используют выходные данные из данного ноутбука с предобработкой
 3. **jane-street-ridge-xgb-nn.ipynb**  - Ансамбль моделей xgb+ridge. score = 0.0058
 4. **ae-mlp.ipynb** AE MLP model. Submission выдает ошибку, хотя в логах ее нет. Что-то не так с group by symbol_id.  

### Notebooks for submitions
1. **predicting-js-boosting.ipynb** для бустинга
2. **submission-ae-mlp.ipynb** для AE MLP
