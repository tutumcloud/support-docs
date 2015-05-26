Tutum can integrate with your **Slack** team to provide notifications about stacks, services, containers and nodes.

## Setting up the integration

Go to your Slack team's integration settings and search for the **Incoming WebHooks** integration:

![](https://s.tutum.co/support/images/slack-incoming-webhooks.png)

Click on **Add**. In the next screen, select the channel where you want Tutum notifications to be posted, and click on **Add Incoming WebHook Integration**:

![](https://s.tutum.co/support/images/slack-select-channel.png)

In the next screen, copy the **Webhook URL** that is displayed:

![](https://s.tutum.co/support/images/slack-webhook-url.png)

Now, go to your [Tutum notification settings page](https://dashboard.tutum.co/account/#container-notifications) and click on the **Add integration** button on the **Slack** row:

![](https://s.tutum.co/support/images/slack-notification-settings.png)

Enter the **Webhook URL** you just copied in the modal shown, and click on **Save integration**:

![](https://s.tutum.co/support/images/slack-configuration-modal.png)

Once configured, select the desired notification level:

* **Off** to not receive any notifications
* **Only failures** to receive notifications about failed actions, containers that stop with a failed exit code and nodes that become unreachable
* **Everything** to receive the above plus notifications about successful actions

