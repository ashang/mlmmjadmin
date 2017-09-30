# mlmmj-admin: RESTful API Interface

[TOC]

## API Endpoints

Replace `<mail>` by real email address of the mailing list account.

HTTP Method | URI | Comment
---|---|---
GET     | `/api/<mail>` | Get profile of an existing mailing list account.
POST    | `/api/<mail>` | Create a new mailing list account.
DELETE  | `/api/<mail>` | Remove an existing mailing list account.
PUT     | `/api/<mail>` | Update mailing list profiles.

## Parameters used to create or update mailing list account

Parameters used to create (`POST /api/<mail>`) or update (`PUT /api/<mail>`) mailing list account:

Parameter | Sample Usage | Default Value | Comment
---|---|---|---
`close_list` | `close_list=yes` | `no` | If set to `yes`, subscription and unsubscription via mail is disabled.
`only_moderator_can_post` | `only_moderator_can_post=yes` | `no` | If set to `yes`, only moderators are allowed to post to it. The check is made against the `From:` header.
`only_subscriber_can_post` | `only_subscriber_can_post=yes` | `yes` | If set to `yes`, only subscribed members are allowed to post to it. The check is made against the `From:` header.
`disable_subscription` | `disable_subscription=yes` | `no` | If set to `yes`, subscription is disabled, but unsubscription is still possible.
`disable_subscription_confirm` | `disable_subscription_confirm=yes` | | If set to `yes`, mlmmj won't send mail to subscriber to ask for confirmation to subscribe to the list. __WARNING__: This should in principle never ever be used, but there are times on local lists etc. where this is useful. HANDLE WITH CARE!
`disable_digest_subscription` | `disable_digest_subscription=yes` | | If set to `yes`, subscription to the digest version of the mailing list is disabled. Useful if you don't want to allow digests and notify users about it.
`disable_digest_text` | `disable_digest_text=yes` | | If set to `yes`, digest mails won't have a text part with a thread summary.
`disable_nomail_subscription` | `disable_nomail_subscription=yes` | | If set to `yes`, subscription to the 'nomail' version of the mailing list is disabled. Useful if you don't want to allow 'nomail' and notify users about it.
`moderated` | `moderated=yes` | `no` | If set to `yes`. Parameter `owner` __or__ `moderators` is required to specify the moderators. Note: `moderators` has higher priority (means only addresses specified by `moderators` are act as moderators).
`moderate_non_subscriber_post` | `moderate_non_subscriber_post=no` | `no` | If set to `yes`, all postings from people who are not allowed to post to the list will be moderated. Default (set to `no`) is denied.
`disable_retrieving_old_posts` | `disable_retrieving_old_posts=yes` | | If set to `yes`, retrieving old posts by sending email to address `<listname>+get-N@` is disabled.
`only_subscriber_can_get_old_posts` | `only_subscriber_can_get_old_posts=no` | `yes` | If set to `yes`, only subscribers can retrieve old posts by sending email to `LISTNAME+get-N@`
`disable_retrieving_subscribers` | `disable_retrieving_subscribers=yes` | `yes` | If set to `yes`, (owner) retrieving subscribers by sending email to `LISTNAME+list@` is disabled. Note: only owner can send to such address.
`disable_send_copy_to_sender` | `disable_send_copy_to_sender=yes` | `yes` | If set to `yes`, senders won't receive copies of their own posts.
`notify_owner_when_sub_unsub` | `notify_owner_when_sub_unsub=no` | `no` | Notify the owner(s) when someone sub/unsubscribing to a mailing list.
`notify_poster_when_moderated` | `notify_poster_when_moderated=no` | `no` | Notify the posters (based on the envelope from) when their post is being moderated.
`disable_archive` | `disable_archive=yes` | `no` | If set to `yes`, emails won't be saved in the archive but simply deleted.
`moderate_subscription` | `moderate_subscription=yes` | `no` | If set to `yes`, subscription will be moderated by owner(s) or moderators specified by `subscription_moderators`. Moderators specified by `subscription_moderators` has higher priority. If set to `no`, subscription is not moderated, also, all moderators which were specified by `subscription_moderators` will be removed.
`subscription_moderators` | `subscription_moderators=<mail1>,<mail2>,<mail3>` | | Specify subscription moderators. Note: if `subscription_moderators` is given, `moderate_subscription` will be set to `yes` automatically. If no valid moderators are given, subscription will be moderated by owner(s).
`owner` | `owner=<mail1>,<mail2>,<mail3>` | | Define owner(s) of the mailing list. Owners will get mails sent to `<listname>+owner@<domain.com>`.
`moderators` | `moderators=<mail1>,<mail2>` | | Specify moderators of the mailing list. Set to empty value will remove all existing moderators.
`subject_prefix` | `subject_prefix=[prefix text]` | | Add a prefix in the `Subject:` line of mails sent to the list. Set to empty value to remove it.
`custom_headers` | `custom_headers=<header1>:<value1>\n<header2>:<value2>` | | Add custom headers to every mail coming through. Multiple headers must be separated by `\n`. Set empty value to remove it. Note: mlmmj-admin will always add `X-Mailing-List: <mail>` and `Reply-To: <mail>` for each mailing list account.
`remove_headers` | `remove_headers=Message-ID,Received` | | Remove given mail headers. NOTE: either `header:` or `header` (without `:`) is ok. Note: mlmmj-admin will always remove `DKIM-Signature:` and `Authentication-Results:`.
`name` | `name=Short description of list` | | Set a short description of the mailing list account.
`footer` | `footer=footer text` || Append footer text to every email sent to the list.

Additional parameters used to update (`PUT /api/<mail>`) mailing list account:

Parameter | Sample Usage | Default Value | Comment
---|---|---|---
TODO `add_owner` | `add_owner=<mail1>,<mail2>,<mail3>` || Add new mailing list owner
TODO `remove_owner` | `remove_owner=<mail1>,<mail2>,<mail3>` || Remove existing mailing list owner
TODO `add_subscriber` | `add_subscriber=<mail1>,<mail2>,<mail3>` || Add new subscriber.
TODO `add_subscriber_without_confirm` | `add_subscriber_without_confirm=<mail1>,<mail2>,<mail3>` || Add new subscriber without asking confirm from subscriber.
TODO `remove_subscriber` | `remove_subscriber=<mail1>,<mail2>,<mail3>` || Remove existing subscriber
TODO `add_moderator` | `add_moderator=<mail1>,<mail2>,<mail3>` || Add new moderator
TODO `remove_moderator` | `remove_moderator=<mail1>,<mail2>,<mail3>` || Remove existing moderator 
TODO `add_subscription_moderator` | `add_subscription_moderator=<mail1>,<mail2>,<mail3>` | | Add new subscription moderators. Note: if `add_subscription_moderator` is given, `moderate_subscription` will be set to `yes` automatically.
TODO `remove_subscription_moderator` | `remove_subscription_moderator=<mail1>,<mail2>,<mail3>` | | Remove existing subscription moderators.
TODO `add_custom_header` | `add_custom_header=<header1>:<value1>\r<header2>:<value2>` | | Add new custom headers
TODO `remove_custom_header` | `remove_custom_header=<header1>,<header2>,<header3>` | | Remove existing custom headers
TODO `add_removed_header` | `add_removed_header=<header1>:,<header2>:,<header3>:` | | Add new headers you want to remove
TODO `remove_removed_header` | `remove_removed_header=<header1>:,<header2>:,<header3>:` | | Remove existing headers you want to remove
TODO `change_email` | `change_email=<mail>` || Change mailing list address to a new one.

## Parameters used to delete mailing list account

> NOTE: Parameters used by `DELETE` http method must be appended to the URL.
> For example:
>
> `/api/<mail>?param=value&param2=value2&param3=value3`

Parameter | Sample Usage | Default Value | Comment
---|---|---|---
`archive` | `archive=yes` | `yes` | If set to `yes` (or no such parameter appended in URL), only account in (SQL/LDAP/...) backend will be removed (so that MTA won't accept new emails for this email address), but data on file system will be kept (by renaming the mailing list directory to `<listname>-<timestamp>`. If set to `no`, account in (SQL/LDAP/...) backend AND all data of this account on file system will be removed.