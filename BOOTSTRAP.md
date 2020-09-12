## Bootstrapping Stack

### Using System GHC and System Cabal

#### Ubuntu 20.04.1

* Install System GHC (`ghc`) and System Cabal (`cabal-install`) packages using the system package manager
* Compile a binary distribution of GHC 8.6.5, and note the path of the bindist for later use (see GHC build instructions, out of scope here)
* Add version constraint to OptParse-Applicative in `stack.cabal` file (`< 0.16.0.0`)
* Run `cabal new-run stack install` in the stack project root directory (where this file is)
* Where there is an error regarding stack being unable to find the bindist - and there will be - go edit the `config.yaml` file for stack and add
  the `setup-info-locations` stanza pointing at a file containing setup location data similar to `https://raw.githubusercontent.com/commercialhaskell/stackage-content/master/stack/stack-setup-2.yaml`
  * As an example for `config.yaml`, for stack:
    ```
    setup-info-locations:
      - /home/someuser/.stack/setup-info.yaml
    ```
  * As an example for `setup-info.yaml`, at `/home/someuser/.stack/setup-info.yaml`:
    ```
    ghc:
      linux-ppc64:
        8.6.5:
          url: "/home/someuser/bindists/ghc-8.6.5-ppc64le.tar.xz"
    ```
* Rereun `cabal new-run stack install` and stack should be installed to your local binary directory, $PATH to taste
