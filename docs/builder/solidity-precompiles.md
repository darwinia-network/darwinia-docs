---
sidebar_position: 103
---

# Solidity Precompiles

## Darwinia

Ethereum compatible:

- `0x0000000000000000000000000000000000000001`: ECRecover
- `0x0000000000000000000000000000000000000002`: Sha256
- `0x0000000000000000000000000000000000000003`: Ripemd160
- `0x0000000000000000000000000000000000000004`: Identity
- `0x0000000000000000000000000000000000000005`: Modexp
- `0x0000000000000000000000000000000000000006`: Bn128Add
- `0x0000000000000000000000000000000000000007`: Bn128Mul
- `0x0000000000000000000000000000000000000008`: Bn128Pairing
- `0x0000000000000000000000000000000000000009`: Blake2F
- `0x0000000000000000000000000000000000000400`: StateStorage
- `0x0000000000000000000000000000000000000401`: Dispatch

Darwinia dedicated:

- `0x0000000000000000000000000000000000000400`: StateStorage
    - This contract is used to get the storage values from substrate modules by storage key.
    - Function signature: `state_storage(bytes)`
    - Params: the substrate storage key
- `0x0000000000000000000000000000000000000401`: Dispatch
    - This contract is used to dispatch the substrate dispatch calls.
    - Function signature: `(bytes)`
    - Params: scale encoded substrate dispatch call

## Crab

Ethereum compatible:

- `0x0000000000000000000000000000000000000001`: ECRecover
- `0x0000000000000000000000000000000000000002`: Sha256
- `0x0000000000000000000000000000000000000003`: Ripemd160
- `0x0000000000000000000000000000000000000004`: Identity
- `0x0000000000000000000000000000000000000005`: Modexp
- `0x0000000000000000000000000000000000000006`: Bn128Add
- `0x0000000000000000000000000000000000000007`: Bn128Mul
- `0x0000000000000000000000000000000000000008`: Bn128Pairing
- `0x0000000000000000000000000000000000000009`: Blake2F

Darwinia dedicated:

- `0x0000000000000000000000000000000000000400`: StateStorage
- `0x0000000000000000000000000000000000000401`: Dispatch
- `0x0000000000000000000000000000000000000402`: KTON
    - KTON contract which compatible with the Ethereum ERC20 protocol.

## Pangoro

Ethereum compatible:

- `0x0000000000000000000000000000000000000001`: ECRecover
- `0x0000000000000000000000000000000000000002`: Sha256
- `0x0000000000000000000000000000000000000003`: Ripemd160
- `0x0000000000000000000000000000000000000004`: Identity
- `0x0000000000000000000000000000000000000005`: Modexp
- `0x0000000000000000000000000000000000000006`: Bn128Add
- `0x0000000000000000000000000000000000000007`: Bn128Mul
- `0x0000000000000000000000000000000000000008`: Bn128Pairing
- `0x0000000000000000000000000000000000000009`: Blake2F
- `0x0000000000000000000000000000000000000400`: StateStorage
- `0x0000000000000000000000000000000000000401`: Dispatch

Darwinia dedicated:

- `0x0000000000000000000000000000000000000400`: StateStorage
- `0x0000000000000000000000000000000000000401`: Dispatch
- `0x0000000000000000000000000000000000000800`: BLS12381
    - function signature: `fast_aggregate_verify(bytes[],bytes,bytes)

## Pangolin

Ethereum compatible:

- `0x0000000000000000000000000000000000000001`: ECRecover
- `0x0000000000000000000000000000000000000002`: Sha256
- `0x0000000000000000000000000000000000000003`: Ripemd160
- `0x0000000000000000000000000000000000000004`: Identity
- `0x0000000000000000000000000000000000000005`: Modexp
- `0x0000000000000000000000000000000000000006`: Bn128Add
- `0x0000000000000000000000000000000000000007`: Bn128Mul
- `0x0000000000000000000000000000000000000008`: Bn128Pairing
- `0x0000000000000000000000000000000000000009`: Blake2F

Darwinia dedicated:

- `0x0000000000000000000000000000000000000400`: StateStorage
- `0x0000000000000000000000000000000000000401`: Dispatch
- `0x0000000000000000000000000000000000000402`: KTON