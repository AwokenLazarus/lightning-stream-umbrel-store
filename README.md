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
- **Lightning Fork**, the Lightning node.

## Add this store and install

1. In Umbrel, open the **App Store**.
2. Click **⋯** in the top right, then **Community App Stores**.
3. Paste `https://github.com/AwokenLazarus/lightning-stream-umbrel-store` and click **Add**.
4. Open the **Lazarus** store and install **Lightning Stream**.

The app connects to your Lightning node by itself. You don't need to copy any keys. Open it from your
Umbrel dashboard and log in with the app password Umbrel shows for it. The first screens walk you
through the rest: making your approval key and signing the starter spending rules.

Updates come through Umbrel in the usual way when this store gets a new version.

## Before you buy: get a channel

The app pays from your own Lightning node, so the node needs a funded channel on the BLAKE2b Lightning
network with a route to the shop. Without one, your first buy fails with "no route".

1. In **Lightning Fork**, open one channel of 20,000 to 50,000 sats. 20,000 is the smallest lnd
   accepts by default, and a shop's ticket is about 1,000 sats.
2. Open it to any well-connected public node, or straight to our test shop's node, which is reachable
   over Tor (Lightning Fork on Umbrel has Tor on):
   - key: `02c86d8dd97ac82338edece395f29369253894033464315c8d9e086a8cafe3a3b6`
   - address: `37g2spzl2oe4smllorb4wkl6n4nm2zcux5ozv5wzwpibxq63h2mayjid.onion:9735`
3. Wait until the channel is active: a few confirmations, then a few minutes.

If a payment can't find a route, check that the channel is active and your side holds more than about
1,000 sats, wait ten minutes, or open a second channel to a different node. Still stuck? Open an issue
at https://github.com/AwokenLazarus/Lightning-Stream/issues with your node's public key.

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
