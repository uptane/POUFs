Profile: 1
Title: Profile Purpose and Guidelines
Version: 1
Last-Modified: 04-04-2019
Author: Marina Moore
Status: Draft
Created: 14-03-2019

# Uptane Implementation Profiles

This repository is the authoritative source for Uptane profile.

## What is a Profile?

A guiding principle of the Uptane framework is to give each implementer as much design flexibility as possible, acknowledging that Uptane needs to run on existing, often customized, software and hardware systems. For this reason, the framework does not specify data binding formats. Yet, this means Uptane can not guarantee Interoperability. To provide a way for two or more Uptane implementations to work together, the framework employs a mechanism called a profile. A profile precisely specifies the wireline format that any implementation using it must obey. Hence, implementations that use the same profile are able to interoperate. In particular, this can be important for ECU suppliers, so that they can have a detailed specification to work with.


A profile contains all the information needed for a third party to design a compatible Uptane implementation. This includes the format and contents of all data transmitted on the wire. It functions like a layer placed over the existing Uptane specification, so certain requirements, such as filenames, file contents, and signatures, do not need to restated in the profile. The only restriction placed upon the creation of any profile is that it MUST NOT alter or violate anything defined in the Uptane specification.

## Adding profiles

Each profile is effectively under the control of its author, and its contents will not be subject to the level of scrutiny or analysis the community provides to the Uptane specification. Instead, the main role of the Uptane community in the profile process will be to provide a common repository.


The format of profiles and this document are inspired by TAPs (https://github.com/theupdateframework/taps/blob/master/tap1.md), as well as the Profiles used in TUF.

### Profile Contents

A profile should include the following sections:

* Preamble -- RFC 822 style headers containing metadata about the profile, including the profile number, a short descriptive title (limited to a maximum of 44 characters), the names, and optionally the contact info for each author, etc. The header should include:
* Profile: <number>
* Title: Profile Template
* Version:
* Last-Modified:
* Author: <list of authors' real names and optionally, email addresses>
* Status: <Draft / Accepted / Obsolete>
* Uptane Version Implemented:
* Created: <date created on, in dd-mmm-yyyy format>
* Abstract -- The abstract provides a short overview of what the profile contains. This may include any encodings used or an overarching design philosophy. If the profile has been updated, the abstract should explain what is changed in the new version.
* Design -- The design section contains a description of any design elements that differ from the Uptane specification. This section will not include the format of data, but will include all other elements of the profile. Any optional features (MAYs) of the Uptane specification used MUST be mentioned here, as well as any recommendations (SHOULDs) that are not followed. In addition, any feature added to the specification that  is needed for compatibility MUST be explained.
* Data formats -- Data formats contain details about the encoding and format of Uptane data as transmitted. The encoding should describe how data is formatted when in transit between the repositories and ECUs. Data that is not transmitted does not need to be included in a profile. Descriptions of formats should include the order of fields to allow for bitwise identical implementations. Every bit of transmitted data MUST be accounted for in the profile. This section may include common formatting used by all metadata files to avoid redundancy. At a minimum, this section will include the format for the following data:
  * Root
  * Snapshot
  * Targets
  * Delegated targets
  * Timestamp
  * Vehicle version manifest
  * ECU metadata -- Each file that is transmitted should be described. In addition to the required files, the following may be included:
    * Time server communication
    * Repository mapping metadata
    * Copyright -- Each profile MUST either be explicitly labeled as placed in the public domain (see this Profile as an example) or licensed under the [Open Publication License](https://opencontent.org/openpub/).

### Workflow

A profile may be authored by any Uptane implementer. This author is responsible for working with the Uptane community to see the profile through the acceptance process. 

In order to allow a profile to be publicly found and implemented, it should be stored on the [Uptane Profiles repository](https://github.com/uptane/profiles). A profile may be submitted to the Uptane repository using the pull request process. Pull requests will follow this workflow as the profile moves from Draft to Accepted.

#### Submitting a Draft Profile

A draft should be posted to the Uptane repository by submitting a pull request. The pull request should contain a profile in the format specified in [Profile Contents](#profile-contents). A draft profile should contain a complete description of the data transmitted, should not duplicate an existing profile, and must be technically sound. If these criteria are met, the pull request will be accepted, and the draft profile will be in the Uptane repository. If these criteria are not met, the proposal may be rejected by the Uptane maintainers.

Once a profile draft is included on the Uptane repository, it will be assigned a profile number. The profile number will be unique, but will remain the same for any subsequent minor changes. However, if the profile is updated for a new Uptane version or if there are changes that would make the profile not backwards compatible, a new profile should be created for these changes.

During or before the draft stage, the profile should be implemented. This implementation may be open or closed source. If the implementation is closed source, the author must attest that the profile can be implemented during discussion with the community.

#### Community Discussion

The author of a profile draft should solicit feedback about the profile from the Uptane community. The community should discuss whether the profile is unique and in line with Uptane requirements. This discussion can happen over the Uptane Forum or through issues on the Uptane repository. The draft should be updated, based on the community feedback, through pull requests to the profile.

#### Accepting Profiles

Once an author has a draft profile and has solicited community feedback, the author may submit a pull request to update the profile’s status to Accepted. If the author has followed the procedure and addressed any community concerns, the pull request will be accepted and the profile will be finalized in the Uptane repository.

No major changes may be made to an accepted profile.

#### Updating a Profile

If a non-trivial change is made to an accepted profile, a new profile should be created for this change following the same process as the original profile. This new profile might fix a bug, add a feature, or conform to a new version of the Uptane specification. The updated profile should refer to the previous version of the profile in its abstract. The abstract should explain why the profile is being updated and which sections have changed. This will allow any implementer who used the previous version of the profile to update their implementation to the new profile.

If the update changes eliminate the need for the old profile, the old profile may be marked as Obsolete.

## Using Profiles

When an Uptane implementation uses a profile, it should list the profile number (or numbers) in its documentation. If the implementation is updated to a new profile version, the profile number should also be updated in the documentation.