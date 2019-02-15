Среда: node 9, husky, ebaymag, zsh

1. Падает скрипт под мак. Лечится изменением
   var child = spawn(path.join(\_\_dirname, 'hookah-mac'), command_args);
2. Нужно явно выдавать права на выполнение папке со скриптами. Если прав нет, все прекомит чеки будут молча фейлиться
3. Судя по ридми нужно запускать 'hookah install' на самом деле 'npm hookah install'
4. Для любителей yarn можно добавить вот такой вариант установки `yarn add -D @arkweid/hookah-js`
5. Пакет лучше ставить как dev dep т.е вот так `npm i @arkweid/hookah-js --save-dev`
6. При запуске хука `yarn run lint:js` (и всех остальных наверное тоже) пропадает подсветка консоли
7. То что создаются сразу 2 папки для хуков (.hookah и .hookah-local) немножко странно
8. Для приложенного сета скриптов получаем вот такой результат (при условии что вообще не меняем .js файлы)

   ```
   RUNNING HOOKS GROUP: pre-commit
     EXECUTE > flow
     EXECUTE > jest
     EXECUTE > lint_css
     EXECUTE > lint_js
   RUNNING LOCAL HOOKS GROUP: pre-commit (SKIP EMPTY)

   SUMMARY:
   [  OK  ] lint_css
   [  OK  ] lint_js
   [ FAIL ] flow
   [ FAIL ] jest
   ```

   пречем отсуствует консольный вывод с ошибками

8) Если запускать только lint_css и lint_js -- консолька съедает вывод этих команд
9) В случае если в lint_js или lint_css есть ошибки их все равно комитят со статусом "OK"
10) В этом репо flow и jest не настроены и должны падать. Но не делать этого молча
