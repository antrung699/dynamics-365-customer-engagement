---
title: Call a customer in the voice channel
description: Use this article to understand how you can make customer calls in Omnichannel for Customer Service.
ms.date: 09/21/2023
ms.custom: bap-template
ms.topic: how-to
author: gandhamm
ms.author: mgandham
---

# Call a customer

[!INCLUDE[cc-use-with-omnichannel](../../includes/cc-use-with-omnichannel.md)]

To be able to call customers, your administrator must configure outbound calling, add you as user to the outbound capacity profile, and then set up outbound profiles. More information: [Outbound calling](../administer/voice-channel-outbound-calling.md)

1. In Customer Service workspace or Omnichannel for Customer Service, go to **Contacts**, and then select a customer to call.
2. On the **Active Conversation** page, locate the **Mobile Phone** field, and then select the call icon to call the customer. You can also select the **Launch dialer** phone icon on the menu bar to quickly call a customer.
     The **Dial number** panel appears. You can perform the following actions:
     - On the dial pad, you can copy, type in a number, or select a number from the recently dialled numbers. The country code dropdown displays the list of supported countries and regions that you can call. You can also view and call from the most recently dialed called numbers. By default, the last 20 calls that you’ve received or made are displayed.
     - In the profile dropdown, the outbound profile and the phone number that you're using to make the call is displayed. This is the outbound calling number that is displayed on the customer's phone when they receive your call.
     - You can call those phone numbers only whose regions are configured in the outbound profiles.
     - The dropdown displays the list of supported countries and regions from all the outbound profiles assigned to you. 
     - When you enter the number you'd like to call, the application identifies the outbound profile that has the dialed number's country or region configured.
     - By default, the number pad is hidden. To display the number pad, select the number pad icon.
       > [!NOTE]
       > - The enhanced outbound dialer is an early access feature. You can opt in early to enable these features in your environment, which will allow you to test these features and then adopt them across your environments. For information about how to enable these features, see [Opt in to early access updates](/power-platform/admin/opt-in-early-access-updates). 
       > - Your administrator must also enable the **Enhanced outbound dialer experience** setting definition in Power Apps.<br>

 If your administrator hasn't enabled the early access feature, when you call a customer, on the number pad that appears, enter the customer's country code, phone number, and then select **Call** to make your call. You don't have to add the plus sign (+) to the number.<br>
3. Select **Call**. 

 > [!NOTE]
 > If you aren't assigned an outbound profile, you won't be able to make a call.


 :::image type="content" source="../media/outbound-dialer.png" alt-text="Outbound dialer for voice calls.":::

When the call connects, you see the customer details on the conversation page. Based on your outbound calling profile, the transcription and recording starts. If your capacity profile has a limit of one outbound call at a time, you can't make another call when a call is in progress.

> [!NOTE]
> If you need more trial minutes or phone numbers, we recommend that you file a request with Microsoft Support.

## Next steps
[Use agent dashboard and call controls in the voice channel](voice-channel-agent-experience.md)  

### See also

[Overview of the voice channel](../administer/voice-channel.md)  
[Use trial phone numbers in the voice channel](../administer/voice-channel-trial-phone-numbers.md)

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
