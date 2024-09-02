+++
description = "Glossary of legal terms used in RGB smart contracts"
template = "page.html"
permalink = "/glossary/legal"
+++

# RGB Legal Glossary

Glossary explaining legal meaning of terms relate to RGB smart contracts.

## RGB contract

RGB contract is an agreement between contract parties structured in a form of bearer digital contract. The contract 
may relate to the both digital of physical assets and events. Contracts which relate to only digital world 
potentially may be settled in an automatic way without involving any third parties or intermediaries outside the 
contract parties. RGB contracts may provide an ability for the broader public, which is not a part of the contract 
parties to participate contract operations via mechanism of valencies and state extensions.

A contract has state and business logic, expressed in terms of ownership rights and executive rights. The contract 
state, rights and conditions of valid operations are defined using RGB schema; only state and operations which 
allowed by the schema declarations and validation scripts are allowed to happen within the contract scope.

## Contract participant

Contract participant is an actor which participate in contract operations.

Contract parties are classified into the following categories:

- _Contract issuer_, an actor creating contract genesis
- _Contract party_ &ndash; all actors which has ownership rights over RGB contract state
- _Public_ &ndash; an actor constructing state extensions. Can exist only in contracts providing valencies and state extensions.

## Contract parties

RGB contract always have a well-defined parties of the contract, which hold ownership rights over atoms of state. 
The state owned by a contract party is called owned state.A contract party is always also a contract participant.

## Contract rights

RGB contract parties have a different rights as a part of the contract conditions defined through RGB schema. The 
rights under RGB contract can be classified into the following categories, defined below:

- [Ownership rights](#ownership-rights)
- [Executive rights](#executive-rights)
- [Public rights](#public-rights)

## Ownership rights

A party having rights over some of the owned contract state. This is exactly the same party which can spend bitcoin 
UTXO serving as a single-use-seal definition for the state assignment.

It is important to note that ownership rights and ability to spend UTXO participating assignment doesn't necessary 
implies ability to update the contract state or construct a valid state transition (see executive rights). See 
rights mismatch section for the details.

## Executive rights

An ability to update the contract state in a final form, i.e. to construct a valid state transition satisfying 
schema validation rules. See also rights mismatch and ownership rights to better understand the difference of 
executive and ownership rights in the scope of RGB smart contract.

## Public rights

A right under some schemata to use a contract valency and construct a valid state extensions, which can be later 
included into the state via reference from a different valid state transition. See state extension for the details.

## Rights mismatch

A mismatch between ownership rights and executive rights; an inability to provide an update to the state owned by a 
party. This is caused due to the schema bugs leading to the impossibility to construct a valid state transition with 
a specific set of ownership rights of the party and/or combination of seal definitions in their assignments.

Rights mismatch may happen in two main cases:

- A user by mistake has assigned different rights to the same UTXO and the schema doesn't provide a way of spending 
  that combination of rights with a valid state transition. This is a reason why properly-designed schema must 
  provide a rights split transition option.
- A schema doesn't provide a way of constructing state transition for a defined owned state. 

Contractum compiler notifies about this two bugs during schema compilation, however schemata designed without 
Contractum may still contain it.
