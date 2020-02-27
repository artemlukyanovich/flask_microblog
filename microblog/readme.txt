https://habr.com/ru/post/346340/

Остановился на:
Регистрация пользователя


Запуск:
export FLASK_APP=microblog.py
flask run

Миграция:
flask db init
flask db migrate( -m "users table")
flask db upgrade
downgrade flask db - для отмены последней миграции

Если в любое время во время работы над сеансом произошла ошибка, вызов db.session.rollback()отменяет сеанс и удаляет любые изменения, сохраненные в нем

При добавлении поста можно вместо user_id указать author=User.query...
(в таблице пользователей в столбце "posts"(db.relationship) backref="author")

g: Документация Flask-SQLAlchemy

shell:
FLASK_APP=microblog.py flask shell - это работает у меня
flask shell - это указано в статье
 ...и команды, к примеру: >>> db


is_authenticated: свойство, которое имеет значение True, если пользователь имеет действительные учетные данные или False в противном случае.

is_active: свойство, которое вернет True, если учетная запись Пользователя активна или False в противном случае.

is_anonymous: свойство, которое вернет False для обычных пользователей, и True, если пользователь анонимный.

get_id(): метод, который возвращает уникальный идентификатор пользователя в виде строки (unicode, если используется Python 2)

***Если занят порт:
>>netstat -tupln
>>kill -9 <copied pid>

Обратите внимание, что некоторые расширения веб-браузера, такие как Ghostery, блокируют изображения Gravatar, поскольку они считают, что Automattic (владельцы Gravatar) могут определять, какие сайты вы посещаете, на основе запросов, которые они получают для вашего аватара. Если вы не видите аватары в своем браузере, скорее всего проблема в расширениях браузера.

После добавления двух новых полей в модель пользователя необходимо осуществить миграцию:
>>flask db migrate -m "new fields in user model"
>>flask db upgrade

Режим отладки - при выключенном приложении (либо перезапустить после ввода):
>>export FLASK_DEBUG=1


Существует два подхода к проверке работоспособности этой функции. Самый простой способ — использовать SMTP-сервер отладки от Python. Это ложный почтовый сервер, который принимает сообщения электронной почты, но вместо их отправки выводит их на консоль. Чтобы запустить этот сервер, откройте второй сеанс терминала и запустите на нем следующую команду:
(venv) $ python -m smtpd -n -c DebuggingServer localhost:8025

Оставьте запущенный SMTP-сервер отладки и вернитесь к своему первому терминалу и установите export MAIL_SERVER = localhost и MAIL_PORT = 8025 (используйте set вместо export, если вы используете Microsoft Windows). Убедитесь, что для переменной FLASK_DEBUG установлено значение 0 или не установлено вообще, так как приложение не будет отправлять электронные письма в режиме отладки.
Запустите приложение и вызовите ошибку SQLAlchemy еще раз, чтобы узнать, как сеанс терминала, на котором работает поддельный почтовый сервер, показывает электронное письмо с полным содержимым стека ошибки.

Второй метод тестирования для этой функции — настроить настоящий почтовый сервер. Ниже приведена конфигурация для использования почтового сервера для учетной записи Gmail:
export MAIL_SERVER=smtp.googlemail.com
export MAIL_PORT=587
export MAIL_USE_TLS=1
export MAIL_USERNAME=<your-gmail-username>
export MAIL_PASSWORD=<your-gmail-password>

Если вы не знакомы с категориями ведения журнала, это DEBUG, INFO, WARNING,ERROR и CRITICAL в порядке возрастания степени тяжести.

Глава 8. После изменения в базе данных осуществить миграцию:
>>flask db migrate -m "followers"
>>flask db upgrade

Примеры команд:
user1.followed.append(user2)
user1.followed.remove(user2


>>pip install flask-mail

в одном окне терминала для теста:
(venv) $ python -m smtpd -n -c DebuggingServer localhost:8025
в другом:
(venv) $ export MAIL_SERVER=localhost
(venv) $ export MAIL_PORT=8025
(venv) $ export FLASK_DEBUG=0

Чтоб настроить гугл почту:
(venv) $ export MAIL_SERVER=smtp.googlemail.com
(venv) $ export MAIL_PORT=587
(venv) $ export MAIL_USE_TLS=1
(venv) $ export MAIL_USERNAME=<your-gmail-username>
(venv) $ export MAIL_PASSWORD=<your-gmail-password>


Чтоб проверить письмо:

в одном окне терминала:
(venv) $ python -m smtpd -n -c DebuggingServer localhost:8025

в другом:
(venv) $ export MAIL_SERVER=localhost
(venv) $ export MAIL_PORT=8025
(venv) $ export FLASK_DEBUG=0

И через flask shell:
(тут почему-то работает через команду именно flask shell)

>>> from flask_mail import Message
>>> from app import mail
>>> msg = Message('test subject', sender=app.config['ADMINS'][0],
... recipients=['your-email@example.com'])
>>> msg.body = 'text body'
>>> msg.html = '<h1>HTML body</h1>'
>>> mail.send(msg)


token:
pip install jwt
pip install pyjwt - до этого у меня не работали методы jwt

Остановился на:
Поскольку эти токены принадлежат пользователям, я собираюсь написать функции генерации и проверки токена как методы в модели User:
