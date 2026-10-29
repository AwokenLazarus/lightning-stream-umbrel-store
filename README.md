# Lightning Stream for Umbrel

This is an Umbrel community app store with one app, **Lightning Stream**. It lets you buy and sell
services over XBT Lightning, paid as you use them: a film by the megabyte, an AI model by the token,
or a miner's hashrate by the piece of work. Buying and selling happen in the same app.

The app's source code, documentation and issue tracker are in
[AwokenLazarus/Lightning-Stream](https://github.com/AwokenLazarus/Lightning-Stream).

## Before you install

Lightning Stream uses the XBT node and the Lightning node already on your Umbrel. It needs these two
apps from paulscode's community store (`https://github.com/paulscode/umbrel-store`), installed and synced first:

- **Knots-BLAKE2b**, the XBT node;
- **Lightning Fork**, the Lightning node. When it asks which Bitcoin node to use, pick
  **Knots-BLAKE2b**, not Umbrel's standard Bitcoin Node.

A first sync of Knots-BLAKE2b from nothing takes days, and Lightning Fork waits until the node is past
block 961,640, the first BLAKE2b block. If you are new to XBT, start the node first.

## Add this store and install

1. In Umbrel, open the **App Store**.
2. Click **⋯** in the top right, then **Community App Stores**.
3. Paste `https://github.com/AwokenLazarus/lightning-stream-umbrel-store` and click **Add**.
4. Open the **Lazarus** store and install **Lightning Stream**.

The app connects to your Lightning node by itself. You don't need to copy any keys. Open it from your
Umbrel dashboard and log in with the app password Umbrel shows for it. The first screens walk you
through the rest: making your approval key, signing the starter spending rules, and confirming that
the app may pay with real money (**Settings → Your node → Pay with real money**).

Updates come through Umbrel in the usual way when this store gets a new version.

## Before you buy: get a channel

The app pays from your own Lightning node, so the node needs a funded channel on the BLAKE2b Lightning
network with a route to the shop. Without one, your first buy fails with "no route".

1. In **Lightning Fork**, open one channel of 20,000 to 50,000 sats. 20,000 is the smallest lnd
   accepts by default, and a shop's ticket is about 900 sats.
2. Open it to a well-connected public node, such as ours, lazarus-xbt (it takes channels of 20,000
   sats or more), reachable over Tor (Lightning Fork on Umbrel has Tor on):
   - key: `033665f1accdf08dd2d2f22f62f8dd70ccd238381402b10c12c0be3e7fd493b8d5`
   - address: `6y4rkcimjbzfhj2j4oidbg4br4xgdfvpbsx7x3ifedv6jgfxg55wtiqd.onion:9735`

   Some nodes take only larger channels; they refuse a smaller one before anything is paid, so a
   refusal costs nothing. A channel straight to a shop's own node pays it from 0.1.17 on; before
   0.1.17 it cannot pay a shop that sells by BOLT 12 offer, ours included.
3. Wait until the channel is active: a few confirmations, then a few minutes.

If you added our shop before 0.1.16, open it under **Services → Sellers** and press **Check for
updates** before **Allow this seller to be paid**: the list saved before then names the shop's old
address, and Allow keeps failing on it.

If a payment can't find a route, check that the channel is active and your side holds more than about
1,000 sats, wait ten minutes, or open a second channel to a different node. Still stuck? Open an issue
at https://github.com/AwokenLazarus/Lightning-Stream/issues with your node's public key.

The whole setup, for Umbrel, StartOS and Linux, is on the website:
https://lazarus-xbt.xyz/stream/start/

## Use AI in your own programs (0.1.19)

Under **Services → AI** the app gives your box an OpenAI-compatible address on your network, such as
`http://umbrel.local:33540/v1`. Any AI app or agent that speaks that API (Open WebUI, coding agents,
your own scripts) can use the AI models of the sellers you allowed, paid per token within your
spending rules. Make a key for each program on that page; each key has its own limit and can be
revoked.

## Please read

- This software moves real sats. It has been tested on mainnet with small amounts only. Start with
  low prices and low limits.
- The app never holds anyone else's money. Your keys stay on your box, and only the app's signer
  can spend, within the rules you sign.
- Each container image is pinned to an exact published build (`ghcr.io/awokenlazarus/...@sha256:...`),
  built from a named commit of the source repository.

## Credits

Thanks to Chris Guida, whose review is the reason Lightning Stream is built on Lightning, and to Kyle
Santiago, whose points shaped its ticket limits. Lightning Fork and Knots-BLAKE2b for Umbrel are by paulscode.

Licence: MIT or Apache-2.0, as in the source repository.
