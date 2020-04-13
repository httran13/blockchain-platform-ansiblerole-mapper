# Overview

This playbook utilizes [blockchain_platform_manager role](https://galaxy.ansible.com/ibm/blockchain_platform_manager) by removing the redundant tasks
of manually modifying the playbook in various variables for BPM-role. You can now specify from a single json the values 
to define the topology of your network and the playbook will map the values appropiately for BPM-role.

You will want to use this for an extremely fast setup to bootstrap your orgs, channels and chaincode. Do not use this
if you require specifics configurations. Current assumptions are made with this initial setup and future
plans are in place to be able to adjust some of these parameters.

## Assumptions

Core assumptions from BPM-role will exists. For this playbook, it will assume:

 - Naming standards such as \<orgName>MSP, \<orgName>.com, \<orgName>Peer\<index>
 - All peers of an org will be committers, endorsers, and only peer1 will be anchor
 - All org's gateways will have visibility to all peers on the network
 - All org will join all channels defined
 - All chaincode will be deployed to all channels defined
 - All secrets are statically defined in templates( you'll be able to supply your own next release )
 - Chaincode CDS file is in the format \<ccName>@\<ccVersion>.cds
 - all wallets, gateways, nodes output from BPM is in the format nodes/\<orgName>, wallets/\<orgName>, gateways/\<orgName>
 - All organizations gateways will be created
 - endorsement policy of contract uses OneOf(1, ...*ALL ORGS MEMEBERS*)
 
# Dependencies and Installation

[blockchain_platform_manager role](https://galaxy.ansible.com/ibm/blockchain_platform_manager) installation and dependencies required

# Var Configuration Properties

### Orgs

- name - Name of organization
- nodeCount - number of nodes to deploy for the organization, must be >1
- tls - tls true/false setting for BPM-role
- dockerPortPrefix - for docker deployment types, the unique port prefix to use
- type - type of organization

### Chans

- name - Name of channel

### Contracts:

- name - Name of the chaincode
- version - Version of the chaincode
- location - directory where the chaincode lives locally