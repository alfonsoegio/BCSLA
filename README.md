# BCSLA

```
ganache-cli -p 7545
```

```
truffle compile && truffle migrate --network development && truffle exec test/testBCLSA.js
```

# Metric record trust between untrusted peers: smart contract approach

## Introduction

Recent publications (see [1] and [2]) analyze the possibility
of making use of blockchain features to approach SLA contract management.

## Monitoring agents

[2] exposes some closer approach about how this SLA management workflow
can be applied to virtualized network functions and services. Anyway
the schema relies on a trusted monitoring solution supported by some agents
lowering a bit the decentralization of the solution.

## Achieving consensus regarding monitoring metrics

Trying to solve the issue about the trusted monitoring and taking as a starting
point the "wrestling" smart-contract presented in [3] one can end up writing some
solidity smart-contract called BCSLA (blockchain SLA). The contract itself is
pretty simple as depicted in the flow diagram below; operator instantiates the
contract into Ethereum Distributed Virtual Machine; customer registers
within the contract instance. From that time, customer and operator
start posting their metric records (adding some stake to the call, to simplify
things, 1 ETH per call) with 4 possible outcomes:

1) Records do not match: The smart contract temporary disables the SLA
and holds the 2 ETH transfered by both: customer & operator:

2) Records match and QoS is above the level stated in the SLA; both
customer and operator get back their respective stakes held by the contract.

3) Records match and QoS is below the SLA; it turns out that an SLA
violation has occurred and customer receives back the stake held from
both: operator and customer.

At first sight, may seem a bit drastic to hold customer's cryptos in case
monitoring metrics differ but it should be added to the model
in order to ensure customer does not try to fake and lower metric
records in order to commit fraud to the operator.

Full code of the smart contract here:

## Possible features to extend the contract

- In order to consider the asimmetry between operator and customer
it maybe nice to have the operator making an initial transfer
directly proportional to the value of the whole contract duration
(initial proof of stake)
and keep retrieving it while posting correct metrics above the SLA
QoS level until the end of the contract.

- Also consider the possibility to create an SLA management
smart contract that can operate recurrently over different
instances to allow some
SLA chaining between different operators and providers: infrastructure
providers, service vendors, network operators and end-users.






[1] https://www.juniper.net/assets/us/en/local/pdf/whitepapers/2000674-en.pdf

[2] https://files.ifi.uzh.ch/CSG/staff/scheid/extern/publications/IFI-2018.02.pdf

[3] https://hackernoon.com/ethereum-development-walkthrough-part-1-smart-contracts-b3979e6e573e
