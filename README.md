# HedgePay — Flawed Business Logic Reward Inflation — PoC

> **Educational Purpose Only** — This PoC is created solely for security
> research and educational purposes. It runs against local mocks, not mainnet.

## Quick Start

```bash
git clone https://github.com/NomosLabs-Security/poc-hedgepay-2026
cd poc-hedgepay-2026
forge install foundry-rs/forge-std --no-git
forge test -vvvv
```

## Details

- **Exploit Date:** 2026-02-25
- **Chain:** BNB Smart Chain
- **Attack TX:** [0x5f2ea6cb...ed137f](https://bscscan.com/tx/0x5f2ea6cb43d14986188fa2f474d9e22502fa95cc76cab72cd6ba1ba146ed137f)
- **Block:** #83268463
- **Expected Output:** Reward pool drain (~$15.7K) via inflated balance notifications
- **Full Analysis:** [NomosLabs Security Intelligence Archive](https://nomoslabs.io/archive/hedgepay-2026)

## Vulnerability

The HPAY token's `_transfer()` function notified the external `RewardManager`
with **pre-fee balances** instead of actual post-fee balances. Since HPAY has
an 18% transfer tax, each transfer created a gap where the reward manager
believed accounts held more tokens than they actually did. By repeatedly
transferring, an attacker could inflate accumulated reward weight and drain
the WBNB reward pool.

## License

MIT — For educational use only.
