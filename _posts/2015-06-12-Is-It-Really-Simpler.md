---
layout: post
title: Is this really simpler?
categories:
  - Personal
  - Code
tags: ['thoughts', 'architecture', 'code', 'web']
type: post
published: true
---

Recently within my team we needed to provide a new website with some prity basic requirements

- small website for marketing info, help articles etc
- non-dev content creators (not general public)
- new content every 48hrs - week

And this requirement basicly lead me down a rabbit hole of decission paralysis over Dynamic vs Static sites.

Firstly, im a beliver in choosing what you know best, what is widely used, and enevatibly whatever gets the job done. I like to play wiht the newest hip tech, but when its reliability im after, newer does not allways mean better.

When thinking about the best technology for our requirements my mind went to Static Site Generators, over somethign more familiar like Wordpress or Durpal* or even a hand crafted Dynaimc . . . well anything.

With tools like Travis, CircleCI and AWS Lambda becoming easier, cheaper and more accessable by the day, the concept of pre-generating all pages whenever data changes or on a schedule, and deploying to something as simple as S3 is incredibly apealing to me. No server side code with possible memory leaks, no database, no opperating system (to some extent), all mean less security holes, in the OS, the application stack, language, databse (injection), less opperations work to impliment backups, performance tuning etc etc.

But why am i thinking like this? whats wrong with Dynamic sites basied on something like Wordpress, running on a traditional LAMP stack? Its been working for years and if its good enough for Facebook, surely its good enough for me?

Well i thought i would write down my toughts to try an clarify, to myself, the thoughts i have that somehow make up the gut feeling that if its possible with a SSG, then thats the right option.

##Worry number A - Databases.

Its a little irrational, and i think a little rational. Databases require, backups, migrations, indexes, etc. Maybe not all right from day one, but sooner or later. This is not something i enjoy, and so therefore scares me a little. I tend to hand of any DB ops i can to a DBaaS and be "done" with it as much as possible.

Migrations can go wrong

##Worry number 2 - Security

My security skills go basicly as far as HTTPS-all-the-things, HASH passwords properly & keep software & OS as up-to-date as possible.

Assuming a SSG product is deployed to something along the lines of S3, hacking a angles are essentally hacking Amazon / the process of getting conent into the system in the first place. But at the end of that there are no computing resources to be had, unlike a Dynamic sites which if compromised by software vulnerabilities in the HTTP server, SSH server (im assuing will be required), the language (dunno, maybe this is possible), DB injection attacks etc, could give the attacker a full machine to use. Obviously both systems fall down if your overall IaaS access creds are compromised.

##Worry number 3 - Web Scale (yes that was sarcasic)

I do not think that my project is going to reach millions of views per second, and premature optomisation (esp in the architecture) can end up causing more problems than it solves. However let do a completely made up, not data back in any way comparision of the two technologies under certain amounts of load.

<table>
  <tr><td><b>Finctional req/s</b></td><td><b>Dynamic site change required</b></td><td><b>Static site change required</b></td></tv>
  <tr><td>1</td><td>DB indexes</td><td>no change</td></tv>
  <tr><td>10</td><td>DB indexes</td><td>no change</td></tv>
  <tr><td>100</td><td>Caching</td><td>no change</td></tv>
  <tr><td>1000</td><td>Multi Machine, DB clustering, god know what else</td><td>no change</td></tv>
</table>

If your getting enough traffic to cause S3 problems in serving static files. Well i have no idea how you solve that, but i would imagine that by that time you will have other issues and/or hopefully lots of money to combat them.
On the other hand the numebr of WordPress instances that basicly stop functioning without Varnish i imagine to be quite high. Certain queries can clog up the DB connection pool and cuase hours of lost time configuring indexs, but most importantly, mean bad experiences for the user while the issue is being addressed, or possibly even downtime.

##Worry number 4 - Recovery

Enevatibly you, or someone else or something else or some world event **[is](https://en.wikipedia.org/wiki/Murphy's_law)** going to blow everything away.

Most systems run on a database backup strategy of daily/weekly/monthly backups. which means you *should* only loose 24 hrs worth of new data if a machine blows up. However if your home grown back solution has been silently failing for a while . . . well then you could have much more serious problems.

With a static site generator you would essentially be putting the new data into a backup first, then restoring your site from said backup. This seems like a fantastic idea, and essentially forces a "can we restore from backup" test into every release.

##Why does it need to be dynamic?

Most people i talk to here say something along the lines of

<quote>Content will change. I (as a developer / ops) do not want extra work every time content is changed.</quote>

which i would totally understand. But SSG's coupled with some process of collecting gthe content in can still enable a workflow where the dev/ops person is not required in order to release content into production.

the killer answer of course is search. Search is possible with client side plugins which have the search data pre-calculated

##What is dynamic?

A change other than code, affects how your site is supposed to look / work.

Content added means new front page, new search results, new sitemap possibly, etc.

When you consider that most "Dynamic" sites are actually impliment some degree of caching in order to reduce load on the machines doing the processing of these stimuli, and a workflow of SSG can takes somewhere beween 0.2s and 3mins to generate and upload a reanonable sized site. Is there really any difference?

If on every wordpress article save, every possible page was rendered and stored into cache, whats the point of having the original instance still running?

Im not even bothered about the technology used to do the generation.

So why do **I** seem to favour SSG over Dynamic when really it does not look like there is a huge amount of difference?

I think my main worries come down to the process for a new article / blog / page / whatever.

Dynamic.

write content -> upload into database -> view on web -> [scheduled backup delay] -> backup databse.

SSG.

write content -> add content to project -> [scheduled build delay] -> deploy new site.


It seems to me that the second process offers a fundamental advatage that you cannot actually get something "out" without it being "backed up" in a way that can regenerate the exact same thing.

This is not allways the case fo databases. Backups can fail, Restores can fail.


 - analogy - JIT production vs stockpiling


 * to others not me, ive not had the priviladge of developing for either platform.

 N.B. Ive been looking for someone to help write the answer to this post, exsoling the virtues of dynamic sites. No takers of yet.