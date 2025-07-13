---
title: GitHub usernames
---

How hard is it to change GitHub username to a short word?

Last week I decided to change mine from a 14 letter word to some 4-6
letter word. Don't ask me why. _I was fed up typing long words!_

The new username should ideally be ---

- Comfortable in speaking
- Easily pronounceable
- Faster to type
- Visually good looking

### The hunt

My quest began manually with initial candidates as _ashr_, _friday_,
_ranj_, _aran_, etc. **All of them turned out to be taken.** It soon
became clear to me that this method isn't going to work.

> _Why do it manually, when a machine can do it for you!_

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

_byof_, _taby_, _cifo_, _ryhy_, _tdry_, _psod_, _jesi_, _udti_,
_ipby_, etc.

These were potentially good candidates for random words, but there
was something I hadn't explored yet.

> _Could it be that I was missing out on some good dictionary words? I
> must be, right?_

To weed out this possibility, I rewrote step 1 to iterate over
3, 4, 5, and 6 letter dictionary words. The script ran for 6 hours
with ~30000 words. The result set was enormous comprising ~5000 words.
(**_Notice ~25000 words were already taken as usernames_**). It took
me over half hour to shortlist 53 out of them.

_train_, _spor_, _render_, _butyne_, _upcut_, _riser_, _talc_,
_brand_, _frenzy_, _july_, _swab_, etc.

> _Wow! There are so many good options. I don't know what's best._

I gave 5 people this list and asked them to anonymously pick a maximum
of 10 names that they considered the best. From the responses I figured
out the most desirable one. **_riser_** it is! Let's apply it.

![Username is already taken](/assets/img/github-usernames-taken.png)

Wait a second. Let's try **_train_**.

![Username is unavailable](/assets/img/github-usernames-unavailable.png)

Ummm, what?

### Realization of truth

It turns out that there are 2 more categories of usernames which
I didn't know about.

- **Reserved words** - Certain words like _train_, _cache_, _tour_,
  _sudo_, _team_, etc are not available as usernames to the public. They
  are reserved for use by GitHub.
- **Squatted names** - When you change your username from A to B, GitHub
  redirects all the requests from A to B. To maintain this link, the
  username A is not made public immediately. However, according to their
  [Name Squatting
  Policy](https://help.github.com/en/articles/name-squatting-policy) you
  can contact GitHub asking them to open username A to public and they'll
  happily do it, if possible.

All right then. I'm going to email them asking to free up **_spor_**!

![Email requesting a
username](/assets/img/github-usernames-email-ashish.png)

_4 hours later_

![Email response declining my
request](/assets/img/github-usernames-email-laurie.png)

Hmmm. Disappointed. At least the support team is incredibly nice.
No worries, we'll get back to manual hunting.

_muly_ - Unavailable

_musy_ - Unavailable

**_musq_** **- Bingo!**

Well, that was quick. I guess humans win this round. Interestingly,
it was a good ride of two days. Got to learn new stuff.

### Conclusion

_So, how hard is it to change GitHub username to a short word?_

Turns out, it's not so trivial.

---

### Source Code

[github-available-usernames](https://github.com/musq/github-available-usernames)
