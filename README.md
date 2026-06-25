# Aztec Staking Payout Public Audit Record

Public audit record for **snoopfear's** Aztec sequencer reward distributions to delegators.

- Provider page: https://stake.aztec.network/providers/25
- Tool source: https://github.com/AztecProtocol/aztec-staking-payout
- Distribution wallet: `0x1F0d98760aE903AF089c847550D0C28183F4b178`
- Provider id: `25`
- Current commission: `25%` / `2500` bps

## What this repo is

This repository is the public audit trail for Aztec provider `25` payouts.

Aztec sequencer rewards are routed to a distribution wallet controlled by the operator. The per-delegator amounts are computed off-chain with the `aztec-staking-payout` tool and then paid from the distribution wallet. The audit files committed here allow delegators and third parties to verify the distribution amounts against on-chain data without relying only on the operator's statement.

> [!NOTE]
> The payout tool holds no funds, deploys no contracts, and does not custody delegator rewards. It computes deterministic payout records from on-chain data. Actual settlement is executed from the operator-controlled distribution wallet.

## Why a payout tool exists

Provider commission rates in the Aztec staking protocol are baked into each delegation's coinbase split contract and cannot be changed retroactively for existing delegations. The off-chain audited payout flow is a tactical mechanism for operators to publish a clear effective commission and distribute rewards from a controlled distribution wallet while making the resulting payouts publicly auditable.

For provider `25`, the public effective commission is `25%`.

## What's in `runs/`

Each settlement range adds audit artifacts under `runs/`.

| File | What it is |
|---|---|
| `epoch-<from>-<to>-<runId>.json` | The raw payout audit record produced by the payout tool. It includes the epoch/checkpoint/L1 block range, reward configuration snapshot, attributed checkpoints, commission, and per-delegator transfer breakdown. |
| `epoch-4017-4225-final-reconciliation.json` | Final on-chain reconciliation for the `4017-4225` range, matching expected transfers against ERC20 `Transfer` events. |
| `epoch-4017-4225-done.json` | Completion record for the `4017-4225` range. |
| `paid-ranges.md` | Human-readable ledger of paid ranges and next payout start epoch. |

## Published ranges

| Range | Status | Delegator payout | Notes |
|---|---:|---:|---|
| `4015-4016` | paid | `262.5 AZTEC` | Initial test payout |
| `4017-4225` | paid | `130,987.5 AZTEC` | Final reconciliation clean, `18/18` transfers |

Next payout should start from epoch `4226`.

## How to verify a distribution

Everything needed to re-derive a payout is in the audit JSON:

1. Open the relevant `epoch-<from>-<to>-<runId>.json` file in `runs/`.
2. Check the epoch/checkpoint/L1 block range, `rewardConfig`, `checkpointsProposed`, commission, and `transfers[]`.
3. Verify that the attributed checkpoint proposal transactions exist on-chain and correspond to the listed attesters.
4. Sum the per-delegator proposal weights, apply the published commission, and compare the result to `transfers[]`.
5. For settled ranges, compare `transfers[]` against the final reconciliation file and the ERC20 `Transfer` events from the distribution wallet.

The `4017-4225` range has final reconciliation status `paid`, with:

- `paidCount: 18`
- `unpaidCount: 0`
- `ambiguousCount: 0`
- `totalPaidAztec: 130,987.5`

## Operator details

| Field | Value |
|---|---|
| Operator | snoopfear |
| Provider id | `25` |
| Distribution wallet | `0x1F0d98760aE903AF089c847550D0C28183F4b178` |
| Commission | `25%` / `2500` bps |
| Payout mode | Audited off-chain payout from distribution wallet |
| Next payout start epoch | `4226` |
