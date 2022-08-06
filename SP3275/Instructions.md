---
label: Instructions
layout: default
icon: ":white_check_mark:"
order: 0
author:
  - name: Matthew Sung
    email: matthew.sung20@sps.nus.edu.sg
    link: https://sps.nus.edu.sg/user/matthew.sung20/
    avatar: https://sps.nus.edu.sg/wp-content/uploads/ultimatemember/171/profile_photo-190x190.jpg?1658781280
---

# Setting up SSH

## Legend
==- Click me to expand!
In this little write-up, certain steps are just for your information. They will be noted by a gray information box, like the one below!

!!!secondary More Information

In a box like this!

!!!

At the same time, some boxes are just a little test to see if you're still following. They have a pretty checkbox beside them and are green!

!!!success Exercise
How many Pis does SPS have?
==- Answer
Honestly, no idea. But great question!
!!!

===

## Why?

Welcome to your very first lesson on Secure SHell (SSH) networking!

You might be wondering why you'd be learning this as part of The Earth. Well, it turns out, working with a monitor and a keyboard in the field is difficult. It'll be easier to use a keyboard and mouse that we carry around in our pockets.. hey, that's a phone, isn't it?

(Diagram of connecting Pi to the phone)

### Interface
We're used to an interactive interface. In the world of programming, this is called a GUI -- or Graphical User Interface. Instead, we'll be using a text based interface, in the command line. This is Secure Shell!

(Picture of Secure Shell Terminal)

In SSH, there is both a server and a client. Just imagine -- the server is the brains doing the work, the client is the one talking to you. It'll be easy to identify that the Pi is the server, and your phone is the client!

### Basic Networking

So, your Raspberry Pi needs to talk to your phone. This means they need to be on the same network.

!!!success "Exercise"

Can you think of a way to create a network when you're outside?

==- Answer
The answer to the question above, which should be obvious, is to use a personal hotspot on your phone.

===
!!!

We will be first creating a network, getting the Pi to join it, then ssh'ing in.

---
Next thing: Different things on a network have different addresses. These addresses are used to find where information is to be delivered to. These are called IP Addresses[^2]! These are usually assigned in sequence of joining, with a common starting prefix!

Let's say I've just returned home, and my phone has connected to my home network. After that, I used my computer on my home network, and finally turned on my printer to print something through Wi-Fi.

The order of stuff connected:
1. The router (always connected!)
2. My phone
3. My computer
4. My printer

If I check the addresses for my devices, it would look like this:

| Order | Device      | IP Address  |
|-------|-------------|-------------|
| 1     | The Router  | 192.168.1.1 |
| 2     | My phone    | 192.168.1.2 |
| 3     | My computer | 192.168.1.3 |
| 4     | My printer  | 192.168.1.4 |

Notice any patterns? There's a common prefix - `192.168.1`, then a dot `.`, then a number in the order of joining!

!!!info Why are we explaining this?
It'll come in handy later, don't worry!
!!!

## Requirements
1. A phone (iOS or Android)
2. A Raspberry Pi
3. Some brain cells [^1]
4. A monitor, keyboard and mouse for setup.

[^1]: Likely will be required. 

![Raspberry Pi](<resources/RPi.png>)


## First Time Setup

### Installation of Termius
We'll be making your phone a SSH client. To do so, download Termius for your phone. QR codes for both platforms attached + linked.

||| iOS
![](<resources/Termius iOS.png>)
[![](<resources/App Store.png>)](https://termi.us/ios)
||| Android
![](<resources/Termius Android.png>)
[![](<resources/Google Play.png>)](https://termi.us/googleplay)
|||

!!! Heads up!
Make sure you're able to bring out this exact same phone for fieldwork!

!!!

For setup, you do not need to create an account -- you'll only be using Termius on this phone.

### Raspberry Pi Setup

1. You'll need to plug in the monitor, keyboard and mouse into the Pi.

2. Start a personal hotspot on the phone.
==- :question: Ahh, I don't know how to start a hotspot!
+++ iOS :iphone:
1. Head to Settings
2. Click on Personal Hotspot
3. Enable "Allow Others to Join"

You're done!
+++ Android :telephone_receiver:
1. Head to Settings
2. Click on Network & Internet
3. Click on Hotspot & Tethering
+++

===

!!!warning Special Characters
You'll have to make sure the name of your hotspot has no special characters! This means renaming your phone to a friendly name. No aprostophes!

Examples:

:x: Matthew's iPhone

:white_check_mark: Matthew iPhone
!!!


3. Once the Pi is up, go to the top right of the screen, and click on the Wi-Fi icon.

4. Select your Wi-Fi network, and key in the password.

5. You're done!

6. Note down the name of your Wi-Fi network, and its password. You'll need it if there's debugging to do on the field!

---

## On-field SSH

!!! :zap: Test before fieldwork!
Right, the title says on-field; but you should really try it once before heading out.
!!!
### Explanation on SSH

Before we continue, let's explain a little more about SSH. We need to tell the client where to log in to.

Two (Three) important details!

- To login to a computer, you need to know where it is first!
This is called an IP Address. [^2]
- Computers also have different users too, so you'll need to know that too.
We use `student` for this module!
- Each user has a password. For the `student` user, it's set to `SPS`.

Now, we have to specify this to our Client!
```
ssh username@127.0.0.1
```
In this case, `username` is our username, and `127.0.0.1` is the IP Address.

After telling this to a client, it will ask the server for permission to log in. Of course, the server would ask for a password, and that's the next thing you'll see.
Don't worry, you won't see stars when you type in your password, but that's alright.

---
### Setup

[^2]: Internet Protocol Address

1. Question: Did you use an Android device or an iOS device for the hotspot?

+++ iOS :iphone:
Congratulations! A tried and tested route.

1. Check if the Raspberry Pi has successfully connected to your hotspot.
Do so by checking in Control Center, and checking the number of connections.
It should say 1 connection.

!!! No connections?
Don't worry, just restart the Pi by turning it off and on again.
!!!

2. Go to Termius.
3. In the sidebar, go to Terminals.

!!!success Short quiz!
The starting prefix for the IP addresses generated by an iOS hotspot is `172.20.10`. What would the address of the first device that gets connected (after the router) be?
==- Answer
`172.20.10.2`
===
!!!
4. In the text bar up top, click it, then key in:
`ssh student@172.20.10.2`

5. You should have a pop up asking for a password. Key in the default password `SPS`.

!!!info Can't find the host?
Don't panic, the device may not be the first thing connecting to your hotspot.. Try with different IP addresses, with the same prefix!
!!!

Congratulations, you're in! Absolute `H A C K E R !`

*Continue on to Step 2 -- SSH Process.*


+++ Android :telephone_receiver:
Congratulations! A tried and tested route.

+++

2. SSH process

Now that you are logged in to the pi, you should see something like this!

(Picture of SSH interface)

This now serves as the primary way to communicate with the Pi.

Just like any graphical interface, we are currently in the home folder.

!!!secondary (Optional!) More Information
How do you check where you are in the filesystem?

`pwd`, or Path to Working Directory, will show you where you are currently at (Working Directory)
![The command line indicates that we're currently in the `folder`]()

---

To see what's in the current directory, we want the server to list the stuff inside! Running `ls` (list) would show what's inside.

---

To move between directories, use `cd` (Change Directory), and specify which folder to go to.

`cd Desktop` moves you to the Desktop folder!

To go back to the parent folder, use `cd ..`.
!!!

Right now, you can just run the script to log data directly. This is similar to double-clicking on the script that is in the desktop, when you were using a monitor. This is done by typing the following into the terminal, then pressing enter.

```
./live_copy.sh
```

!!!secondary (Optional!) More information
The little `./` before the name of the script tells us that we are trying to run the script.

!!!success Little quiz!
How do you run the `live_results.sh` script?
==- Answer
`./live_results.sh`
===
!!!

You should now see something like this, showing that the data is being logged! When the numbers flash, a new reading has been taken and it's highlighting the changes since the last readings.

### Gracefully Shutting Down
!!!danger Force Shutdown
Shutting your Pi down forcefully is bad (by removing the power) -- it won't know that it needs to save your data.
!!!

To shut down your Pi and save all the data inside, run:
```
./shutdown.sh
```
---
## :clipboard: Quick Reference Guide!

1. Create your personal hotspot.
2. Open Termius and navigate to Terminal.
3. SSH into the Pi.
    `ssh student@(ip address)`
    Password is `SPS`.
4. Run the data copying script.
    `./live_copy.sh`


