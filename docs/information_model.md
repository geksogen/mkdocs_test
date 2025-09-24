# 7 Информационная модель

## 7.1 Модель предметной области

В рамках MVP проекта были выделены основные сущности с атрибутами и определены связи между ними.

Базовыми сущностями являются:

- Клиент 
- Сотрудник 
- Меню 
- Категория_товара 
- Ингредиент 

![](../diagrams/class.jpg)

## 7.2 Модель данных

![](../diagrams/roborestaurantsdb.png)

## 7.2.1 Описание таблиц БД

### 7.2.1.1 Таблица «Клиенты» (clients)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| client_id | BIGSERIAL | Уникальный идентификатор клиента |
| phone | VARCHAR(20) | Номер телефона |
| is_loyalty_member | BOOLEAN | Участник бонусной программы |
| password_hash | VARCHAR(255) | Хэш пароля |
| created_at | TIMESTAMPTZ | Дата регистрации |
| last_login | TIMESTAMPTZ | Последний вход в систему |

### 7.2.1.2 Таблица «Сотрудники» (employees)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| employee_id | BIGSERIAL | Уникальный идентификатор сотрудника |
| first_name | VARCHAR(50) | Имя сотрудника |
| last_name | VARCHAR(50) | Фамилия сотрудника |
| role | employee_role | Роль в системе |
| login | VARCHAR(50) | Логин для входа |
| password_hash | VARCHAR(255) | Хэш пароля |
| phone | VARCHAR(20) | Контактный телефон |
| created_at | TIMESTAMPTZ | Дата приема на работу |
| is_active | BOOLEAN | Статус активности |

### 7.2.1.3 Таблица «Бонусные счета» (bonus_accounts)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| bonus_account_id | BIGSERIAL | Уникальный идентификатор счета |
| client_id | BIGINT | Владелец счета |
| bonus_type | VARCHAR(20) | Тип бонусной программы |
| balance | DECIMAL(15,2) | Текущий баланс бонусов |
| expiry_date | DATE | Срок действия бонусов |
| created_at | TIMESTAMPTZ | Дата создания счета |

### 7.2.1.4 Таблица «Действия с бонусами» (bonus_actions)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| bonus_action_id | BIGSERIAL | Уникальный идентификатор операции |
| bonus_account_id | BIGINT | Связанный бонусный счет |
| order_id | BIGINT | Связанный заказ |
| amount | DECIMAL(15,2) | Сумма операции |
| action_type | bonus_action_type | Тип операции |
| action_date | TIMESTAMPTZ | Дата операции |

### 7.2.1.5 Таблица «Категории товаров» (categories)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| category_id | BIGSERIAL | Уникальный идентификатор категории |
| name | VARCHAR(100) | Название категории |
| description | TEXT | Описание категории |
| created_at | TIMESTAMPTZ | Дата создания |
| is_active | BOOLEAN | Активность категории |

### 7.2.1.6 Таблица «Товары» (products)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| product_id | BIGSERIAL | Уникальный идентификатор товара |
| category_id | BIGINT | Категория товара |
| tech_card_id | BIGINT | Технологическая карта |
| name | VARCHAR(100) | Название товара |
| type | VARCHAR(50) | Тип товара |
| proteins | DECIMAL(10,2) | Содержание белков |
| fats | DECIMAL(10,2) | Содержание жиров |
| carbohydrates | DECIMAL(10,2) | Содержание углеводов |
| calories | DECIMAL(10,2) | Калорийность |
| description | TEXT | Описание товара |
| photo_url | VARCHAR(255) | Ссылка на изображение |
| price | DECIMAL(15,2) | Цена товара |
| is_available | BOOLEAN | Доступность для заказа |
| created_at | TIMESTAMPTZ | Дата создания |
| updated_at | TIMESTAMPTZ | Дата обновления |

### 7.2.1.7 Таблица «Комбобургеры» (comboburgers)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| comboburger_id | BIGINT | Ссылка на базовый товар |
| min_ingredients | INTEGER | Минимальное количество ингредиентов |
| max_ingredients | INTEGER | Максимальное количество ингредиентов |

### 7.2.1.8 Таблица «Меню» (menus)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| menu_id | BIGSERIAL | Уникальный идентификатор меню |
| name | VARCHAR(100) | Название меню |
| type | VARCHAR(50) | Тип меню |
| start_date | TIMESTAMPTZ | Дата начала действия |
| end_date | TIMESTAMPTZ | Дата окончания действия |
| is_active | BOOLEAN | Активность меню |
| created_at | TIMESTAMPTZ | Дата создания |

### 7.2.1.9 Таблица «Акции» (promotions)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| promotion_id | BIGSERIAL | Уникальный идентификатор акции |
| menu_id | BIGINT | Связанное меню |
| name | VARCHAR(100) | Название акции |
| description | TEXT | Описание акции |
| type | promotion_type | Тип акции |
| value | DECIMAL(15,2) | Значение акции |
| conditions | TEXT | Условия акции |
| start_date | TIMESTAMPTZ | Дата начала |
| end_date | TIMESTAMPTZ | Дата окончания |
| is_active | BOOLEAN | Активность акции |

### 7.2.1.10 Таблица «Ингредиенты» (ingredients)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| ingredient_id | BIGSERIAL | Уникальный идентификатор ингредиента |
| name | VARCHAR(100) | Название ингредиента |
| proteins | DECIMAL(10,2) | Содержание белков |
| fats | DECIMAL(10,2) | Содержание жиров |
| carbohydrates | DECIMAL(10,2) | Содержание углеводов |
| calories | DECIMAL(10,2) | Калорийность |
| image_url | VARCHAR(255) | Ссылка на изображение |
| price_per_unit | DECIMAL(15,2) | Цена за единицу |
| is_required | BOOLEAN | Обязательный ингредиент |
| is_available | BOOLEAN | Доступность ингредиента |
| created_at | TIMESTAMPTZ | Дата создания |

### 7.2.1.11 Таблица «Технологические карты» (tech_cards)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| tech_card_id | BIGSERIAL | Уникальный идентификатор карты |
| name | VARCHAR(100) | Название технологической карты |
| description | TEXT | Описание карты |
| xml_data | XML | XML-инструкции для роботов |
| version | INTEGER | Версия карты |
| is_actual | BOOLEAN | Актуальность карты |
| created_at | TIMESTAMPTZ | Дата создания |
| updated_at | TIMESTAMPTZ | Дата обновления |

### 7.2.1.12 Таблица «Состав комбобургеров» (comboburger_composition)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| composition_id | BIGSERIAL | Уникальный идентификатор состава |
| comboburger_id | BIGINT | Связанный комбобургер |
| ingredient_id | BIGINT | Связанный ингредиент |
| order_index | INTEGER | Порядок добавления ингредиента |
| price_at_time | DECIMAL(15,2) | Цена на момент добавления |
| created_at | TIMESTAMPTZ | Дата создания |

### 7.2.1.13 Таблица «Корзины» (carts)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| cart_id | BIGSERIAL | Уникальный идентификатор корзины |
| client_id | BIGINT | Владелец корзины |
| total_amount | DECIMAL(15,2) | Общая стоимость |
| created_at | TIMESTAMPTZ | Дата создания |
| updated_at | TIMESTAMPTZ | Дата обновления |
| items | JSONB | Состав корзины в формате JSON |
| items_count | INTEGER | Количество позиций |

### 7.2.1.14 Таблица «Заказы» (orders)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| order_id | BIGSERIAL | Уникальный идентификатор заказа |
| client_id | BIGINT | Клиент |
| cart_id | BIGINT | Корзина заказа |
| employee_id | BIGINT | Сотрудник (для возвратов) |
| order_number | VARCHAR(20) | Номер заказа |
| status | order_status | Статус заказа |
| created_at | TIMESTAMPTZ | Дата создания |
| receive_time | TIMESTAMPTZ | Время получения |
| delivery_method | delivery_method | Способ получения |
| payment_method | payment_method | Способ оплаты |
| total_amount | DECIMAL(15,2) | Общая сумма заказа |
| amount_to_pay | DECIMAL(15,2) | Сумма к оплате |
| bonuses_used | DECIMAL(15,2) | Использовано бонусов |

### 7.2.1.15 Таблица «Чеки» (receipts)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| receipt_id | BIGSERIAL | Уникальный идентификатор чека |
| order_id | BIGINT | Связанный заказ |
| payment_date | TIMESTAMPTZ | Дата и время оплаты |
| receipt_data | TEXT | Данные чека (замаскированные) |
| payment_status | payment_status | Статус оплаты |

### 7.2.1.16 Таблица «Роботы» (robots)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| robot_id | BIGSERIAL | Уникальный идентификатор робота |
| name | VARCHAR(100) | Название робота |
| status | robot_status | Статус робота |
| ip_address | INET | IP-адрес робота |
| last_known_state | TEXT | Последнее известное состояние |
| created_at | TIMESTAMPTZ | Дата создания |
| last_heartbeat | TIMESTAMPTZ | Последний сигнал активности |

### 7.2.1.17 Таблица «Производственные задания» (production_tasks)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| production_task_id | BIGSERIAL | Уникальный идентификатор задания |
| order_id | BIGINT | Связанный заказ |
| robot_id | BIGINT | Назначенный робот |
| status | production_status | Статус задания |
| priority | INTEGER | Приоритет выполнения |
| queue_time | TIMESTAMPTZ | Время постановки в очередь |
| start_time | TIMESTAMPTZ | Время начала выполнения |
| end_time | TIMESTAMPTZ | Время завершения |

### 7.2.1.18 Таблица «Складские записи» (stock_records)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| stock_record_id | BIGSERIAL | Уникальный идентификатор записи |
| ingredient_id | BIGINT | Связанный ингредиент |
| quantity | DECIMAL(15,3) | Количество на складе |
| unit | VARCHAR(20) | Единица измерения |
| receipt_date | TIMESTAMPTZ | Дата поступления |
| expiry_date | TIMESTAMPTZ | Срок годности |
| min_stock_level | DECIMAL(15,3) | Минимальный остаток |
| created_at | TIMESTAMPTZ | Дата создания |

### 7.2.1.19 Таблица «Журнал событий» (event_logs)
| Атрибут | Тип | Описание |
|---------|-----|----------|
| log_id | BIGSERIAL | Уникальный идентификатор записи |
| employee_id | BIGINT | Сотрудник (если применимо) |
| log_level | log_level | Уровень важности события |
| message | TEXT | Текст сообщения |
| log_data | TEXT | Данные события (замаскированные) |
| timestamp | TIMESTAMPTZ | Временная метка |

Система использует следующие перечислимые типы данных:

### employee_role - Роли сотрудников системы
- ADMIN - Администратор системы
- ASSORTMENT_MANAGER - Менеджер по ассортименту
- PRODUCTION_MANAGER - Менеджер на производстве
- STOREKEEPER - Кладовщик
- CASHIER - Кассир

### order_status - Статусы выполнения заказов
- CART - Товары в корзине
- PENDING_PAYMENT - Ожидает оплаты
- PAID - Оплачен
- IN_PROGRESS - В процессе приготовления
- READY - Готов к выдаче
- COMPLETED - Выдан клиенту
- CANCELLED - Отменен
- REFUND - Возврат средств

### payment_status - Статусы платежных операций
- PENDING - Ожидает обработки
- SUCCESS - Успешно выполнен
- FAILED - Не удался
- REFUNDED - Возвращен

### payment_method - Способы оплаты заказов
- CASH - Наличными средствами
- CARD - Банковской картой
- BONUSES - Бонусными баллами

### delivery_method - Способы получения заказов
- IN_HALL - Самовывоз из зала
- TAKEOUT - Навынос

### bonus_action_type - Типы операций с бонусными баллами
- ACCRUAL - Начисление баллов
- WRITE_OFF - Списание баллов

### promotion_type - Типы маркетинговых акций
- PERCENT_DISCOUNT - Процентная скидка
- GIFT - Бесплатный подарок (мерч)
- BONUS_X2 - Двойное начисление бонусов

### robot_status - Статусы роботизированного оборудования
- ONLINE - В сети и доступен
- OFFLINE - Не в сети
- ERROR - Аварийное состояние
- MAINTENANCE - На техническом обслуживании

### 2.1.9 production_status - Статусы производственных заданий
- QUEUED - В очереди на выполнение
- IN_PROGRESS - В процессе выполнения
- COMPLETED - Успешно выполнено
- ERROR - Выполнение с ошибкой

### 2.1.10 log_level - Уровни логирования
- INFO - Информационное сообщение
- WARN - Предупреждение
- ERROR - Ошибка выполнения
- DEBUG - Отладочная информация

