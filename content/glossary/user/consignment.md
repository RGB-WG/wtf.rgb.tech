+++
description = "Consignment is data package exchanged between users of RGB smart contracts"
permalink = "/glossary/user/consignment"
+++

# Consignment

Data package exchanged between users (peers) when they are using RGB smart contracts (or participate some other
client-side validation protocol).

<aside>
    <h2>History</h2>
    <p>The term was first introduced in Spring 2020 by Maxim Orlovsky and was used through all versions of RGB made
    after, starting from v0.1.0.</p>
</aside>

In blockchain world, the data are stored in a public ledger (blockchain) and replicated by each peer. This leads
to the loss of privacy, informational centralization and poor scalability. RGB smart contracts use client-side 
validation, which keeps the data on the peers site and doesn't put them into a blockchain or any shared ledger.
The data are exchanged between peers on an ad-hoc basis, only when needed, in pure peer-to-peer way, which significantly
improves the privacy, scalability and decentralization. The package of the data exchanged by peers specific to some
particular RGB contract is called <dfn>consignment</dfn>.

<aside>
    <h2>Non-consignment packages which peers can exchange</h2>
    <p>Consignments are not the only type of data packages which peers exchange in client-side validation protocols.
    There is another package type named <a href="disclosure">disclosure</a>, which is not a contract-specific. Unlike
    consignment, disclosures are used to provide the networks or third-parties with some information which otherwise
    would remain private.</p>
    <p>Another type of client-side data packages are <a href="kit">kits</a>. They are used by contract developers to
    distribute information about interfaces, schemata, type and script libraries.</p>
</aside>


## Types of consignments

There are two main types of consignments: _contract_ and _transfer_.

<a name="contract"><dfn>Contract consignments</dfn></a> are used to provide a user with an information required to use
some specific RGB contract. They are usually distributed by the contract issuers, but may also be downloaded from asset
or contract registries and explorers (like <https://rgbex.io>), or sent peer-to-peer, from a user to a user.

<a name="transfer"><dfn>Transfer consignments</dfn></a> are used by contract clients for
[state transfers](rgb-payment#state-transfer) from one user to another. For instance, when a payment is made, the sender
of the payment must provide the beneficiary with a transfer consignment.


## How do consignments look like?

Consignments are usually binary files, which do not contain human-readable information.

When a users need to send consignment data through a channel which doesn't support a binary format, they have an
option to use binary-to-text encoding (see [ASCII armoring](ascii-armoring)). In RGB, armoring is done in Base85, and
the encoded data are accompanied by additional headers and checksums. Here is a typical ASCII-armored contract
consignment, in a cut version: 

<aside>
    <p>In this example you can see that the armoring headers include information on the consignment
    <a href="#types-of-consignments">type</a>, version, contract id, used schema and interface implemented by the
    contract.</p>
    <p>Base85 encoding uses all alphanumeric characters and all other printable ASCII chars, which allows to achieve
    shorter representation than with Base64 encoding.</p>
</aside>

    -----BEGIN RGB CONSIGNMENT-----
    Id: rgb:csg:3yJCUNgH-xxfXcHX-E1dfL80-kT2R4z5-BJptGHf-sEERkJI#grace-austria-current
    Version: 2
    Type: contract
    Contract: rgb:pHRSdpDs-!wc6x7N-C4F4nPQ-PO!22oI-UUpEV6f-00RRQZM
    Schema: rgb:sch:lOk3!8GHPOTYbmEPaNg!tsUh1trhOA!VobyCWo2q6VM#talent-easy-vincent
    Interface: RGB20Replaceable
    Check-SHA256: 7ba3f563f39177820e2bb66f51022db9865547015b11a55a36aab2fb49b7f23c
    
    0ssI2005NfH~YbdJmlDJVGn57KDNan*4p7X50#<3f?AEL=~DoUInZVR0000m07D^JRC!cxG%a#)bxc-a
    O)XJIRykrMP%TwjN^o{`Gc9>xRc%=|K`mu>WKcynV*vmHpbvUQRh+9Pt&l(-@t+}8R@c3%)}vg<ht@H5
                       ... here we skip few hundreds of lines ...
    (u?g--(Ch+6*7N1n=+qwe6YFx|MoP&lb}4dCIbUOOjQU%P((>bMN?D*Qb$4|01E&B0MMWh0S5~J0RRgK
    000XC0szR`2LU-S0MVci0S5#C0096100000
    
    -----END RGB CONSIGNMENT-----


<aside>
    <p>Consignment id is not the same as a <a href="contract-id">contract id</a>, even for the contract consignments.
    Contract id is based on the contract genesis, while consignment id depends on other
    <a href="#which-data-consignments-do-include">consignment data</a>, like secondary asset issuance and other public
    contract operations. Thus, same contract may have multiple contract consignments, for instance corresponding
    different issues of the asset.</p>
</aside>

## Consignment ids

Consignments are identified by their ids. Like most of other ids used in RGB, consignment id is a form of URL,
starting with `rgb:csg` prefix, followed by [Baid64](baid64)-encoded SHA256 hash over all consignment data. The
last part of the URL is a mnemonic fragment made of three words, representing the id checksum. This mnemonic can
be used for simple consignment identification visually or in speech.

An example of the consignment id:<br/>`rgb:csg:3yJCUNgH-xxfXcHX-E1dfL80-kT2R4z5-BJptGHf-sEERkJI#grace-austria-current`


## How consignments are sent?

<aside>
    <p>A peer-to-peer network <dfn title="Storage and messaging network"><a href="storm">Storm</a></dfn> is being
    developed as a part of <a href="https://uviolet.net">Ultraviolet</a> effort. Once developer, it will be used as a
    default data availability network for RGB information exchange.</p>
</aside>

Consignments are sent peer-to-peer, usually from contract issuers to contract users (*contract consignments*), or
from payers to beneficiaries (*transfer consignments*). Peers are free to use any channel for the consignment, including
even messengers, e-mail, QR codes or paper. However, the most typically consignments are sent either directly, with a
use of [RGB Node](rgb-node), or via [RGB RPC](rgb-rpc) relays, which remove a requirement for both sender and receiver
to be on-line at the same time. The privacy of the data in this case may be achieved by a cryptographic encoding of the
consignments, when receiver provides the sender with its public key as a part of the [RGB invoice](rgb-invoice).


## What if I lose a consignment?

It depends. If you lose a *contract consignment*, you can easily recover it from the contract issuer, other users or
asset explorer sites like <https://rgbex.com>.

If you are a beneficiary of a payment, and you have lost a *transfer consignment* before you have accepted it into your
RGB [stash](stash), you won't be able to see or use your assets unless you recover the consignment. In such a case
consignment can be recovered by either asking the sender to provide you with it once again.

In order to prevent consignment loss it is recommended to use several relays and accept the consignment into your stash
the moment you receive it. Once the consignment is accepted, there is no need to keep its data and its loss doesn't 
prevent any threat to your assets and contract state.


## What is a typical size of the consignment?

<aside>
    <h2>Can the size of consignments be reduced?</h2>
    <p>
    Some contracts, for instance issued under <a href="rgb20">RGB20</a> standard, may use a special mechanism called
    *burn-and-replace*, where an issuer is allowed to shorten the history of the asset by burning part of its supply and
    issuing the same amount anew. This helps to reduce the growth of the transfer consignments for high-velocity assets.
    </p>
</aside>

The size of the consignment can vary; it also depends on its [type](#types-of-consignments).

For *contracts* the size is usually an order of magnitude of kilobytes; however, if a contract represents an asset with
multiple issues (like  stablecoin), its size may be measured in megabytes.

For *transfers*, the size heavily depends on the history of the contract operations included in the consignment.
Typically, the size of the consignment growth few hundred megabytes with each transfer; thus usually it is an order of
hundreds of kilobytes to tens of megabytes. However, high-velocity assets may have transfer consignments over the years
grown to several gigabytes.


## Which data consignments do include?

Consignments include the data about the RGB smart contract, including its [genesis](genesis) and complete
[operation](operation) history. Additionally, they include [schema](schema), under which the contract is issued,
interfaces, implemented by it, and [data type](type-library) and [script libraries](script-library) used by the
contract.
