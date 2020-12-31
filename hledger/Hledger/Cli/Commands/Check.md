check\
Check for various kinds of errors in your data. 
*experimental*

_FLAGS

hledger provides a number of built-in error checks to help
prevent problems in your data. 
Some of these are run automatically; or,
you can use this `check` command to run them on demand,
with no output and a zero exit code if all is well.
Some examples:

```shell
hledger check      # basic checks
hledger check -s   # basic + strict checks
hledger check ordereddates uniqueleafnames  # basic + specified checks
```

Here are the checks currently available:

### Basic checks

These checks are always run automatically, by (almost) all hledger commands,
including `check`:

- **parseable** - data files are well-formed and can be 
  [successfully parsed](hledger.html#input-files)

- **autobalanced** - all transactions are [balanced](hledger.html#postings), 
  inferring missing amounts where necessary, and possibly converting commodities 
  using [transaction prices] or automatically-inferred transaction prices

- **assertions** - all [balance assertions] in the journal are passing. 
  (This check can be disabled with `-I`/`--ignore-assertions`.)

### Strict checks

These additional checks are run when the `-s`/`--strict` ([strict mode]) flag is used.
They can also be run by specifying their names as arguments to `check`:

- **accounts** - all account names used by transactions 
  [have been declared](hledger.html#account-error-checking)

- **commodities** - all commodity symbols used 
  [have been declared](hledger.html#commodity-error-checking)

### Other checks

These checks can be run only by specifying their names as arguments to `check`:

- **ordereddates** - transactions are ordered by date (similar to the old `check-dates` command)

- **payees** - all payees used by transactions have been declared

- **uniqueleafnames** - all account leaf names are unique (similar to the old `check-dupes` command)

### Add-on checks

These checks are not yet integrated with `check`, but are available as
[add-on commands] in <https://github.com/simonmichael/hledger/tree/master/bin>:

- **hledger-check-tagfiles** - all tag values containing / (a forward slash) exist as file paths

- **hledger-check-fancyassertions** - more complex balance assertions are passing

You could make your own similar scripts to perform custom checks;
Cookbook -> [Scripting](scripting.html) may be helpful.


[transaction prices]: hledger.html#transaction-prices
[balance assertions]: hledger.html#balance-assertions
[strict mode]: hledger.html#strict-mode
[add-on commands]: hledger.html#add-on-commands