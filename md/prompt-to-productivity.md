---
marp: true
theme: default
size: 16:9
paginate: true
style: |
  @import url("https://fonts.googleapis.com/css2?family=Karla:wght@400;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap");
  section {
    background: radial-gradient(900px 600px at 85% -15%, #161616 0%, #000 60%);
    color: #e8e8e8;
    font-family: "Karla", Helvetica, sans-serif;
    padding: 50px 62px;
  }
  h1 { font-size: 56px; margin: 0 0 8px; letter-spacing: -1px; color: #fff; font-weight: 800; }
  h2 { font-size: 32px; color: #b5d6da; font-weight: 700; margin: 0 0 16px; }
  section::after { color: #555; font-size: 16px; }
  ul { font-size: 22px; margin-top: 8px; }
  li { margin: 6px 0; color: #cfcfcf; }
  strong { color: #fff; }
  .kicker { color: #b5d6da; font-family: "JetBrains Mono", monospace; font-size: 21px; letter-spacing: 3px; }
  .lead2 { color: #9a9a9a; font-size: 25px; margin: 8px 0 22px; max-width: 92%; line-height: 1.4; }
  .goal { background: #0d0d0d; border-left: 3px solid #b5d6da; border-radius: 6px; padding: 13px 18px; font-size: 21px; color: #cfcfcf; }
  .note { color: #8f8f8f; font-size: 20px; margin-top: 14px; }
  .cap { color: #b5d6da; font-size: 20px; margin: 0 0 6px; font-weight: 600; }
  pre { background: #0c0c0c !important; border: 1px solid #1c1c1c; border-radius: 10px;
        font-size: 16.5px; line-height: 1.45; padding: 14px 18px; margin: 6px 0; }
  code { font-family: "JetBrains Mono", monospace; }
  :not(pre) > code { background: #141414; color: #b5d6da; padding: 2px 8px; border-radius: 6px; font-size: 0.84em; }
  .flow { display: flex; flex-direction: column; gap: 9px; font-size: 21px; margin: 4px 0 12px; }
  .step { background: #0d0d0d; border: 1px solid #1c1c1c; border-radius: 10px; padding: 11px 18px; }
  .step .s { color: #b5d6da; font-weight: 700; }
  .cols { display: flex; gap: 22px; margin: 6px 0 12px; }
  .col { flex: 1; background: #0d0d0d; border: 1px solid #1c1c1c; border-radius: 10px; padding: 15px 19px; }
  .col h3 { font-size: 20px; margin: 0 0 6px; }
  .col.manual h3 { color: #d9a441; }
  .col.auto h3 { color: #b5d6da; }
  .col ul { font-size: 18px; margin: 0; padding-left: 18px; }
  .res li { margin: 7px 0; font-size: 21px; }
  .res b { color: #b5d6da; }
  .big2 { display: flex; gap: 30px; align-items: stretch; margin: 8px 0 12px; }
  .card2 { flex: 1; background: #0d0d0d; border: 1px solid #1c1c1c; border-radius: 12px; padding: 18px 22px; }
  .card2 .t { color: #8f8f8f; font-size: 18px; text-transform: uppercase; letter-spacing: 1px; }
  .card2 .v { font-size: 30px; font-weight: 800; color: #fff; margin-top: 6px; line-height: 1.2; }
  .svc { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 10px; }
  .svc span { background: #0d0d0d; border: 1px solid #2a3a3c; color: #b5d6da; border-radius: 8px; padding: 6px 12px; font-size: 17px; font-weight: 600; }
  .foot { position: absolute; bottom: 34px; left: 62px; color: #555; font-size: 19px; }
---

<!-- _paginate: false -->

<span class="kicker">AI-POWERED AUTOMATION WITH AZURE</span>

# From Prompt to Productivity

<div class="lead2">A build walkthrough — how we took the way we sort email by hand and turned it into an Azure service that does it for us.</div>

<div class="goal"><strong>The goal:</strong> clear a 5,000-email backlog and keep it clear — no app, no rules engine, no manual sorting.</div>

<div class="foot">Hardip Patel · hardip.me</div>

---

## Who I am

- **Hardip Patel** — Engineer at **Atyantik Technologies**.
- I build full-stack apps and data pipelines for a living.
- And I *over-engineer my own life, one sync pipeline at a time* — my music, reading, and health metrics are all auto-tracked.
- This talk is one of those projects: I pointed it at my **inbox**.

<div class="note">hardip.me · github.com/knightkill</div>

---

## First: how we sort email by hand

The loop every one of us runs, all day:

- **Open** an email — read the sender and subject.
- **Decide** — does this actually need *me*? (a real person, money, my clients…)
- **Act** — keep it in Primary, or label it and archive it.
- **Repeat** — a few thousand times.

<div class="note">Result: 5,000 unread, the important stuff buried, and eventually you just give up.</div>

---

## Then: the same loop, automated

<div class="cols">
  <div class="col manual"><h3>You, by hand</h3>
  <ul><li>open &amp; read</li><li>decide: keep / archive</li><li>label &amp; move</li><li>repeat ×1000s</li></ul></div>
  <div class="col auto"><h3>The automation</h3>
  <ul><li>Timer fetches new mail</li><li>Azure OpenAI decides</li><li>code labels &amp; archives</li><li>every 10 min, unattended</li></ul></div>
</div>

<div class="note">The trick: <strong>write your judgment down once</strong>, in plain English, and let the machine apply it to every email.</div>

---

## How it decides — without hallucinating

<div class="cap">The model must fill a typed verdict — so it can't invent a label.</div>

```python
class TriageVerdict(BaseModel):       # the contract the model must satisfy
    reason: str                       # decide out loud first
    category: Category                # a closed enum, not free text
    labels: list[Label]              # only real Gmail labels
    importance: int = Field(ge=0, le=100)
    keep_in_primary: bool

verdict = client.beta.chat.completions.parse(
    model="gpt-5.4-nano",
    messages=[{"role": "system", "content": policy},   # policy.md = the rules
              {"role": "user",   "content": email}],
    response_format=TriageVerdict,         # ← it can't reply with anything else
).choices[0].message.parsed
```

<div class="note">Editing <code>policy.md</code> changes behaviour — no code, no redeploy of logic.</div>

---

## How it acts on a real inbox — safely

<div class="cap">Guards + dry-run wrap every mutation. Archive = remove the INBOX label.</div>

```python
def apply_verdict(svc, msg, verdict, *, dry_run=True):
    if is_protected(msg):                  # starred / VIP / threads I replied to
        return {"action": "skipped"}
    add    = [label_id(l) for l in verdict.labels]
    remove = [] if verdict.keep_in_primary else ["INBOX"]   # archive out of Primary
    if dry_run:                            # default: log, touch nothing
        return {"action": "dry-run", "add": add, "remove": remove}
    svc.users().messages().modify(
        userId="me", id=msg["id"],
        body={"addLabelIds": add, "removeLabelIds": remove},
    ).execute()                            # idempotent + written to an audit log
```

---

## How we set it up — Azure + Gmail

<div class="cap">Azure (one-time): create the function with an identity, vault the secrets, deploy.</div>

```bash
az functionapp create --runtime python --assign-identity ...   # managed identity
az keyvault secret set --vault-name $KV -n gmail-token-json --file token.json
func azure functionapp publish $APP --python --build remote
```

<div class="cap" style="margin-top:14px">Gmail (one-time): consent once, then run headless forever.</div>

- OAuth **Desktop** client → consent in the browser → get a **refresh token**.
- Store that token in **Key Vault** → the cloud function signs in with **no browser**.

---

## The Azure pieces — and why each

<ul class="res">
  <li><b>Azure OpenAI</b> — runs the classifier (gpt-5.4-nano) with structured output.</li>
  <li><b>Functions</b> (Consumption + Timer) — runs every 10 min; serverless, pay-per-run.</li>
  <li><b>Key Vault + Managed Identity</b> — holds secrets; no keys ever live in code.</li>
  <li><b>Blob Storage</b> — processed-set + audit log, so the function stays stateless.</li>
</ul>

```python
@app.timer_trigger(schedule="0 */10 * * * *")          # the automation: every 10 min
def handle_scheduled_triage(t): run_triage()

SecretClient(KV_URI, DefaultAzureCredential()).get_secret(name)   # identity, not keys
```

---

## What we achieved

<div class="big2">
  <div class="card2"><div class="t">Before</div><div class="v">5,000 unread<br/>everything in one pile</div></div>
  <div class="card2"><div class="t">After</div><div class="v">Primary holds only<br/>what needs me</div></div>
</div>

- Runs **every 10 minutes, unattended** — ~**$0** on Consumption (App Insights hard-capped).
- **What we learned:** gpt-5 needs `max_completion_tokens`; Linux Consumption won't remote-build a zip (use `func publish`); structured output makes it trustworthy, dry-run makes it safe.
- **Next:** Azure Document Intelligence to read PDF/attachment content into the verdict.

<div class="foot">github.com/knightkill · the pattern works on any inbox</div>

<!-- SPEAKER: numbers drift as the timer runs, so this slide stays qualitative. If you want a hard count, pull it live from the audit log right before the talk. -->
