Wallet Containers
==================

**Specification Status:** Strawman

**Latest Draft:**
  [https://identity.foundation/wallet-containers](https://identity.foundation/wallet-containers)

Editors:
~ [Sam Curren](https://www.linkedin.com/in/samcurren)

Participate:
~ [GitHub repo](https://github.com/decentralized-identity/wallet-containers)
~ [File a bug](https://github.com/decentralized-identity/wallet-containers/issues)
~ [Commit history](https://github.com/decentralized-identity/wallet-containers/commits/main)

------------------------------------

## Abstract

This spec details a Universal Container for Wallet Backups, in a way that promotes common data formats and also allows for wallet specific data. This enables both backup and restore flows for a single wallet, and also migration from one wallet to another by backing up from one and restoring to the other. Defining a common structure will allow us to 

This work includes the specification of data combination, compression, and encryption, as well as metadata structures and overall backup structure. We recognize that not all information should be backed up and restored to another wallet. This work defines the structure, and the work about what to back up and in what form is left to other work.

This work does not include syncronization between multiple wallets owned by the same entity.


## Getting Started


**Usage**

## Table of Contents


## Term References

### Definition Lists


## Considerations
- Desirable to be able to use stream processing libraries for the creation and consumption of the backup file.
- Allow for both standards based and application specific data formats


## Encryption
- The backup should use an independent key for the backup files - it is recommended that the key be used for subsequent backups to ease key management. See Key Recovery section.
- Recommendation: JWE
- Encrypt after compression, as good encryption should have no repeating information.
- AES GCM256 (#108 UWspec)
- Argon2 - key stretching


## Key Recovery
- It is important for users to be able to use their encrypted backup file, and for this they will need the decryption key.
- This spec outlines the flow for presenting the decryption key to the user, and receiving the key back for processing of the application.
- A good example here is the warrenty that comes with Tilley hats: "Put this warrenty in the top drawer of your dresser on the left side, so we can remind you where it is."


## Internal Structure
- Internal Manifest file that records the contents of the rest of the file, including which files are standard formats, and which are application specific.
- We should use text-based, human-readable format so that it is at least partially self-documenting


## Compression
- gzipped tar file
- this allows for the bundling together of a variety of different files, not all of the same format.
- Example: Open Office files, are really just a zip file with a different extension. Inside are a collection of the resource files necessary to create the subject file.
- to the user, this is just a single file, and users don't need to be aware of the internals.

## Storage / Export
- This spec can have some recommendations, but otherwise out of scope.
- Handing the file to the OS file storage, and then using mobile or otherwise regular backups is a good idea.
- Systems should be capable of handing a backup file directly to the user or accepting one from them to enable portability or otherwise manually handled backup and restore flows.

### Default References


### Normative References


### Informative References

- [Universal Wallet Spec](https://w3c-ccg.github.io/universal-wallet-interop-spec/#locked-wallet)
- [IIW35 Session Notes - Dmitri and Scott](https://docs.google.com/document/d/1XkhDU-vD3urmKwCPZt-G9Vnuu3ZcZ56LlRmRUdUvSXc/edit)
- [IIW35 Session Notes - Lance](https://hackmd.io/@_NzO6WTHQNqQ7DdYbcc2RQ/rkubge4Is)
- [Aries Backup and Restore Notes](https://hackmd.io/eJbWrh7BSiaJXkP-p0Q5mg)


[[spec-inform]]
