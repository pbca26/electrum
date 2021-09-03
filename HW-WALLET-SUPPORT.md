## Chips Electrum Wallet HW test results with BTC app on Ledger Nano X

### Legacy (p2pkh) address test:
  1) Derive receive address (receive) - pass<b>*</b>
  2) Transaction signing (send) - pass<b>**</b>

### p2sh-segwit (p2wpkh-p2sh) address test:
  1) Derive receive address (receive) - pass<b>*</b>
  2) Transaction signing (send) - pass<b>**</b>

### Native segwit (p2wpkh) address test:
  1) Derive receive address (receive) - pass
  2) Transaction signing (send) - pass

Only Native segwit addresses are working out of the box. p2pkh and p2wpkh-p2sh require firmware fixes.

<b>*</b> Address derivation is working but it shows a BTC address on device screen. It will require a fork of BTC app for Ledger with CHIPS specific address bits changes baked into it. Same goes for Trezor, changes on firmware level are required in order for users to see KMD like addresses on the screen.

<b>**</b> Transaction signing is working but it shows a BTC address on device screen. It will require a fork of BTC app for Ledger with CHIPS specific address bits changes baked into it. Same goes for Trezor, changes on firmware level are required in order for users to see KMD like addresses on the screen.
