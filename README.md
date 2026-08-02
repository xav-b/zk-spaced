# zk-spaced

Spaced repetition memoization for [zk](https://github.com/mickael-menu/zk).

## Setup

### Install

1. Have rust and cargo install: e.g. [using rustup](https://rustup.rs/)
2. Build it: `cargo build --release`
3. Move the binary into your `$PATH`: e.g. `mv target/release/zk-spaced ~/.local/bin/`
4. `command -v zk-spaced` (don't try to run it, it's designed to wait for zk
   entries on stdin and will wait for it)

### Configuration

Add an alias either to your `~/.config/zk/config.toml` or to the notebook
specific configuration:

```toml
[alias]
review = "zk list --quiet --tag review --format json | zk-spaced"
```

You can adjust the tag `review` to match all notes/cards you want to learn.
Make sure to tag the notes.

TODO Make it collapsed

1. Prepare where we will store the cards: `mkdir $ZK_NOTEBOOK_DIR/anki`
2. Create a new template: `$EDITOR $ZK_avavevev/.zk/templates/anki.md`

```md
---
id: {{dir}}.{{extra.deck}}.{{slug title}}-{{id}}
title: {{title}}
created: {{format-date now}}
modified: {{format-date now}}
tags: [review, {{dir}}, {{dir}}.deck.{{extra.deck}}]
---

# {{title}}

{{content}}

```


3. Update the configuration: `$EDITOR $ZK_NOTEBOOK_DIR/.zk/config.toml`


```yaml
[alias]
review = "zk list --quiet --tag review --format json | zk-spaced"
anki = 'zk new anki --title="${*:2}" --extra deck=$1'
deck = 'zk list --tag "review OR anki"'
```


4. Example usage:
- `zk anki <deck> <front of the card>`
- New card: `zk anki life How to treat a jellyfish bite`
- List cards: `zk deck`

## Usage

Once you run `zk review` for each note that is due, you will see a panel with
the title. Think about the fact you want to remember and press <kbd>s</kbd> to
reveal the body of the note. Based on your own estimate press a number between
<kbd>0</kbd> and <kbd>5</kbd> to rate yourself from total blackout to perfect
recall.

---

### Future plans

- [ ] migrate to https://github.com/gyscos/Cursive or https://github.com/ratatui/ratatui
- [ ] Render markdown when showing the card body
- [ ] Add a screenshot preview to this readme
