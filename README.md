# AdWorm

A small two-head scoring network, retrained to steer a worm toward food, and a single page that runs it in the browser.

## Background

This network started as a 105 KB ONNX model (107,881 bytes, 25,218 parameters) inside a third-party SDK bundled with a mobile merge game. The SDK fed it a player profile (ad watches, session length, logins, currency, board fill, country, device) and the next 63 pieces on offer. One head predicted how many seconds the player would keep playing. The other predicted the chance they would watch an ad. The SDK appears to use those two scores to choose which item a generator drops. This repository keeps the architecture, discards those objectives, and retrains both heads to steer a worm toward food. The included weights are the result.

This is an independent experiment. It is not affiliated with the SDK's maker or the game's publisher.

## What the page does

`index.html` is self-contained, with the weights embedded. It makes no network requests and loads no external assets. Open it from disk.

A worm moves across a field and scores 13 candidate turns about eight times a second. The page normalizes the two outputs across those candidates, adds them, and takes the best turn. A second weight set also receives hunger, slow noise, and 90 body sensors. The brain switch swaps between the two.

Click anywhere in the field to move the food. The score mode selects both outputs, steering only, or approach only.

The signal map is a sampled view of the same forward pass. Hover or tap a node to move the inspector to that neuron. Blue is positive, rust is negative. The grid under the map lists every value in every layer; select a cell to inspect it.

## License

Public domain. See `LICENSE`.
