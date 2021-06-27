# Project-Fundamental-SQL-Group-By-and-Having
Project SQL dari DQLab Academy
<hr>

### <b>Mendapatkan jumlah nilai pinalty</b>
Pada pelayanan terdapat customer yang mendapatkan pinalty yang diakibatkan telat membayar.

Carilah customer-customer id dan jumlah pinalty dari yang dibayarkan oleh customer yang mendapatkan pinalty.

maka hasil akan seperti berikut:<br>
<img src="https://miro.medium.com/max/229/1*KXUjxuq-EAXhiF1KcgO6MA.png">


Berikut Codenya:
```
select customer_id, SUM(pinalty)
from invoice
group by customer_id
having sum(pinalty) >0

```

### <b>Mencari customer yang mengganti layanan</b>
Dalam pelayanan jaringan internet akan terjadi perubahan paket yang dilakukan oleh konsumen tersebut.
Sekarang kita akan mencari konsumen-konsumen yang melakukan perubahan layanannya.

Ada 3 table yang dibutuhkan dalam mencari data tersebut:
- customer
- subscription
- product<br>
Lakukanlah query dengan petunjuk sebagai berikut:

Filtrasi dahulu customer_id yang memiliki subscription lebih dari 1 pada table subscription.
Kemudian query tersebut digunakan untuk mendapatkan nama customer pada table customer dan lakukan join antara subscription dan product untuk mendapatkan product_name, gunakan function group_concat untuk product_name.

Sehingga akan menghasilkan seperti dibawah ini: <br>
<img src="https://miro.medium.com/max/576/1*UEQQWIiZEKr30FOV9Ie2IA.png">


Berikut Codenya:
```
SELECT t1.name, group_concat(t3.product_name) FROM customer t1 JOIN subscription t2 ON t1.id = t2.customer_id JOIN product t3 ON t2.product_id=t3.id WHERE t1.id IN (
  select customer_id
  from subscription
  group by customer_id
  having count(customer_id)>1

)
GROUP BY t1.name
```
