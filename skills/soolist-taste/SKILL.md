---
name: soolist-taste
description: Reads the user's taste profile in Soolist — per list, the scale, which dimensions they weigh most, how many things they rated and how generously, their favorites and least favorites, and what they are in the middle of or planning — compares their taste with another person's, and suggests people they may know. Use when the user asks what they like, wants a recommendation, asks how their taste compares with a friend's, or wants people to follow.
---

# Taste profile

## Quick start

1. Follow `soolist-session`.
2. Call `taste_profile_show` once. It covers every one of the user's own lists.
3. Answer from it; open a topic with `topics_show` only when you need its dimension scores or notes.

## Reading it well

- `averagePercent` (0–100) compares generosity across lists with different scales; `averageScore` is on the list's own scale.
- `dimensions` weights show what matters most to them in that list (higher weight = matters more).
- `top` and `bottom` use each topic's latest rating. `bottom` is worst first.
- `inProgress` and `planned` are what they are doing next — do not recommend those back as new.

## Comparing with someone

- `taste_compare` with a `username` (from a friend, a note author, or `friends_suggestions`).
- `agreement` is 0–100 over the titles both rated (`overlap`). While `reliable` is false, call it an early signal.
- `agreements` / `disagreements` name the titles; scores are on each person's own scale (`scaleMin`–`scaleMax`).
- `theyLoved` is a ready-made recommendation list: titles the other person scored highly that the user has not tried.
- An error means one of them turned taste matching off or the person cannot be seen. Say so; do not retry with other spellings.

## People they may know

- `friends_suggestions` lists friends of friends and space mates, best taste match first, with `sharedRatedTitles`, `agreement`, `mutualFriends`, and `sharedSpaces` as the reasons.
- `tasteMatching: false` means the user turned taste matching off in privacy settings; there are no suggestions until they turn it back on.
- There is no tool to send a friend request; point them to the person's profile in Soolist.

## Hard boundaries

- The profile includes private lists. Do not quote it anywhere public (for example in a shared note) unless the user asks.
- Recommend things that are not already in the profile. If you want to add one, create a topic and mark it `planned` (`soolist-track`) only after the user agrees.
- Passing something on to a friend is `soolist-recommend`.
- The web app has a "Copy taste profile" button in account settings that copies the same summary as text.
