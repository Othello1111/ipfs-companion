# Notes on Developing with `libdweb`

> [`mozilla/libdweb`](https://github.com/mozilla/libdweb) hosts a community
effort to implement experimental APIs for Firefox WebExtensions with a goal of
enabling dweb protocols in Firefox through browser add-ons. The long term goal
of this project is to integrate these APIs into the WebExtensions ecosystem.

See also:
- [#343](https://github.com/ipfs-shipyard/ipfs-companion/issues/343): _Create WebExtensions Experiments to Prototype Missing APIs_


## TL;DR

1. Having `firefox-nightly` in `$PATH`, execute commands below to checkout, build and run Companion extension in libdweb-enabled context:
   ```
   git clone -b libdweb --recurse-submodules --depth 1 https://github.com/ipfs-shipyard/ipfs-companion.git
   npm run libdweb
   ```

2. Optional Smoke-Test:
   - Open `ipfs://bafkreickb4yq3sr3q2xqn3z3wzimilsa4wkbx25azqbvcnihq65moyjcvi`
   - Open `ipns://docs.ipfs.io`
   - Confirm `ipfs://` protocol remains in Location Bar ([example](https://ipfs.io/ipfs/bafybeie5gq4jxvzmsym6hjlwxej4rwdoxt7wadqvmmwbqi7r27fclha2va))

## Developer Notes


### Install Firefox Nightly

- Get latest Nightly from http://nightly.mozilla.org/
   - libdweb won't run in regular release, it has to be nightly or developer edition

### How to Build and run libdweb-enabled bundle

```
# checkout libdweb branch into a new directory
# including submodules (namely ./libdweb)
git clone -b libdweb --recurse-submodules --depth 1 https://github.com/ipfs-shipyard/ipfs-companion.git

# install deps and build
npm run libdweb:build

# run  (assumes firefox-nightly on PATH)
npm run libdweb:firefox
```

### Manually Deploy in Firefox with libdweb APIs ✂️

To run your extension in libdweb context:

```
export MOZ_DISABLE_CONTENT_SANDBOX=1
web-ext run --firefox=/path/to/nightly/firefox-bin --browser-console --url about:debugging
```

or use alias:

```
npm run libdweb:firefox
```


Additional notes:

- If you want `libdweb:firefox` to work, ensure `firefox-nightly` is on your `$PATH`
   - if `firefox-nightly` is missing, create it in unpacked directory via `ln -s firefox firefox-nightly`
- After initially running `libdweb:build` it is ok to use `yarn watch` – it will work as expected

## Appendix: Smoke-Testing libdweb APIs

#### Protocol Handler API

1. Open `ipfs://bafkreickb4yq3sr3q2xqn3z3wzimilsa4wkbx25azqbvcnihq65moyjcvi`
1. Open `ipns://docs.ipfs.io`
1. Confirm `ipfs://` protocol remains in Location Bar ([example](https://ipfs.io/ipfs/bafybeie5gq4jxvzmsym6hjlwxej4rwdoxt7wadqvmmwbqi7r27fclha2va))

## References

- [ipfs-companion/issues/#343](https://github.com/ipfs-shipyard/ipfs-companion/issues/343) – Create WebExtensions Experiments to Prototype Missing APIs
- https://github.com/mozilla/libdweb/ – Extension context containing an experimental libdweb APIs
- https://github.com/orgs/libdweb – API adapters for seamless libdweb integration
- `#dweb` @ [irc.mozilla.org](https://wiki.mozilla.org/IRC#Connect_to_the_Mozilla_IRC_server)