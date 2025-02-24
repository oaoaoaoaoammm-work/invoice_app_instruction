### Инструкция 

связь заказов с ```orders_table``` из таблицы ```onec_parsed_docs``` идет по полю ```invoice_product_order_id``` т.е.

берем поле ```invoice_product_order_id``` из таблицы ```onec_parsed_docs``` и находим заказ в таблице ```orders_table``` по полю ```order_num```

Когда заказ уже в зоне отгрузки, тогда в таблице ```orders_table``` у него должен быть статус ```status=МАРКИРОВАН``` и поле ```delivery_qr``` не должно быть ```NULL```, также поле ```artikul``` должно соответствовать артикулу из закрытой накладной из 1С, иначе программа не сможет проверить и сопоставить сканируемый код

Чтобы протолкнуть заказ вручную, в таблице ```onec_parsed_docs``` меняем ```is_checked``` с ```FALSE``` на ```TRUE```

Чтобы повторно распечатать накладную, в таблице ```onec_parsed_docs``` меняем ```is_printed``` с ```TRUE``` на ```FALSE```, остальные поля перезапишутся автоматически

Приложение получает заказ из таблицы ```orders_table``` по следующим полям:
```python
# MarketplaceOrders = orders_table
...
MarketplaceOrders.delivery_qr == code,
MarketplaceOrders.updated >= start_of_day,
MarketplaceOrders.updated <= end_of_day
...
```

Сравнивает с 1С по следующим полям:
```python
# OneCParsedDocs = onec_parsed_docs
...
OneCParsedDocs.invoice_product_articul == order_row.artikul,
OneCParsedDocs.invoice_product_order_id == order_row.order_num,
OneCParsedDocs.checked_by.is_(None)
...
```
