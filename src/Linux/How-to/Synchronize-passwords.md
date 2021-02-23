# Синхронизация паролей

## Ключ GPG

### Создание

1. Генерация ключа
~~~~
$ gpg --full-generate-key
~~~~

2. Проверяем сгенерированный ключ
~~~~
$ gpg -k --keyid-format LONG
~~~~

###  Бэкап

Очень важно создать копии ключей и сохранить их на разных носителях безопасном месте.

Экспорт публичного ключа
~~~~
$ gpg --export -a exynil@gmail.com > public.pgp
~~~~

Экспорт секретного ключа
~~~~
$ gpg --export-secret-key -a exynil@gmail.com > secret.pgp
~~~~

Создаем сертификат отзыва
~~~~
gpg --gen-revoke -a exynil@gmail.com > revocation_cert.pgp
~~~~

### Удаление главного ключа

3. Экспортируем `sub` ключ
~~~~
$ gpg --export-secret-subkey -a "exynil@gmail.com" > sub_key.pgp
~~~~

4. Удлаляем главный ключ
~~~~
$ gpg --delete-secret-key "exynil@gmail.com"
~~~~

5. Импортируем `sub` ключ
~~~~
$ gpg --import sub_keys.pgp
~~~~

6. Проверяем
~~~~
$ gpg -K
~~~~

> знак `#` рядом с `sec` означает что primary часть секретного ключа отсутствует в нашей связке ключей.

## Настройка pass

1. Инициалиализируем `pass`

~~~~
$ pass init 833C48F952F07A96
~~~~

> - `833C48F952F07A96` - это идентификатор `sub` ключа который мы ранее создали
> - Все пароли  в pass будут шифроваться ключом под идентификатором `833C48F952F07A96`
> - Появится директория `~/.password-store` с файлом `.gpg-id`
> - В файле `gpg-id` будет храниться идетификатор `sub` ключа

## Настройка GIT

```
git config --global user.name "Maxim Kim"
git config --global user.email "exynil@gmail.com"
```

## Настройка репозитория

1. Создаем приватный репозиторий на гитхаб

2. Инициализируем git в директории  `~/.password-store`

~~~
$ git init
~~~

~~~~
$ git remote add origin https://github.com/exynil/password-store.git
~~~~

~~~~
$ git add .
~~~~

~~~~
$ git commit -m "initial commit"
~~~~

~~~~
$ git push origin master
~~~~

## Настройка смартфона

1. На смартфон устанавливаем две программы 

[Password Store](https://f-droid.org/ru/packages/dev.msfjarvis.aps/) - для управления пароля в смартфоне
[OpenKeychain](https://f-droid.org/en/packages/org.sufficientlysecure.keychain/) - для управления ключами

### OpenKeychain

1. Копируем экспортированный `sub` ключ на телефон

2. В приложении OpenKeychain импортируем `sub` ключ

###  Password Store

1. Настраиваем репозиторий в Password Store

репозиторий: `git@github.com:exynil/password-store.git`
тип авторизации: `ssh`

> Приложение предложит сгенерировать пару `ssh` ключей

2. Сгенерированный ключ добавляем в `github`

### хештеги:  #pass #gpg #шифрование  #пароль #безопасность