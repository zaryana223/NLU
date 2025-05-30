# Разметка данных для задач понимания естественного языка (NLU) на русском языке

Здесь хранятся все файлы и коды, которые были использованы в работе с моделями. 

Данные:

ru.test_adapt.conll - 500 адаптированых тестовых данных датасета xSID-ru

ru.valid_adapt.conll - 300 адаптированных тестовых данных датасета xSID-ru

xSID-ru - датасет, перевод на русский язык датасета [xSID](https://github.com/mainlp/xsid/tree/main/data/xSID), 500 тестовых, 300 валид данных. 

озвучка_test_adapt - озвученные тест данные (500  штук), используются в тетрадке *Курсовая_работа_озвучка.ipynb*

озвучка_valid_adapt - озвученные тест данные (150  штук), используются в тетрадке *Курсовая_работа_озвучка.ipynb*, нужны для оценки качества работы модели vosk-model-small-ru-0.22 и GigaAM 

cities_test_adapt.conll - 1125 примеров, датасет с городами России, собранный с помощью *Автоматические_данные_для_разметки.ipynb*	

cities_test_adapt.raw.txt - датасет с городами России в формате raw файла 

cities_test_adapt.raw_0.conll - предсказание модели mdeberta-v3-base 

comparison_cities.csv - csv файл, где хранится правильный датасет (оригинальный) и предсказанный моделью, использовались для получения метрик из кода *Метрики.ipynb* (города России)

comparison_gigaAM.csv - csv файл, где хранится правильный датасет (оригинальный) и предсказанный моделью, использовались для получения метрик из кода *Метрики.ipynb* (тестовые данные), предсказанные данные были озвучены с помощью vosk

comparison_test_adapt.csv - csv файл, где хранится правильный датасет (оригинальный) и предсказанный моделью, использовались для получения метрик из кода *Метрики.ipynb* (тестовые данные)

comparison_vosk.csv - csv файл, где хранится правильный датасет (оригинальный) и предсказанный модели, использовались для получения метрик из кода *Метрики.ipynb* (тестовые данные_vosk), предсказанные данные были озвучены с помощью vosk

metrics_epoch_15.json - доля правильных ответов с лучшими параметрами (метрика Accuracy)

nlu.xsid_test_adapt.out - предсказания модели mdeberta-v3-base (тест данные)

nlu.xsid_test_adapt.out.eval - итоговая оценка модели на тест данных 

ru.test_vosk.raw.conll - тест данные, которые были преобразованы моделью vosk, и файл переделан в формат raw, для того чтобы текстовая модель смогла сделать предсказание

ru.test_vosk.raw_0.conll - предсказания модели mdeberta-v3-base

ru_GigaAM.raw_0.conll - предсказания модели mdeberta-v3-base

ru_GigaAM_0.raw.txt - тест данные, которые были преобразованы моделью GigaAM, и файл переделан в формат raw, для того чтобы текстовая модель смогла сделать предсказание

xSID.ipynb - фреймворк machamp, где дообучалась модель, инструкция по использованию на их [github](https://github.com/machamp-nlp/machamp/tree/master)

Автоматические_данные_для_разметки.ipynb - с помощью данного кода был получен датасет городов России, правило того как работать: 

1. examples_test (сначала отчистить от r=right) - изначальные примеры; gaps_test - то что меняем; fillers (собрать данные сразу с переводом на английский) - то на что меняем; generated_test - итог 

2. функция conjugate – ищет среди слов глагольные категории, и если в выражении есть глагол, то возвращает его без изменений; если же глаголов нет, то склоняет все слова подходящих частей речи (имена, прилагательные, числительные и т.п.) в заданный падеж, приводя их к нужной форме после поиска формы в именительном падеже
3. функция change – выполняет замену фрагмента в разметке данных NLU: находит указанный отрезок текста, удаляет исходные токены в заданных границах (по номерам строк), вставляет на их место новое выражение (согласованное по падежу), корректирует номера строк, обновляет разметку сущностей и при необходимости добавляет знаки препинания.
4. функция generation – читает информацию из трех файлов и применяет функцию change
5. функция changename – более простая функция, нужна для имен, имя оно всегда заменяет одну позицию, поэтому не нужно менять остальные блоки.
функция generationnames – меняет одно имя, затем второе, если их два, если имя одно, то одно

Курсовая_работа_озвучка.ipynb - код, где происходило преобразование речи в текст, инструкция к [GigaAM](https://github.com/salute-developers/GigaAM), инструкция к [vosk-model-small-ru-0.22](https://alphacephei.com/vosk/models). Привести все аудио к формату wav, код там имеется, закинуть две папки с тестовыми и валид данным на гугл диск, и просто запустить код, все сохраниться на гугл диске. Далее в конце подсчитать метрики WER и CER, чтобы выбрать лучшую модель. 

Метрики.ipynb - когда получили предсказания от модели, идем в данный код, берем ориг файл, который мы сделали raw, где есть id, и восстанавливаем id с помощью кода там, потом берем ориг файл и предсказание модели и делаем csv, после этого можно посчитать метрики Accuracy

