# Django


Не удаётся переименовать поле в модели. Django ничего не предлагает и удаляет старое поле и создаёт новое.

Причина: Для того чтобы Django понял что поле необходимо переименовать, а не удалить. Необходимо оставить аттрибут verbose_name неизменённым.