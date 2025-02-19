---
nav_title: Data Retention
article_title: Data Retention
alias: /data_retention/
description: "This reference article covers general Braze data retention information."
page_type: reference
page_order: 2.5

---

<!--
Warning! Don't make any changes to this document without approval from the legal department.
-->

# Braze Data Retention Information

*Last revised on January 20th, 2023*

> This article covers general Braze data retention information.<br><br>Data stored in Braze is retained and usable for segmentation, personalization, and targeting for the lifetime of the Customer's account. This means data such as user profile attributes, custom attributes, custom events, and purchases are stored indefinitely for active users unless removed by the Customer, for the duration of the contract.<br><br>Braze has features, processes, and APIs in place to automatically implement good data hygiene practices for compliance with GDPR and other best practices. These are described below.

## Data Retention Handled by Customers Through Braze's Dashboard or API

Braze enables its customers to delete entire User Profiles and Attribute data themselves from their workspace.

This means you can: 
- Delete user profiles using the Braze [Delete user API endpoint]({{site.baseurl}}/api/endpoints/user_data/post_user_delete/) 
- Delete (null) or amend attributes on user profiles using the Braze [Track user API endpoint]({{site.baseurl}}/api/endpoints/user_data/post_user_track/)

Behavioral events cannot be deleted from a User Profile (custom events, sessions, campaigns, purchases). To remove those events, you must delete the entire User Profile.

For privacy compliance, you may need to delete all personal data pertaining to a User upon the User's request. You can find instructions on our [data protection technical assistance]({{site.baseurl}}/help/dp-technical-assistance/#the-right-to-erasure) page.

{% alert note %}
A User may have multiple profiles, and you may need to delete multiple profiles to delete all data pertaining to a single User. Follow instructions on the data protection technical assistance page on how to fully delete all data regarding a User.
{% endalert %}

## Data Retention Handled by Braze for Specific Features of the Braze Services

#### Braze Database: Automatic Archiving/Deletion of Churned Users

Each week, Braze runs a process to remove Inactive and Dormant Users from the Braze Services. In general, these are users who are not reachable (for example, have no email address, no phone number, no push token, do not use your apps or visit your websites), have had no activity recorded on their user profile, and have not been messaged or engaged with using Braze. This is done to adhere to GDPR principles and best practices. You can read more about this process on our [user archival definitions]({{site.baseurl}}/user_guide/data_and_analytics/user_data_collection/user_archival/) page.

{% alert note %} 
Customers have full control over whether or not a user is Inactive or Dormant and can prevent archiving of user profiles by recording a data point at regular intervals. Braze Canvas offers the ability to do this automatically, allowing you to effectively turn off this functionality for some or all of your Inactive or Dormant Users. 
{% endalert %}

#### Campaign and Canvas Interactions Data 

{% tabs %}
{% tab Campaign Interactions Data %}
##### What is it?

Campaign Interactions are data related to End Users' interactions with a campaign. They are used for retargeting filters and to determine campaign re-eligibility.

##### When is it deleted?

Braze automatically deletes from the Customer's workspaces the Campaign Interactions for campaigns that have not sent any messages in 25 calendar months and are not used for retargeting in any campaigns, Canvases, or Content Cards in an active status.

##### What happens after deletion?

- Campaigns with no Campaign Interactions cannot be used in retargeting filters for campaigns, Canvases, and Segments.
- Any active campaign that has not sent any messages in 25 months, and is not being used for retargeting in any active campaigns, Canvases, or Cards, will be stopped because campaign eligibility resets. You can re-launch the campaign after reviewing the re-eligibility setting.

##### How to reset the clock to avoid deletion?

To retain Campaign Interactions for a particular campaign, you can send a message using that campaign at least once within the 25 months since the last message was sent or use that campaign in the **Received Message from Campaign** filter in any active campaign, Canvas, or Card. You can request a shorter data retention than 25 months via your Braze customer success manager.

{% endtab %}
{% tab Canvas Interactions Data %}

##### What is it? 

Canvas Interactions are data related to End Users' interactions with a Canvas or Canvas step. They are used for retargeting filters and to determine Canvas re-eligibility.

##### When is it deleted?

Braze automatically deletes from the Customer's workspaces the Canvas Interactions for Canvases that have not sent any messages in 25 calendar months and are not used for retargeting by any active campaigns or Canvases.

##### What happens after deletion?

- Canvases with no Canvas Interactions cannot be used in retargeting filters for campaigns, Canvases, and Segments.
- Any active Canvas that has not been used to send messages in 25 months, and is not being used for retargeting in any active campaigns, Canvases, or Cards, will be stopped because Canvas eligibility resets. You can re-launch the Canvas after reviewing the re-eligibility setting.
- You will not be able to reference these Canvas Interactions in retargeting features, such as filters, and you will not be able to pull the deleted data from the `/users/export` API.

##### How to reset the clock to avoid deletion?

To retain Canvas Interactions for a particular Canvas, you can send a message using that Canvas at least once within the 25 months since the last message was sent or use that Canvas in the **Received Message from Campaign** filter in any active campaign, Canvas, or Card. You can request a shorter data retention than 25 months via your Braze customer success manager.
{% endtab %}
{% endtabs %}

## Data Retention Handled by Braze

The below retention policies pertain to Braze's compliance with GDPR and privacy regulations and are regarding transient data storage as it passes through our internal systems. These retention policies do not impact the Braze Services and are informational for your legal and privacy teams.

#### Braze Servers: Short-term Retention for Recovery Purposes

Data sent by Braze to certain subprocessors may still exist in Braze's internal systems for up to 90 days.

#### Braze Data Lake Data Retention

Data available to Customers within the Braze dashboard is mostly aggregated. Detailed logs are kept in a separate database created by Braze (the "Data Lake", formerly known as "BI Database"). Data Lake data is used for aggregate reporting and other advanced functionality.

If you use our APIs to delete user profiles or delete or amend attributes from user profiles, it may take up to two weeks for that data to be deleted from Braze's Data Lake. Deletion of data in the Data Lake will not affect segmentation or personalization but rather ensures the data is removed from all Braze systems.

#### Braze Backup Servers

When data is deleted from your production instance, the data remains in Braze's backup servers for six months and is then deleted according to our internal processes.
