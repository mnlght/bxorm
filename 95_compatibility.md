# Обратная совместимость

С выходом объектов в модуле `main` версии `18.0.4` изменились некоторые внутренние механизмы ORM. Ситуации достаточно редкие и по не совсем корректные изначально, по сути появилось больше строгости в их обработке.

- Имена полей теперь регистронезависимы. До этого можно было описать два поля `LAST_NAME` и `last_name`, и это было бы ли разные поля. Теперь же такая сущность не сможет инициализироваться. Изменение связано с [именованными методами](70_objects.md#named) в Объектах.
- В выборке нельзя присвоить одноименный алиас в другом регистре, например getList(['select' => ['id' => 'ID']]).
- Поле `BooleanField` раньше допускало пустую строку в качестве значения, что могло привести к дальнейшему ошибочному трактованию значения. Теперь пустая строка недопустима, можно указывать true/false или значения `values`, указанные в конфигурации поля.


В объектах пока что не поддерживаются:
- Поля с сериализацей, поскольку в них существует противоречие: тип поля указывается как `StringField` или `TextField`, а фактически в нем хранится массив, что не соответствует заявленному типу. В ближайших обновлениях мы планируем добавить новый тип поля `ArrayField`.