# Aries RFC 0324: Request Credential Protocol 1.0
- Authors: Derek Trider (SecureKey Technologies)
- Status: [PROPOSED](/README.md#proposed)
- Since: 2019-11-22
- Status Note: Supplements the [issue-credential](../0036-issue-credential/README.md) protocol. Implementation is being explored by SecureKey.
- Start Date: 2019-11-21
- Tags: feature, protocol

## Summary

Specifies how an agent can obtain a credential from an issuer by starting the exchange with a [request-credential](../0036-issue-credential/README.md#request-credential) message.

## Motivation

The [issue-credential](../0036-issue-credential/README.md) protocol states that credential issuance can begin with the holder sending a request-credential message. However, the details of how this should work are not present in the RFC. It generally seems to assume that Hyperledger Indy is being used, which doesn't support starting from a [request-credential](../0036-issue-credential/README.md#request-credential) message. For non-Indy based implementations, being able to start from a [request-credential](../0036-issue-credential/README.md#request-credential) message is valuable for certain situations.

The expected outcome of implementing this flow is that, for situations where no negotiation is required, a holder should be able to get a credential from an issuer without requiring the [propose-credential](../0036-issue-credential/README.md#propose-credential) or [offer-credential](../0036-issue-credential/README.md#offer-credential) steps. This RFC fills in that missing piece of the [issue-credential](../0036-issue-credential/README.md) protocol.

## Tutorial

Since this RFC supplements the [issue-credential](../0036-issue-credential/README.md) protocol, start there and read until you reach the end of the [request-credential](../0036-issue-credential/README.md#request-credential) section.

This RFC adds some fields to the [request-credential](../0036-issue-credential/README.md#request-credential) schema. These fields are in addition to the existing fields defined in [issue-credential](../0036-issue-credential/README.md) RFC.  Note that these fields match fields that exist in the [propose-credential](../0036-issue-credential/README.md#propose-credential) schema.

The new fields are:

* `credential_proposal` -- an optional JSON-LD object that represents the credential data that Prover wants to receive. It matches the schema of [Credential Preview](../0036-issue-credential/README.md#preview-credential).
* `schema_id` -- optional filter to request credential based on a particular Schema. This might be helpful when requesting a version 1 passport instead of a version 2 passport, for example.
* `cred_def_id` -- optional filter to request credential based on a particular Credential Definition. This might be helpful when requesting a commercial driver's license instead of an ordinary driver's license, for example.

The usage of these fields will depend on whether this message is intended to start the [issue-credential](../0036-issue-credential/README.md) protocol, or whether it's in response to an [offer-credential](../0036-issue-credential/README.md#offer-credential) message, both of which are allowable flows:

* If this message is intended to start the protocol: The credential_proposal, schema_id and cred_def_id fields should be used in the same way as they are for a propose-credential message.
* If this message is in response to an offer-credential message: The credential_proposal, schema_id and cred_def_id fields should not be used.

## Reference

This protocol supplements [Aries RFC 0036: Issue Credential Protocol 1.0](../0036-issue-credential/README.md).

## Drawbacks

The additional fields that this RFC adds to the [request-credential](../0036-issue-credential/README.md#request-credential) schema are the same as what's already in [propose-credential](../0036-issue-credential/README.md#propose-credential). This could be considered a violation of the [DRY principle](https://en.wikipedia.org/wiki/Don't_repeat_yourself).

## Rationale and alternatives

Existing implementations of the [issue-credential](../0036-issue-credential/README.md) RFC that use Hyperledger Indy (which requires a [request-credential](../0036-issue-credential/README.md#request-credential) message to be preceded by an [offer-credential](../0036-issue-credential/README.md#offer-credential) message) will continue to work alongside this RFC. No changes to those existing implementations will be required.

By having this protocol as separate from the existing [issue-credential](../0036-issue-credential/README.md) RFC, implementers of the [issue-credential](../0036-issue-credential/README.md) protocol are free to choose how exactly to support the "holder begins with a request" scenario. This RFC is just one possible solution. There may be other ways that are more applicable to different use cases.

## Prior art

The fields used in this proposal are the same as in the [propose-credential](../0036-issue-credential/README.md#propose-credential) schema, which is defined in [Aries RFC 0036](../0036-issue-credential/README.md).

## Unresolved questions

Would it be better if this RFC was merged into [Aries RFC 0036: Issue Credential Protocol 1.0](../0036-issue-credential/README.md), instead of being its own RFC?
   
## Implementations

The following lists the implementations (if any) of this RFC. Please do a pull request to add your implementation. If the implementation is open source, include a link to the repo or to the implementation within the repo. Please be consistent in the "Name" field so that a mechanical processing of the RFCs can generate a list of all RFCs supported by an Aries implementation.

Name / Link | Implementation Notes
--- | ---
 |  |
