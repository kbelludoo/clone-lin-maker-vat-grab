# clone-lin-maker-vat-grab

Experimental **LIN** clone of MakerDAO / Sky `Vat.grab` — the Dai and USDS
CDP confiscation kernel (signed `ink`/`art` updates, `dtab = art*rate` cancelled
into `vice`/`sin`, collateral credited to the clipper via `_sub(gem, dink)`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/vat.sol` sha256 `9016fd94f0f1b014abf184edab86a3f5843042b17e3734407e0f0fabb920f49f` blob `ff90bbed5b36e54318bd5461cbf32e4167df2b28`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_vat_grab.lin`](src/lin_maker_vat_grab.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_vat_grab_c11.c`](test/oracles/maker_vat_grab_c11.c)
- **Proofs (lin-open only):** `examples/maker_vat_grab/` and `make maker-vat-grab-proof`
- **Class:** EXPERIMENTAL uint64-scale, `RAY' = 1e9`. Not mainnet `RAY=1e27`. Not wad×ray rad. Not a production vat replacement.

Named goldens: BARK seize `1e9` ink+art → **grab_ok=1**, clipper gem `1e9`, vice `1e18`; UNDERWATER art `2e9` on ink `1e9` still **grab_ok=1** with unbacked **vice=2e18`; ink underflow → **0**; naive i64 `7e18*3e18` wraps to **-5389669316318724096**; 128-bit muldiv fail-closes to **0**. No `live==1` gate (unlike `frob`).

## Reproduce proofs (in lin-open)

```bash
make maker-vat-grab-proof
# or: python3 test/prove_maker_vat_grab_external.py
```

## Not claimed

Uint256 / RAY=1e27 / wad×ray rad mainnet parity.
LIN replacing Maker, Sky, vat, Dog, Clipper, or the EVM. TVL or dollar savings. zk soundness.
`wish` / `wards` / `urns` mappings. `vat.frob` (see clone-lin-maker-vat-frob).
