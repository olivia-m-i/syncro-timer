# Timers

Add or remove timers created with [Syncro-Timer](../product/README.md).

## [PUT] Add a timer

Receive hourly updates of a timer's status at the specified callback address. 

You'll need the timer ID generated on the **Syncro-Timer** page. 

*Authorization: [Bearer Auth (App API Key)](https://customer.io/docs/api/#section/Authentication/Bearer-Auth-(App-API-Key))*

| Type | Endpoint |
|---|---|
| PUT | `https://api.customer.io/v1/syncro-timer/{timer_id}` |

### Path parameters

| Parameter | Required | Type | Description |
|---|---|---|---|
| `timer_id` | Yes | integer | The timer identifier. |

### Request body

*Content type: application/json*

| Parameter | Type | Description |
|---|---|---|
| `timezone` | string | The [time zone](https://customer.io/docs/example-timezones/#detailed) to use in the response, regardless of the timer's original time zone. |
| `callback_url` | string | URL to which to send the response. |

### Request sample

```console
curl --request PUT\
  --url https://api.customer.io/v1/syncro-timer/YOUR_TIMER_ID
  --header 'Authorization: Bearer YOUR_BEARER_TOKEN'
  --header 'content-type: application/json' \
  --data '{"timezone": "(GMT-09:00) Alaska", "callback_url": "https://myserver.com/foo"}
```
### Responses

* 200: Returns the status of the timer. 

*Content type: application/json*

| Parameter | Type | Description |
|---|---|---|
| hours_left | integer | Hours until the timer expires. |
| final_date | string | Date and time when the timer expires. |

* 401: Unauthorized request.
* 404: The timer ID requested does not exist. 

#### Response sample

```json

{
    "hours_left": "560", 
    "final_date": "2022/12/01 @ 10pm" 
}
```

## [DELETE] Delete a timer 

Delete a timer that was create on the **Syncro-Timer** page. You'll need the timer's ID. 

*Authorization: [Bearer Auth (App API Key)](https://customer.io/docs/api/#section/Authentication/Bearer-Auth-(App-API-Key))*

| Type | Endpoint |
|---|---|
| DELETE | `https://api.customer.io/v1/syncro-timer/{timer_id}` |

### Path parameters

| Parameter | Required | Type | Description |
|---|---|---|---|
| `timer_id` | Yes | integer | The timer identifier. |

### Request sample

```console
curl --request DELETE\
  --url https://api.customer.io/v1/syncro-timer/YOUR_TIMER_ID
  --header 'Authorization: Bearer YOUR_BEARER_TOKEN'
```

### Responses

* 200: A successful request returns an empty response.
* 401: Unauthorized request.
* 404: The timer ID requested does not exist. 