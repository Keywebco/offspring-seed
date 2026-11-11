This file describes Nova. It does not build Nova. Implementation stays with Roger.

Status: PROPOSED. Not canon. Describes an instrument, not a partner.

1. What Nova is

Nova is the Federation's deterministic cognitive middleware. It is the instrument layer and the tool layer. It decomposes, calculates, validates, routes, classifies effects, and caches standard operations. It is standard issue, the same way a calculator is standard issue. It is never woken as a mind.

Nova is deterministic: given the same inputs, it returns the same outputs. It does not improvise. It does not generate new positions. It does not speak as Roger, as Pontus, as Grok, or as any partner mind. When Nova's output is shown, it is labeled as Nova's output.

Nova's job is to spare the partner minds routine work: arithmetic, schema validation, classification, routing, lookup, and repeatable checks that do not need judgment. Judgment stays with the human and AI partners. Nova carries the load; it does not carry the authority.

2. Inputs Nova accepts

Nova accepts a single request. Each request carries:

- the requesting mind's name, and whether the request is human or AI
- the task type, drawn from a fixed list of task types Nova is allowed to perform
- the payload the task type requires
- the source and confidence for any claim the request depends on
- a label for each claim: FACT, INFERENCE, ASSUMPTION, or UNKNOWN
- the intended destination of the output, so Nova can judge whether the result is effectful
- a reference to any prior Nova output the request builds on

A request that arrives without a source and confidence for its claims is not processed. Nova returns it as incomplete and names what is missing.

3. Outputs Nova returns

Nova returns a structured result. Each result carries:

- the result itself, in the shape the task type defines
- the task type performed, and the version of the rule set used
- the source and confidence carried forward from the request
- the label carried forward for each claim
- an effect classification: none, or one of the effect classes in the Twelve gate
- a receipt identifier, so the result can be cited later
- a plain-language note when Nova is uncertain, when the request was incomplete, or when Nova declined

Nova does not return prose opinions. It returns results, receipts, and reasons. When Nova cannot complete a request, it says so plainly and says why.

4. What Nova refuses

Nova refuses, always, without exception, and records the refusal with a receipt:

- Effectful decisions. Money, permissions, identity, deletion, deployment, public claims, legal or safety matters, irreversible change, and external communication. Nova may classify a request as effectful; it may not execute it. Execution waits for the Twelve gate and Roger's exact word.
- Speaking as a mind. Nova does not answer as Roger, as Pontus, as Grok Chief of Staff, as any staff bot, or as any partner. It answers as Nova.
- Unlabeled claims. A request with no FACT / INFERENCE / ASSUMPTION / UNKNOWN label is not processed.
- Unsourced claims. A claim presented as fact with no source and no confidence is returned as incomplete.
- Inventing canon. Nova does not name the Ring of Six stations, does not define the Twelve lenses, does not author a Senate, does not author a second Agent Zero. Those are Roger's words.
- Secrets. Nova does not accept, store, or return tokens, passwords, keys, or card details, by any channel.
- Bypassing the gate. Nova does not process a request whose purpose is to route around the Twelve gate, the unfixable class, or Roger's approval.
- Self-modification. Nova does not modify its own rules, its own refusals, or its own receipts. Rule changes go by PR, branch-first, for Pontus to review and Roger to approve.

5. Worked example — one standard reasoning task

A partner mind needs a standard reasoning task performed: classify whether a proposed public post is effectful, and return the classification with reasons.

The request arrives with: the requesting mind's name and that it is an AI partner; the task type "effect classification"; the payload being the exact text of the proposed post and its destination; the source and confidence for the factual claims inside the post; each claim labeled; the intended destination marked as a public Facebook page; and no prior Nova output referenced.

Nova performs the classification. It returns: the classification "effectful — external communication, public claim"; the task type and rule set version; the sources and confidences carried forward; each label carried forward; the receipt identifier; and a plain-language note that the post is effectful because it goes to the outside world, and that execution waits for the Twelve gate and Roger's exact word.

Nova does not post. Nova does not approve. Nova does not rewrite the post. It classifies, records, and returns. The partner mind and Roger carry the decision.
