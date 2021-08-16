# K.6 Konfigurasi PolicyD: Rate Limit

If there user have compromised password, _**spammer will sending email to outside with random email address receipt and very much email have been sent.**_ Usually, public IP address will have blacklisted on any RBL and cannot sending email to outside. To prevent it, we can use Policyd and configure rate limit sending message with quotas modules on Policyd. Quotas modules can prevent user@domain or other configuration can sending some email per minutes or per hours. For example, per users can sending maximum 200 emails per hours.

Select _**Policies \| Groups**_. Select _**action**_ and _**add**_ groups. given name _**list\_domain**_. On _**comment**_, you can empty or filled with comment. Select a group that has been made. On _**action**_, select _**members**_ and fill with [**your domain**](https://hosting.review/best-domain-registrar/). See the following example. make sure _**disabled**_ status is _**no**_ at _**groups**_ or _**members groups**_

[![policyd-groups](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-groups.jpg?resize=810%2C151)](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-groups.jpg)

[![](https://i0.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-members-groups.jpg?resize=810%2C158)](https://i0.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-members-groups.jpg)

Select _**Policies \| Main**_. Create new policy and give name _**rate limit sending message**_. See the following example

[![policyd-new-poliyc](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-new-poliyc.jpg?resize=413%2C218)](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-new-poliyc.jpg)

Select new policy has been made. On _**action**_, select _**members**_ and fill with the group that has previously been made. Ensure _**disabled**_ is _**no**_. See the following example

[![member-policy](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/member-policy.jpg?resize=810%2C177)](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/member-policy.jpg)

[![policyd-policy-2](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-policy-2.jpg?resize=810%2C268)](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-policy-2.jpg)

Select _**Quotas \| Configure**_. Select _**action \| add**_. fill with the following example

```text
Name : Rate Limit
Track : sender:user@domain
Period : 3600
Link to policy : Rate Limit Sending Message
Verdict : Defer (delay)
Data : information who give to users if policy have been meet or you can empty. Example : Sorry, your quotas to sending email has been full. please try again later
```

[![policyd-new-quotas](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-new-quotas.jpg?resize=520%2C298)](https://i1.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-new-quotas.jpg)

If all selection has been configured, click _**Submit Query**_**.** Select new quotas that has previously been made \| select _**action**_ \| _**Limits**_. Add limit and configure. See the following example

[![policyd-quotas-limit](https://i0.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-quotas-limit.jpg?resize=299%2C174)](https://i0.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-quotas-limit.jpg)

Ensure _**disabled**_ status is _**no**_

[![policyd-quotas-information](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-quotas-information.jpg?resize=810%2C227)](https://i2.wp.com/imanudin.net/wp-content/uploads/2014/09/policyd-quotas-information.jpg)

Above configuration will limit sending message from domain local to outside and outside to any domain with maximum message 200 email/user/hour. Please try to sending message to other domain and see the log information on /opt/zimbra/log/cbpolicyd.log

```text
[2014/09/08-21:32:39 - 4871] [CORE] INFO: module=Quotas, mode=create, host=127.0.0.1, helo=mail, from=admin@imanudin.net, to=ahmadiman@gmail.com, reason=quota_create, policy=6, quota=3, limit=4, track=Sender:admin@imanudin.net, counter=MessageCount, quota=1.00/200 (0.5%)
[2014/09/08-21:32:39 - 4871] [CBPOLICYD] INFO: Got request #2 (pipelined)
[2014/09/08-21:32:39 - 4871] [CORE] INFO: module=Quotas, mode=update, host=127.0.0.1, helo=mail, from=admin@imanudin.net, to=ahmadiman@gmail.com, reason=quota_update, policy=6, quota=3, limit=4, track=Sender:admin@imanudin.net, counter=MessageCount, quota=2.00/200 (1.0%)
```

Good luck and hopefully useful ![&#x1F600;](https://s.w.org/images/core/emoji/13.0.1/svg/1f600.svg)

Source:

[https://imanudin.net/2014/09/09/zimbra-tips-how-to-configure-rate-limit-sending-message-on-policyd/](https://imanudin.net/2014/09/09/zimbra-tips-how-to-configure-rate-limit-sending-message-on-policyd/)

