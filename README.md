Bitcoin Core++ integration/staging tree
=====================================

What is Bitcoin Core++?
---------------------

IN DEVELOPMENT: Do not use.
Remaining work:
1. Indefinite duration Versionbit 27 tests based on higher activation thresholds.
2. Larger CompactBlock support (larger indices). Adjusting bucket checking sizes.
3. Benchmark tests.

Bitcoin Core++ is a long-term patch designed to remove block size limits from the consensus layer in the least divisive way possible.
Bitcoin Core++ is an exact copy of Bitcoin Core without any branding changes and the absolute minimal functional changes to remove
block size and sig op limits from the consensus layer after a formal more restrictive BIP8 versionbits activation.
Changes:
1. User-Agent is changed to Satoshi++.
2. Bit 27 in versionbits signals the support of the hardfork. This is the most likely bit to never conflict with any other BIP softfork activation signal.
3. If BIP++1 is activated, versionbit 27 will always be considered the hardfork bit henceforth. There should only be consensus forming around one hardfork at any time.
The rest of the bits will remain softfork signalling defined by BIP8.
Once 99% of the last 2016 blocks signal support then size constraints no longer apply after the next immediate difficulty retarget period.

Every major release of Bitcoin Core will have BIP++1 changes rebased here and re-released with the exact same version tag.

Bitcoin Core++ changes are referred to as BIP++1 and has no associated BIP.
Bitcoin Core++ does not accept any other BIP++'s. Only PR's related to changes in BIP++1 will be considered.
If BIP++1 gets activated this project/patch will end.
For anything else please follow formal contribution processes at https://github.com/bitcoin/bitcoin.

Why Bitcoin Core++?
---------------------
Hardforks are designed to be very difficult to implement and contentious by design. Due to this https://github.com/bitcoin/bitcoin will never
merge in an intentional non bug-fix hardfork into its staging branch, even if it denies the existance that technology exponentially gets faster over time
and a fixed block size limit rule inevitably slowly becomes mores outdated regardless of Lightning networks adoption rate.
This patch provides a mechanism to signal support for removing, or supporting an increase in the block size rule, after which a formal BIP can be prepared when
activation appears to be gaining significant support. This client will always support whatever size limits adjustments that a formal BIP proposes upto a 1GB pre-weighted limit.
The inevitablity of increasing economic support for larger blocks will lead to another blocksize war. This repository is here to try prevent the creation of another fractured chain.

Isn't unlimited block/sigop size dangerous?
---------------------
Yes it is, but its important to ephasise this is a long-term signalling patch and designed to follow the 4MB weighted network economic majority network as much as technically possible
and still provide the latest Bitcoin Core improvements that thousands have contributed to and reviewed.
The removal of checking block size/op limits in code is so support of this change is taken seriously if activation gets close.
This allows Bitcoin Core clients to automatically notice and warn about an activated rule at 90% without forking the network until the much more difficult 99% threshold is reached.
A proper BIP should be proposed that operates concurrently to signal the new upper limit or algorithm to use.

Are the changes safe?
---------------------
This patch is one small commit that can easily be compared.

What are the hardware requirements?
---------------------
To keep the patch minimal, non consensus code buffer sizes have already increased.
Certain file IO buffer sizes in Bitcoin Core++ automatically become adjusted to 1GB even without activation.
Therefore a machine with atleast 16GB of RAM should be used which is becoming much more common.

--End of readme Bitcoin Core++ adjustment--

Bitcoin Core integration/staging tree
=====================================

https://bitcoincore.org

For an immediately usable, binary version of the Bitcoin Core software, see
https://bitcoincore.org/en/download/.

What is Bitcoin Core?
---------------------

Bitcoin Core connects to the Bitcoin peer-to-peer network to download and fully
validate blocks and transactions. It also includes a wallet and graphical user
interface, which can be optionally built.

Further information about Bitcoin Core is available in the [doc folder](/doc).

License
-------

Bitcoin Core is released under the terms of the MIT license. See [COPYING](COPYING) for more
information or see https://opensource.org/licenses/MIT.

Development Process
-------------------

The `master` branch is regularly built (see `doc/build-*.md` for instructions) and tested, but it is not guaranteed to be
completely stable. [Tags](https://github.com/bitcoin/bitcoin/tags) are created
regularly from release branches to indicate new official, stable release versions of Bitcoin Core.

The https://github.com/bitcoin-core/gui repository is used exclusively for the
development of the GUI. Its master branch is identical in all monotree
repositories. Release branches and tags do not exist, so please do not fork
that repository unless it is for development reasons.

The contribution workflow is described in [CONTRIBUTING.md](CONTRIBUTING.md)
and useful hints for developers can be found in [doc/developer-notes.md](doc/developer-notes.md).

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test on short notice. Please be patient and help out by testing
other people's pull requests, and remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/test), written
in Python.
These tests can be run (if the [test dependencies](/test) are installed) with: `test/functional/test_runner.py`

The CI (Continuous Integration) systems make sure that every pull request is built for Windows, Linux, and macOS,
and that unit/sanity tests are run automatically.

### Manual Quality Assurance (QA) Testing

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

Translations
------------

Changes to translations as well as new translations can be submitted to
[Bitcoin Core's Transifex page](https://www.transifex.com/bitcoin/bitcoin/).

Translations are periodically pulled from Transifex and merged into the git repository. See the
[translation process](doc/translation_process.md) for details on how this works.

**Important**: We do not accept translation changes as GitHub pull requests because the next
pull from Transifex would automatically overwrite them again.
