Tutum currently uses private SSH keys to provision the nodes that it manages. Unfortunately, it is not currently possible for you to SSH into nodes that have been provisioned by Tutum. 

Fret not, however, as that will be changing soon. We plan to allow users to bring their own SSH key(s) which will automatically be added to `~/.ssh/authorized_keys` when the node is provisioned. This will let you SSH directly into each and every of their tutum-managed nodes, giving you the ability to run other applications/services alongside your containers. 

Expect this feature to be ready during Q1 2015.