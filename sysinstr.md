### Инструкция 

связь заказов с ```orders_table``` из таблицы ```onec_parsed_docs``` идет по полю ```invoice_product_order_id``` т.е.

берем поле ```invoice_product_order_id``` из таблицы ```onec_parsed_docs``` и находим заказ в таблице ```orders_table``` по полю ```order_num```

Когда заказ уже в зоне отгрузки, тогда в таблице ```onec_parsed_docs``` у него должен быть статус ```status=МАРКИРОВАН``` и поле ```delivery_qr``` не должно быть ```NULL```



