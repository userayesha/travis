# Знакомство с Travis

<div align="center">
    <a href="https://travis-ci.com/">
        <img src="https://travis-ci.com/images/logos/Tessa-pride-4.svg" width="175">
    </a>
</div>
<br />

<div align="center">

[![Build Status](https://travis-ci.org/dwyl/learn-travis.svg?branch=master)](https://travis-ci.org/dwyl/learn-travis)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/dwyl/learn-travis/issues)
[![HitCount](https://hits.dwyl.io/dwyl/learn-travis.svg)](https://hits.dwyl.io/dwyl/learn-travis)

</div>

Наше ***краткое руководство*** по **Travis CI** (*Непрерывная Интеграция*)
для ***начинающих***

##  Индекс

1.  [Зачем](#зачем)
2.  [Что](#что)
    1.  [Основные преимущества Travis-CI](#ключевые-преимущества)
3.  [Как](#как)
    1.  [Предпосылки](#предпосылки)
    2.  [Начало работы](#начало-работы)
    3.  [Создание файлов для проекта](#создание-файлов-для-проекта)
    4.  [Определение тестов](#определение-тестов)
    5.  [Наблюдение за неудачами](#наблюдение-за-неудачами)
    6.  [Правильный код для прохождения сборки](#правильный-код-для-сборки)
4.  [Пример](#пример)
5.  [Использование переменных окружений с Travis!](#переменные-окружения)
    1. [Включение переменных окружений в вашем `.travis.yml` файле](#переменные-окружения-travis.yml)
    2. [Добавление переменных окружений в веб-интерфейс](#переменные-окружения-web-интерфейс)
    3. [Безопасные (Зашифрованные) переменные среды](#защищенные-переменные-окружения)
6.  [**Непрерывная _доставка_**](#непрерывная-доставка)
    1. [Добавление зашифрованных ключей SSH]()
7.  [Elm Lang](#elm-lang)
8.  [Elixir](#elixir-lang)
9.  [Установка Travis-CLI на Ubuntu](#установка-travis-cli-на-ubuntu)
10.  [Двигаться дальше](#двигаться-дальше)
    1.  [Дополнительно об Общей CI (Непрерывная интеграция)](#общая-ci)
    2.  [Спецификация Travis](#спецификация-travis)
    3.  [Конкуренты](#конкуренты)

<a name="зачем"></a>
## Зачем?

Тестирование вашей работы (чтобы **убедиться**, что она работает должным образом) является наиболее важной частью проекта.

![Toilet Roll Blocks Seat FAIL](https://user-images.githubusercontent.com/194400/28815447-5458823c-7699-11e7-8c65-bcf9e4569388.png "Toilet Roll Blocks Seat from Closing. Fail!")

> ***CI*** поможет тебе **тестировать рано и часто**, чтобы обнаружить "*проблемы интеграции*"
_пока не стало слишком поздно ..._
> **Travis CI** избавляет от *необходимости* использовать собственный CI, чтобы вы могли сосредоточиться на своем проекте/продукте!

<a name="что"></a>
## Что?

> **Н**епрерывная **И**нтеграция - это процесс разработки программного обеспечения
> в котором **вся работа по разработке интегрирована** в заранее определенное время
> или событие, и полученная ***работа автоматически проверена и построена***.
> Идея состоит в том, что **ошибки разработки** выявляются очень рано в этом процессе.

Если вы ***полный новичек*** в Непрерывной Интеграции (CI)
мы ***рекомендуем прочитать*** [**статью CI в Википедии**](https://ru.wikipedia.org/wiki/Continuous_integration)
и [статью о CI](https://www.martinfowler.com/articles/continuousIntegration.html) Мартина Фаулера.

**Заметка**: Оба они довольно *объемными*
но содержат всю необходимую информацию.
Прочтите их! Если у вас остались вопросы,
[*спроси*!](https://github.com/dwyl/learn-travis/issues)

<a name="ключевые-преимущества"></a>
### *Основные преимущества Travis-CI*:

- **Ничего для** ***Установки*** (Travis имеет Веб-основу,
  *А* ***Не*** ***тяжелую Java***
  *Приложение, которое вы должны разместить самостоятельно*<sup>1</sup>)
- **Бесплатно** как для *Использования* так и с **Открытым исходным кодом** (MIT Лицезция) см: https://about.travis-ci.com/
- Хорошо **интегрируется** с **GitHub** (*без лишних усилий разработчика*!)


<sup>1</sup>Мы использовали [Jenkins CI](https://jenkins-ci.org) в прошлом для *клиенских* проектов,  
и **Jenkins** имеет
[***крутое обучение***](https://shop.oreilly.com/product/0636920010326.do)
для *резработчиков-новичков*.  
**Travis** *по контрасту* ***уступает*** ему!

<a name="как"></a>
## Как?

Этот учебник займет у вас **20 минут** и ***сэкономит вам часы***
разочарования! #**БезМозгов**

<a name="предпосылки"></a>
### Предпосылки

+ **Компьютер** *с* ***установленым*** **node.js**
+ любой **текстовый редактор**
+ машина с системой Debian (Например Ubuntu)

Если у вас их нет, смотрите: https://github.com/dwyl/start-here.
Если у вас нет системы Linux, этот учебник будет по-прежнему применяться, за исключением
некоторые из используемых инструментов и главы 6.

<a name="начало-работы"></a>
### Начало работы

Подпишитесь на [Travis Getting Started](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci/) руководство:

> Посетите: https://travis-ci.com/ и нажмите "**Войти через GitHub**" "регистрация" не требуется.

![Travis Login with GitHub](https://user-images.githubusercontent.com/7784660/42061902-fed5be72-7b2b-11e8-9f70-7c4eec7e1807.jpg "Sign in with GitHub")

> Вы будете перенаправлены на GitHub, где вам нужно нажать "**Авторизовать приложение**"

![Authorize Travis at GitHub](https://user-images.githubusercontent.com/7784660/42060974-e6384036-7b28-11e8-9aa1-1535dabe0dee.jpg "Authorize Travis GitHub")

**Заметка**: Если вы когда-нибудь захотите *остановить* доступ Travis к вашей учетной записи GitHub,
просто посетите: https://github.com/settings/applications и нажмите на *отозвать*.

> Как только вы разрешите доступ, вы будете перенаправлены обратно в Travis  
> где вам нужно будет включить конкретный репозиторий Git. 
> Вы также можете сделать это в своем профиле Travis:
https://travis-ci.com/profile

<a name="создание-файлов-для-проекта"></a>
### Создание файлов для проекта

В данном примере структура проекта и файлы, которые вам понадобятся:

```
папка_проекта
|_.travis.yml
|_hello.js
|_package.json
|_другие_файлы
```

Как только вы подключили свой проект к Travis, каждый раз, когда вы загружаете новую версию в GitHub
Трэвис будет искать файлы по всей папке вашего проекта, строить ваш проект и
запускать все тесты автоматически. Таким образом, вам не нужно указывать, какие папки
Travis должен проверить - он всегда **проверяет все**!

Но для начала, создадим файл `.travis.yml` и вставим следующий код:

```yml
language: node_js
node_js:
 - "node"
```

**.travis.yml** это основной конфигурационный файл Travis
что говорит travis-ci, что ожидать и как себя вести для нашего приложения.

В этом случае этот файл сообщает Travis, что мы запускаем *Node.js*. Не только это, оно также
говорит Travis использовать последнюю версию Node.js. Вы также можете указать конкретные
версии, если вы хотите настроить процесс сборки:

 - https://docs.travis-ci.com/user/languages/javascript-with-nodejs/
 - https://docs.travis-ci.com/user/customizing-the-build/
 
Поскольку этот конкретный файл очень важен, обязательно поместите его в
корневую папку вашего проекта и проверьте его через
[Travis-CLI](#установка-travis-cli-на-ubuntu) или через [WebLint](https://lint.travis-ci.com/).

Во вторых, давайте создадим наш `hello.js` файл путем вставки следующего кода:

```javascript
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello Travis!\n')
}).listen(1337, '127.0.0.1');
console.log('Server running at http://127.0.0.1:1337/');
```
<a name="определение-тестов"></a>
### Определение тестов

Ранее мы упоминали, что Travis запускает все тесты автоматически. Но
откуда он знает, где тесты? И какие файлы нужно запустить?

Это в файле **package.json**. Этот файл содержит элемент `scripts`, где вы можете
укажите команду `test`, которую Travis будет искать и запускать!

Создайте файл `package.json` и вставьте следующее:

```javascript
{
  "name": "learn-travis-YOURNAME",
  "description": "Simple Travis-CI check for JSHint (Code Linting)",
  "author": "your name here :-)",
  "version": "0.0.1",
  "devDependencies": {
    "jshint": "^2.6.0"
  },
  "scripts": {
    "test": "jshint hello.js"
  }
}
```

Этот файл говорит Travis запустить `jshint` в нашем файле` hello.js`.
`jshint` это программа, которая анализирует качество кода, поэтому она идеально подходит для использования теста!

Чтобы запустить тестовую команду, нам нужно установить модуль узла `jshint` из NPM:

```sh
npm install jshint --save-dev
```

Теперь вы можете запустить команду `test` *локально*, набрав `npm test` в своем терминале.

Если вы это сделаете, вы увидите, что тест не прошел. Но мы не будем знакомить тебя с Travis.
вы можете запускать тесты вручную, это работа для Travis! Давайте посмотрим, как Travis может выполнять тесты
автоматически!

<a name="наблюдение-за-неудачами"></a>
### Наблюдение за неудачами

Сохранить все файлы, которые вы только что создали и отправьте их на GitHub.
Travis автоматически просканирует ваш репозиторий и заберет
файл **.travis.yml** который сообщит Travis, что **node.js** проект/приложение
дальше Travis просмотрит файл **package.json** и проверит
запись **скрипты** (*конкретно **test**)
Travis скачает все модули, перечисленные в вашем *devDependencies*
и попытается запустить тестовый сценарий **npm test**.

В нашем случае мы просим Travis **найти** файл **hello.js**
и так как в файле отсутствовала точка с запятой в 4-й строке,
это и послужило ошибкой в процессе сборки!

```javascript
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello Travis!\n')  // Test fails here!
}).listen(1337, '127.0.0.1');
console.log('Server running at http://127.0.0.1:1337/');
```

![Travis Build Failing](https://user-images.githubusercontent.com/7784660/42061581-02169b84-7b2b-11e8-9349-fb2e2c8800f5.png "Travis Build Failing")

![Travis Build Failing Error Message](https://user-images.githubusercontent.com/194400/28815609-d7ec720c-7699-11e7-9376-56d438b1d2d8.png "Travis Build Failing Error Message")

В **строке 343** мы пропустили точку с запятой.

<a name="правильный-код-для-сборки"></a>
### Правильный код для прохождения сборки

Просто добавьте точку с запятой в 4-ю строку **hello.js**, сохраните, создайте коммит и отправьте ваши изменения:

```javascript
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello Travis!\n'); // build should pass now!
}).listen(1337, '127.0.0.1');
console.log('Server running at http://127.0.0.1:1337/');
```

И наш "**build**" теперь ***passing***!

![Travis Build Passing](https://user-images.githubusercontent.com/194400/28816018-33a38120-769b-11e7-9f2f-28b7e325e9ed.png "Travis Build Passing")

![Build Status](https://user-images.githubusercontent.com/7784660/42061710-52037982-7b2b-11e8-9e1c-1f9330e8adbf.png "Build Status: Passing")

<a name="пример"></a>
## Пример

@dwyl мы используем Travis-CI для намного *большего* чем для кодирования! Мы используем Travis-CI для
***автоматического*** запуска наших модульных/интеграционных тестов.  
Если вы новичек в ***автоматическом тестировании***, мы рекомендуем
***Полное учебное пособие для начинающих по тестированию***:

 - https://github.com/dwyl/learn-tdd  

Который покажет вам, как использовать Travis-CI
чтобы проверить ваш код, как положено!

<a name="переменные-окружения"></a>
## Использование *переменных окружений* с Travis!

> Если вы ***новичек в переменных окружений***
просмотрите наш ***вводный урок*** (*для начинающих*):
https://github.com/dwyl/learn-environment-variables/

Часто ваше прилодение **переменные окружения** для хранения
ключей, паролей или других конфидиционных данных, которые вы не захотите сложный код в вашем
коде; Travis-CI делает это **легко**:

Существует **три способа** рассказать Travis-CI о ваших переменных окружений:

<a name="переменные-окружения-travis.yml"></a>
### 1. Включение переменных окружений в вашем `.travis.yml` файле

Самый простой и явный способ перечисления переменных сред
это добавить их к вашему `.travis.yml` файлу:

```yml
language: node_js
node_js:
 - "node"
env:
- MY_VAR=EverythingIsAwesome
- NODE_ENV=TEST
```
Интересная часть - это ключ `env:`, где вы можете затем перечислить
ваши переменные среды и их соответствующие значения.

<a name="переменные-окружения-web-интерфейс"></a>
### 2. Добавление переменных окружений в веб-интерфейс

Другой способ сообщить Travis-CI о переменных сред
это добавить их в web-базу пользовательского интерфейса (Web UI)
на странице настроек вашего проекта:

![add travis-ci environment variables Web UI](https://user-images.githubusercontent.com/194400/28816067-5a2c99ee-769b-11e7-92da-c9187e0c8aa2.png)

*Заметка* как добавить переменные среды в веб-интерфейс Travis
по умолчанию они скрыты (*из журнале сборки*).
Это *не* запрещает вам случайно `console.log`
их и выстовить пароль/ключ.

Так что будьте осторожны, когда console.logging ...!

<a name="защищенные-переменные-окружения"></a>
### 3. **Безопасные** (Защищенные) переменные среды

Если вы храните конфиденциальную информацию (*такие, как ключи API или пароли базы данных*)
для использования в вашем приложении узла, ***самый лучшиее*** использовать
[travis ruby gem](https://docs.travis-ci.com/user/encryption-keys/)
для **защиты** ваших ключей:

На вашем компьютере должен быть установлен ruby,
если у вас его еще нет, мы рекомендуем установить его с
[RVM](https://stackoverflow.com/a/14182172/1148249):

```sh
\curl -L https://get.rvm.io | bash -s stable --ruby
rvm install current && rvm use current
```
После установки ruby вы можете установить **travis ruby gem**:

```sh
gem install travis
```

После установки gem вы зашифруете переменную, выполнив команду
в вашем терминале (*убедитесь, что вы находитесь в рабочем каталоге проекта*)

```sh
travis encrypt MY_SECRET=super_secret
```

Тип `yes` для подтверждения вашего проекта, после этого вы должны увидеть зашифрованную переменную:

![learn-travis-encrypted-variable](https://user-images.githubusercontent.com/194400/28816106-7ed7e1c2-769b-11e7-9601-39de2ec31e62.png)

Вставьте это в `.travis.yml` файл, сохраните, создайте коммит и отправьте на GitHub!


<a name="непрерывная-доставка"></a>
## Непрерывная _доставка_ 🚀

**Непрерывная доставка** (**НД**) это подход к программной инженерии
в которых команды производят программное обеспечение в **коротком цикле**,
обеспечение может быть **надежно выпущена** в **_любое_ время.**
Он направлен на создание, тестирование и выпуск программного обеспечения
с большей скоростью и частотой.
Такой подход позволяет сократить затраты, время и риски, связанные с внесением изменений
позволяя более добавочные обновления для применения в производстве.
Простая и посторяемая **непрерывная доставка**
важно для непрерывной поставки. <br />
https://en.wikipedia.org/wiki/Continuous_delivery

Travis-CI может помочь с **процессом развертывания**
и есть _много_ инструментов которые можно использовать для развертывания приложения(й)
для широкого спектра поставщиков "облачной инфраструктуры" или "платформ".

> _**Заметка**: мы считаем это "**современная**" тема.
Если вы еще не использовали Heroku (с крючками GitHub)
мы **настоятельно рекомендуем** использовать этот подход в **первую** очередь
см:_ https://github.com/dwyl/learn-heroku <br />
_Как только ваше приложение имеет "тягу", и вы "переросли Heroku"
(или ваш "владелец продукта/клиент" не "позволяет" вам использовать Heroku)
вернитесь к этой теме и нашему учебнику "**DevOps**:_
https://github.com/dwyl/learn-devops

### Добавление зашифрованных ключей SSH

Мы решили дать это пошаговое руководство на нашей собственном файле/страница
(_чтобы не "загромождать" основной учебник для начинающих_):
[`encrypted-ssh-keys-deployment.md`](https://github.com/dwyl/learn-travis/blob/master/encrypted-ssh-keys-deployment.md)

<br /><br />

<a name="elm-lang"></a>
## Elm-lang

@dwyl мы используем (_и **настоятельно рекомендуем**_) Elm.

> Если вы новичок в Elm см.:
[https://github.com/dwyl/**learn-elm**](https://github.com/dwyl/learn-elm)

Если вам нужн _простой_ `.travis.yml` файл для использование с проектами Elm,
пожалуйста см: https://github.com/nelsonic/photo-groove/blob/master/.travis.yml

Более подробно см. наш выпуск расследование этого:
https://github.com/dwyl/learn-travis/issues/31
(_мы посмотрели на несколько известных проектов Elm, чтобы выделить config/script_)


<a name="elixir-lang"></a>
## Elixir-lang

@dwyl мы используем (_и **настоятельно рекомендуем**_) Elixir для серверных приложений.

> Если вы новичок в Elixir пожалуйста см:
[https://github.com/dwyl/**learn-elixir**](https://github.com/dwyl/learn-elixir)

Чтобы начать работу, проекту Elixir нужны только следующие строки
в файле `.travis.yml`:

```yml
language: elixir
elixir:
  - 1.6
env:
  - MIX_ENV=test
script:
  - mix test
```

Если вам нужн _простой_ `.travis.yml` файл
для использование с проектами Elixir, пожалуйста см:
https://github.com/dwyl/hits-elixir/blob/master/.travis.yml


<a name="установка-travis-cli-на-ubuntu"></a>
## Установка Travis-CLI на Ubuntu

> Может быть полезно, если необходимо, например, зашифровать ключи в программе установки с помощью внешних
> инструментов развертывания, таких как s3, чтобы просто проверить синтаксис .travis.yml делая простую "корпию travis"
> или любые другие дополнительные операции

Процесс установки на официальной странице https://github.com/travis-ci/travis.rb#installation не хватает немного помощи и деталей.
Даже при установке пакета разработки ruby могут возникнуть проблемы.
Но процесс, кажется, работает безупречно с RVM (Ruby version manager), как описано выше: https://rvm.io/rvm/install

Просто выполните следующие команды:

```sh
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
\curl -sSL https://get.rvm.io | bash -s stable --ruby
```

теперь добавьте эту строку в конце файла ~/.bashrc:
source "$HOME/.rvm/scripts/rvm"

```sh
source ~/.bashrc
gem install travis
travis --version
```
<a name="двигаться-дальше"></a>
## Двигаться дальше

Этот урок предназначен только для первого знакомства с Travis и миром CI.
Если вам понравилось то, что вы видели до сих пор, вы можете углубиться в следующие темы
что улучшит ваше понимание CI в целом, Travis и других инструментов, поддерживающих Node.js.

<a name="общая-ci"></a>
### Дополнительно об Общей CI (Непрерывная интеграция)

- Непрерывная интеграция статья Википедии: https://en.wikipedia.org/wiki/Continuous_integration
- Статья Мартина Фаулера о CI: https://www.martinfowler.com/articles/continuousIntegration.html
- CI руководство для начинающих видео: https://vimeo.com/19596466
- Большая книга о CI: https://www.amazon.com/Continuous-Integration-Improving-Software-Reducing/dp/0321336380/

<a name="спецификация-travis"></a>
### Спецификация Travis

- Travis начало работы: https://about.travis-ci.com/docs/user/getting-started/
- Подкаст Эп.32 (Travis) видео: https://build-podcast.com/travisci/
- [@sayanee_](https://twitter.com/sayanee_)'s Подкаст GitHub: https://github.com/sayanee/build-podcast/tree/master/032-travisci
- Руководство по переменным среды Travis-CI: https://docs.travis-ci.com/user/environment-variables/

<a name="конкуренты"></a>
### Конкуренты

- Сравнение программного обеспечения CI: https://en.wikipedia.org/wiki/Comparison_of_continuous_integration_software
- Travis CI альтернативы https://www.quora.com/What-are-the-alternatives-to-Travis-CI-Are-there-any-alternative-hosted-CI-services-for-open-source-projects
- circle-ci: https://circleci.com/, [learn-circleci](https://github.com/dwyl/learn-circleci)
- codeship: https://codeship.com/, [learn-codeship](https://github.com/dwyl/learn-codeship)

<!--
<a name="todo"></a>
## TODO

- **ВСЕ** Диаграммы на Google Image Search для непрерывной интеграции ужасны!
https://www.google.com/search?q=continuous+integration&source=lnms&tbm=isch
*мы* нам либо нужно найти время, чтобы нарисовать его, либо попросить/поручить кому-нибудь сделать это для нас!
-->
