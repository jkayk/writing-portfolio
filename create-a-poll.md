<!-- You can see the online version of this page on:  https://sendbird.com/docs/chat/v3/platform-api/message/polls/create-a-poll -->

# Create a poll

This action creates a poll with at least one option. You can configure various settings for your poll, including when the poll will close and whether to allow voting for multiple options.

After creating a poll, to share the poll with other users in a channel, the poll must be [sent as a message](https://sendbird.com/docs/chat/v3/platform-api/message/messaging-basics/send-a-message).

---

## HTTP request

```bash
POST https://api-{application_id}.sendbird.com/v3/polls
```

---

## Request body

The following table lists the properties that this action supports.

| Required | | |
| --- | --- | --- |
| Property name | Type | Description |
| title | string | Specifies the title of a poll. The length is limited to 2,048 characters. |
| options | array of strings | Specifies an array of poll options that a user can vote for. At least one option should be provided, and the length of each option is limited to 2,000 characters.<br/>The maximum number of options that can be added to a poll differs depending on your Sendbird plan. For further information, contact our [sales team](https://sendbird.com/contact-sales). |

| Optional | | |
| --- | --- | --- |
| Property name | Type | Description |
| allow_user_suggestion | boolean | Determines whether to allow users other than the creator of the poll to add new options to the poll. (Default: `false`) |
| allow_multiple_votes | boolean | Determines whether to allow users to vote for multiple options. (Default: `false`) |
| close_at | long | Specifies when the poll closes and no longer accepts votes in Unix seconds. If the value of this property is `-1`, the poll is open indefinitely. |
| created_by | string | Specifies the unique ID of the user who creates the poll. |
| data | object | Specifies a JSON object of one or more key-value items to store additional poll information. |

---

## Response

If successful, this action returns a [poll resource](https://sendbird.com/docs/chat/v3/platform-api/message/polls/polls-overview#4-list-of-properties-in-a-poll) in the response body.

```json
{
	"status": "open",
	"allow_user_suggestion": true,
	"title": "April lunch date",
	"allow_multiple_votes": true,
	"created_at": 1657267925,
	"updated_at": 0,
	"created_by": "Kay",
	"id": 2217,
	"voter_count": 0,
	"close_at": -1,
	"options": [
		{
			"text": "April 15 (Fri)",
			"created_at": 1657267925,
			"updated_at": 0,
			"created_by": "Kay",
			"vote_count": 0,
			"poll_id": 2217,
			"id": 3591
		}
	]
}
```

In the case of an error, an error object is returned. A detailed list of error codes is available [here](https://sendbird.com/docs/chat/v3/platform-api/error-codes).
