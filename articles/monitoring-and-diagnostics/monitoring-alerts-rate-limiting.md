---
title: Rate limiting for SMS, emails, Azure App push notifications and webhooks | Microsoft Docs
description: Understand how Azure limits the number of possible SMS, email, Azure App push or webhook notifications from an action group.
author: dukek
manager: chrad
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics

ms.assetid:
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/8/2017
ms.author: dukek

---

# Rate limiting for SMS messages, emails, Azure App push notifications and webhook posts
Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number, email address or device. Rate limiting ensures that alerts are manageable and actionable.

The rate limit thresholds are:

 - **SMS**: No more than 1 SMS every 5 minutes.
 - **Email**: 100 messages in an hour.
 - **Azure App Push Notifications**: There is no rate limiting for push notifications.
 - **Webhooks**: There is no rate limiting for webhooks.

## Rate limit rules
- A particular phone number or email is rate limited when it receives more messages than the threshold allows.
- A phone number or email can be part of action groups across many subscriptions. Rate limiting applies across all subscriptions. It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.  
- When an email address is rate limited, an additional notification is sent to communicate the rate limiting. The notification states when the rate limiting expires.

## Next steps ##
* Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).
* Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.  
* Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).
