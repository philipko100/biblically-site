# biblically.app

The public website for the Biblically iOS app: a landing page, the privacy
policy required by App Store Connect, and a support page (also required).

Static HTML, no build step. Served by GitHub Pages from `main` at the repo
root, with `CNAME` pointing the apex domain `biblically.app` at it.

```
index.html          landing page
privacy/index.html  → https://biblically.app/privacy
support/index.html  → https://biblically.app/support
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

- **No analytics or tracking SDKs of any kind.** Check `package.json`.
- **No cookies on this site.** There is no consent banner because none is needed.
- **The Daily Focus selection never leaves the device** — Apple's Screen Time
  framework returns an opaque reference the app cannot resolve.
- **OpenAI receives only the passage text and reference**, never anything
  identifying the user. Check the request built in
  `supabase/functions/explain-verse/index.ts`.
- **Account deletion is immediate and permanent**, with no retention window.
  Check `supabase/functions/delete-account/index.ts` and the cascade on the FKs.
- **Nothing is sold, licensed, or shared for anyone else's purposes.**

Religious belief — the tradition setting, the intake answers, and journal
content — is GDPR Article 9 special category data. The policy processes it on
the basis of explicit consent and for app functionality only. Do not weaken
that section without understanding why it is worded as it is.

The App Store privacy questionnaire must agree with this page. If one changes,
change the other in the same pass.

Update the "Last updated" date whenever the substance changes.
