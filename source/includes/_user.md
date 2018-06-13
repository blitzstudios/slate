# User

> To fetch a user object, use this code:

```shell
# With shell, you can just curl the username or user_id
curl "https://api.sleeper.app/v1/user/<username>"
curl "https://api.sleeper.app/v1/user/<user_id>"
```

> You will get a JSON response that looks something like this:

```json
{
  "username": "sleeperuser",
  "user_id": "12345678",
  "display_name": "SleeperUser",
  "avatar": "cc12ec49965eb7856f84d71cf85306af"
}
```

We do not perform authentication as our API is read-only and only contains league information.

Via the `user` resource, you can GET the user object by either providing the `username` or `user_id` of the user.

`GET https://api.sleeper.app/v1/user/<username>`

`GET https://api.sleeper.app/v1/user/<user_id>`

<aside class="notice">
Keep in mind that the <code>username</code> of a user can change over time, so if you are storing information, you'll want to hold onto the user_id.
</aside>
