# utility_t-c

Privacy policies and terms & conditions for apps published by **SkIndie Dev**, hosted with GitHub
Pages. Google Play requires a permanent, publicly reachable privacy policy URL per app — this repo
is where those URLs live.

## Layout

```
index.html              landing page listing every app
styles.css              shared stylesheet — all apps use it
whiteboard/
  privacy-policy.html   ← URL for Play Console
  terms.html
folio/
  privacy-policy.html   ← URL for Play Console
  terms.html
```

One folder per app, sharing one stylesheet. Apps get separate documents rather than one combined
policy because each collects different things; a shared document would have to describe the union
of every app's data use, which would be inaccurate for each app individually.

## Enabling Pages

**Settings → Pages → Build and deployment → Deploy from a branch → `main` → `/` (root)**

URLs become:

```
https://snewdeveloper.github.io/utility_t-c/
https://snewdeveloper.github.io/utility_t-c/whiteboard/privacy-policy.html
https://snewdeveloper.github.io/utility_t-c/whiteboard/terms.html
https://snewdeveloper.github.io/utility_t-c/folio/privacy-policy.html
https://snewdeveloper.github.io/utility_t-c/folio/terms.html
```

Give the privacy policy URL to Play Console under *Policy → App content → Privacy policy*, and in
the Data Safety form. It must keep working for as long as the app is listed.

## Adding a future app

1. `mkdir <app>/` and copy an existing app's two HTML files in as a starting point.
2. Fix the relative paths — pages reference `../styles.css` and the wordmark links to
   `../index.html`.
2b. Give the app its own palette: add a `body.app-<name>` token block at the end of `styles.css`
   and set `<body class="app-<name>">` on both pages. The stylesheet stays shared; only the
   colours move.
3. **Rewrite the content to match what that app actually does.** Do not ship the whiteboard text
   with the name swapped: the data-collection tables, permission lists and third-party services
   are specific to each app, and a policy describing behaviour an app does not have is a
   compliance problem, not a cosmetic one.
4. Add an `.app-group` block to `index.html`.

## Keeping policies accurate

A policy is a factual claim about the software. When an app's behaviour changes, the policy
changes in the same release — not later. For Whiteboard specifically, the current documents assert
that no board content leaves the device except through the user's own Android backup and their own
share actions. Shipping cloud sync without rewriting those sections would make the published
policy false.

Source of truth for the Whiteboard text (with commentary on why each section says what it does)
lives in the app repo under `legal/` and `docs/`.

For Folio, the equivalent source lives in the app repo under `PRIVACY.md` and `docs/`. The current
documents assert that no document content leaves the device, that the app ships no analytics
provider and no crash reporter, and that text recognition runs on-device. Adding Firebase, a
backend, or any cloud processing would make the published policy false and must be accompanied by
a rewrite of sections 2, 5 and 13 of the privacy policy in the same release.
