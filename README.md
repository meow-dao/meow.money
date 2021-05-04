# MEOW Core [MEOW, 𝕸]

![MEOW]https://media.discordapp.net/attachments/837707670512468058/838707859143393290/YingYangWhiskers.png?width=674&height=674)

[![Build Status](https://travis-ci.com/dogecoin/dogecoin.svg?branch=master)](https://travis-ci.com/dogecoin/dogecoin)

MEOW is fork of Dogecoin's state in 2021 after upgrades. It is a cryptocurrency like Bitcoin in which you leverage the native token for transaction fees, although it does not use SHA256 as its proof of work (POW). Taking development cues from Tenebrix and Litecoin,
MEOW currently employs a simplified variant of scrypt.
- **Website:** [meow.ventures.](http://meow.ventures)

## License – Much license ⚖️
MEOW Core is released under the terms of the MIT license. See
[COPYING](COPYING) for more information or see
[opensource.org](https://opensource.org/licenses/MIT)

## Development and contributions – omg developers
Development is ongoing, and the development team, as well as other volunteers,
can freely work in their own trees and submit pull requests when features or
bug fixes are ready.

#### Version strategy
Version numbers are following ```major.minor.patch``` semantics.

#### Branches
There are 3 types of branches in this repository:

- **master:** Stable, contains the latest version of the latest *major.minor* release.
- **maintenance:** Stable, contains the latest version of previous releases, which are still under active maintenance. Format: ```<version>-maint```
- **development:** Unstable, contains new code for planned releases. Format: ```<version>-dev```

*Master and maintenance branches are exclusively mutable by release. Planned*
*releases will always have a development branch and pull requests should be*
*submitted against those. Maintenance branches are there for **bug fixes only,***
*please submit new features against the development branch with the highest version.*

#### Contributions ✍️

Developers are strongly encouraged to write [unit tests](src/test/README.md) for new code, and to
submit new unit tests for old code. Unit tests can be compiled and run
(assuming they weren't disabled in configure) with: `make check`. Further details on running
and extending unit tests can be found in [/src/test/README.md](/src/test/README.md).

There are also [regression and integration tests](/qa) of the RPC interface, written
in Python, that are run automatically on the build server.
These tests can be run (if the [test dependencies](/qa) are installed) with: `qa/pull-tester/rpc-tests.py`

Changes should be tested by somebody other than the developer who wrote the
code. This is especially important for large or high-risk changes. It is useful
to add a test plan to the pull request description if testing the changes is
not straightforward.

## Very Much Frequently Asked Questions ❓

### How much meow can exist? – So many kitties! 🐕
Mid 2021 (approximately a year and a half after release) there will be
approximately <TBD> coins.
Each subsequent block will grant <TBD> coins to encourage miners to continue to
secure the network and make up for lost wallets on hard drives/phones/lost
encryption passwords/etc.


### Such mining information ⛏

MEOW uses a simplified variant of the scrypt key derivation function as its
proof of work with a target time of one minute per block and difficulty
readjustment after every block. The block rewards are fixed and halve every
<TBD> blocks. Starting with the 600,000th block, a permanent reward of
10,000 MEOW per block will be issued.  

Originally, a different payout scheme was envisioned with block rewards being
determined by taking the maximum reward as per the block schedule and applying
the result of a Mersenne Twister pseudo-random number generator to arrive at a
number between 0 and the maximum reward.

This was changed starting with block 145,000, to prevent large pools from gaming
the system and mining only high reward blocks. At the same time, the difficulty
retargeting was also changed from four hours to once per block (every minute),
implementing an algorithm courtesy of the DigiByte Coin development team, to
lessen the impact of sudden increases and decreases of network hashing rate.

**The current block reward schedule:**

1–99,999: 0–1,000,000 MEOW

100,000–144,999: 0–500,000 MEOW

145,000–199,999: 250,000 MEOW

200,000–299,999: 125,000 MEOW

300,000–399,999: 62,500 MEOW

400,000–499,999: 31,250 MEOW

500,000–599,999: 15,625 MEOW

600,000+: 10,000 MEOW

**The original block reward schedule, with one-minute block targets and four-hour difficulty readjustment:**

1–99,999: 0–1,000,000 MEOW

100,000–199,999: 0–500,000 MEOW

200,000–299,999: 0–250,000 MEOW

300,000–399,999: 0–125,000 MEOW

400,000–499,999: 0–62,500 MEOW

500,000–599,999: 0–31,250 MEOW

600,000+: 10,000 MEOW

### Wow plz make meowd/meow-cli/meow-qt

  The following are developer notes on how to build MEOW on your native platform. They are not complete guides, but include notes on the necessary libraries, compile flags, etc.

  - [OSX Build Notes](doc/build-osx.md)
  - [Unix Build Notes](doc/build-unix.md)
  - [Windows Build Notes](doc/build-windows.md)

### Such ports

- RPC 22555
- P2P 22556

## Development tips and tricks

**compiling for debugging**

Run `configure` with the `--enable-debug` option, then `make`. Or run `configure` with
`CXXFLAGS="-g -ggdb -O0"` or whatever debug flags you need.

**debug.log**

If the code is behaving strangely, take a look in the debug.log file in the data directory;
error and debugging messages are written there.

The `-debug=...` command-line option controls debugging; running with just `-debug` will turn
on all categories (and give you a very large debug.log file).

The Qt code routes `qDebug()` output to debug.log under category "qt": run with `-debug=qt`
to see it.

**testnet and regtest modes**

Run with the `-testnet` option to run with "play meows" on the test network, if you
are testing multi-machine code that needs to operate across the internet.

If you are testing something that can run on one machine, run with the `-regtest` option.
In regression test mode, blocks can be created on-demand; see qa/rpc-tests/ for tests
that run in `-regtest` mode.

**DEBUG_LOCKORDER**

MEOW Core is a multithreaded application, and deadlocks or other multithreading bugs
can be very difficult to track down. Compiling with `-DDEBUG_LOCKORDER` (`configure
CXXFLAGS="-DDEBUG_LOCKORDER -g"`) inserts run-time checks to keep track of which locks
are held, and adds warnings to the debug.log file if inconsistencies are detected.
