* POUF:
* Title:
* Version:
* Last-Modified:
* Author:
* Status:
* Uptane Version Implemented:
* Created:

# Abstract

# Protocols

This section describes the protocols used to transmit data in the implementation. At a minimuc, this should answer the following questions:

What encoding format is used? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#meta_structures)

Are any files hosted? What protocol is used to transmit hosted files?

## Message Handler Table

What messages are sent by Uptane entities?


| Request | Sender | Receiver | Data | Response | Specification Reference |
| ------- | ------ | -------- | ---- | -------- | ----------------------- |


# Operations
This section includes descriptions of optional features from the standard, as
well as any additional features supported by the implementation. At a minimum,
this should include the following:

Which ECU is used as the primary ECU?
* The primary ECU MAY be the same ECU that communicates with the server (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#rfc.section.5).

What delegation features are supported (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#targets_role_delegations)?
* How does the implementation get a secure source of time?
* Are custom delegated targets roles supported?
* Are terminating delegations supported?
* Are multi-role delegations (TAP 3) supported?

What value is used for the public key identifier? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#common_metadata)

Does the root file support mapping roles to urls (TAP 5)? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#root_meta)

Is there any additional or custom metadata included in targets metadata? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#targets_meta, https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#custom-metadata-about-images)

How are the filenames for delegations listed? Are wildcards supported? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#delegations_meta)

Does snapshot include the root filename and version number? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#snapshot_meta)

How many repositories does the implementation use? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#repo_mapping_meta)

How does the implementation specify repository mapping metadata? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#repo_mapping_meta)

How do ECUs securely access the current time? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#server-repository-implementation-requirements)

Is the image repository interface public? Does it require authentication? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#image-repository)

Is the director repository interface public? Does it support encryption? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#director_repository)

How does the director repository identify a vehicle? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#directing-installation-of-images-on-vehicles)

Does the director repository make any additional checks? What does it do it a check fails? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#directing-installation-of-images-on-vehicles)

What additional data about ECUs and vehicles is stored in the inventory database? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#inventory_db_)

Is the ECU key symmetric? Is the same key used for encryption and signing? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#build-time-prerequisite-requirements-for-ecus)

Does the implementation support sending diffs of the vehicle version manifest? If so, how can the director request the full manifest? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#construct_manifest_primary)

Do any secondaries not have storage? If so, how will they request images from the primary and should they backup their previous working image? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#send_images_primary)

What are the preconditions for installing an image? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#install_image)

Does the primary write version reports to disk? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#create_version_report)

Do full verification secondaries check that all metadata from the director and image repositories match? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#full_verification)

Does the primary ECU check that the targets metadata from the director repository only contains ECU ids present on the vehicle? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#full_verification)

Does the root, snapshot, timestamp, or targets verification process differ from the suggestions in the standard? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#check_root)

# Usage

What filesystem is used by the image repository? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#image-repository)

What filesystem is used by the director repository? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#director_repository)

What database system is used for the inventory database? (https://uptane.github.io/papers/ieee-isto-6100.1.0.0.uptane-standard.html#inventory_db)

How are keys managed?

What steps are taken to initialize the image and directory repositories?

Are ECUs registered with a repository? How does this work?

## Data Table

| Location | Data |
| -------- | ---- |
|Primary ECU | |
| Full verification secondary ECU |  |
| Partial verification secondary ECU |  |
| Director Repository | |
| Image Repository | |
| ... | |

# Formats
This section details the data definitions used for files transmitted as part of Uptane. This should include at least the following:
* General metadata format (including signature header)
* Root metadata
* Snapshot metadata
* Timestamp metadata
* Targets metadata, including any custom fields
* Delegated targets metadata, if different than targets metadata
* ECU metadata and vehicle version manifest
