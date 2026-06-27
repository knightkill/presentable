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
    padding: 56px 68px;
  }
  h1 { font-size: 56px; margin: 0 0 8px; letter-spacing: -1.5px; color: #fff; }
  h2 { font-size: 34px; color: #38bdf8; font-weight: 700; margin: 0 0 22px; }
  section::after { color: #475569; font-size: 16px; }
  ul { font-size: 23px; margin-top: 14px; }
  li { margin: 9px 0; color: #cbd5e1; }
  strong { color: #fff; }
  .kicker { color: #38bdf8; font-family: "JetBrains Mono", monospace; font-size: 22px; letter-spacing: 2px; }
  .tag { font-family: "JetBrains Mono", monospace; background: #0f2942; color: #7dd3fc; padding: 2px 10px; border-radius: 7px; font-size: 0.82em; }
  .lead2 { color: #94a3b8; font-size: 26px; margin: 8px 0 26px; max-width: 92%; line-height: 1.4; }
  .goal { background: #0f172a; border-left: 4px solid #38bdf8; border-radius: 8px; padding: 14px 20px; font-size: 22px; color: #cbd5e1; }
  .flow { display: flex; flex-direction: column; gap: 12px; font-size: 22px; margin: 4px 0 18px; }
  .step { background: #0f172a; border: 1px solid #1e293b; border-radius: 12px; padding: 13px 20px; }
  .step .s { color: #38bdf8; font-weight: 700; }
  .svc { display: flex; gap: 10px; flex-wrap: wrap; margin-top: 8px; }
  .svc span { background: #0f2942; border: 1px solid #1e3a5f; color: #7dd3fc; border-radius: 10px; padding: 7px 14px; font-size: 19px; font-weight: 600; }
  .stats { display: flex; gap: 40px; margin: 8px 0 16px; }
  .stat .n { font-size: 80px; font-weight: 800; line-height: 1; }
  .stat .l { color: #94a3b8; font-size: 20px; text-transform: uppercase; letter-spacing: 1px; }
  .foot { position: absolute; bottom: 38px; left: 68px; color: #475569; font-size: 19px; }
---

<!-- _paginate: false -->

<span class="kicker">AI-POWERED AUTOMATION WITH AZURE</span>

# From Prompt to Productivity

<div class="lead2">A build walkthrough: how we turned a plain-English policy into an Azure service that triages a Gmail inbox automatically — and what it took to make it trustworthy and unattended.</div>

<div class="goal"><strong>The goal:</strong> clear a 5,000-email backlog and keep it clear — with no app, no rules engine, and no manual sorting.</div>

<div class="foot">Hardip Patel · anormaly labs</div>

<!--
SPEAKER: Frame as "here's what we built and how", not a product pitch. The problem is universal (graveyard inbox).
State the goal plainly, then spend the talk showing the mechanics. Live: show the real 5k-unread inbox.
-->

---

## How it decides — without hallucinating

<div class="flow">
  <div class="step"><span class="s">1 · policy.md</span> &nbsp; plain-English keep/archive rules — the only "config"</div>
  <div class="step"><span class="s">2 · Azure OpenAI</span> &nbsp; classifies each email against that policy</div>
  <div class="step"><span class="s">3 · typed verdict</span> &nbsp; reason · category · labels · importance · keep_in_primary</div>
</div>

- We force **structured output**, so the model must return a valid verdict — it can't invent a label.
- The model only **decides**; deterministic code does the acting.
- Behaviour changes by editing `policy.md` — **no code change, no redeploy of logic**.

<!--
SPEAKER: This is the core technique. Live: run the classifier on a few real emails, show the typed verdict.
Then edit one policy line and re-run so a verdict flips — proving the policy is the only thing that drives behaviour.
-->

---

## How it acts on a real inbox — safely

- Applies labels and archives through the Gmail API (`messages.modify`).
- **Dry-run by default** — it logs what it *would* do before anything is touched.
- **Never-touch allowlist**: starred, important, VIP senders, threads you've replied to.
- **Idempotent** — a processed-set (in Blob) means it never re-acts on the same message.
- **Audited** — every decision is written as a line you can read back, and undo.

<!--
SPEAKER: The point: acting on real mail is the risky part, so the safety mechanisms ARE the feature.
Live: show the dry-run table over the real inbox, then the audit log. Mention undo = re-add INBOX.
-->

---

## How it runs — unattended on Azure

<div class="flow">
  <div class="step"><span class="s">Timer</span> &nbsp; Azure Functions runs the pipeline every 10 minutes</div>
  <div class="step"><span class="s">Secrets</span> &nbsp; Key Vault via managed identity — no keys in code</div>
  <div class="step"><span class="s">State</span> &nbsp; processed-set + audit log in Blob (the function itself is stateless)</div>
  <div class="step"><span class="s">Auth</span> &nbsp; headless Gmail — refresh token from Key Vault, no browser</div>
</div>

<div class="svc">
  <span>Azure OpenAI</span><span>Functions (Timer)</span><span>Key Vault + Managed Identity</span><span>Blob Storage</span><span>App Insights</span>
</div>

<!--
SPEAKER: How it became an automation. Live: curl the deployed /api/triage and show the JSON summary.
Emphasise managed identity (no secrets in code) and that the function is stateless (state lives in Blob).
-->

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
- Structured output is what makes the decisions trustworthy; dry-run first makes them safe.
- Next: Azure Document Intelligence to read PDF/attachment content into the verdict.

<!--
SPEAKER: Close on the engineering reality, not a sell. Real numbers (refresh from the audit log before the talk),
honest cost, the gotchas that cost us time, and what's next. Then Q&A.
-->
