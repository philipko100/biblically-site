# biblically.app

The public website for the Biblically iOS app: a landing page, the privacy
policy required by App Store Connect, and a support page (also required).

Static HTML, no build step. Served by GitHub Pages from `main` at the repo
root, with `CNAME` pointing the apex domain `biblically.app` at it.

```
index.html          landing page
privacy/index.html  → https://www.biblically.app/privacy
terms/index.html    → https://www.biblically.app/terms
support/index.html  → https://www.biblically.app/support
style.css           shared styles, light and dark
CNAME               the custom domain
.nojekyll           skip Jekyll processing; these are plain files
```

Kept in its own repository because the app repo is private, and GitHub Pages
only serves public repositories on the free plan.

## Editing the privacy policy

The policy states what the app actually does, and several of its claims are
unusually strong. Verify each one still holds in the app repo before editing,
because they are load-bearing both legally and for the App Store privacy label:

- **The app DOES have analytics** (PostHog, `posthog-react-native`). The policy
  used to claim it had none; that became false the moment the SDK landed, and
  the "Usage analytics" section now describes it. If the event set changes,
  change that section in the same pass — the events are listed individually.
- **Analytics can be turned off** in the app under Me → Privacy. The policy
  promises this; `setAnalyticsEnabled` in `src/lib/posthog.ts` delivers it.
  Do not remove one without the other.
- **No cookies on this site.** There is no consent banner because none is needed.
- **The Daily Focus selection never leaves the device** — Apple's Screen Time
  framework returns an opaque reference the app cannot resolve.
- **OpenAI receives only the passage text and reference**, never anything
  identifying the user. Check the request built in
  `supabase/functions/explain-verse/index.ts`.
- **Account deletion is immediate and permanent**, with no retention window.
  Check `supabase/functions/delete-account/index.ts` and the cascade on the FKs.
  A five-year retention clause was drafted and then removed: the function
  hard-deletes and the foreign keys cascade, so there is nothing retained to
  describe. Do not reintroduce a retention period unless the app starts
  soft-deleting — the claim has to match the code.
- **Nothing is sold, licensed, or shared for anyone else's purposes.**

Religious belief — the tradition setting, the intake answers, and journal
content — is GDPR Article 9 special category data. The policy processes it on
the basis of explicit consent and for app functionality only. Do not weaken
that section without understanding why it is worded as it is.

The App Store privacy questionnaire must agree with this page. If one changes,
change the other in the same pass.

Update the "Last updated" date whenever the substance changes.

## Editing the terms

Two clauses are load-bearing and were written against what the app actually
does. Do not loosen either without changing the app to match:

- **Your content stays yours.** The licence granted is only what is needed to
  store, sync and display a user's own content back to them; it is
  non-exclusive and ends on deletion. Nothing is sold, licensed or shared, and
  nothing trains an AI model. This must agree with the privacy policy, which
  says the same — a terms/policy contradiction is itself a legal problem.
- **The Apple block is mandatory.** A custom EULA distributed through the App
  Store has to state that the agreement is with the developer and not Apple,
  that Apple has no maintenance or support obligation, that Apple is not
  responsible for claims, and that Apple is a third-party beneficiary entitled
  to enforce. Removing it risks rejection.

The age statement, the subscription terms and the deletion description must
stay consistent with the privacy policy and with App Store Connect.
