# TLab 2023. Domain-specific content generation

## Обзор статьи

- **Название статьи**: "DreamBooth: Fine Tuning Text-to-Image Diffusion Models for Subject-Driven Generation"

- **Авторы статьи**: Nataniel Ruiz, Yuanzhen Li, Varun Jampani, Yael Pritch, Michael Rubinstein, Kfir Aberman, _Google Research, 2022_

- **Текст статьи**: https://arxiv.org/abs/2208.12242

- **Страница проекта**: https://dreambooth.github.io/

### Тема и проблематика

**Тема статьи**: разработка новой техники для файн-тьюнинга Text-to-Image диффузионных моделей в целях повышения качества генерации изображений на основе ограниченного набора примеров (few-shot image generation).

**Проблематика**: предшествующие Text-to-Image диффузионные модели показывали слабые результаты во few-shot генерации персонализированных изображений, также им присущи такие проблемы, как переобучение и language drift.

**Актуальность**: способность к точной few-shot генерации изображений может быть очень полезна для различных приложений в компьютерном зрении — к ним относятся смена контекста, "написание" в том или ином художественном стиле, изменение ракурса, добавление различных деталей, изменение характеристик изображения.

### Идеи и результаты

**Основная идея**: представление и детальное описание новой и более эффективной техники файн-тьюнинга, которая не меняет архитектуру модели, снижает риски переобучения, language drift и улучшает subject-driven генерацию.

**Новые идеи**: концепция использования самых редких токенов из словаря в качестве уникальных идентификаторов объектов и новая функция потерь — autogenous class-specific prior preservation loss. 

**Результаты**:

- Авторы статьи создали датасет из 30 различных классов (кошки, собаки, разные неодушевленные объекты) и сравнили на нем результаты использования техники DreamBooth на основе Imagen/Stable Diffusion и еще одной техники файн-тьюнинга Textual Inversion. Качество и достоверность (fidelity) измеряли с помощью трех метрик: DINO, CLIP-I, CLIP-T. Наилучшие результаты продемонстрировало применение DreamBooth к Imagen — в этом случае сгенерированные изображения оказались ближе всех остальных к настоящим изображениям.

- У метода DreamBooth есть ряд ограничений: сложность воспроизведения некоторых контекстов, в некоторых случаях изменение контекста может повлиять на внешний вид объекта, переобучение, разные уровни сложности генерации разных объектов — неодушевленные объекты могут поддаваться генерации лучше, чем одушевленные.


## Запуск решения и дообучение весов под выбранный домен

### Setup

- Создать новую директорию, в которой будет лежать файл ```LORA_Colab.ipynb``` и папка ```data```, в которой будут лежать все необходимые наборы изображений: либо фотографии самого объекта, либо фотографии класса, к которому объект относится.
- В секции Training присвоить переменной ```IMAGES_FOLDER_OPTIONAL``` значение, соответствующее пути до директории, в которой лежат фотографии объекта
- В секции Training присвоить переменной ```PROMPT``` значение, соответствующее текстовому описанию объекта
- Если при обучении будет выставлен флаг ```--with_prior_preservation''', то в секции Training необходимо присвоить переменной ```CLASS_DIR``` значение, соответствующее пути до директории, в которой лежат фотографии класса
- Если при обучении будет выставлен флаг ```--with_prior_preservation''', то в секции Training необходимо присвоить переменной ```CLASS_PROMPT``` значение, соответствующее текстовому описанию фотографии с объектами-представителями класса
- Запустить все ячейки ноутбука ```LORA_Colab.ipynb```
- В секции Inference присвоить переменной ```INFERENCE_PROMPT``` значение, соответствующее текстовому описанию изображения, которое вы хотите получить
