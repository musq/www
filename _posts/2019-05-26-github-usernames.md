---
layout: post
title: GitHub usernames
categories: Hackathon
---

How hard is it to change GitHub username to a short word?

Last week I decided to change mine from a 14 letter word to some 4-6
letter word. Don't ask me why. *I was fed up typing long words!*

The new username should ideally be ---

- Comfortable in speaking
- Easily pronounceable
- Faster to type
- Visually good looking

### The hunt

My quest began manually with initial candidates as *ashr*, *friday*,
*ranj*, *aran*, etc. **All of them turned out to be taken.** It soon
became clear to me that this method isn't going to work.

> *Why do it manually, when a machine can do it for you!*

It was time to fire up python. I wrote a script to ---

1. Generate random 4 letter pronounceable words with less than 3
syllables
1. Check if this word has already been pinged
1. If not, ping this username's GitHub profile page and log this ping
for step 2
1. If the response code is 404, it means this username's profile page
doesn't exist. So, it's available. Store this username in a file

I let the script run overnight with a 0.2 second delay between each
request (to avoid being blacklisted by GitHub for spamming their
servers). Out came 516 usernames, of which **I shortlisted 16 fitting
the aforementioned four criteria**.

*byof*, *taby*, *cifo*, *ryhy*, *tdry*, *psod*, *jesi*, *udti*,
*ipby*, etc.

These were potentially good candidates for random words, but there
was something I hadn't explored yet.

> *Could it be that I was missing out on some good dictionary words? I
> must be, right?*

To weed out this possibility, I rewrote step 1 to iterate over
3, 4, 5, and 6 letter dictionary words. The script ran for 6 hours
with ~30000 words. The result set was enormous comprising ~5000 words.
(***Notice ~25000 words were already taken as usernames***). It took
me over half hour to shortlist 53 out of them.

*train*, *spor*, *render*, *butyne*, *upcut*, *riser*, *talc*,
*brand*, *frenzy*, *july*, *swab*, etc.

> *Wow! There are so many good options. I don't know what's best.*

I gave 5 people this list and asked them to anonymously pick a maximum
of 10 names that they considered the best. From the responses I figured
out the most desirable one. ***riser*** it is! Let's apply it.

![Username is already taken](/assets/img/github-usernames-taken.png)

Wait a second. Let's try ***train***.

![Username is unavailable](/assets/img/github-usernames-unavailable.png)

Ummm, what?

### Realization of truth

It turns out that there are 2 more categories of usernames which
I didn't know about.

- **Reserved words** - Certain words like *train*, *cache*, *tour*,
*sudo*, *team*, etc are not available as usernames to the public. They
are reserved for use by GitHub.
- **Squatted names** - When you change your username from A to B, GitHub
redirects all the requests from A to B. To maintain this link, the
username A is not made public immediately. However, according to their
[Name Squatting
Policy](https://help.github.com/en/articles/name-squatting-policy) you
can contact GitHub asking them to open username A to public and they'll
happily do it, if possible.

All right then. I'm going to email them asking to free up ***spor***!

![Email requesting a
username](/assets/img/github-usernames-email-ashish.png)

*4 hours later*

![Email response declining my
request](/assets/img/github-usernames-email-laurie.png)

Hmmm. Disappointed. At least the support team is incredibly nice.
No worries, we'll get back to manual hunting.

*muly* - Unavailable

*musy* - Unavailable

***musq*** **- Bingo!**

Well, that was quick. I guess humans win this round. Interestingly,
it was a good ride of two days. Got to learn new stuff.

### Conclusion

*So, how hard is it to change GitHub username to a short word?*

Turns out, it's not so trivial.

---

### Source Code

[github-available-usernames](https://github.com/musq/github-available-usernames)
