minichain_state_db
====

Inefficient, but human-readable state tree database

* No path encoding
* Human understandable indexing
* Human readable with `explorer` and `notepad`.

Interface
----
```cs
var sdb = new StateDB();

// Random wallet addresses
var a = UniqID.Generate();
var b = UniqID.Generate();
var c = UniqID.Generate();

// Push initial state.
var state = sdb.PushState(null, new WalletState[]
{
    new WalletState() { addr = a, balance = 0 },
    new WalletState() { addr = b, balance = 0 },
    new WalletState() { addr = c, balance = 0 }
});
state = sdb.PushState(state, new WalletState[]
{
    new WalletState() { addr = a, balance = 10 },
    new WalletState() { addr = b, balance = 20 },
    new WalletState() { addr = c, balance = 30 }
});
state = sdb.PushState(state, new WalletState[]
{
    new WalletState() { addr = a, balance = 10 }
});
// Push zero change.
state = sdb.PushState(state, new WalletState[]
{
});
```
