# August 2nd, 2017 Meeting Summary

## Main topics:

- Farmer reputation and contact discovery
- Standard definition for file system use as in FileZilla

## Detailed meeting logs

## Farmer reputation and contact discovery

### Background

Currently new farmers are discovered by having farmers subscribe to topics via quasar publish-subscribe over kademlia network. Contracts are published to three farmers from a renter that are interested in the topic and this repeats up to six hops. New farmers in the network can then see these contracts and send offers to renters, in which the renter can then use to send data on the farmer. In [SIP6](https://github.com/Storj/sips/blob/master/sip-0006.md) the model shifts to have have renters keep a database of contacts, and to communicate directly to farmers. Renters will need to discover farmers asynchronously to negotiating contracts, this is not yet detailed in SIP6. There are several ways that this can be done, a few of which: A) Contacts are built using the existing routing tables, and limited by the total number of renters run. B) Reverse the publish-subscribe to have renters subscribe to topics. C) Have farmers configure to specific renters and contact directly, already the case with "trusted key" configuration on farmers. There are a few vulnerabilities that should be considered, including Sybil and Eclipse attacks.

### Comments

shawn mentioned SIP2 as mitigation against Sybil attacks from farmers. braydonf brought up that having to have STORJ tokens to earn STORJ tokens could be a barrier to entry, and shawn and meije agreed, stating it could create UX problems. braydonf then proposed using a proof-of-work challenge for new farmers to provide similar benefit, where the difficulty would adjust based on the current number of contacts being added to a renter, other metrics after the initial contact would then be established. greenlock mentioned that many people run storjshare on existing mining rigs, and was concerned that it may affect the reliability. It was later cleared up that it would be a one time challenge. Many agreed that this would help, and meije commented that it could also be a quick verification of CPU capacity to run a node, a micro strees test. littleskunk mentioned that he doesn't think an additional challenge is needed, as there is already the data to detect slow farmers, and the bandwidth is a better metric. littleskunk was also concerned about the performance difference between a pi3 (Raspberry Pi) and more power servers, and that using PoW (proof-of-work) could discourage slower CPUs from joining the network. mattdawgak was not concerned. braydonf mentioned that there could be alternatives, using STORJ tokens (as detailed in SIP2), and using Ethereum contract to register farmers. Other concerns about using many nodeIDs on a single IP address were mentioned, however IP addresses are fairly inexpensive now with IPv6.

### Action items

- Implement and test ideas discussed for contact discovery

## Standard definition for file system use as in FileZilla

### Background

The FileZilla integration with Storj introduces a way to have directory support on top of a bucket and bucket entry based system of storing files. Initial testing has shown that when a bucket has many entries the performance degrades as it's possible to list everything in the bucket from the API initially, thus directories with deeply nested structures are not well supported.

### Comments

kaloyan.raev asked about the folder support in the FileZilla integration, and if there should be a spec around it for others to implement. braydonf mentioned that it's implemented by having `/` in bucket entry names. kaloyan.raev mentioned that there has been discussion on the topic at https://community.storj.io/channel/dev?msg=xxKgrC5HPwba2koF and that implementing all on the client side is a bit complicated.

### Action items

- Open issue for SIP to address nested directory support

## Participants

- alexey
- braydonf
- bryanchriswhite
- greenlock
- heunland
- kaloyan.raev
- knowledge
- littleskunk
- mattdawgak
- meije
- moby
- shawn
