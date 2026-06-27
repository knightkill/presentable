---
marp: true
theme: default
size: 16:9
paginate: false
style: |
  @import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap");
  section {
    background: radial-gradient(1200px 600px at 80% -10%, #10243f 0%, #0b1120 55%);
    color: #e2e8f0;
    font-family: "Inter", Arial, sans-serif;
    padding: 60px 72px;
  }
  h1 { font-size: 60px; margin: 0 0 6px; letter-spacing: -1.5px; color: #fff; }
  h2 { font-size: 30px; color: #38bdf8; font-weight: 700; margin: 0 0 28px; }
  .sub { color: #94a3b8; font-size: 26px; margin-bottom: 36px; }
  .tag { font-family: "JetBrains Mono", monospace; background: #0f2942; color: #7dd3fc;
         padding: 3px 12px; border-radius: 8px; font-size: 0.8em; }
  .big { font-size: 120px; font-weight: 800; line-height: 1; color: #fff; }
  .pain { font-size: 34px; color: #cbd5e1; margin-top: 20px; }
  .pain b { color: #f59e0b; }
  .azure { color: #38bdf8; font-weight: 700; }
  .flow { display: flex; flex-direction: column; gap: 14px; font-size: 24px; margin-top: 6px; }
  .step { background: #0f172a; border: 1px solid #1e293b; border-radius: 14px; padding: 16px 22px; }
  .step .s { color: #38bdf8; font-weight: 700; }
  .svc { display: flex; gap: 12px; flex-wrap: wrap; margin-top: 26px; }
  .svc span { background: #0f2942; border: 1px solid #1e3a5f; color: #7dd3fc;
              border-radius: 10px; padding: 8px 16px; font-size: 20px; font-weight: 600; }
  .stats { display: flex; gap: 40px; margin: 30px 0 10px; }
  .stat .n { font-size: 96px; font-weight: 800; line-height: 1; }
  .stat .l { color: #94a3b8; font-size: 22px; text-transform: uppercase; letter-spacing: 1px; }
  .foot { position: absolute; bottom: 42px; left: 72px; color: #475569; font-size: 20px; }
  .kicker { color: #38bdf8; font-family: "JetBrains Mono", monospace; font-size: 22px; letter-spacing: 2px; }
---

<!-- _class: lead -->

<span class="kicker">AI-POWERED AUTOMATION WITH AZURE</span>

# From Prompt to Productivity

<div class="pain">My inbox: <b>5,000 unread</b>.<br/>One English paragraph in <span class="tag">policy.md</span> fixed it.</div>

<div class="foot">Hardip Patel · anormaly labs</div>

<!--
SPEAKER: Open on the pain — everyone in the room has a graveyard inbox. Show the REAL 5,000-unread screenshot here.
Promise: by the end you'll see one English paragraph turn into an Azure automation that triages this inbox unattended.
Don't sell "native Azure platform" — sell "applied Azure OpenAI + production agent patterns." Keep it honest.
-->

---

## The architecture

<div class="flow">
  <div class="step"><span class="s">PROMPT</span> &nbsp; policy.md — plain-English keep/archive rules</div>
  <div class="step"><span class="s">CLASSIFY</span> &nbsp; Azure OpenAI (gpt-5.4-nano) → typed verdict, can't hallucinate a label</div>
  <div class="step"><span class="s">ACT</span> &nbsp; label + archive in Gmail · never-touch allowlist · idempotent · audited</div>
  <div class="step"><span class="s">AUTOMATE</span> &nbsp; Azure Functions Timer — every 10 min, unattended</div>
</div>

<div class="svc">
  <span>Azure OpenAI</span><span>Functions (Timer)</span><span>Key Vault + Managed Identity</span><span>Blob Storage</span><span>App Insights</span>
</div>

<!--
SPEAKER: Walk top-to-bottom. The one idea: the LLM only DECIDES; deterministic code ACTS. Structured output is the anti-hallucination spine.
Then the live moment — curl the deployed /api/triage and show the JSON {processed, kept, archived}. "This has been running every 10 minutes."
Honesty beat: Document Intelligence for attachments is roadmap (M4), not yet wired — say so; an Azure crowd respects it.
Secrets via managed identity, not keys in code. ~$0 on Consumption + a hard App Insights cap.
-->

---

## One policy → a triaged inbox

<div class="stats">
  <div class="stat"><div class="n" style="color:#e2e8f0">31</div><div class="l">Triaged live</div></div>
  <div class="stat"><div class="n" style="color:#16a34a">11</div><div class="l">Kept in Primary</div></div>
  <div class="stat"><div class="n" style="color:#f59e0b">20</div><div class="l">Archived &amp; labeled</div></div>
</div>

<div class="pain" style="margin-top:24px">Edit one line in <span class="tag">policy.md</span> → a verdict flips.<br/>No code. No redeploy of logic. <span class="azure">That's the whole pitch.</span></div>

<div class="foot">github.com/knightkill · the pattern is reusable on any inbox</div>

<!--
SPEAKER: The payoff slide. Do the live policy-flip here (in DRY-RUN): move "recruiter" to KEEP, re-run, watch the verdict change.
Land the close: one English file became an Azure automation that triages mail unattended — and you can read every decision in the audit log.
Update these numbers from the live audit log right before the talk. Q&A.
-->
