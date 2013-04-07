# The Complete (hopefully) Guide to Setting Up a Website

*Disclaimer:* The following information has been pooled from multiple sources, found by trial and error, or extrapolated. No responsibility is taken by the author for any incorrect or incomplete information, nor for any unintended effects it may cause. Use the information below at your own risk.

---
## Introduction/Preamble

When I first wanted to make this website, there was a lot of things I didn't know. And I got lots of misinformation from a variety of sources (that I can't remember right now). So I'm going to try to make this a comprehensive guide to setting up a website on Windows, Mac, or Linux. This is going to be a work in progress until I have time to gather screenshots, so bear with me. And, just one last thing: READ THROUGH THE WHOLE TUTORIAL FIRST!

The screenshots will eventually be on all platforms, but for the moment, they are just on Windows. For registrars, I will have screenshots for [name.com](http://name.com) and [NameCheap](http://namecheap.com).

Before we start with the whole website thing, you need to get to know how websites work. Say I am trying to connect to [`en.wikipedia.org`](http://en.wikipedia.org). My computer contacts something called a DNS server. What the DNS server does is it looks up the corresponding IP address of the domain name. So for Wikipedia, the IP address is `208.80.154.225`. I know you're thinking, *"What's an IP address?"* This is slightly difficult to explain. There are 2 different kinds of IP addresses: local IPs and public IPs. In a more general sense, an IP address is a computer's address. 

In a local IP, it's your computer's address *in your home network.* Say you have 2 computers at your house both connected to the Internet. They will each have their own address in your home network. It will probably be something along the lines of `192.168.x.y` (where `x` and `y` vary). That is your computer's address in your home network. It is the only one in your home network with that address.

In a public IP, it's your *network's* address on the entire Internet. I say network because every computer connected to the same Internet connection will have the same public IP. However, your network is the only one in the world with that IP address. 

So, anyways, back to connecting to Wikipedia. Your computer then contacts Wikipedia's IP address (`208.80.154.225`) and says (metaphorically), "Hey Mr. Server! I'm looking for Wikipedia! Is that here?" and the server responds, "Oh, hell yeah! Let me just send you this HTML file that has the front page of Wikipedia on it!"

And there you go. Your computer just connected to Wikipedia and loaded the main page. 

Now, back to making your own:

First, you have to decide if you want to buy a domain. Depending on the extension (i.e. `.com`, `.org`, or `.cc`), it probably will cost around $10 USD a year.

Now, this document is going to split. I'm going to assume for now that you want to buy a domain. If you don't, skip down past the domain section.

---
## Getting a domain

### Picking a domain

First, you need to pick a domain name that isn't already taken. It should be memorable and have a sort of ring to it. If you can get an actual word, it's an added bonus. If you aren't sure where to start, try your name. For instance, if your name is `Joe Bobly`, you might want to consider `joebobly.com` or, in this specific case, `joebob.ly` I recommend using [Domai.nr][1] to get ideas. It'll automatically try to figure out extensions that fit in the word (like `joebob.ly`). However, it's availability checker isn't very good. (It gives lots of false positives and negatives.) I'd recommend checking the availability on [name.com][2] or [IWantMyName][3].

Now that you have your idea in mind (and it's available), it's time to buy.

### Buying the domain

Head over to a registrar website that has good prices. I recommend [name.com][2] again, because it has a simple, easy to use configuration page with lots of options. However, [Namecheap][4] sometimes has better prices.

(Side note: Please **don't** use GoDaddy. The CEO [hunts elephants][5] and may or may not buy the domain you're trying to get and try to sell it to you. That happened to me once and somebody on Gizmodo Whitenoise said they do it a lot. I, however, can't find a link at the moment. Just don't use GoDaddy.)

Once you've found the domain you want to buy on a registrar, purchase it using a credit card. You may or may not want whois privacy (if it's free, get it, but if not, it's up to you). Name.com does a pretty good job of explaining what whois privacy is:

> Whois Privacy allows you to register domain names privately by protecting your contact details such as name, email, address, and phone number from public view.

If someone wants to buy a domain, they must give all of their information, including street address and phone number, to the ICANN (the Internet Corporation for Assigned Names and Numbers). The ICANN then puts that information on public display through whois. If you do a whois search (go to [who.is][6]) on any domain, you get all that info about the person. If you buy whois privacy, however, it hides that info (do a whois search on `boj.cc`, for example).

Anyways, now purchase your domain, with or without whois privacy. (From now on, I'm going to pretend the domain you bouht was `joebob.ly`.) Now, you need to find the dashboard for domains. Find somewhere where it says `Edit DNS Records` or `DNS Record Management` or something. Depending on your registrar, there should be a page for modifying DNS settings. Don't mess with the nameserver addresses (I'll explain those later). There should be a few columns. One of them should be `Type`. Change it to `A`. This tells the DNS server that you want an `A` record. [From Wikipedia](https://en.wikipedia.org/wiki/A_record#A), an `A record`:
>Returns a 32-bit IPv4 address, most commonly used to map hostnames to an IP address of the host, but also used for DNSBLs, storing subnet masks in RFC 1101, etc.

Woah, wait what? That made no sense, right? Let's break that down:
>Returns a 32-bit IPv4 address

We can ignore the 32-bit part. An IPv4 address is just a fancy name for an IP address (well, for our purposes). So back to the `A record` definition. It basically tells the DNS server, "If anyone connects to you looking for `joebob.ly`, send them to this IP address!" The DNS server will gladly do that, as that is its job (remember the Wikipedia example?).

Now, you need to look up your IP address. It's really not hard to look up your IP--it's sent to every website you go to. The most convienient IP address lookup is at [l2.io/ip](http://l2.io/ip). Copy that number, as you are going to need it very shortly.

Now, enter that number in the `Answer` (or similar, as always) section of your domain control panel. For the host, leave it blank if you want people to connect to your website by going to `joebob.ly`, or enter `www` if you want them to connect by going to `www.joebob.ly`. 

Hit save, and we are done configuring your domain!

Now, if you go to `joebob.ly`, your website should be there!

Well, not actually. But, you're halfway there!

##Setting up your server

---

Side note: If you did not buy a domain, you will connect to your website by going to your IP. Find that by going [here.](http://l2.io/ip)

This tutorial is only going to cover self-hosting the website, as that's what I do and know how to do. However, be warned that this requires your computer to be open 24/7. 

There are bundles of software that you need to host websites. They are called [`_AMP`](https://en.wikipedia.org/wiki/AMP_%28solution_stack%29) programs, where the `_` represents the operating system. The `AMP` part stands for [Apache](https://www.apache.org/) [MySQL](https://www.mysql.com/) [PHP](http://www.php.net/), generally. 

Apache hosts the website, MySQL stores data, and PHP is a programming language for the web.

There is a program I haven't looked into yet, called [`XAMPP`](http://www.apachefriends.org/en/xampp.html), which stands for Cross-Platform (X) Apache MySQL PHP Perl. Feel free to try to set that up, but I have no experience with it whatsoever. Just putting that out there.

Now, you need to port forward. This tells your router to send all of the traffic on port 80 (the default port websites run on) over to your computer. Go to [portforward.com](http://portforward.com/) for a terrific guide. Select your router and choose Apache for the program.

###Windows:

Download a program called [`WAMP`](http://www.wampserver.com/en/). This is what you are going to need to actually host the website. It's really not that hard to configure. If you've made it this far in the tutorial, you can do it! If you need any help with that, there is a forum on its site.

###Mac:

Download a program called [`MAMP`](http://www.mamp.info/en/index.html). his is what you are going to need to actually host the website. It's really not that hard to configure. If you've made it this far in the tutorial, you can do it! If you need any help with that, there is a forum on its site (I believe).

###Linux:
Because I don't have a Linux box, I can't do any more of the tutorial for now. However, there is a [really good tutorial](http://lamphowto.com/) on somebody else's website. Just follow that, and you'll be up and running!


##Test

Connect to your website by going to [localhost](http://localhost). If any page loads, you set up the `_AMP` correctly! If not, see below. Now, go to [canyouseeme.org](http://canyouseeme.org/) and press `Check your Port!` If it says `Success!`, then move on. If not, though, go to Troubleshooting below. Our final test: Call up a friend and ask them to go to your website. If they can, you are good! Go ahead and replace `index.php` with any HTML page you can conjure up, and you are good to go!

If you don't have any friends, go to [HideMyAss](http://hidemyass.com) or [Zend2](http://zend2.com) and try to connect through there.

##Troubleshooting

###Did you port forward correctly?

Go back to the portforward guide, fix what you did wrong, and [check again!](http://canyouseeme.org/)

###Could you connect through `localhost`?

If no, see if you can find your mistake, and if not, go to the corresponding forum!

###Your friend can't connect, but portchecking worked and so did the `localhost` test?

Double check your DNS records for your domain.


##One last message

Have fun! Try to learn HTML (go [here](http://codecademy.com) or [here](http://w3schools.com)). Also, please **don't** email me about any problems you have! I'm not free online tech support. I just wanted to put this guide on the Internet so people don't have trouble like I did!


###TL;DR: If you don't have the patience to read this, good luck coding the HTML for your website.

 [1]: http://domai.nr
 [2]: http://name.com
 [3]: http://iwantmyname.com
 [4]: http://namecheap.com
 [5]: http://www.huffingtonpost.com/2011/03/31/bob-parsons-godaddy-ceo-elephant-hunt_n_843121.html
 [6]: http://who.is
