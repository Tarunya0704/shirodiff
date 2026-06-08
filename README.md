<p align="center">
  <img src="assets/logo.png" alt="shiroDiff" width="80" />
</p>

<h1 align="center">shiroDiff</h1>

<p align="center">
  <strong>Catch visual regressions before they ship.</strong><br>
  A GitHub bot that screenshots your pages before and after every PR, diffs them pixel-by-pixel, and posts the results. Zero config.
</p>

<p align="center">
  <a href="https://github.com/apps/shirodiff"><img src="https://img.shields.io/badge/Install-GitHub%20App-2ea44f?style=for-the-badge&logo=github" alt="Install"></a>
</p>

---

## What it does

When you open a pull request, shiroDiff automatically:

1. Builds your app at the **base** branch (before your changes)
2. Builds your app at the **head** branch (after your changes)
3. Takes full-page screenshots of both
4. Runs pixel-level comparison (pixelmatch + SSIM)
5. Posts a PR comment with **before**, **after**, and **diff** images

No signup. No config file. No CI pipeline changes. Just install and every PR gets visual review.

<p align="center">
  <img src="assets/pr-comment-example.png" alt="shiroDiff PR comment showing before/after/diff screenshots" width="700" />
</p>

---

## Install — 30 seconds

1. **Click** → [Install shiroDiff](https://github.com/apps/shirodiff)
2. **Pick** which repos you want it on
3. **Done.** Open a PR and watch it work.

That's it. No API keys. No YAML files. No dashboard.

---

## What you get on every PR

| What | Details |
|------|---------|
| **Before screenshot** | Your app rendered at the base branch |
| **After screenshot** | Your app rendered at the head branch |
| **Diff overlay** | Changed pixels highlighted in red |
| **Pixel change %** | Exact percentage of pixels that changed |
| **SSIM score** | Structural similarity — catches layout shifts that pixel diff misses |
| **Composite score** | Combined quality score for quick pass/fail decisions |

If nothing visual changed, you get a clean ✅ — no noise.

---

## Why shiroDiff?

**The problem:** Developers review code diffs, not visual diffs. A 3-line CSS change can break a layout, shift a button, or mess up mobile spacing — and nobody catches it until production.

**Existing tools are painful:**
- **Percy / Chromatic** — $400+/month, requires Storybook setup, CI pipeline integration, days of configuration
- **Manual QA** — someone clicks through staging before every merge, doesn't scale
- **Nothing** — most teams just merge and hope (this is the real competitor)

**shiroDiff:** Install a GitHub App. That's the whole setup. Works on every PR automatically.

---

## Supported frameworks

- ✅ Next.js (App Router & Pages Router)
- 🔜 Vite + React
- 🔜 Remix
- 🔜 Nuxt

Currently optimized for Next.js projects. More frameworks coming based on demand — [open an issue](../../issues) to request yours.

---

## How it works under the hood

```
PR opened / updated
       ↓
shiroDiff receives GitHub webhook
       ↓
Clones repo at base commit → npm install → npm run dev → Playwright screenshot
Clones repo at head commit → npm install → npm run dev → Playwright screenshot
       ↓
pixelmatch + SSIM comparison → diff image generated
       ↓
PR comment posted with all images + scores
```

Screenshots are taken at **1440×900** viewport (desktop). Mobile viewport support coming soon.

---

## Scoring explained

shiroDiff reports three scores, each catching different types of regressions:

- **Pixel change %** — raw percentage of pixels that differ. Good for catching color changes, new elements, removed elements.
- **SSIM (Structural Similarity)** — measures structural layout similarity. Catches shifts, reflows, and spacing changes that pixel diff might underweight.
- **Composite** — weighted combination for a single pass/fail number. >95% is usually safe. <90% deserves a close look.

---

## Roadmap

- [x] Before/after screenshots on every PR
- [x] Pixel-level diff with red overlay
- [x] SSIM + pixelmatch + composite scoring
- [ ] AI-powered plain-English change descriptions ("nav shifted 8px right, button color changed from blue to green")
- [ ] Multiple page support via `.shirodiff.yml` config
- [ ] Mobile + desktop viewport comparison
- [ ] Slack/Discord notifications on high-severity changes
- [ ] Figma design comparison (compare PR against source Figma file)
- [ ] Configurable thresholds and auto-approve for low-change PRs

---

## Privacy & security

- shiroDiff only accesses repos you explicitly install it on
- Code is cloned temporarily for screenshots, then deleted immediately
- Screenshots are stored as assets in your own repo (orphan branch `visualbot-assets`)
- No code is stored, logged, or sent to third parties
- No analytics or tracking on your codebase

---

## Pricing

**Free during beta.** Install it, use it, break it, tell us what's missing.

Paid tiers coming later for teams that need unlimited repos, AI analysis, and priority support.

---

## Feedback & issues

This is early. Things will break. When they do:

- [Open an issue](../../issues) with the error from the PR comment (shiroDiff always reports what went wrong)
- Or DM [@Tarunya200407](https://twitter.com/Tarunya200407) on Twitter

Every bug report makes this better for everyone.

---

<p align="center">
  <sub>Built by <a href="https://github.com/Tarunya0704">Tarunya</a> · Powered by Playwright + pixelmatch + SSIM</sub>
</p>
