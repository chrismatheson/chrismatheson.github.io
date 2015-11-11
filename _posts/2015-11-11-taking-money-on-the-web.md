---
layout: post
title: Taking money on the web
categories:
  - Personal
  - Code
tags: ['thoughts', 'sagepay', 'paypal', 'research', 'code', 'web']
type: post
published: true
---

The next step for unitsofsound is to move the home version onto the web. This means taking money over the web. I have a rough idea
of how much pain this will be, but im soon to find out for sure.

Currently unitsofsound is bought almost exclusively by schools and dyslexia centers who do so with purchase orders and phone calls
rather than webpages and credit/debit cards. This works for them and i have no burning desire to change that. However, i thinkg that
this will not be acceptible to the general public who are our target for the home version. So i begin my journey into what it takes
to accept online payments.

##Knowledge so far

My understanding of online payments so far is not exact to say the least. Ive herd of a few buzz words, companies and terms...

- paypal - yup, used them, know what there about from a customers POV
- strpe - more hipster version fo paypal
- payment gateway - someone/thing who takes payment? do i **need** one? is paypal (etc) a payment gateway?
- merchent account - dunno, some fancy word for interacting with banks?
- magento - php framework for a webshop (i think) hosted option?
- tax rules - sure there was some tax rules etc that have chagned recently

##Goals & requirements

###**NO OPS**

I want to reduce opperations costs as much as possible, SaaS options are welcomed, automations if not, keep it as simple as possible
so there is less to maintain & monitor. This extends a little into the payments, as in, is there a way to refund? what about fraud?
i really dont want to hold credit card info!

###International payments

Maybe not from day 1, but unitsofsound os on the web and one major bonus of that was to futher the reach of students to outside the UK.
so we will need to be able to take payments from USA/Canada and possibly other countries. Ive no idea what repocussions this has in terms
of charges, tax, exchanerates etc.

###Unified flow

Keeping the whole experience fast & painless for the user is a must. Ill bounce out to a know site (paypal etc) if the benifits are there
but if possible it would be desirable to keep the whole thing on our domain.


##TBC

This is a learing journey so ill try and report back progress, descisions etc in the future
