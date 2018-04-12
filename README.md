minichain_state_db
====

Inefficient, but human-readable state tree database

Differences between production-level databases
----
* No path encoding
* Human understandable indexing
* Human readable with `explorer` and `notepad`.

Why we should use state-tree based DB
----
* Saves only the changes on the disk.
* Can easily revert state to specific point.
* Can read state from specific point.

disadvantages
----
* `GetState` operation is not an `O(1)`.

Interface
----
__STORE__
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

__READ__
```cs
var P = "POINT_OF_STATE";

var a_WalletState_At_P = sdb.ReadState(P, a);
```
