# Advisor Email Training

Two pages for the Keypath advisor team, on writing emails people actually answer.

| Page | File | What it is |
| --- | --- | --- |
| Who Wrote It Better | `index.html` | A five round quiz. Judge three versions of every line, build an email, see what happens. |
| Write So They Write Back | `guide.html` | The written guide the game is built on. |
| The Email Deck | `deck.html` | A 28 slide version of the guide, for running live in a huddle. |

Both pages share a favicon, `favicon.svg`, embedded directly in each file so they stay self contained.

All three link to each other, so the hub only needs one link. Point it at the root.

No build step, no dependencies, no install. Three HTML files.

## The game

Five rounds, one per part of an email: subject line, first line, the middle, the ask,
the close. Three options a round, one weak, one okay, one strong, shuffled.

It plays as a quiz. During the rounds there is no feedback, no grading and no running score.
Your pick drops into the draft and you move on. Everything is revealed at the end: your score,
every line graded with the reasoning, the strongest option for anything you missed, and what
happened next.

Two points strong, one okay, none weak. Ten per scenario. Eight scenarios: four on student contact
covering warm, firm but kind, repair and last chance, plus four deliberately silly ones (an all
staff email about the office fridge, getting money back off a friend, ending a reply-all storm,
and asking a neighbour about her rooster) that drill the same
five part structure without anyone having to think about their own job.

Click a tile or press A, B or C. The keyboard shortcuts make it quick to run live with a
room voting out loud.

## Editing the writing

All the game content sits at the very top of `index.html` inside `const SCENARIOS = [`.
Everything below that is the engine and you should not need to touch it.

Each scenario:

```
{
  id: "assessment",
  name: "The missing assessment",
  tone: "Warm",
  blurb: "shows on the menu card",
  student: "Sarah Mitchell",
  brief: "the situation the player reads",
  steps: [ ...five rounds... ],
  outcomes: { strong: {...}, mixed: {...}, weak: {...} }
}
```

Each round:

```
{
  part: "Subject line",
  job: "Make the promise",
  prompt: "the instruction shown to the player",
  tiles: [
    { tier: 0, text: "the weak option", why: "why it is weak" },
    { tier: 1, text: "the okay option", why: "why it is only okay" },
    { tier: 2, text: "the strong option", why: "why it works" }
  ]
}
```

`tier` is the score. The three options are shuffled every play, so the order you write them
in does not matter.

`outcomes` is the student's reply. `strong` shows at 8 or more, `mixed` at 5 to 7, `weak` at
4 or below.

### Adding a scenario

Copy a whole scenario block, paste it inside the square brackets, change the text, give it a
new `id`. Every scenario needs five rounds and every round needs three tiles.

### What will break it

- A missing comma between blocks.
- A curly quote instead of a straight one. Editing in Word will do this silently and the page
  will go blank. Use Notepad, VS Code, or edit on GitHub directly.
- Using the same `id` twice.

A blank page after an edit means a syntax error. Undo the last change.

## Deploying

Same as the GROW portal.

```bash
git add -A && git commit -m "your message" && git push
```

GitHub Pages redeploys in about a minute.

Do not put the working copy inside OneDrive. OneDrive sync and git repositories corrupt each
other. The working copy lives at `C:\Users\greg.banks\github\advisor-email-training`.

## Known limitations

- Scenarios and outcomes are written examples, not real cases. Swap the student ones for real
  anonymised ones when they are available.
- The tone advice in the guide, particularly the firm section, has not been signed off by
  anyone at Keypath.
- Scores are held in memory for the session only. Refreshing clears them. Recording scores
  per advisor needs a backend, which this does not have.
- Fonts load from Google Fonts. Behind a firewall that blocks them, both pages still work and
  fall back to system fonts.

## The deck

`deck.html` is the same material as the guide, condensed for presenting. 28 slides.

- Arrow keys, space, or the on-screen buttons to move.
- `C` opens the contents grid so you can jump to any slide. `Esc` closes it.
- Swipe left and right on a phone or tablet.
- Every slide is deep linkable. `deck.html#14` opens straight on the three checks.
- `Home` and `End` jump to the first and last slide.

Use the deck to run a huddle and the guide as the thing people go back to afterwards.
