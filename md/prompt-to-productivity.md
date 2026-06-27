---
marp: true
theme: default
size: 16:9
paginate: true
style: |
  @import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap");
  section {
    background: radial-gradient(1200px 600px at 80% -10%, #10243f 0%, #0b1120 55%);
    color: #e2e8f0;
    font-family: "Inter", Arial, sans-serif;
    padding: 52px 64px;
  }
  h1 { font-size: 54px; margin: 0 0 8px; letter-spacing: -1.5px; color: #fff; }
  h2 { font-size: 32px; color: #38bdf8; font-weight: 700; margin: 0 0 18px; }
  h3 { margin: 0 0 8px; }
  section::after { color: #475569; font-size: 16px; }
  ul { font-size: 22px; margin-top: 10px; }
  li { margin: 7px 0; color: #cbd5e1; }
  strong { color: #fff; }
  .kicker { color: #38bdf8; font-family: "JetBrains Mono", monospace; font-size: 22px; letter-spacing: 2px; }
  .tag { font-family: "JetBrains Mono", monospace; background: #0f2942; color: #7dd3fc; padding: 2px 10px; border-radius: 7px; font-size: 0.82em; }
  .lead2 { color: #94a3b8; font-size: 25px; margin: 8px 0 24px; max-width: 92%; line-height: 1.4; }
  .goal { background: #0f172a; border-left: 4px solid #38bdf8; border-radius: 8px; padding: 13px 18px; font-size: 21px; color: #cbd5e1; }
  .note { color: #94a3b8; font-size: 21px; margin-top: 16px; }
  .flow { display: flex; flex-direction: column; gap: 11px; font-size: 21px; margin: 4px 0 16px; }
  .step { background: #0f172a; border: 1px solid #1e293b; border-radius: 12px; padding: 12px 18px; }
  .step .s { color: #38bdf8; font-weight: 700; }
  .cols { display: flex; gap: 24px; margin: 6px 0 14px; }
  .col { flex: 1; background: #0f172a; border: 1px solid #1e293b; border-radius: 12px; padding: 16px 20px; }
  .col h3 { font-size: 21px; }
  .col.manual h3 { color: #f59e0b; }
  .col.auto h3 { color: #38bdf8; }
  .col ul { font-size: 19px; margin: 0; padding-left: 18px; }
  .res li { margin: 8px 0; }
  .res b { color: #38bdf8; }
  .stats { display: flex; gap: 38px; margin: 6px 0 14px; }
  .stat .n { font-size: 76px; font-weight: 800; line-height: 1; }
  .stat .l { color: #94a3b8; font-size: 19px; text-transform: uppercase; letter-spacing: 1px; }
  .svc { display: flex; gap: 9px; flex-wrap: wrap; margin-top: 8px; }
  .svc span { background: #0f2942; border: 1px solid #1e3a5f; color: #7dd3fc; border-radius: 9px; padding: 6px 12px; font-size: 18px; font-weight: 600; }
  .foot { position: absolute; bottom: 36px; left: 64px; color: #475569; font-size: 19px; }
---

<!-- _paginate: false -->

<span class="kicker">AI-POWERED AUTOMATION WITH AZURE</span>

# From Prompt to Productivity

<div class="lead2">A build walkthrough — how we took the way we sort email by hand and turned it into an Azure service that does it for us.</div>

<div class="goal"><strong>The goal:</strong> clear a 5,000-email backlog and keep it clear — no app, no rules engine, no manual sorting.</div>

<div class="foot">Hardip Patel · hardip.me</div>

<!-- SPEAKER: One line on the universal pain (graveyard inbox), then the goal. Keep it a walkthrough, not a sell. -->

---

## Who I am

- **Hardip Patel** — Engineer at **Atyantik Technologies**.
- I build full-stack apps and data pipelines for a living.
- And I *over-engineer my own life, one sync pipeline at a time* — my music, my reading, my health metrics are all auto-tracked.
- This talk is one of those projects: I pointed it at my **inbox**.

<div class="note">hardip.me · github.com/knightkill</div>

<!-- SPEAKER: Keep it short and human. The hook: "and now I've automated my inbox — here's how." -->

---

## First: how we sort email by hand

The loop every one of us runs, all day:

- **Open** an email — read the sender and subject.
- **Decide** — does this actually need *me*? (a real person, money, my clients…)
- **Act** — keep it in Primary, or label it and archive it.
- **Repeat** — a few thousand times.

<div class="note">Result: 5,000 unread, the important stuff buried, and eventually you just give up.</div>

<!-- SPEAKER: Ground the talk in the manual process. This human judgment is exactly what we're going to capture. -->

---

## Then: the same loop, automated

<div class="cols">
  <div class="col manual"><h3>You, by hand</h3>
  <ul><li>open &amp; read</li><li>decide: keep / archive</li><li>label &amp; move</li><li>repeat ×1000s</li></ul></div>
  <div class="col auto"><h3>The automation</h3>
  <ul><li>Timer fetches new mail</li><li>Azure OpenAI decides</li><li>code labels &amp; archives</li><li>every 10 min, unattended</li></ul></div>
</div>

<div class="note">The trick: <strong>write your judgment down once</strong>, in plain English, and let the machine apply it to every email.</div>

<!-- SPEAKER: This is the whole arc on one slide — same loop, different worker. The rest of the talk drills into the right side. -->

---

## How it decides — without hallucinating

<div class="flow">
  <div class="step"><span class="s">1 · policy.md</span> &nbsp; plain-English keep/archive rules — the only "config"</div>
  <div class="step"><span class="s">2 · Azure OpenAI</span> &nbsp; classifies each email against that policy</div>
  <div class="step"><span class="s">3 · typed verdict</span> &nbsp; reason · category · labels · importance · keep_in_primary</div>
</div>

- We force **structured output**, so the model must return a valid verdict — it can't invent a label.
- The model only **decides**; deterministic code does the acting.
- Change behaviour by editing `policy.md` — **no code, no redeploy of logic**.

<!-- SPEAKER: Live — classify a few real emails, show the typed verdict, edit one policy line so a verdict flips. -->

---

## How it acts on a real inbox — safely

- Applies labels and archives through the Gmail API (`messages.modify`).
- **Dry-run by default** — logs what it *would* do before touching anything.
- **Never-touch allowlist** — starred, important, VIP senders, threads you replied to.
- **Idempotent** — a processed-set in Blob means it never re-acts on the same mail.
- **Audited** — every decision is a line you can read back, and undo.

<!-- SPEAKER: Acting on real mail is the scary part, so the safety mechanisms ARE the feature. Show the dry-run table + audit log. -->

---

## How we set it up — Azure + Gmail

**Azure (one-time):**
- `az login` → resource group → Function App + Storage account → Key Vault
- give the Function a **managed identity**, grant it *read* on the Key Vault
- put the secrets in Key Vault, then deploy with `func azure functionapp publish`

**Gmail (one-time):**
- create an OAuth **Desktop** client → consent once in the browser → get a **refresh token**
- store that token in **Key Vault**, so the cloud function signs in **headless** — no browser

<!-- SPEAKER: This is the part people actually ask about. Call out the headless-token-in-KeyVault trick — there's no browser in the cloud. -->

---

## The Azure pieces — and why each

<ul class="res">
  <li><b>Azure OpenAI</b> — runs the classifier (gpt-5.4-nano) and gives us structured output.</li>
  <li><b>Azure Functions</b> (Consumption + Timer) — runs the pipeline every 10 min; serverless, pay-per-run.</li>
  <li><b>Key Vault + Managed Identity</b> — holds every secret; the function reads them with its identity, so no keys live in code.</li>
  <li><b>Blob Storage</b> — the processed-set + audit log; lets the function stay stateless.</li>
  <li><b>Application Insights</b> — logs &amp; telemetry, hard-capped so cost can't run away.</li>
</ul>

<div class="svc">
  <span>Azure OpenAI</span><span>Functions (Timer)</span><span>Key Vault + Managed Identity</span><span>Blob Storage</span><span>App Insights</span>
</div>

<!-- SPEAKER: One line per service — what it does and why it's there. This is the "with Azure" payoff. -->

---

## What we achieved — and learned

<div class="stats">
  <div class="stat"><div class="n" style="color:#e2e8f0">31</div><div class="l">Triaged live</div></div>
  <div class="stat"><div class="n" style="color:#16a34a">11</div><div class="l">Kept in Primary</div></div>
  <div class="stat"><div class="n" style="color:#f59e0b">20</div><div class="l">Archived &amp; labeled</div></div>
</div>

Running every 10 minutes, ~$0 on Consumption (App Insights hard-capped).

**What we learned along the way:**
- gpt-5 models need `max_completion_tokens` (not `max_tokens`); don't override temperature.
- Linux Consumption won't remote-build a zip — deploy with `func azure functionapp publish`.
- Structured output makes decisions trustworthy; dry-run first makes them safe.
- Next: Azure Document Intelligence to read PDF/attachment content into the verdict.

<!-- SPEAKER: Close on the engineering reality + what's next. Refresh the numbers from the audit log before the talk. Q&A. -->
