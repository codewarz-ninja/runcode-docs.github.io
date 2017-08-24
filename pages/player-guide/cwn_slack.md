---
title: The Codewarz Slack Team
keywords: slack,slackchat
summary: "Codewarz is on slack.com! Join us on slack for questions, comments, or good company."
sidebar: cwn_sidebar
permalink: cwn_slack.html
folder: player-guide
---

## Follow us on twitter
*[@codewarz_ninja](https://twitter.com/codewarz_ninja)
*[@funtimes_ninja](https://twitter.com/funtimes_ninja)
*[@ohai_ninja](https://twitter.com/ohai_ninja)
*[@ryko212](https://twitter.com/ryko212)
*[@ehlo_nazwadi](https://twitter.com/ehlo_nazwadi)

## Join us on slack.com

Codewarz has a slackchat channel for questions, comments, submission feedback,
and general interaction with the rest of the codewarz community.

When you receive an account invite, you should also have received an invite to
join our slack channel at [codewarzteam.slack.com](https://codewarzteam.slack.com).

For more detailed documentation on slack chat, visit their help site here: (https://get.slack.help/hc/en-us/categories/200111606-Using-Slack) 

## Installing Slack Apps

Slack chat has several apps you can [download](https://slack.com/downloads/) for whichever platform you're using.  By installing one of the apps, you'll be able to take advantage of the slack links we use in the rest of this documentation.

Slack Apps are available for desktop as well as mobile devices.

## Codewarz Public Slack Channels

When you join us on slack, you'll find two basic channels available:

* [#general](slack://channel?team=T0HJEJNAH&id=C0HJEJNBF) - discuss anything related to Codewarz **do not share solutions**
* [#codewarz-game-channel](slack://channel?team=T0HJEJNAH&id=C0HJFMKU3) - intended for general discussion about challenges; this is also where `solves-wootbot` will post feedback about player submissions **do not share solutions**

## Codewarz Private Slack Messages

You can send private messages to anyone you see online.  This is the preferred
method to speak with an admin if you have an issue.

If you think you're having an issue with a challenge, first look closely at both
the problem description, as well as the example provided on the challenge page.
Then make doubly sure you've done thorough testing on any edge cases not explicitly
ruled out of the problem definition.  An admin can help out if you're totally stuck,
but don't abuse the help.  Be prepared to discuss what you've tried.

## Send a message to an admin
* [Chat with Funtimes](slack://user?team=T0HJEJNAH&id=U0HJJ9ZSB)
* [Chat with Nazwadi](slack://user?team=T0HJEJNAH&id=U0JM4TJC8)
* [Chat with Ohai](slack://user?team=T0HJEJNAH&id=U0HJEMKTP)
* [Chat with Ryko212](slack://user?team=T0HJEJNAH&id=U0HJE697E)

**Do not collaborate on solutions through private messages.**

## Chat Bots

We have also implemented a few chat bots to keep things interesting.

* solves-wootbot - `wootbot` hangs out in the #codewarz-game-channel and lets
  everyone in the room know when a player's submission passed, failed, or died while running
* grace - `Grace` is a nod to Grace Hopper, and provides helpful information regarding
  player stats, challenge stats, player scores, and the top 10 high scores

### Grace Commands

Grace is the friendly codewarz chat bot that provides some helpful integrations with the Codewarz public API.  The following commands are available from any public channel as well as by messaging Grace directly.  When following the examples below, remember that you don't need to include the `<` and `>` characters - they're just there to show the template.

* `!highscore` - provides the top 10 highest scorers on the Codewarz `Internets` leaderboard
* `!chall <challenge_name>` - provides information about a specific challenge.  Example: `!chall hello_world`
* `!userstats <username>` - provides player statistics about a specific user.  Example: `!userstats nazwadi`
* `!faq <#>` - provides the description for a specified faq number. Example: `!faq 1`
* `!score <username>` - provides the player score for a specified player.  Example: `!score nazwadi`

{% include links.html %}
