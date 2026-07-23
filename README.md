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

| Rollup | Range | Status | Delegator payout | Notes |
|---|---:|---:|---:|---|
| V4 | `4015-4016` | paid | `262.5 AZTEC` | Initial test payout |
| V4 | `4017-4225` | paid | `130,987.5 AZTEC` | Final reconciliation clean, `18/18` transfers |
| V4 | `4226-4485` | paid | `144,375 AZTEC` | Final reconciliation clean, `17/17` transfers |
| V4 | `4486-4789` | paid | `145,950 AZTEC` | Final reconciliation clean, `17/17` transfers |
| V4 | `4790-4951` | paid | `76,387.5 AZTEC` | Corrected for four zero-fixed-reward checkpoints; `16/16` transfers |
| V5 | `0-872` | paid | `136,500 AZTEC` | First V5 payout range; `18/18` transfers |

Next payout should start from **V5 epoch `873`**.

## V4 to V5 Rollup transition

The V5 Rollup introduced a separate epoch sequence beginning at epoch `0`.

The final V4 payout covered epochs `4790-4951`. The first V5 payout covered
epochs `0-872`. These are separate Rollup-scoped ranges and are not overlapping
payments.

The V4 range required an on-chain reward correction because four attributed
provider checkpoints were included in a proof batch that received zero fixed
sequencer reward. Full details and hashes are published in
`runs/v4-v5-transition-20260723.md`.

### README maintenance after each payout

After a new payout range is completed and published:

1. Add a new row to the table above.
2. Update `Next payout should start from epoch ...`.
3. Update the same next-start epoch in the `Operator details` table below.
4. Make sure the new range artifacts exist in `runs/`:
   - `epoch-<from>-<to>-<runId>.json`
   - `epoch-<from>-<to>-final-reconciliation.json`
   - `epoch-<from>-<to>-done.json`
   - updated `paid-ranges.md`

## How to verify a distribution

Everything needed to re-derive a payout is in the audit JSON:

1. Open the relevant `epoch-<from>-<to>-<runId>.json` file in `runs/`.
2. Check the epoch/checkpoint/L1 block range, `rewardConfig`, `checkpointsProposed`, commission, and `transfers[]`.
3. Verify that the attributed checkpoint proposal transactions exist on-chain and correspond to the listed attesters.
4. Sum the per-delegator proposal weights, apply the published commission, and compare the result to `transfers[]`.
5. For settled ranges, compare `transfers[]` against the final reconciliation file and the ERC20 `Transfer` events from the distribution wallet.

For each settled range, the corresponding final reconciliation file should show:

- `paidCount == expectedCount`
- `unpaidCount == 0`
- `ambiguousCount == 0`
- `totalPaidAztec == totalExpectedAztec`

For transaction-level proof, check each paid entry in the reconciliation file against the ERC20 `Transfer` event from the distribution wallet to the listed recipient for the exact `amountWei`.

## Operator details

| Field | Value |
|---|---|
| Operator | snoopfear |
| Provider id | `25` |
| Distribution wallet | `0x1F0d98760aE903AF089c847550D0C28183F4b178` |
| Commission | `25%` / `2500` bps |
| Payout mode | Audited off-chain payout from distribution wallet |
| Next payout start | V5 epoch `873` |
