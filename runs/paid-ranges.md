# Aztec payout paid ranges

## Test payout

- Range: 4015-4016
- Counted checkpoints: 1
- Delegator payout: 262.5 AZTEC
- Operator retention: 87.5 AZTEC
- Recipient: 0x7535A04Ba04152f5446e2e94D6dd6d9F8643D246
- Tx: 0x3b670309d665c7e0e3b8dc60969a2544e7d65a167c372b9e3fad3e385f367aef
- Next payout should start from: 4017

## Paid payout 4015-4016

- Status: paid
- Range: 4015-4016
- Audit: runs/epoch-4015-4016-mqtkcviw-edae7d.json
- Safe JSON: runs/epoch-4015-4016-mqtkcviw-edae7d.safe.json
- Recipient: 0x7535A04Ba04152f5446e2e94D6dd6d9F8643D246
- Amount: 262.5 AZTEC (262500000000000000000)
- Tx: 0x3b670309d665c7e0e3b8dc60969a2544e7d65a167c372b9e3fad3e385f367aef
- Receipt: not published; verify by tx hash on-chain
- Next payout should start from: 4017

## Paid payout 4017-4225

- Status: paid / final on-chain reconciliation clean
- Range: 4017-4225
- Provider ID: 25
- Audit: runs/epoch-4017-4225-mqtl7gkp-3ab058.json
- Final reconciliation: runs/epoch-4017-4225-final-reconciliation.json
- Done record: runs/epoch-4017-4225-done.json
- Paid transfers: 18 / 18
- Delegator payout total: 130,987.5 AZTEC
- Operator retention according to audit: 43,662.5 AZTEC
- Incident loss accepted by operator: 51,712.5 AZTEC
- Incident tx: 0xa2463a2377a95f70020fa10dcccc410ee703ef93cb5064de378fdd7723cf9e0a
- Transfer mode actually completed: direct ERC20.transfer transactions from encrypted Foundry account
- Next payout should start from: 4226

## Paid payout 4226-4485

- Status: paid / final on-chain reconciliation clean
- Range: 4226-4485
- Provider ID: 25
- Audit: runs/epoch-4226-4485-mr3fxnju-ab21d2.json
- Final reconciliation: runs/epoch-4226-4485-final-reconciliation.json
- Done record: runs/epoch-4226-4485-done.json
- Paid transfers: 17 / 17
- Delegator payout total: 144,375 AZTEC
- Operator retention according to audit: 48,125 AZTEC
- Transfer mode: direct ERC20.transfer from encrypted Foundry account
- Next payout should start from: 4486

## Paid payout 4486-4789

- Status: paid / final on-chain reconciliation clean
- Range: 4486-4789
- Provider ID: 25
- Audit: runs/epoch-4486-4789-mrf0z3qc-b0692e.json
- Final reconciliation: runs/epoch-4486-4789-final-reconciliation.json
- Done record: runs/epoch-4486-4789-done.json
- Paid transfers: 17 / 17
- Delegator payout total: 145,950 AZTEC
- Operator retention according to audit: 48,650 AZTEC
- Transfer mode: direct ERC20.transfer from encrypted Foundry account
- Next payout should start from: 4790


## Paid payout V4 4790-4951

- Status: paid / final on-chain reconciliation clean
- Rollup: `0xAe2001f7e21d5EcABf6234E9FDd1E76F50F74962`
- Range: `4790-4951`
- Provider ID: `25`
- Original nominal audit: `runs/epoch-4790-4951-mrxk946d-f1b3c9.json`
- Corrected audit used for payment: `runs/epoch-4790-4951-mrxk946d-f1b3c9-v4-reward-corrected.json`
- Reward reconstruction: `runs/v4-epoch-4790-4951-reward-reconstruction.json`
- Final reconciliation: `runs/v4-epoch-4790-4951-final-reconciliation.json`
- Done record: `runs/v4-epoch-4790-4951-done.json`
- Paid transfers: `16 / 16`
- Delegator payout total: `76,387.5 AZTEC`
- Fixed operator retention: `25,462.5 AZTEC`
- Zero-fixed-reward checkpoints: `116703`, `116709`, `116710`, `116716`
- Transfer mode: direct `ERC20.transfer`
- V4 payout sequence complete; V5 uses a separate epoch sequence.


## Paid payout V5 0-872

- Status: paid / final on-chain reconciliation clean
- Rollup: `0x91ff8bbd8ebb07893010d50a48a1609e5ebd8e34`
- Range: `0-872`
- Provider ID: `25`
- Audit: `runs/epoch-0-872-mrxmt825-56fc6d.json`
- Final reconciliation: `runs/v5-epoch-0-872-final-reconciliation.json`
- Done record: `runs/v5-epoch-0-872-done.json`
- Paid transfers: `18 / 18`
- Delegator payout total: `136,500 AZTEC`
- Fixed operator retention: `45,500 AZTEC`
- Transfer mode: direct `ERC20.transfer`
- Next V5 payout should start from epoch `873`.
