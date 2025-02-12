Домашнее задание к лекции «Модули»

Важно: каждая задача выполняется в виде отдельного проекта с собственным GitHub репозиторием.

Важно: на данные задачи требование отсутствия ошибок в ESLint не распространяется (но вы можете его запустить и изучить ошибки, которые вам будут показаны).

Важно: решения должны быть построены на базе шаблона Webpack (для задач под номерами 1 и 2).

В личном кабинете на сайте netology.ru в поле комментария к домашней работе вставьте ссылки на ваши GitHub-проекты.
Webpack
Легенда

Ваш проект разросся и необходимо его разделить на модули. Модули помогают обеспечить изолированность кода и внести порядок в проект. Но для работы с модулями необходимо настроить загрузчик модулей (удостоверьтесь с помощью сервиса caniuse.com что модули поддерживаются не везде).
Описание

Используйте следующую структуру, чтобы настроить экспорт в бандл:

    каталог src:
        каталог css
            файл style.css (в качестве содержимого используйте body { color: #999; })
        каталог js
            файл app.js (в качестве содержимого используйте console.log('app worked'))
        файл index.html (шаблон для HTMLWebpackPlugin) (содержимое файла - произвольно, скрипты и стили должны подключаться автоматически, за счёт использования HTMLWebpackPlugin и MiniCssExtractPlugin)
        файл index.js (Webpack entry point)
    файл webpack.config.js
    файл package.json
    другие файлы

Убедитесь, что после экспорта, бандл запускается и работает (создайте для этого скрипт в npm, который запускает HTTP-сервер для каталога dist). HTTP-сервер выберите сами.
Import/Export
Легенда

Вы успешно настроили загрузку модулей с Webpack и сборку приложения. Пришло время всё грамотно разделить на модули!
Описание

Разделите всё приложение на модули:

    Модуль Domain - где будет храниться логика предметной области (персонажи, атаки и т.д.)
    Модуль Game - отвечающий за работу приложения (загрузку и сохранение)
    Модуль App - отвечающий за запуск приложения

Заглушки для модулей:

файл domain.js:

class Character {
}

файл game.js

class Game {
  start() {
    console.log('game started');
  }
}

class GameSavingData {
}

function readGameSaving() {
}

function writeGameSaving() {
}

файл app.js

const game = new Game();
game.start();

Организуйте:

    Из модуля domain экспорт класса Character в качестве default'ного
    В модуле game импорт класса Character
    Экспорт из модуля game класса Game в качестве дефолтного, класса GameSavingData и функций readGameSaving и writeGameSaving
    В модуле app.js одним импортом импортируйте Game, GameSavingData и функции readGameSaving, writeGameSaving (их при импорте переименуйте в loadGame и saveGame соответственно)

С самими функциями и классами ничего делать не нужно, нужно только правильно расставить инструкции import/export.