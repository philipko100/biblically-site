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

It describes what the app actually does. Before changing it, check the claim
still holds in the app repo — the specific things it promises are: no analytics
SDKs of any kind, the Daily Focus selection never leaving the device (Apple's
Screen Time framework does not expose it), OpenAI receiving only passage text
and never the user's identity, and account deletion being immediate and
permanent. Update the effective date when the substance changes.
