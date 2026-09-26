# TokenLens Evaluation Data

Evaluation data for the paper *TokenLens: An AI-Powered Multi-Source Framework for Real-Time Solana Token Risk Assessment* (SSWC 2026).

## Contents

| Path | Description |
|---|---|
| `data/evaluation_results.csv` | One row per token: contract address, name, symbol, ground-truth label (`truth`), TokenLens verdict, mapped class (`pred`), risk score, null-field count, latency (ms) |
| `data/corpus/<SYMBOL>/normalized.json` | Frozen 47-field normalised input passed to the LLM |
| `data/corpus/<SYMBOL>/ai.json` | Schema-validated model output (verdict, risk score, summary, red/green flags, note, sections) |
| `data/excluded_out_of_scope/` | Four stablecoin/governance tokens (USDS, CHZ, PRIME, PYUSD) run during corpus construction and excluded as out of scope |
| `prompt/system_prompt.txt` | Prompt template and scoring rubric used for LLM synthesis (`${...}` is replaced by the normalised token data) |

## Evaluation setup

- 29 Solana tokens: 10 Low Risk, 9 Medium Risk, 10 High Risk.
- Labels assigned by the first author from RugCheck ratings and DEXScreener market profiles (token age, liquidity, volume, observed liquidity removals). Labels are proxies, not confirmed outcomes.
- Each token was run once through the live system in June 2026 using DeepSeek-v4-pro (`reasoning_effort: "high"`, thinking enabled).
- Verdict-to-class mapping: SAFE -> Low, CAUTION -> Medium, RISKY/SCAM -> High.

## Reproducing the LLM stage

The live data APIs change over time. To re-evaluate the LLM stage independently of them, pass each `normalized.json` with `prompt/system_prompt.txt` to the model and compare against `ai.json`.

## Licence

Data released under CC BY 4.0. The TokenLens system source code is proprietary and not included.
