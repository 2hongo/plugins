# 2hongo for Claude

Teach and practice Japanese in Claude, grounded in [2hongo](https://www.2hongo.com)'s dictionary.

The plugin has two halves. A **skill** teaches Claude how to explain, correct, and drill Japanese
consistently — it needs no 2hongo account and works entirely from the conversation. An
**MCP connector** adds 2hongo's stored dictionary data, so readings, meanings, curated examples,
JLPT level, and frequency come from a source rather than from recall.

## Install

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install 2hongo@claude-community
```

Prefer no plugin? The same tools are available as a custom remote connector — add
`https://www.2hongo.com/api/mcp` as a custom connector in Claude and skip the package entirely.

## Account and authentication

The teaching skill works immediately, with no account.

The dictionary tools require a **free** 2hongo account. On the first tool call Claude opens the
2hongo authorization page; sign in or create an account, approve the connection, and Claude
resumes what you asked for. There is no subscription step and no upgrade prompt in that flow —
existing Premium and Pro subscriptions are simply recognized.

The connection uses OAuth 2.1 with PKCE. Access tokens are short-lived and limited to the
permissions you approved; disconnecting the plugin revokes them immediately. 2hongo never receives
your Claude conversation — only the specific word or query a tool call carries.

## Try it

```
Break down 「昨日は友達と映画を見に行った」 for me. I'm around N4.
```

```
Look up 込む in 2hongo and show me the readings and a couple of real examples.
```

```
I wrote 「私は日本語を勉強しました三年間」. Correct it and explain what moved and why.
```

## Tools

| Tool                      | What it returns                                                                                   |
| ------------------------- | ------------------------------------------------------------------------------------------------- |
| `search_words`            | Dictionary matches for a spelling or reading, as stable slugs                                     |
| `search_by_meaning`       | Entries found from a description of the meaning, in any supported language                        |
| `get_word`                | One entry: readings, localized meanings, curated examples, relationships, JLPT and frequency data |
| `get_word_audio`          | The recording, plus a link to the word's page on 2hongo                                           |
| `search_grammar`          | Grammar patterns matching a pattern form or a meaning                                             |
| `get_grammar`             | One pattern's authored explanation, formation, register, and worked examples                      |
| `get_review_summary`      | Words due today, reviews done today, and the current streak                                       |
| `get_study_plan`          | The current 2hongo study plan and which items are done                                            |
| `get_learner_profile`     | Your level and goal settings, plus the stage 2hongo paces you at and your progress through it     |
| `get_practice_set`        | Due, weak, and recently started items from your record, with authored questions where available   |
| `check_reading_fit`       | How much of a text you have already met on 2hongo, and its words and grammar worth learning       |
| `get_content_brief`       | Words and grammar you are learning for Claude to write into new Japanese, and the level to use    |
| `get_progress_insights`   | Recent activity, vocabulary accuracy trends, learning signals, and a concrete next step           |
| `get_jlpt_readiness`      | Coverage of a JLPT level across 2hongo grammar, kanji, vocabulary, basics, and prerequisites      |
| `record_usage_evidence`   | A structured correct-use or error signal for a word or grammar sense the learner produced         |
| `save_word`               | Saves a word into the notebook and its review schedule                                            |
| `update_learning_state`   | Marks a word or grammar sense as learning or known                                                |
| `submit_practice_results` | Grades authored answers and records due-item results, including misses                            |

The last twelve read or change your 2hongo account, so Claude asks for those permissions separately
when you connect — a connection that only searches the dictionary never gets them.

`check_reading_fit` never sends your text to 2hongo. Claude sends only the dictionary forms of its
words, their readings and counts, and the names of the grammar it noticed, and 2hongo keeps none of
them. Likewise, `get_content_brief` is told only whether Claude is writing a story, a dialogue,
examples, or an explanation — never what it is about. Claude writes the text; 2hongo supplies what
to weave in.

Vocabulary and grammar follow the same tiers as the website: a free account reads N5 and N4 in full
plus a set of showcase patterns above that, and gets a preview — metadata, formation, meaning, one
example — of the rest. Meaning search has a daily allowance. `get_learner_profile` returns your own
settings on any account; the stage and progress it derives from your study record come with Premium
and Pro. Personalized practice selection, reading checks, and writing briefs follow the same
boundary. Progress insights follow it too, and explicitly leave accuracy unavailable where 2hongo
does not yet keep per-review history. JLPT readiness follows the same boundary and reports only
coverage of 2hongo's inventory — never a test score or pass prediction. Submitting practice results
is available to every account tier. `record_usage_evidence` follows the personalization boundary. It
stores only the word or grammar sense, result, optional issue category, day, and calling client —
never the learner's sentence — after the learner is told. Every entry appears under Account Settings
→ AI Evidence and can be deleted there. The tools say when you have hit one of those boundaries;
they never offer to sell you anything.

Claude cannot play audio inline, so `get_word_audio` hands you a 2hongo word-page link to listen
there. Everything else returns normally.

## Troubleshooting

- **"Connect a free 2hongo account"** — the connection lapsed or was revoked. Re-authorize the
  plugin from `/plugin`, or re-add the connector.
- **A word isn't found** — Claude resolves conjugated forms to the dictionary form before looking
  a word up, but it can miss. Ask it to search the dictionary form directly — 見に行った → 行く.
- **Claude answers without consulting 2hongo** — that is the skill working as designed for generic
  explanation. Ask it to look the word up in 2hongo when you want sourced data.

Anything else: [2hongo.com/en/contact](https://www.2hongo.com/en/contact).

## Links

[Help](https://www.2hongo.com/en/help) · [Privacy](https://www.2hongo.com/en/privacy) ·
[Terms](https://www.2hongo.com/en/terms) · [About](https://www.2hongo.com/en/about)

## License

MIT — see [LICENSE](./LICENSE).

---

This repository is **generated**. It is mirrored from the 2hongo web repository by
`pnpm plugin:sync`, so pull requests opened here are overwritten by the next sync. Please report
issues through [2hongo.com/en/contact](https://www.2hongo.com/en/contact) instead.
