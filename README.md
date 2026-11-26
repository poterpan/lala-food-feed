# threads-food-feed

Automatically generated food-venue data derived from the public Threads posts and replies of
[@zeke_6973](https://www.threads.com/@zeke_6973) (拉拉熊), produced by a private pipeline
(collection → LLM extraction → venue matching).

Primary consumer: [lala-food](https://github.com/2xin15/lala-food). Files under `lala/` use the
same shapes as lala-food's own `extra.json`, `notes.json`, `posts.js` and `data.js`, so a site can
read the feed and fall back to its local files when the feed is unavailable.

| File | Content |
|---|---|
| `lala/extra.json` | `visited_from_wish` / `visited_add` generated from Threads evidence |
| `lala/notes.json` | must-order items and a one-line comment in the account's own words |
| `lala/posts.json` | the account's own posts per venue (CID) found by the pipeline |
| `lala/data.js`, `lala/posts.js` | lala-food's current public data with the overlay already applied |
| `venues.json` | the pipeline's own venue model (stance, experience, sources) |
| `meta.json` | generation time, counts, schema version |

Every venue carries its Threads source URLs. Updated automatically after each collection run.
