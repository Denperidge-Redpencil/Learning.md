# Things to check out

<details>
<summary>Foreword-ish</summary>


I will be honest: at the point of typing this, the only alternative for me to work on would be continuing [semantikeys](https://github.com/Denperidge-Redpencil/semantikeys) and I am not feeling that right now. I think the toothache I have is making me catty (pun not intended) and it's 6am.

My brain was pingponging as it does; and recalled mentions of things like rocket.chat vs matrix and vendor-lockin being relevant topics. Then I recalled seeing score spec which could be relevant. Then that kept bouncing so I decided I should probably just do a write-up because I hate to admit that among my favourite activities are painstaking research and write-ups.


</details>


## Rocketchat - Matrix bridge
[blog announcement](https://matrix.org/blog/2022/05/30/welcoming-rocket-chat-to-matrix) - [docs](https://docs.rocket.chat/guides/administration/admin-panel/settings/federation/matrix-bridge)

Moving platforms sucks. Because there's no good way to do it. People are used to the workflows and UI's of the previous thing, and may not like the new thing. But using two different but functionally similar platforms is how you get miscommunications. This bridge might allow a slow transition! I wanna test if this perhaps could even import previous conversations. ~~If you're reading this and it hasn't been strikethroughed, I haven't yet.~~ But either way, it's worth checking out.

### Update: findings

See [denperidge-redpencil/rockatrix](https://github.com/Denperidge-Redpencil/rockatrix) to test it out for yourself!

- Some federated functionality is [locked behind enterprise editon and/or not encryptable](https://docs.rocket.chat/guides/administration/admin-panel/settings/federation/matrix-bridge/matrix-users-guide/create-a-federated-rooms#creating-a-multi-user-direct-message-using-slash-command-enterprise-edition-only)
- The Rocket.chat settings say the following: `No user should connect to the homeserver with third party clients, only Rocket.Chat`. I don't know if this refers to the people wanting to send messages through rocket.chat itself to Matrix users, or if they mean that all Matrix traffic should go through Rocket.chat.
    - The [docs](https://docs.rocket.chat/guides/administration/admin-panel/settings/federation/matrix-bridge/matrix-admin-guide/matrixbridge-configuration) say `We strongly recommend not connecting to this Matrix homeserver using other Matrix clients, if you want to do that, please configure another Matrix homeserver instance.`.


## Score spec
[repo](https://github.com/score-spec/spec) - [website](https://score.dev/)

Score is essentially a container/workload configuration tool that translates into {Docker, Kubernetes, custom stuff}. Switching to Score would possibly be very time consuming and not worth the effort, but it is good to keep this jotted down somewhere; in case other container technologies are to be implemented or Docker begins being wack.



## GitHub Actions
I love GitHub Actions. I don't make a profit of my personal projects, and Actions allows me to build & deploy to Pages and Surge without having to worry about building everything locally and then ftp/ssh'ing it into another location. I bring that knowledge into my work, because streamlining & automating development is a very worthwhile pursuit. That being said, if GitHub decides to change Actions/Pages, that would not be ideal, so I feel apprehensive about recommendng/

Here's a few things that might be interesting

### Locally running Actions
This is more of a band-aid if anything in terms of safety around GitHub Actions (as it is merely a local implementation of GitHub Actions), but it's still good to write down: https://github.com/nektos/act.

### Jekyll vs CircleCI vs Drone vs Haskell vs Woodpecker
Okay first of all, lets get a few of the confusing things out of the way

- A bunch of these I have found on the [gitea awesome list](https://gitea.com/gitea/awesome-gitea#devops). This is because Gitea is self-hostable, and the (seemingly) most free hosted git service [Codeberg](https://codeberg.org/) uses Gitea and is even [linked on the gitea page](gitea.com).
- Woodpecker is an open source fork from the last Drone commit before their license became proprietary.
- Drone =/= Harness, however, Harness *did* [buy Drone](https://www.prnewswire.com/news-releases/harness-acquires-continuous-integration-pioneer-droneio-and-commits-to-open-source-301106473.html) and Drone is becoming Harness Community Edition.
- Gitea.com notes that it uses gitea to developer gitea which is great and it also notes that this practice is called [dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food) which brightens my day.



