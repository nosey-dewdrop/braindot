# nymphee — Personal Branding SaaS (living doc)

> Name: **nymphee** (nymph + -ee, coined/ownable; trademark & SaaS space checked clear 16 Jul).
> Chosen over "fae" (common word, weak/risky mark). Working name — locks once the business model firms up.
>
> Status: repo + folder created 16 Jul night. Docs written, NO code yet. Build starts at FAZ 0 / LOOP-01
> tomorrow with a fresh head. Next session's first agenda item = the BUSINESS MODEL open questions (below).

---

## What this is

A motor that systematically produces personal branding. NOT a slopware, NOT a naked AI wrapper —
stitchu-level real engineering. A layered AI system: the LLM is ONE removable node, not the product.

**Architectural first law (Damla's hard rule):** swap the underlying LLM (GPT→Llama→Claude) and the
product MUST NOT collapse. This is guaranteed by (a) a human-designed pipeline as the skeleton, (b) our
OWN trained models (voice + flop), (c) accumulating benchmark data. The LLM only drafts text inside one node.

**Framing (Damla, 16 Jul):** like Mindra / Compuvi / Dream Games — none invented something from zero;
they connected AI *well* and sold to the right buyer. "Wrapper" is not death. BADLY-connected wrapper with
no clear buyer is death. Our architecture is well-connected. The open piece is the BUSINESS MODEL (below).

---

## The 6 layers + MOAT vs BORU (pipe) split

Business truth: the layers are NOT equal. Engineering energy goes to MOAT, not pipes.

| Layer | Class | Why | Eng. effort |
|---|---|---|---|
| L1 — Source indexing | BORU (pipe) | scan/index is commodity (embeddings/pgvector), anyone builds it | one loop, cheap |
| **L2 — Voice profile** | **MOAT** | trained model, deepens with the user's own writing, uncopyable (data+time) | many loops, all depth |
| L3 — Format/tone decision | BORU | "reels or essay" rule; rule-based is enough | one loop, simple |
| L4 — Platform routing | BORU | platform-specific templating/orchestration; copyable | one loop, simple |
| **L5 — Flop filter** | **MOAT** | trained scoring, grows with real performance data, uncopyable | many loops, all depth |
| **L6 — Benchmark/measure** | **MOAT** | accumulating voice-accuracy + flop-prediction data = the valuation proof | many loops, all depth |

**Rule (spine of the plan):** pipes just WORK — fastest, cheapest, LLM inside if needed. MOAT gets ALL depth.
What we SELL is the moat; pipes aren't even worth talking about. A rival copies pipes in a week; the moat
is data + time, forkable only as code, never as the accumulated data.

---

## The contracts (how layers talk)

Each layer hands the next a typed, fixed object. As long as the contract stays fixed, the engine inside
(incl. the LLM) can change → this is where "swap the LLM, product survives" passes. ⭐ = moat contract,
must be defined most rigorously (that's where the value flows).

- **S1 · L1→L3** `SourceIndex` (pipe): `{ topics:[{id,tema,kaynak_ref,ozet}], user_domain }`
- **S2 · L2→(L3,L4,L5)** `VoiceContract` ⭐: `{ ton, kelime_dagarcigi[], sinirlar[], imza, ornekler[], voice_model_id }`
   — every lower layer MUST obey this. Heart of the moat. `voice_model_id` points at the trained model;
   the model can change, the contract stays.
- **S3 · L3→L4** `FormatDecision` (pipe): `{ fikir_id, format, ton_modu, dil, durak_sayisi }`
- **S4 · L4→L5** `DraftCandidate` (pipe→moat boundary): `{ platform, dil, icerik, voice_contract_ref, format_ref }`
   — an LLM may produce this; L5 doesn't care which LLM, contract is fixed.
- **S5 · L5→L6** `ScreenResult` ⭐: `{ candidate_ref, flop_skoru, gecti, neden, flop_model_id }`
- **S6 · L6→(L2,L5) FEEDBACK** ⭐: `{ tuttu_mu:gercek_performans, ses_tuttu_mu → training signal }`
   — the MOST valuable contract. Feeds real-world outcome back into the moat models → system trains itself
   → data accumulates → moat deepens. Rivals have no such loop.

**Law:** pipe contracts (S1,S3,S4) simple & changeable. Moat contracts (S2,S5,S6) fixed & rigorous —
the company's value flows through those three interfaces.

---

## Cold start — solved by design, not patched

The moat models need real performance data (S6): "did this post land? did it keep the voice?" With zero
customers there's no data → no moat → no customers → no data. Classic chicken-egg; most SaaS die here.

**Solution: the first user is DAMLA.** Damla is already becoming a content creator; she has 49 projects +
build-in-public material. She produces that content THROUGH this system (not by hand), publishes it,
measures what landed / flopped = the first S6 data. Cold start isn't a problem to solve later — it's the
by-product of work Damla will do anyway.

Triple value (Levels PhotoAI precedent — trained on his own photos first):
1. **Moat seed** — Damla's content + land/flop measures = first training data for L2 and L5.
2. **Sales demo** — "I built my own brand with this tool, here are the numbers" = live proof to an agency,
   and the proof it's not a wrapper.
3. **Build-in-public content** — building the tool IS the content Damla will make. Tool = content's material,
   content = tool's data. The loop feeds itself.

Architectural consequence (baked in from day 1): L6 real-performance input exists from the first loop
(even manual: "this reels got 12k, this got 400"). S6 is designed assuming the first user is Damla.
Matches the B2C-single-user-first decision: no multi-tenant yet, Damla's account, Damla's data, Damla's loop.

---

## Build order — VERTICAL SLICE, not horizontal

**Trap (we will NOT do this):** perfect L1 → perfect L2 → L3... Horizontal build. Result: months with zero
output because no single layer is a product. Motivation dies, "it works for me" never happens, cold-start
data never starts.

**Correct:** take a THIN slice of every layer, wire it end-to-end so a real piece of content actually comes
out and gets published. stitchu logic: first a full dress (rough seams, but wearable), THEN add collar/sleeve
— not a perfect collar on a dress that never ships.

**Order:** 1) narrow but end-to-end vertical (one platform, real output, real measure — "works for me" day 1)
→ 2) deepen the moat (loops on L2/L5/L6 once data accumulates) → 3) pipes widen (many platforms/features, last).
**Rule:** don't enter FAZ 1 before FAZ 0 ships — the moat needs the vertical that feeds it, or there's no data to train.

---

## Loop queue (stitchu BENCHMARK-58 style — one loop perfected per session)

### FAZ 0 — VERTICAL SLICE (one goal: one piece of content comes out in Damla's voice, published, measured)
- **LOOP-01** thin L1: roughly scan Damla's 49 projects + old posts → simple topic list (plain list, not
  pgvector — pipe, just works). Proof: topic list file exists.
- **LOOP-02** thin L2: first `VoiceContract` extracted from Damla's texts (ton/imza/sinir) — not a model yet, v0.
  Moat seed. Proof: VoiceContract v0 written.
- **LOOP-03** thin L3+L4: pick ONE platform (proposal: LinkedIn — Damla's CEO/honest-engineer tone already
  defined) → turn one idea into a platform draft (LLM inside, pipe). Proof: a real draft exists.
- **LOOP-04** thin L5: simplest flop filter — rule-based v0 (has hook? length? repetition?). Model later.
  Proof: draft gets a flop score + reason.
- **LOOP-05** thin L6: publish → feed the real number (views/engagement) back by hand → first `ScreenResult`
  + S6 data. **"Works for me" happens here + cold-start data begins.** Proof: one published post + its measure logged.
- → FAZ 0 done = one piece of content, in Damla's voice, through this system, published and measured. Narrow but whole.

### FAZ 1 — MOAT DEPTH (data started; turn L2/L5 into real motors)
- L2 rule→trained voice model (Damla's data); L5 rule→trained flop score; build L6 benchmark. Each = many loops.

### FAZ 2 — WIDEN (pipes open)
- many platforms, TR+EN, many formats, then multi-tenant (B2B).

---

## BUSINESS MODEL (matured 16 Jul night — Damla + mentor, still in progress)

CORRECTION to earlier draft: **Damla is NOT an agency selling a service. nymphee is Damla's PRODUCT.**
She sells the product; content creators buy it if they want. No middleman. Agencies = a *possible later*
channel (bulk sale), NOT required. This is the clean B2C model Damla wanted from the start.

### What we sell — the creator's "hands and arms" (end-to-end)
nymphee does the WHOLE content job, not one slice: **idea/program + writing + publishing**, keeping the
user's voice. A "machine ghostwriter" (human ghostwriters cost $2-5k/mo; nymphee is a small fraction).
- **idea/program** — never-run-dry weekly content plan (kills the #1 burnout cause: "what do I post")
- **writing** — every piece in the user's voice (L2 moat: doesn't sound like AI slop → trust survives)
- **publishing** — user uploads reels/carousel; nymphee decides when/where/how and posts it
End-to-end = rival tools each solve one slice (Supergrow writes, Buffer posts); nymphee = all in one.
"Hands and arms" = irreplaceable: cancelling nymphee = losing your arms (embedded in daily workflow).

### Why a SUBSCRIPTION survives (Damla's sharp catch: "one-time won't sustain a sub")
Voice is learned ONCE (true, one-time). But content NEVER ends — every week needs fresh ideas/posts, and
publishing is embedded in the daily workflow. Value is tied to the ongoing FLOW, not a single output →
monthly sub lives. Netflix logic: not one film, a new thing every month. Cancel = content stops entirely.

### WHO buys — ideal customer (matured, corrected)
Not the "quiet high-status engineer" (mentor's earlier miss — engineers already have social status).
The real target: **"low status, high income" = influencers/creators** — lots of money (content IS their
income, tool = business expense), but low social status ("dismissed as fluff"). Why ideal:
- **money is there** → low price sensitivity, can pay premium (don't join the cheap-tool race)
- **pain is sharpest** → must post EVERY day or go broke; the 90%-burnout / 71%-considered-quitting crowd
- **moat fits them** → serious enough that AI-slop kills their reputation → only voice-preserving tool works
- **status pain too** → quality content lifts them out of the "fluff" stigma (two pains, one tool)

**FIRST user = Damla herself** — the **dev × influencer × fun** intersection (Bilkent CS + 49 projects +
build-in-public + whimsy/talkative). Rare, growing niche (Karpathy/Levels type: technical but visible/fun).
Damla IS her own ideal customer → builds it for herself → sells to people like her (she knows their language).
Cold start + demo + sales story all merge in one person: Damla.

**Staged audience:** 1) small creators / dev-influencer intersection (Damla's kin, sharpest pain, blank page)
→ 2) big creators already producing (different pain: "scale without burning out") → 3) agencies (bulk).
Same motor, two sales messages: small = "I make you visible", big = "scale without burnout". Win ONE first
(small/dev-influencer) — don't blur the message trying to sell both at once.

### STILL OPEN (next sessions, in order — Damla asked for mentorship here)
1. **How much / pricing** — monthly sub, what tier, what number. (Premium — money-rich audience.) NEXT.
2. **Why YOU vs Mindra/rivals** — one-sentence moat pitch. (Rivals produce AI-slop; nymphee preserves voice
   + filters flops. Damla's fuel: 49 projects, C++ engine, live self-demo = uncommon founder proof.)

**ORDER for coming sessions (Damla's call 16 Jul):** keep talking BUSINESS MODEL → then DESIGN → THEN start
building the layers (code). Business + design fully firm before any layer code. Vision (full "hands & arms":
idea+write+publish+reels+carousel+LinkedIn+X, every platform) stays as the TARGET in this doc — writing it
down PROTECTS the idea, it is not lost. First BUILD = one arm (LinkedIn, end-to-end), rest added in order.

Reminder of what sells: pain + trust, not the product. Outbound first 10 customers (go to them, DM), not ads.
Damla's story is the sales fuel. Sell the MOAT layers, never the pipes.

---

## Tech stack (proposal, not locked — decide at "hadi kur")

Web-first. Frontend Damla's line (NOT generic center-column landing — see her design law). Backend Supabase
(auth + Postgres + pgvector when L1 needs it). Motors in Python (trained models). Payments Polar.sh
(Stripe closed to TR individuals). Landing/dashboard = stitchu line (calm, technical, data-forward), not whimsy.

## Design law
Generic "center-stacked, empty-sides, hero→feature→feature→CTA" landing is FORBIDDEN (Damla, AI-tell).
Aesthetic = stitchu line (she said "çok tatlı"): calm, technical, data-forward (scores/percentages visible),
whimsy NOT. Should feel like a serious work tool for an influencer agency (Linear/Vercel/Retool density).
Same calm-technical language works for both B2C and B2B.

## Reference
Mindra (precise problem + detailed algorithm model). Pieter Levels / levels.io (closest human to Damla;
PhotoAI cold-start-on-own-data precedent). Dream Games (didn't invent, cleanly-connected + right audience).
