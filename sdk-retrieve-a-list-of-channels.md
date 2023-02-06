<!-- You can see the online version of this page on: https://sendbird.com/docs/chat/v4/javascript/channel/retrieving-channels/retrieve-a-list-of-channels -->

# Retrieve a list of channels

You can retrieve a list of OpenChannel objects using the `next()` method of an [`OpenChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_openChannel.OpenChannelListQuery.html) instance and a list of GroupChannel objects using the `next()` method of a [`GroupChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_groupChannel.GroupChannelListQuery.html) instance. The `GroupChannelListQuery` instance returns both public and private group channels that the current user has joined. To retrieve a list of all public group channels regardless of membership status, use the [`PublicGroupChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_groupChannel.PublicGroupChannelListQuery.html) instance as described later on this page.

> Note: You can also search for specific [open channels](https://sendbird.com/docs/chat/v4/javascript/channel/searching-channels/search-open-channels-by-name-or-url-or-custom-types) and [group channels](https://sendbird.com/docs/chat/v4/javascript/channel/searching-channels/search-group-channels-by-name-url-or-other-filters) with keywords and filters.

---

## Open channels

Create an [`OpenChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_openChannel.OpenChannelListQuery.html) instance to retrieve a list of open channels matching the specifications set by `OpenChannelListQueryParams`. After a list of open channels is successfully retrieved, you can access the data of each open channel from the result list through the channels parameter of the callback handler.

```ts
const query: OpenChannelListQuery = sb.openChannel.createOpenChannelListQuery();

if (query.hasNext) {
	const channels: OpenChannel[] = await query.next();
}
```

---

## Group channels

Create a [`GroupChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_groupChannel.GroupChannelListQuery.html) instance to retrieve a list of group channels matching the specifications set by `GroupChannelListQueryParams`.

You can set the `GroupChannelListQueryParams`'s `includeEmpty` property to true to allow users to view empty channels, which include channels that are empty because the view chat history option is turned off to prevent new members from seeing previous conversations. You can determine whether to turn on the chat history option on [Sendbird Dashboard](https://dashboard.sendbird.com/auth/signin) under **Settings** > **Chat** > **Channels** > **Group channels**.

After a list of group channels is successfully retrieved, you can access the data of each channel from the result list through the channels parameter of the callback handler.

```ts
const params: GroupChannelListQueryParams = {
	includeEmpty: true,
	myMemberStateFilter: MyMemberStateFilter.JOINED,
	order: GroupChannelListOrder.LATEST_LAST_MESSAGE,
	limit: 15, // The value of the pagination limit could be set up to 100.
};
const query: GroupChannelListQuery =
	sb.groupChannel.createMyGroupChannelListQuery(params);

if (query.hasNext) {
	const channels: GroupChannel[] = await query.next();
}
```

---

## All public group channels

If you want to retrieve a list of all [public](https://sendbird.com/docs/chat/v4/javascript/channel/overview-channel#2-group-channel-3-choose-a-type-of-a-group-channel) group channels regardless of the current user's membership status, use the [`PublicGroupChannelListQuery`](https://sendbird.com/docs/chat/v4/javascript/ref/classes/_sendbird_chat_groupChannel.PublicGroupChannelListQuery.html) instance and set membershipFilter to MembershipFilter.ALL in `PublicGroupChannelListQueryParams`.

The `hasNext()` method checks if there are more public group channels to retrieve and the `next()` method will return them. After a list of public group channels is successfully retrieved, you can access the data of each channel from the result list through the channels parameter of the callback handler.

```ts
const params: PublicGroupChannelListQueryParams = {
	includeEmpty: true,
	membershipFilter: MembershipFilter.ALL,
	order: PublicGroupChannelListOrder.CHRONOLOGICAL,
	limit: 15, // The value of the pagination limit could be set up to 100.
};
const query: PublicGroupChannelListQuery =
	sb.groupChannel.createPublicGroupChannelListQuery(params);

if (query.hasNext) {
	const channels: GroupChannel[] = await query.next();
}
```

---

## Supergroup channels

To retrieve a list of Supergroup channels, you can set the `superChannelFilter` property to `SuperChannelFilter.SUPER` in either the `GroupChannelListQuery` or `PublicGroupChannelListQuery` instance. The `superChannelFilter` property works much like other [search filters](https://sendbird.com/docs/chat/v4/javascript/channel/searching-channels/search-group-channels-by-name-url-or-other-filters). Use `GroupChannelListQuery` when only searching for group channels that the current user belongs to, and use `PublicGroupChannelListQuery` when searching for all public group channels regardless of the current user's membership status.

When queried channels are returned, you can check that the channel is a Supergroup channel by looking at whether the `isSuper` property has a value of `true`.

#### Using GroupChannelListQuery

```ts
const params: GroupChannelListQueryParams = {
	superChannelFilter: SuperChannelFilter.SUPER,
};
const query: GroupChannelListQuery =
	sb.groupChannel.createMyGroupChannelListQuery(params);
const channels: GroupChannel[] = await query.next();
```

#### Using PublicGroupChannelListQuery

```ts
const params: PublicGroupChannelListQueryParams = {
	superChannelFilter: SuperChannelFilter.SUPER,
};
const query: PublicGroupChannelListQuery =
	sb.groupChannel.createPublicGroupChannelListQuery(params);
const channels: GroupChannel[] = await query.next();
```
