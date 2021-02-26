---
title: "Code Through Assignment - pushoverr"
author: "Tim Ness"
date: "`r format(Sys.time(), '%d %B, %Y')`"
output:
  html_document:
    df_print: paged
    highlight: haddock
    theme: darkly
    toc: yes
    toc_float: yes
    number_sections: TRUE
  pdf_document:
    toc: yes
  word_document:
    toc: yes
---

```{r include = FALSE}

library(pushoverr)

```
***

# Introduction to pushoverr

'pushoverr' is a package that sends push notifications from R to a selected device. It works in conjunction with the Pushover app which must be installed on the device. 

The package was developed by Brian Connolly in 2016. It was created so R scripts could send messages to the user while the user was away from their computer.

In this introduction, we'll be looking at the basic setup of the app and the process for sending messages.

<br>

**Dig Deeper:** You can learn more on [**Connolly's GitHub page **](https://github.com/briandconnelly/pushoverr) or the [**package introduction**](https://cran.r-project.org/web/packages/pushoverr/pushoverr.pdf) directly on CRAN. You can check out pricing guides and detailed support articles on the [**app's official website**](https://pushover.net/).

<br>

***

# Setting Up 'pushoverr'

There are two components needed to make the process work:

1. The 'pushoverr' package installed and loaded into R or R Studio
2. The Pushover app installed on the device on which you will be receiving notifications

Note: The app has a 30 day free trial phase and then costs a $5 one-time fee for a single user. Business or team accounts can also be purchased.

<br>

##Install and Load the 'pushoverr' Package in R

Install 'pushoverr' using the code below:

<br>

```{r eval = FALSE}

install.packages("pushoverr")
library(pushoverr)
```

<br>

##Set up the Pushover App

The Pushover app is available to download and send alerts for Android, iOS, and Desktops. Find and download it from the Apple App Store or Google Play Store.

<br>

![App Store](https://i.imgur.com/z0HBqOn.png)

<br>

Create an account with an email address and password. You will automatically be given a user key which will be emailed to you and can be found in your settings in the app or your account on the 'pushoverr' website.

<br>

![Email](https://i.imgur.com/iO3cqRZ.jpg)

<br>

You must also navigate to 'Settings' and then to 'Your Applications' to set up an API Token. Both the user key and the API token will be needed.

![API token](https://i.imgur.com/m8leC9C.jpg)

<br>

***

# Sending Messages

While the package contains quite a few functions to allow you to customize messages, we'll go through a few common functions here regarding how to send different types of priortizied messages.

<br>

##Adding Tokens to Your Environment

You will need the user key and API token every time you want to send a message. If you do not want to include them as arguments each time, you can add them to your R environment.

Use this code to make additions to your R environment. It will open up another blank tab called '.Renviron' in which you can add "permanent" arguments.

<br>

```{r eval = FALSE}
usethis::edit_r_environ()
```

<br>

In the blank '.Renviron' tab, enter your user key and API token like this. 

PUSHOVER_USER = "User Key"

PUSHOVER_APP = "API Token"

Each will actually be a long string of numbers and letters like 'alseinrnd785alskwyrkj495alksdfj'.

Once you have added them, you will need to restart R, making sure to save changes.

<br>

##Sending a Standard Message 

If you have set up the user key and API token in the R environment, then sending a standard message is very easy, with one argument - the message. This notification will make the sound (or not make any sound) and abide by the quiet hours set in the recipients Pushover app settings.

<br>

```{r eval = FALSE}
pushover(message = "Is this thing on?")
```

<br>

If you have not added the user key and API token to the environment, then they will need to be added as separate arguments.

<br>

```{r eval = FALSE}
pushover(message = "Is this thing on?", user = <USER KEY>, app = <APP TOKEN>)
```


<br>

Here is what the push notification looks like.

![push notification](https://i.imgur.com/jVzxjcX.png)

<br> 

And here is what the app's inbox looks like on an iPhone.

![Pushover inbox](https://i.imgur.com/BSPb7ja.png)

<br>

##Sending More Polite Messages

You can send a message that won't even show up with a notification but will only go directly to the app's inbox without making a noise.

<br>

```{r eval = FALSE}
pushover_silent(message = "Zzzzzzzzz")
```

<br>

A message that will generate a push notification but not attempt to make any noise or vibration is a quiet message.

<br>

```{r eval = FALSE}
pushover_quiet(message = "Zzzzzzzzz")
```
<br>

##Adding Urgency to Your Messages

If you need to make sure your message gets through, there are also two categories to add some urgency.

A high priority message will show a push notification and make a sound even during the recipient's set quiet hours. In the app's inbox, the message preview will have a High Priority note.

<br>

```{r eval = FALSE}

pushover_high(message = "Wake up!")
```

<br>

And finally, an emergency message will send repeated push notifications until the message is opened and the recipient clicks or taps a link acknowledging that they've received the message.

<br>

```{r eval = FALSE}
pushover_emergency(message = "The script is coming from inside the house")

```

![Inbox Emergency](https://i.imgur.com/vTKIcN2.png)

![Emergency Acknowledgement](https://i.imgur.com/hhU2TCk.png)
<br>

***

# Summary

'pushoverr' is a responsive tool that can be useful to users who want to know when developments or alterations are being made in a script. It could send a message when a scenario has finished running, or when a large data set has been imported. Or it could alert a user when a website made with R has been engaged or modified. If you want to know what is happening with your script but don't want to stay at your computer and watch it run, then 'Pushoverr' is an excellent solution.

<br>

***

# Further Resources

Check out these links to learn more about package 'pushoverr'.

* [**Pushover App website**](https://pushover.net/)
* [**CRAN Introduction to Pushoverr**](https://cran.r-project.org/web/packages/pushoverr/pushoverr.pdf)
* [**Brian Connolly's GitHub page**](https://github.com/briandconnelly/pushoverr)
* [**Using pushover with R**](https://seanmeyerdesign.com/using-pushover-with-r/)
* [**pushoverr: Send Push Notifications using Pushover**](https://rdrr.io/cran/pushoverr/)
