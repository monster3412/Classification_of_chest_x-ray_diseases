
🩺 Классификатор рентгеновских снимков легких

YOLOv8 модель для выявления патологий по рентгенограммам

📌 Основные возможности
🔹 Автоматическая диагностика 4 состояний:

✅ COVID-19

✅ Вирусная пневмония

✅ Помутнения легких (Lung Opacity)

✅ Норма (здоровые пациенты)

🔹 Точность:

96.3% на валидации

97.1% на тестовых данных


🎯 Примеры работы


1. Одиночный снимок

  🔍 image 1/1 /content/Normal-2.png: 256x256 Normal 1.00, Lung_Opacity 0.00, Viral Pneumonia 0.00, COVID 0.00, 594.2ms
  Speed: 50.7ms preprocess, 594.2ms inference, 0.1ms postprocess per image at shape (1, 3, 256, 256)

  💡 Результат: Normal (100.00%)


2. Пакетная обработка

  Найдено 2 изображений для обработки:

  Обработка изображений: 100%|██████████| 2/2 [00:01<00:00, 1.38it/s]

  Изображение: Lung_Opacity-5.png
  Класс: Lung_Opacity
  Уверенность: 100.00%

  Изображение: Normal-2.png
  Класс: Normal
  Уверенность: 100.00%


📊 О модели:

Архитектура: YOLOv8x-cls


⚙️ Гиперпараметры обучения

📐 Основные настройки
{
  "data": "yolo_dataset6",          # Путь к датасету
  "imgsz": 256,                     # Размер входного изображения (px)
  "epochs": 10,                     # Полное количество эпох
  "batch": 64,                      # Размер батча
  "optimizer": "AdamW",             # Оптимизатор
  "device": "cuda",                 # Использование GPU/CPU
  "amp": True                       # Mixed Precision Training
}
🎛️ Тонкая настройка

{
  "learning_rate": {
    "initial": 0.001,               # Стартовый LR
    "final": 0.00002,               # Финальный LR (lr0 * lrf)
    "warmup_epochs": 2              # Прогрев обучения
  },
  
  "regularization": {
    "weight_decay": 0.0012,         # L2-регуляризация
    "dropout": 0.23                 # Dropout слои
  },
  
  "augmentation": {
    "degrees": 0,                   # Вращение (отключено)
    "scale": 0.04,                  # Масштабирование (±4%)
    "translate": 0.07               # Сдвиг (±7%)
  }
}




Датасет:

Модель обучена на COVID-19 Radiography Database с Kaggle: https://www.kaggle.com/datasets/tawsifurrahman covid19-radiography-database



🚀 Запуск с готовой моделью:

1. Скачайте файл "Using the model Classification_of_chest_x_ray_diseases in (1).ipynb" и запустите первые 3 блока

2. Загрузите снимок рентгена одного из классов

3. Выберите функцию "prediction_for_one_image" если хотите предсказать значение 1 снимка или "prediction_for_many_images" если хотите для предсказать значение для нескольких снимков (необходимо вставить в функцию только путь до изображения)
