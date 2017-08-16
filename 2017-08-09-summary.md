# August 9th, 2017 Meeting Summary

## Main topics

- Farmer payout incentives
- Users flooding network with data and deleting it

## Detailed meeting logs

https://community.storj.io/channel/dev?msg=YvpDGcFxNbJa89f6a

## Farmer payout incentives

### Background

A legacy system has been in place since early beta testing for sending payments to farmers with once a month payouts. Data is collected throughout the month and used to generate a payout sheet, which is reviewed and then payments are sent in batch. This was originally using the SJCX on the bitcoin block chain with counterparty. Over the last several months this has changed to use the Ethereum block chain and the STORJ ERC20 token. There has been several models used to try to incentivize new nodes joining the network, and payouts have been heavily subsidized.

### Comments

meije was concerned on how the network is going to stop people from downloading from their own node and making a huge profit, and that if the farmer gets more than the renter pays he will continue to do so, as seen with this last months top paid farmer. braydonf addressed backup.pete issue mentioned earlier: by better keeping track of when a farmer goes offline from the payouts perspective should help revolve issues with farmers deleting data they know is not their own. braydonf also mentioned that there are several accounting issues isn't very good, and has several holes in it, specifically around contract lengths and mirroring, and issues with using exchange reports as the source data. backup.pete suggested preventing downloading where the source ip and destination are the same, however knowing that you have the shards in your possession is the difficult part. moby mentioned that this should be helped with SIP6 because it will be a lot harder because where the data is stored isn't based on the shard hash, and that it won't be easy to tell that a particular shard is going to end up on a particular farmer. braydonf mentioned that better detecting deleted data will also help by having a audit performed with the current PING that is used to determine if a farmer is offline. meije said the solution here is to not pay farmers more than the renters pay. backup.pete brought up issues with the model in which farmers with a lot of data are paid more than farmers with less data, as it creates an incentive to scrub and start over. braydonf mentioned that this is opposite of what's desired. meije mentioned that having better feedback and less first of the month payout surprises from deleting all data.

### Action items

- Keep better accounting of farmer storage events https://github.com/Storj/bridge/issues/481
- Improve the frequency in which calculations are made, and provide an API to see estimations https://github.com/Storj/bridge/issues/432
- Have more economically sound payouts (not paying more than renters are paying)
- Perform a random shard audit during farmer up-time monitoring to verify that shards have not been deleted https://github.com/Storj/bridge/issues/480

## Users flooding network with data and deleting it

### Background

Many data storage services do not charge for users for the bandwidth of uploading data and then charged on the download of data and the length the data is stored instead. The accounting for storage events to a bridge does not track upload bandwidth and only tracks when a complete file is stored, the length of time it's stored, and the bandwidth of downloading the file.

### Comments

braydonf mentioned that rate limiting by upload bytes should help with this issue. backup.pete thought this was a bad idea, and that it should be as fast as possible. blackduck said that would keep real renters away. meije then mentioned that faster audits to detect deleted data and to signal farmers to delete the shards could help, and that rate limiting would be a problem. braydonf said that some of the rate limiting is temporary until things can scale. blackduck also said that deletion of files should be passed to farmers, and nothing else is needed.

### Action items

- Have the bridge notify farmers when files are deleted so that actual data is deleted, related issue: https://github.com/Storj/bridge/issues/478

## Participants

- alexander
- backup.pete
- blackduck
- braydonf
- khgkdhgf
- meije
- moby
