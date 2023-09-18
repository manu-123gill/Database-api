# Frappe Database api
## Start shell
```sh
$ bench --site library.in console

Apps in this namespace:
frappe, library_mang, frappe_whatsapp, movie_tickets

In [1]:  import frappe

```sh

## Let’s get a count of User in the database.

 In [2]: frappe.db.count('User')
Out[2]: 7



