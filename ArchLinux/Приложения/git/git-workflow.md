# Git Workflow: Перенос срочных фиксов из main в develop

## Кейс: Срочный фикс в production

### Ситуация

У вас есть две ветки:
- **`main`** — стабильная ветка, которая идет в production
- **`develop`** — ветка разработки, которая идет впереди `main` с новыми фичами

**Проблема:** Обнаружен критический баг в production, который нужно срочно исправить.

**Требования:**
1. Фикс должен попасть в `main` (production)
2. Фикс должен попасть в `develop`, чтобы не потеряться при будущих merge'ах
3. История должна оставаться чистой, без избыточных merge commit'ов

### Неправильный подход (проблема)

Если использовать обычный merge для переноса фикса из `main` в `develop`:

```bash
# 1. Создать ветку от main и внести изменения
git checkout main
git checkout -b chore/update-nginx-conf
# ... внести изменения ...
git commit -m "chore: обновил конфиг nginx"

# 2. Замерджить в main
git checkout main
git merge --no-ff chore/update-nginx-conf

# 3. ❌ ПРОБЛЕМА: Замерджить ветку в develop
git checkout develop
git merge --no-ff chore/update-nginx-conf
```

**Что происходит:**
- Если ветка была создана от merge commit'а (который уже включал `develop`), то при merge в `develop` Git принесет всю историю из `main`
- В истории `develop` появятся дублирующиеся merge commit'ы
- История становится запутанной и избыточной

---

## Решение: Использование cherry-pick

### Описание подхода

**Cherry-pick** — это команда Git, которая позволяет взять конкретный коммит из одной ветки и применить его к другой ветке, создав новый коммит с теми же изменениями, но с другим хешем.

**Преимущества:**
- ✅ Чистая история — в `develop` появится только один коммит с фиксом
- ✅ Не приносит лишнюю историю из `main`
- ✅ Быстро и просто
- ✅ Изменения не теряются

### Пошаговая инструкция

#### Шаг 1: Создать ветку от main и внести изменения

```bash
# Переключиться на main
git checkout main

# Создать новую ветку для фикса
git checkout -b chore/update-nginx-conf

# Внести необходимые изменения
# Например, отредактировать файл docker/nginx.conf
vim docker/nginx.conf

# Закоммитить изменения
git add docker/nginx.conf
git commit -m "chore: обновил конфиг nginx"
```

**Важно:** Запомните хеш коммита (например, `2900060c`) или используйте `git log` для его поиска.

#### Шаг 2: Замерджить фикс в main

```bash
# Переключиться на main
git checkout main

# Замерджить ветку с фиксом
git merge --no-ff chore/update-nginx-conf

# Отправить изменения в удаленный репозиторий
git push origin main
```

#### Шаг 3: Применить фикс в develop через cherry-pick

```bash
# Переключиться на develop
git checkout develop

# Найти хеш коммита с фиксом (если не помните)
git log main --oneline | head -5

# Применить коммит через cherry-pick
git cherry-pick <commit-hash>
# Например: git cherry-pick 2900060c

# Если возникли конфликты, разрешите их и продолжите:
# git add <resolved-files>
# git cherry-pick --continue

# Отправить изменения в удаленный репозиторий
git push origin develop
```

### Пример полного workflow

```bash
# === ШАГ 1: Создание фикса ===
git checkout main
git checkout -b hotfix/nginx-config
vim docker/nginx.conf
git add docker/nginx.conf
git commit -m "chore: обновил конфиг nginx"
COMMIT_HASH=$(git rev-parse HEAD)  # Сохранить хеш коммита

# === ШАГ 2: Merge в main ===
git checkout main
git merge --no-ff hotfix/nginx-config
git push origin main

# === ШАГ 3: Cherry-pick в develop ===
git checkout develop
git cherry-pick $COMMIT_HASH
git push origin develop

# === ОПЦИОНАЛЬНО: Удалить временную ветку ===
git branch -d hotfix/nginx-config
```

### Обработка конфликтов при cherry-pick

Если при cherry-pick возникли конфликты:

```bash
# 1. Git автоматически остановит процесс
# 2. Разрешите конфликты в файлах
vim <conflicted-file>

# 3. Добавьте разрешенные файлы
git add <resolved-files>

# 4. Продолжите cherry-pick
git cherry-pick --continue

# ИЛИ отмените cherry-pick, если нужно
git cherry-pick --abort
```

### Проверка результата

После выполнения всех шагов проверьте историю:

```bash
# Проверить, что коммит есть в обеих ветках
git log main --oneline | grep "обновил конфиг"
git log develop --oneline | grep "обновил конфиг"

# Проверить, что файлы одинаковые в обеих ветках
git diff main develop -- docker/nginx.conf
# Должно быть пусто (нет различий)
```

### Визуализация результата

После правильного применения cherry-pick история будет выглядеть так:

```
main:    [merge commit] ← фикс замерджен
          |
          * [фикс: обновил конфиг nginx]

develop: * [фикс: обновил конфиг nginx] ← применен через cherry-pick
          |
          * [другие коммиты develop]
```

Оба коммита содержат одинаковые изменения, но имеют разные хеши, что нормально для cherry-pick.

---

## Когда использовать cherry-pick

✅ **Используйте cherry-pick когда:**
- Нужно перенести срочный фикс из `main` в `develop`
- Нужно применить один или несколько конкретных коммитов в другую ветку
- Важна чистота истории

❌ **Не используйте cherry-pick когда:**
- Нужно перенести всю ветку целиком (лучше использовать merge)
- Коммиты связаны друг с другом и должны идти вместе
- Работаете с публичными ветками, где уже есть другие коммиты поверх ваших

---

## Дополнительные команды

### Cherry-pick нескольких коммитов

```bash
# Применить диапазон коммитов
git cherry-pick <commit1>^..<commit2>

# Или несколько отдельных коммитов
git cherry-pick <commit1> <commit2> <commit3>
```

### Cherry-pick без автоматического коммита

```bash
# Применить изменения, но не коммитить автоматически
git cherry-pick --no-commit <commit-hash>

# Затем можно внести дополнительные изменения и закоммитить вручную
git commit -m "chore: обновил конфиг nginx (с дополнительными правками)"
```

### Просмотр изменений перед cherry-pick

```bash
# Посмотреть, что изменит cherry-pick
git show <commit-hash>

# Или с diff
git diff develop <commit-hash>
```

