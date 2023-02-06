<!-- You can see the online version of this page on:  https://sendbird.com/docs/chat/v3/platform-api/message/polls/polls-overview -->

# Polls

The polls feature provides an easier way to gather feedback from members in a channel. To post a poll in a channel, you must send a message that contains the poll you created. Polls can only be sent with [text messages](https://sendbird.com/docs/chat/v3/platform-api/message/message-overview#2-message-types) in certain [group channels](https://sendbird.com/docs/chat/v3/platform-api/channel/channel-overview#2-channel-types-3-group-channel). See the [limitations](#limitations) section below to learn more about which type of channels and messages support polls.

The following are some of the ways that polls can be customized.

- Allow users to vote for a single option or multiple options.
- Allow users other than the creator of the poll to add new options.
- Display a partial list of voters for each option.
- Add `data` which can contain additional information such as a supplementary explanation for each poll option in a key-value pair.

---

## Using polls

### Prerequisite

To use polls in your Sendbird application, you must activate the feature on [Sendbird Dashboard](https://dashboard.sendbird.com/auth/signin). Go to **Settings** > **Chat** > **Features** and turn on the **Polls** feature.

### Limitations

Refer to the following limitations when using polls.

- The maximum number of options that can be added to a poll differs depending on your Sendbird plan. For further information, contact our [sales team](https://sendbird.com/contact-sales).
- Polls can't be sent in the following message types: file messages, admin messages, and [scheduled](https://sendbird.com/docs/chat/v3/platform-api/message/scheduled-messages/scheduled-messages-overview) text messages.
- Polls information isn't included in the [export](https://sendbird.com/docs/chat/v3/platform-api/data-export/data-export-overview#2-data-types-3-message) result of the message data containing polls.
- The table below shows the types of channels that support polls. See the [channel types](https://sendbird.com/docs/chat/v3/platform-api/channel/channel-overview#2-channel-types) section to learn about the differences among various channel types.

|       | Open channel  |            Group channel             | Supergroup channel |
| ----- | :-----------: | :----------------------------------: | :----------------: |
| Polls | Not supported | Supported, except ephemeral channels |   Not supported    |

---

## Resource representation

The following tables show the list of properties in a [poll resource](#list-of-properties-in-a-poll) and a [poll option resource](#list-of-properties-in-a-poll-option).

#### List of properties in a poll

| Property name | Type | Description |
| --- | --- | --- |
| id | integer | The unique ID of a poll. |
| title | string | The text of a poll's title. |
| options | array of objects | An array of options that a user can vote for. |
| voter_count | integer | The number of voters who casted a vote on a poll. |
| created_by | string | The unique ID of the user who created a poll. |
| status | string | The status of a poll. The value can be `removed`, `open`, or `closed`. |
| allow_user_suggestion | boolean | Indicates whether to allow users other than the creator of the poll to add new options to the poll.                                   |
| allow_multiple_votes  | boolean | Indicates whether to allow users to vote for multiple options. |
| created_at | long | The time when a poll is created in Unix seconds. |
| updated_at | long | The time when a poll is updated in Unix seconds. |
| close_at | long | The time when a poll was closed or will be closed in Unix seconds. If the value of this property is `-1`, the poll status remains `open`. |
| data | object | A JSON object of one or more key-value items to store additional information related to a poll.                                       |

#### List of properties in a poll option

| Property name | Type | Description |
| --- | --- | --- |
| poll_id | integer | The unique ID of a poll that a poll option belongs to. |
| id | integer | The unique ID of a poll option. This value is unique within a poll. |
| text | string | The text that describes a poll option. |
| vote_count | integer | The number of votes casted on a poll option. |
| created_by | string | The unique ID of the user who created a poll option. |
| created_at | long | The time when a poll option is created in Unix seconds. |
| updated_at | long | The time when a poll option is updated in Unix seconds. |
| partial_voter_list | array of objects | An array of users who voted for this poll option. Up to ten users can be shown. |

---

## Actions

The following table shows a list of actions supported for polls. API endpoints are relative to the [base URL](https://sendbird.com/docs/chat/v3/platform-api/prepare-to-use-api#2-base-url) allocated to your Sendbird application. In this page, the base URL for the following endpoints is `https://api-{application_id}.sendbird.com/v3`.

> Note: If you want to know the ID and base URL of your application, sign in to [Sendbird Dashboard](https://dashboard.sendbird.com/), go to **Settings** > **Application** > **General**, and check the **Application ID** and **API request URL**.

#### List of actions

| Action | HTTP request |
| --- | --- |
| [List polls](https://sendbird.com/docs/chat/v3/platform-api/message/polls/list-polls) | `GET` **/polls**<br />Retrieves both open and closed polls in the client app. |
| [Get a poll](https://sendbird.com/docs/chat/v3/platform-api/message/polls/get-a-poll) | `GET` **/polls/{poll_id}**<br />Retrieves information on a poll. |
| [Create a poll](https://sendbird.com/docs/chat/v3/platform-api/message/polls/create-a-poll) | `POST` **/polls**<br />Creates a poll. |
| [Update a poll](https://sendbird.com/docs/chat/v3/platform-api/message/polls/update-a-poll) | `PUT` **/polls/{poll_id}**<br />Updates information of a poll. |
| [Close a poll](https://sendbird.com/docs/chat/v3/platform-api/message/polls/close-a-poll) | `PUT` **/polls/{poll_id}/close**<br />Closes a poll. |
| [Delete a poll](https://sendbird.com/docs/chat/v3/platform-api/message/polls/delete-a-poll) | `DELETE` **/polls/{poll_id}**<br />Deletes a poll. |
| [Get a poll option](https://sendbird.com/docs/chat/v3/platform-api/message/polls/get-a-poll-option) | `GET` **/polls/{poll_id}/options/{option_id}**<br />Retrieves an option of a poll. | 
| [Add a poll option](https://sendbird.com/docs/chat/v3/platform-api/message/polls/add-a-poll-option) | `POST` **/polls/{poll_id}/options**<br />Adds an option to a poll. |
| [Update a poll option](https://sendbird.com/docs/chat/v3/platform-api/message/polls/update-a-poll-option) | `PUT` **/polls/{poll_id}/options/{option_id}**<br />Updates an option in a poll. |
| [Delete a poll option](https://sendbird.com/docs/chat/v3/platform-api/message/polls/delete-a-poll-option) | `DELETE` **/polls/{poll_id}/options/{option_id}**<br />Deletes an option from a poll. |
| [Cast or cancel a vote](https://sendbird.com/docs/chat/v3/platform-api/message/polls/cast-or-cancel-a-vote) | `POST` **/polls/{poll_id}/vote**<br />Allows users to cast or cancel their vote. |
| [List voters of a poll option](https://sendbird.com/docs/chat/v3/platform-api/message/polls/list-voters-of-a-poll-option) | `GET` **/polls/{poll_id}/options/{option_id}/voters**<br />Retrieves a list of users who voted for an option. |
