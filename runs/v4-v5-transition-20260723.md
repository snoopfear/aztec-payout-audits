# Provider 25 V4 → V5 payout transition

This record covers the payout transition from the previous Rollup contract to
the V5 Rollup contract.

## Rollup ranges

| Rollup | Epoch range | Delegator payout | Transfers |
|---|---:|---:|---:|
| V4 `0xAe2001f7e21d5EcABf6234E9FDd1E76F50F74962` | `4790-4951` | `76,387.5 AZTEC` | `16/16` |
| V5 `0x91ff8bbd8ebb07893010d50a48a1609e5ebd8e34` | `0-872` | `136,500 AZTEC` | `18/18` |

Total paid to delegators: `212,887.5 AZTEC`.

## V4 reward correction

The initial V4 audit attributed 295 provider checkpoints using the nominal
fixed reward of 350 AZTEC per checkpoint.

On-chain reconstruction of the V4 proof batches showed that checkpoints
`116703`, `116709`, `116710`, and `116716` were included in proof batch
`116694-116723`, which received zero fixed sequencer reward.

The corrected V4 settlement therefore contains:

- attributed provider checkpoints: `295`
- reward-bearing provider checkpoints: `291`
- fixed reward: `101,850 AZTEC`
- delegator share: `76,387.5 AZTEC`
- fixed operator retention: `25,462.5 AZTEC`

Variable transaction fees were excluded from the fixed-reward delegator split,
consistent with the payout methodology used for previous ranges.

## Audit artifacts

### V4

- Original nominal audit:
  `epoch-4790-4951-mrxk946d-f1b3c9.json`
- Corrected audit used for payment:
  `epoch-4790-4951-mrxk946d-f1b3c9-v4-reward-corrected.json`
- On-chain reward reconstruction:
  `v4-epoch-4790-4951-reward-reconstruction.json`
- Final reconciliation:
  `v4-epoch-4790-4951-final-reconciliation.json`
- Completion record:
  `v4-epoch-4790-4951-done.json`

### V5

- Audit:
  `epoch-0-872-mrxmt825-56fc6d.json`
- Final reconciliation:
  `v5-epoch-0-872-final-reconciliation.json`
- Completion record:
  `v5-epoch-0-872-done.json`

The next payout range begins at **V5 epoch `873`**.
