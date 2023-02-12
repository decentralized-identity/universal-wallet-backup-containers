# Standard Wallet Backup Container


## Session Convener: (Telegram)Sam Curren & Lance Bird (RootsID)  
## Notes-taker(s): Scott Phillips (Trinsic), Dmitri Zagidulin (MIT/DCC)

Tags / links to resources / technology discussed, related to this session: 


Discussion notes, key understandings, outstanding questions, observations, and, if appropriate to this discussion: action items, next steps: 


### Intro
Starting with: Orie's Universal Wallet Interop Spec (Wallet Export Container)
Conversation has progressed since then https://w3c-ccg.github.io/universal-wallet-interop-spec/#locked-wallet 


Where should the spec live?? 
DIF Wallet Security WG 


#### Bundle
Regardless, of encryption envelope, what are we actually exporting? (What goes into the bundle?)
If we're using .tar archive, we can put multiple files into the export. For example, see Open Office File Format. (OpenXML Specification)


#### Compression

TBD


#### Encryption
Out of the box Zip encryption - not good
Reasonable start: .tag.gz archives
see https://github.com/w3c-ccg/universal-wallet-interop-spec/issues/108 
What are we zipping? That is, what is the cryptographic envelope?
Recommend: JWE
Issue: password(/passphrase)-encrypt it or not?
if yes, you should use Argon2 (instead of PBKDF2 or SCrypt) "key stretching algorithm" (which takes a password (which you're hopefully storing in a password manager) and iterates/hashes it a bunch, and creates a symmetric key suitable for encryption). 
Ideally, we want the key mgmt steps to mesh with the human instructions (see Tilly hat "put your warranty into the top drawer on the left)).

Software doesn't do it as much with the rise of cloud storage, but backup and restore is still valuable
We need to have a good technical solution, but it can't bother the user or it won't be adopted.
Jobs For the Future is focusing on wallet interoperability for backup and restore
Backup is about data structures, and storage of the private keys
When I think about all the data in a wallet, I have 3 things
Backup should be bundled
Should be compressed (convenience and storage)
Should be encrypted for security
I would love a nerd to be able to take this, and with the encryption key: decrypt, uncompress, unbundle with standard tooling
It would be nice if encrypted zip files were worth it, but they aren't.
Common tool usage would be useful for nerds, but not for normal people.
.tar.gz would be a good option, but there isn't a good encryption.
Encrypt after compression, since good encryption won't have repeating information (and thus won't compress at all)
There are non-trivial interactions between encryption and differential backups
If you can avoid pass-key encryption, and rely on other key management, that's ideal.
The weakest link is the user.
In the future, it would be ideal to have MIM key-splitting (eg to shard the key out to the old lady's kids(
In the short term, maybe generate a passphrase, print it out, and store it in the fireproof safe.
Encrypt notes:
AES GCM256 (#108 UWspec)
Argon2 - key stretching
If you don't immediately share the key via DIDs, you still have the problem of what key can people remember.
More focus on thekeys being part of the process. (ex, tilly hat warranty in bottom left dresser drawer)
Better to allow agility and then tell people to not use certain options.
Use JWE: JSON Web Encryption as the envelope

Use Argon2 instead of PBKDF2



What's the process of involving Ubikey in this workflow?
Punt on this, let's talk to ubikey people.
Standard practice is generate symmetric key, encrypt with HSM (Ubikey). Then encrypt the bulk data with the symmetric key in software
The other option that will be valuable for muggles:
Store in the device key-store.
Rather not directly involve biometrics
Bundle Contents
Manifest file with metadata about what is in the container
You can have more forward cmpatibility, and more ability to evolve the spec quickly.
Allow for continuation files?
Identify standard ways of designating special files (dids, vcs, etc)
CESR: Composable Event Streaming Representation
Let's just assume JSON for now
How to handle files we don't understand - custom file information
Office OpenXML spec (_rels.xml links to other formats)
We should use text-based, human-readable format so that it is at least partially self-documenting

#### Open Wallet Foundation is only doing implementations, not specs and standards.
