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

In [9]: users = frappe.db.get_values("User", filters={}, fieldname=["name", "email"], as_dict=True)

In [10]: users
Out[10]: 
[{'name': 'baljeet@gmail.com', 'email': 'baljeet@gmail.com'},
 {'name': 'ram@gmail.com', 'email': 'ram@gmail.com'},
 {'name': 'manu@gmail.com', 'email': 'manu@gmail.com'},
 {'name': 'inder@gmail.com', 'email': 'inder@gmail.com'},
 {'name': 'preet@gmail.com', 'email': 'preet@gmail.com'},
 {'name': 'Guest', 'email': 'guest@example.com'},
 {'name': 'manugill694@gmail.com', 'email': 'manugill694@gmail.com'},
 {'name': 'Administrator', 'email': 'admin@example.com'}]

```
## Ordering

```sh
In [11]:  users = frappe.db.get_values("User", filters={}, fieldname=["name", "email"], as_dict=True, order_by='creation')

In [12]: users
Out[12]: 
[{'name': 'baljeet@gmail.com', 'email': 'baljeet@gmail.com'},
 {'name': 'ram@gmail.com', 'email': 'ram@gmail.com'},
 {'name': 'inder@gmail.com', 'email': 'inder@gmail.com'},
 {'name': 'manu@gmail.com', 'email': 'manu@gmail.com'},
 {'name': 'preet@gmail.com', 'email': 'preet@gmail.com'},
 {'name': 'manugill694@gmail.com', 'email': 'manugill694@gmail.com'},
 {'name': 'Guest', 'email': 'guest@example.com'},
 {'name': 'Administrator', 'email': 'admin@example.com'}]

In [13]:  users = frappe.db.get_values("User", filters={}, fieldname=["name", "email"], as_dict=True, order_by='creation desc')

In [14]: users
Out[14]: 
[{'name': 'baljeet@gmail.com', 'email': 'baljeet@gmail.com'},
 {'name': 'ram@gmail.com', 'email': 'ram@gmail.com'},
 {'name': 'inder@gmail.com', 'email': 'inder@gmail.com'},
 {'name': 'manu@gmail.com', 'email': 'manu@gmail.com'},
 {'name': 'preet@gmail.com', 'email': 'preet@gmail.com'},
 {'name': 'manugill694@gmail.com', 'email': 'manugill694@gmail.com'},
 {'name': 'Guest', 'email': 'guest@example.com'},
 {'name': 'Administrator', 'email': 'admin@example.com'}]

In [15]: frappe.db.get_value("User", filters={"name": "Administrator"}, fieldname="*")
Out[15]: 
{'name': 'Administrator',
 'creation': datetime.datetime(2023, 7, 25, 14, 59, 59, 840539),
 'modified': datetime.datetime(2023, 9, 5, 10, 30, 41, 725647),
 'modified_by': 'Administrator',
 'owner': 'Administrator',
 'docstatus': 0,
 'idx': 0,
 'enabled': 1,
 'email': 'admin@example.com',
 'first_name': 'Administrator',
 'middle_name': None,
 'last_name': None,
 'full_name': 'Administrator',
 'username': 'administrator',
 'language': None,
 'time_zone': 'Asia/Kolkata',
 'send_welcome_email': 1,
 'unsubscribed': 0,
 'user_image': None,
 'role_profile_name': None,
 'gender': None,
 'birth_date': None,
 'interest': None,
 'banner_image': None,
 'desk_theme': 'Light',
 'phone': None,
 'location': None,
 'bio': None,
 'mute_sounds': 0,
 'mobile_no': None,
 'new_password': '',
 'logout_all_sessions': 1,
 'reset_password_key': None,
 'last_reset_password_key_generated_on': None,
 'last_password_reset_date': None,
 'redirect_url': None,
 'document_follow_notify': 0,
 'document_follow_frequency': 'Daily',
 'follow_created_documents': 0,
 'follow_commented_documents': 0,
 'follow_liked_documents': 0,
 'follow_assigned_documents': 0,
 'follow_shared_documents': 0,
 'email_signature': None,
 'thread_notify': 0,
 'send_me_a_copy': 0,
 'allowed_in_mentions': 1,
 'module_profile': None,
 'home_settings': None,
 'simultaneous_sessions': 1,
 'restrict_ip': None,
 'last_ip': '127.0.0.1',
 'login_after': 0,
 'user_type': 'System User',
 'last_active': datetime.datetime(2023, 9, 18, 16, 45, 3, 999864),
 'login_before': 0,
 'bypass_restrict_ip_check_if_2fa_enabled': 0,
 'last_login': '2023-09-18 10:40:50.460636',
 'last_known_versions': '{"frappe": {"title": "Frappe Framework", "description": "Full stack web framework with Python, Javascript, MariaDB, Redis, Node", "branch": "version-14", "version": "14.40.3"}}',
 'api_key': None,
 'api_secret': None,
 'onboarding_status': '{"Main Workspace Tour":{"is_complete":true},"Users Workspace Tour":{"is_complete":true},"User List Tour":{"is_complete":true}}',
 '_user_tags': None,
 '_comments': None,
 '_assign': None,
 '_liked_by': None}

In [18]: user = frappe.db.get_value("User", filters="Administrator")

In [19]:  user = frappe.db.get("User", "Administrator")

In [20]: users = frappe.db.sql("select name from tabUser");

In [21]: users
Out[21]: 
(('Administrator',),
 ('manugill694@gmail.com',),
 ('Guest',),
 ('preet@gmail.com',),
 ('inder@gmail.com',),
 ('manu@gmail.com',),
 ('ram@gmail.com',),
 ('baljeet@gmail.com',))

In [22]:  users = frappe.db.sql("select name, email from tabUser", as_dict=True);

In [23]: users
Out[23]: 
[{'name': 'Administrator', 'email': 'admin@example.com'},
 {'name': 'baljeet@gmail.com', 'email': 'baljeet@gmail.com'},
 {'name': 'Guest', 'email': 'guest@example.com'},
 {'name': 'inder@gmail.com', 'email': 'inder@gmail.com'},
 {'name': 'manu@gmail.com', 'email': 'manu@gmail.com'},
 {'name': 'manugill694@gmail.com', 'email': 'manugill694@gmail.com'},
 {'name': 'preet@gmail.com', 'email': 'preet@gmail.com'},
 {'name': 'ram@gmail.com', 'email': 'ram@gmail.com'}]

In [24]: users = frappe.db.sql("select name, email from tabUser", as_list=True);

In [25]: users
Out[25]: 
[['Administrator', 'admin@example.com'],
 ['baljeet@gmail.com', 'baljeet@gmail.com'],
 ['Guest', 'guest@example.com'],
 ['inder@gmail.com', 'inder@gmail.com'],
 ['manu@gmail.com', 'manu@gmail.com'],
 ['manugill694@gmail.com', 'manugill694@gmail.com'],
 ['preet@gmail.com', 'preet@gmail.com'],
 ['ram@gmail.com', 'ram@gmail.com']]

In [26]:  users = frappe.db.sql("select u.name, l.language_code from tabUser as u inner join tabLanguage as l on u.language=l.name", as_dict=True);

In [27]: users
Out[27]: 
[{'name': 'baljeet@gmail.com', 'language_code': 'en'},
 {'name': 'inder@gmail.com', 'language_code': 'en'},
 {'name': 'manu@gmail.com', 'language_code': 'en'},
 {'name': 'manugill694@gmail.com', 'language_code': 'en'},
 {'name': 'preet@gmail.com', 'language_code': 'en'},
 {'name': 'ram@gmail.com', 'language_code': 'en'}]



```




