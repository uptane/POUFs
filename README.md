POUF: 1
Title: POUF Purpose and Guidelines
Version: 1
Last-Modified: 10-05-2019
Author: Marina Moore
Status: Draft
Created: 14-03-2019

# Uptane Implementation POUFs

This repository is the authoritative source for Uptane POUFs.

## What is a POUF?

A guiding principle of the Uptane framework is to give each implementer as much design flexibility as possible, acknowledging that Uptane needs to run on existing, often customized, software and hardware systems. For this reason, the framework does not specify data binding formats. Yet, this means Uptane can not guarantee Interoperability. To provide a way for two or more Uptane implementations to work together, the framework employs a mechanism to describe the protocol, operations, usage, and formats (POUF). A POUF precisely specifies the wireline format that any implementation using it must obey. Hence, implementations that use the same POUF are able to interoperate. In particular, this can be important for ECU suppliers, so that they can have a detailed specification to work with.


A POUF contains all the information needed for a third party to design a compatible Uptane implementation. This includes the protocol and contents of all data transmitted on the wire as well as design choices that impact the functionality of the system. It functions like a layer placed over the existing Uptane specification, so certain requirements, such as filenames, file contents, and signatures, do not need to restated in the POUF. The only restriction placed upon the creation of any POUF is that it MUST NOT alter or violate anything defined in the Uptane specification.

## Adding POUFs

Each POUF is effectively under the control of its author, and its contents will not be subject to the level of scrutiny or analysis the community provides to the Uptane specification. Instead, the main role of the Uptane community in the POUF process will be to provide a common repository.


The format of POUFs and this document are inspired by TAPs (https://github.com/theupdateframework/taps/blob/master/tap1.md), as well as the POUFs used in TUF.

### POUF Contents

A POUF should include the following sections:

* Preamble -- RFC 822 style headers containing metadata about the POUF, including the POUF number, a short descriptive title (limited to a maximum of 44 characters), the names, and optionally the contact info for each author, etc. The header should include:
* POUF: <number>
* Title:
* Version:
* Last-Modified:
* Author: <list of authors' real names and optionally, email addresses>
* Status: <Draft / Accepted / Obsolete>
* Uptane Version Implemented:
* Created: <date created on, in dd-mmm-yyyy format>
* Abstract -- The abstract provides a short overview of what the POUF contains. This may include any encodings used or an overarching design philosophy. If the POUF has been updated, the abstract should explain what is changed in the new version.
* Protocol -- The protocol used to transmit data should be described here. If relevant, the version of the protocol and any customizations should be explained so that any implementor will have a bitwise identical use of the protocol.
* Operations -- The operations section contains a description of any design elements that differ from the Uptane specification. This section will not include the format of data, but will include all other elements of the POUF. Any optional features (MAYs) of the Uptane specification used MUST be mentioned here, as well as any recommendations (SHOULDs) that are not followed. In addition, any feature added to the specification that is needed for compatibility MUST be explained.
* Formats -- Data formats contain details about the encoding and format of Uptane data as transmitted. The encoding should describe how data is formatted when in transit between the repositories and ECUs. Data that is not transmitted does not need to be included in a POUF. Descriptions of formats should include the order of fields to allow for bitwise identical implementations. Every bit of transmitted data MUST be accounted for in the POUF. This section may include common formatting used by all metadata files to avoid redundancy. At a minimum, this section will include the format for the following data, including all fields required by the Uptane specification:
  * Root
  * Snapshot
  * Targets
  * Delegated targets
  * Timestamp
  * Vehicle version manifest
  * ECU metadata -- Each file that is transmitted should be described. In addition to the required files, the following may be included:
    * Time server communication
    * Repository mapping metadata
* Usage -- The usage section should contain an overview of how data is handled in the POUF. To do so, it will include the following tables:
  * Message Handler Table -- This table will include all messages that will be transmitted by the implementation. Each entry should include at least the sender, receiver, data (including signatures), and the expected response.
  * Data Table -- All data stored on each Uptane entity should be described in this table. This includes which keys are stored on each entity as well as any other required data. At a minimum, data stored on Primary ECUs, Secondary ECUs, the director repository, and the image repository must be described.
* Copyright -- Each POUF MUST either be explicitly labeled as placed in the public domain or licensed under the [Open Publication License](https://opencontent.org/openpub/).

### Workflow

A POUF may be authored by any Uptane implementer. This author is responsible for working with the Uptane community to see the POUF through the acceptance process.

In order to allow a POUF to be publicly found and implemented, it should be stored on the [Uptane POUF repository](https://github.com/uptane/profiles). A POUF may be submitted to the Uptane repository using the pull request process. Pull requests will follow this workflow as the POUF moves from Draft to Accepted.

#### Submitting a Draft POUF

A draft should be posted to the Uptane repository by submitting a pull request. The pull request should contain a POUF in the format specified in [POUF Contents](#pouf-contents). A draft POUF should contain a complete description of the data transmitted, should not duplicate an existing POUF, and must be technically sound. If these criteria are met, the pull request will be accepted, and the draft POUF will be in the Uptane repository. If these criteria are not met, the proposal may be rejected by the Uptane maintainers.

Once a POUF draft is included on the Uptane repository, it will be assigned a POUF number. The POUF number will be unique, but will remain the same for any subsequent minor changes. However, if the POUF is updated for a new Uptane version or if there are changes that would make the POUF not backwards compatible, a new POUF should be created for these changes.

During or before the draft stage, the POUF should be implemented. This implementation may be open or closed source. If the implementation is closed source, the author must attest that the POUF can be implemented during discussion with the community.

#### Community Discussion

The author of a POUF draft should solicit feedback about the POUF from the Uptane community. The community should discuss whether the POUF is unique and in line with Uptane requirements. This discussion can happen over the Uptane Forum or through issues on the Uptane repository. The draft should be updated, based on the community feedback, through pull requests to the POUF.

#### Accepting POUFs

Once an author has a draft POUF and has solicited community feedback, the author may submit a pull request to update the POUF’s status to Accepted. If the author has followed the procedure and addressed any community concerns, the pull request will be accepted and the POUF will be finalized in the Uptane repository.

No major changes may be made to an accepted POUF.

#### Updating a POUF

If a non-trivial change is made to an accepted POUF, a new POUF should be created for this change following the same process as the original POUF. This new POUF might fix a bug, add a feature, or conform to a new version of the Uptane specification. The updated POUF should refer to the previous version of the POUF in its abstract. The abstract should explain why the POUF is being updated and which sections have changed. This will allow any implementer who used the previous version of the POUF to update their implementation to the new POUF.

If the update changes eliminate the need for the old POUF, the old POUF may be marked as Obsolete.

## Using POUFs

When an Uptane implementation uses a POUF, it should list the POUF number (or numbers) in its documentation. If the implementation is updated to a new POUF version, the POUF number should also be updated in the documentation.
