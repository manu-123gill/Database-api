# Frappe Database api

## Start shell

```sh
$ bench --site library.in console

Apps in this namespace:
frappe, library_mang, frappe_whatsapp, movie_tickets

In [1]:  import frappe

```
## Let’s get a count of User in the database.

```sh
In [2]: frappe.db.count('User')
Out[2]: 7

Add few Users using /desk#List/User/List and get the count again.
In [2]: frappe.db.count('User')
Out[2]:8

You can add filter conditions too in count.

In [3]: frappe.db.count('User', filters={'email': 'inder@gmail.com'})
Out[3]: 1

In [4]: frappe.db.count('User', filters={'email': ('in', ['ram@gmail.com', 'preet@gmail.com'])})
Out[4]: 2

```
## get_values()

```sh
In [5]: users = frappe.db.get_values("User", filters={})

In [6]: users
Out[6]: 
(('baljeet@gmail.com',),
 ('ram@gmail.com',),
 ('manu@gmail.com',),
 ('inder@gmail.com',),
 ('preet@gmail.com',),
 ('Guest',),
 ('manugill694@gmail.com',),
 ('Administrator',))

In [7]: users = frappe.db.get_values("User", filters={}, fieldname=["name", "email"])

In [8]: users
Out[8]: 
(('baljeet@gmail.com', 'baljeet@gmail.com'),
 ('ram@gmail.com', 'ram@gmail.com'),
 ('manu@gmail.com', 'manu@gmail.com'),
 ('inder@gmail.com', 'inder@gmail.com'),
 ('preet@gmail.com', 'preet@gmail.com'),
 ('Guest', 'guest@example.com'),
 ('manugill694@gmail.com', 'manugill694@gmail.com'),
 ('Administrator', 'admin@example.com'))




```



