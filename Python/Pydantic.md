Для чего нужен `from_attributes = True`

~~~~python
from pydantic import BaseModel


class User(BaseModel):
    id: int
    name: str

    class Config:
        from_attributes = True


# Создание объекта User из словаря
user_dict = {"id": 1, "name": "Alice"}
user_from_dict = User(**user_dict)
print(user_from_dict.id, user_from_dict.name)  # Выведет: 1 Alice


# Создание объекта User из объекта с атрибутами
class UserData:
    def __init__(self, id: int, name: str):
        self.id = id
        self.name = name


user_obj = UserData(id=2, name="Bob")
user_from_obj = User.model_validate(user_obj)
print(user_from_obj.id, user_from_obj.name)
~~~~