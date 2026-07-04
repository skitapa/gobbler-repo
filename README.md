# gobbler module repository

The **public storefront** for [gobbler](https://github.com/skitapa/gobbler) modules:
a minisign-signed `index.json` plus the module artifacts it references. This is the
only thing a gobbler node ever downloads from the network for its module center.

- **Trust model**: every gobbler binary ships the project's minisign public key
  (key id `F87076C75F0B25A6`). A node verifies `index.json.minisig` against that
  key, then verifies each artifact's sha256 from the signed index, **before**
  anything touches disk. Unsigned or tampered content is refused, always —
  there is no override flag.
- **Publishing** happens from the gobbler source tree (`repo/gen` builds
  `index.json` + artifacts; the key holder signs with `minisign -Sm index.json`)
  and lands here as plain files.
- Nothing in this repository is executable by cloning it; modules only run after
  a gobbler node verifies and installs them.
