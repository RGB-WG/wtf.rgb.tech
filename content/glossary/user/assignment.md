+++
description = "Combination of state (data) with single-use seal definition"
layout = "page"
permalink = "/glossary/user/assignment"
+++

# Assignment

Assignment is a combination of some data (*state*) with a specific
[single-use seal definition](single-use-seal#seal-definition), like bitcoin transaction outpoint.

<aside>
    <h2>History</h2>
    <p>The term was first introduced in Spring 2020 by Maxim Orlovsky and was used through all versions of RGB made
    after, starting from v0.1.0.</p>
</aside>

Assignments exist on a client side, and are never part of blockchain. While single-use seal definition *references*
some on-chain data structures (like transaction outpoints), this is a mere pointer which is not on-chain.

In other words, assignment creates a binding between certain value, known only to a user and existing offchain, and
a specific public single-use resource (i.e. single-use seal). This binding is also not publicly known, unless the
user creating the assignment would disclose it.


## Give me an example

Let's assume you are an asset issuer, either a fungible token under a [RGB20](rgb20) standard, or NFT under
[RGB21](rgb21). The issue is just a declaration, put in the RGB [contract](contract) [genesis](genesis) and known only
to you, plus those whom you'd tell (i.e. share the [contract consignment](consignment#contract) with). The declaration
should read "hereby I declare the issue of N tokens, owned by this bitcoin transaction outpoint". Here, the declaration
is the *assignment*, the *N tokens* part is the assigned state, and the provided bitcoin transaction outpoint, owning
the issued tokens, is a *signle-use seal definition*.


## What assignments are used for?

Assignments are a part of all types of RGB contract [operations](operation), including contract [genesis](genesis), 
[state transitions](state-transition) and [state extensions](state-extension). They are created by contract users and
act as operation outputs -- similar to the role of bitcoin transaction outputs.


## How assignments are look like?

<aside>
    <p>It is invalid to say that a state is "bound" or "attached" to a bitcoin transaction output; use the term
    <em>assigned</em> instead.</p>
</aside>

You won't meet assignments directly when working with RGB: they are hidden deep inside [RGB Core](rgb-core) library.
The only place where RGB user can face them is terminologically: when someone talks about client-side validation,
the right way to say is that some data or a state is *assigned* by a user ("client") to a public single-use seal
definitions and validated in that way.
