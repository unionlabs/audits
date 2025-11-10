# 004 - CosmWasm Access Management

CosmWasm implementation of [OpenZeppelin][oz]'s [`AccessManaged.sol`][am] and [`Pausable.sol`][ps].
This contract module makes available a `Restricted<T>` wrapper. This should wrap the
`ExecuteMsg` for the contract. All entrypoints will be permissioned according to an "authority":
a contract like `access_manager` that follows the `ExecuteMsg`/`QueryMsg` interface,
implementing a policy that allows certain callers to access certain functions.
NOTE: The `Restricted<T>` wrapper will apply access control to *all* methods by default.
Internal methods can be marked as such by prefixing the JSON name with
`Selector::INTERNAL_PREFIX` with
`#[serde(rename)]`, however this will make the methods fully public to call and access must be
checked by the access managed contract itself.


## Scope

The following new core contracts for access management:

- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/access-manager
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/access-managed
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/pausable
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/upgradable

The integration of this access management system with the following contracts:

- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/ibc-union/core
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/ibc-union/app/ucs03-zkgm
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/cw-unionversal-token
- https://github.com/unionlabs/union/tree/accessmanaged/cosmwasm/cw-escrow-vault

For these integrations, please make sure that not only are the usages of `Restricted` and `Pausable` correct, but also ensure that we are not _missing_ usages of `Restricted` and `Pausable` where we should have used them, or any misconfiguration in our types that can cause unintended behavior. Also ensure that upgradability is properly Restricted.

## Commit hash

Use the HEAD of `unionlabs/union/accessmanaged`. We will give notice of any new commits / small changes during audit. When linking in the audit, please link using a permalink to the latest commit.


[oz]: https://www.openzeppelin.com
[am]: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v5.4.0/contracts/access/manager/AccessManaged.sol
[ps]: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v5.4.0/contracts/utils/Pausable.sol
[et]: https://serde.rs/enum-representations.html#externally-tagged
[selector]: https://docs.soliditylang.org/en/latest/abi-spec.html#function-selector

