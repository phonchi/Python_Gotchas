## Use dictionary/set comprehension
```
# Old style: passing a list comprehension to the `dict` function
users_by_id = dict([(user.id, user.name) for user in users])

users_by_id = {user.id: user.name for user in users}
```
