# everme

Everme is a private, censorship resistant and perpetually hosted linktree alternative (and in the future personal webpage builder) for everyone (but especially for activists).
But what does this mean exactly?

1. Private: Tracking free, optionally sponsored (and hence anonymous) payments for activists, whistleblowers, journalists, etc.
2. Censorship resistant: Page is only deletable by the owner, or can even be chosen to be entirely undeletable. Made possible by decentralized, on-chain hosting.
3. Perpetually hosted: Pay a one-time fee to host your page forever and pay a little for any changes you want to make.

## Features

-   censorship resistant
-   optionally private (through third-person funding)
-   perpetually hosted (one-time fee, always online)
-   creative page builder (future feature, possibly cooperation with mmm.page?)
-   optionally the entire page or just some contents can be encryption protected
-   document, audio or video uploads to crypto networks like irys, aarweave, filecoin or livepeer.
-   e2e encrypted, private analytics

## Economic model / payments

Everme applies usage based billing and collects the (MAS) value locked in pages that are being taken down.
The fees are comprised of a (one-time) page registry fee, fees associated to content updates and the costs of running a massa provider.

There is also the option to add a small, monthly billed amount that is donated to open source and sustainability related causes.
Each user can choose from a list of causes which they want to support and whether that should be listed on their everme page.

Note that the everme page will continue to be hosted, even if a user decides to cancel everme usage based billing. In that case however, a user has to run their own provider or use another, public provider. Should they want to change the page contents, they have to continue billing again.

## Sponsoring / Activism support

When offering private webservices, the biggest threat to privacy is payments. Crypto onramps require the offering company to KYC the customer, thereby forcing the customer to (partially) disclose their identities. Everme allows this by allowing anyone to pick public funding as a payment method for their page. This then publishes their everme page temporarily (for e.g. one month) on everme infrastructure, with a fundraising notice on the page. Any user that visits this page can then pick to fund the everme page fee (either with MAS directly or through fiat). If this user has a everme page themselves, they can choose to display the activists they funded in return.

Funding can be one-time or continuous, where a user also chooses to fund the future changes an activist makes to their page. They can also set up limits to the funding.

## Architecture

Everme consists of the following puzzle pieces:

-   client-side only frontend
-   betterauth for authentication, with massa plugin for alternative auth through massa station and lit protocol plugin for embedded wallet generation.
-   polar for subscription management
-   massa chain with forked deweb smart contract
-   server side automations (e.g. temporarily publish pages, take down pages)

### Authentication

We want to offer both traditional means of authentication (email, passkeys etc.) and web3 authentication (massa station).
That is why we also build a plugin for betterauth to authenticate through massa station.

If not authenticating through massa station but through traditional (web2) means, we set up a wallet for the users in the background.
This can be done by minting a programmable keypair (PKP) with lit protocol that acts as a massa wallet and can be retrieved by proving a login method (webauthn, passkey, social login).

### Smart Contract

The smart contract is a fork of the official deweb smart contract, as we want to make sure the funds released from a page flow back to the official everme wallet.

## Roadmap

**1. Basic functionality MVP**

A sellable product that allows users to create a basic everme

-   Only the default everme page design
-   create, update, delete everme pages, with the following possible elements:
    -   image
    -   headline
    -   description
    -   basic socials (whatsapp, signal, TG, X, etc.)
    -   links
-   Register, connect, change a massa domain
-   authenticate with passkey, email or massa station
-   if not authenticated with massa station, autogenerates embedded massa wallet
-   payment method management through polar, manage usage based billing
-   view invoices
-   manage authentication methods

Payment is submitted through polar in fiat and then accredited to the user within the everme massa smart contract.

## Money laundering protection

Everme is not a platform for money laundering and tries to make abuse as unattractive as possible.
That is why it is not possible for a user to recollect the crypto once spent by taking a page down.
The released funds flow back to the official everme wallet, hence making it a useless means for money laundering.

## KYC requirements & Anonymity

Due to the design of everme described in the money laundering section, one can argue that we are not onramping even if we accept fiat payments on everme and in return create a page on chain. That is because the value from the page cannot be traded further.

We don't need to collect personal information for tax requirements when they pay for our product (only for B2C sales), as e.g. posteo demonstrates That implies that we will treat each client as a customer, not a business.

But even if we don't need to collect data about our users, a fiat payment still gives us some insight (e.g. paypal handle). That's why everme offers the option for users to create a "fund me" link, through which another user (could be both on the platform or foreign) pays the costs for the page creation.

It is hence possible to interact with everme at various levels of anonymity by using e.g. passkeys for auth and by using a funding request to get funded by other users.

## Privacy

Everme is a client-side only web application, accompanied by a set of API's to interact with for deploying self-built websites. Authentication and payment KYC obviously stores information about the user. For ultimate privacy it is recommended to use a VPN like nym to shield your IP address from recording (even though we dont record it).
Privacy is verifiable by our source available MIT license: You can view the everme source code and run it on your own device, directly from source.
