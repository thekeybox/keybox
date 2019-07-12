# KEYBOX  WHITE PAPER

Valuable enterprise data is vulnerable to hacks, whether stored in the Cloud or on-premise. Data at rest and data transfers between organisations increase the risk of breaches. Key management and recovery remain an issue and current storage technologies rarely comply with data regulations and privacy laws (e.g. GDPR). Keybox addresses all of these issues.

>With data fragmentation, Keybox sets the new standard in data management best practice, offering enterprises of all sizes data security, control and traceability

## SECURING DATA 


Keybox stores data in encrypted fragments across multiple, decentralised private or public nodes, such that penetrating any node cannot yield any decipherable information. Authorised users recombine data from fragments using smart contract technology.

### Tried and tested security algorithms

Keybox uses MIT’s Shamir Secret Sharing to fragment data together with smart contracts to control and monitor data access

### Permissioned blockchain

Keybox leverages a proven, permissioned Blockchain, which has several unique advantages over other distributed ledger protocols, including territoriality and scalability

### Strong focus on usability

The Keybox API and SDK offer enterprises a seamless experience in managing their data at rest or in transit, within their existing data infrastructure.

## How Keybox work

 
Keybox leverages some unique features of Activeledger, for example, Activity Streaming. Activeledger is able to create consensus even being in different networks if managed correctly. This is how our virtual networks for Keybox will operate. When creating a new activity stream to hold a secure data record, we can use deterministic stream names to ensure on each network that the new activity stream has the same id. Inside this activity stream, we will have the metadata such as ownership details. Once we have the activity stream on the 4** networks, we can either create a tunnel or data passthrough*** from the connected client to append data to the activity stream. This appended data will be 1 of the 4 parts of the secret sharing algorithm. Now we have the secret parts securely separated from each other and Keybox becomes the controller (but not the owner, or access to the data).

When it comes to data retrieval each network would validate the request to make sure they should release their data. This releasing of data would generate a token allowing the requester direct access (again via tunnel or passthrough***) to download the parts for them to combine and retrieve the original data for their consumption. We would still enforce policies such as read notification, and that the requester has “deleted the data” notification (providing an audit trail that it happened, even if they only “say” they did).

This network method will not require such strict health checks because if a node goes down unexpectedly because the data is not sitting in the volatile memory, we haven’t lost anything. When the node comes back online (even with a new hard drive) it will eventually get back to its original dataset. The advantage of this is that we can use other secret sharing/fragmenting methods (instead of Shamir's secret sharing). For example, we could take the data and chunk it in 4 parts each node still has junk data because it requires them all. Without Shamir's secret sharing we could then encrypt the chunked data with either public keys or passwords. (Shamir's can be considered encryption and double encryption is not always the best solution depending on the application.) One advantage of this would be reduced data storage requirements.  In summary, this gives Keybox a lot of flexibility in how it can manage the network and the intelligence of that network. If we do decide to adopt secret sharing, another layer of security is possible when it comes to recombining the data. If you only require 2 parts to restore the original data we don't have to allow access to all 4 virtual networks for the data part retrieval phase.

** Can be any size networks, With any size total nodes. It all depends on how they decide the split and manage the data. 4 with 8 nodes is an example representation of how it could look.

*** Any data that is transmitted will be encrypted. Part of our authentication system of the user will be to either have access to an existing public private keypair or have a generated key pair for just this session.

```

i. Keybox encrypts and fragments data into multiple unique parts

ii. The fragments are distributed across a decentralized network of private or public nodes

iii. Only a subset of the fragments is needed to recreate the whole

iv. The data can only be accessed through the recombination process via smart contracts

v. A redundancy threshold ensures that the failure of a node does not affect the integrity of the data

```

## Fragmentation process

There will be 2 possibilities for the fragmentation process. On-device or Remote. Each method does the same thing but remote allows for people with low powered devices to still protect their data by using a service run by us. This service would have to be designed to be secure and be offered as a backup for if they cannot fragment their own data.

1.  Select data to be protected and wrap it up into a single object (So each secure record has only 1 object to maintain)
    
2.  Convert that object into a safe string data type.
    
3.  Run the safe string through Shamir's secret sharing algorithm (May need to chunk the data as there is a theoretical limit)
    

    a.  The X parts of Y will be configured based on the available network nodes and as well of any geolocation / personal preferences.**
        
    b.  If the "limit" is 10mb worth of data, we would chunk it into 2x5mb worth of data and fragment them separately.
        
    c.  If the device cannot fragment it will fall back to the remote method via the API to perform the fragmentation, and the remote device will receive all the fragmented parts.
    

5.  Create a new transaction to create a seeded activity stream with the metadata.
    
6.  Upload each fragmented part to the above seeded activity stream volatile data area (Each node receiving different dataset)
    
7.  Run another transaction to get the network to initiate the differential consensus (Making sure everyone has different data on the same stream)
    
8.  Confirmation that the data is both secured and unknown to a single entity.
    

** This could become rather complex we could have 1 large network of 100 nodes, or networks of smaller networks and give the user the choice how the data is disbursed. The reason for this would be to fragment the data further across so many locations which an attacker wouldn't know where to attack. It also allows for 1 administrator to run multiple nodes but never has more than 1 (or possibly more depending on X of Y) part of the fragments.

![How fragmentation works](https://lh3.googleusercontent.com/PkEcZ6gCkMxN_chF1dhDB4vlmLskdmLztDLm5-0Z-HcXAH1wBVXehwUXNgyPL-yaEXVwLMBbYtM "How fragmentation works")

## KEYBOX INTEGRATION**

We provide an API and SDK to allow enterprises a seamless experience in managing their data at rest or in transit. Clients can use their existing infrastructure to host the solution or can use the secure Keybox hosted node environment. 

### How to use the Keybox API

The API UI can be found at https://poc.keybox.co. There is a swagger UI available under "API Explorer".  
All of the API endpoints can be tested in the explorer by expanding the relevant sections and clicking the "Try it out". Endpoints

> Write 
> Inspect 
> Get 
> Delete
> Write
> Returns: A reference

The write endpoint is used to add data to the Keybox. Data can be sent as text or as an Octet-stream. The name and extension of the file is not stored. When uploading it is recommended that both are stored with the returned reference. This can be used to correctly rename the file upon downloading.

> Inspect
> Receives: Reference  
> Returns: Fragbits

The inspect endpoints returns a list of the fragments created when the uploaded data was sharded.

> Get
> Receives: Reference  
> Returns: Uploaded data

The get function takes the stored reference and returns the un-fragmented data.

> Delete
> Receives: Reference

The delete function takes the reference and deletes the fragmented data.

# USE CASES

Below are examples of where and how Keybox can be applied: for data at rest; for data in transit or sharing; for key management and recovery; for compliance and for data theft obstruction.
  

## 1 - DATA AT REST : Protecting Archive Data with Keybox

### Enterprise customer data (Cloud-based or on premise)

  

Customer data is stolen every day from enterprises, e.g. hotels. Keybox allows sensitive data to be stored or backed up in decentralised, secure fragments. The data can be accessed instantly for business logic and may not even need to be recovered in its entirety to return specific data requests.

  ### Cloud-based shared data storage solutions (e.g. Dropbox)

  

Keybox can sit as a layer between a user and their database, providing an additional security layer to deliver greater control of access.

### Digital Asset Custody

 
Keybox is the safest way to store keys for digital assets that also allows low-latency recovery. Where hot wallets are not secure and cold storage is slow/inefficient, Keybox provides instant access with highest grade security.

Private keys can be recombined at the point of trade, or for more security, trades executed without fully recombining the key.

  

## 2 - DATA IN TRANSIT /SHARING : Sharing Data Safely with Keybox

  
### Sharing Data Securely (e.g. file export, Open Banking, Compliance & Audit)


Large corporates frequently need auditors or regulators to access and review sensitive information. Banks need to collaborate with Fintechs. Corporates frequently need to export sensitive data. Keybox can allow authorised third party access in secure way, with specific, permissioned key access and a full audit trail.


### Secure Investor Identity Verification

To comply with KYC/AML, investors have to provide highly sensitive documents to complete transactions (personal details, proof of wealth, residency, address). This data transfer poses a risk. Keybox can allow entities to share data access exclusively and for a limited time period to specific persons, with low risk.

### Transaction Data Rooms

To complete corporate transactions, a great deal of sensitive data is stored in data rooms. Access to and transfer of this data poses a risk. Keybox can allow data sharing for a limited time period to specific entities, with low risk.

  
## 3 - DEVICE/USER KEY RECOVERY : Supporting Lost Access

### Lost Phone

One of the most common mobile/online support issues is loss of access to a device or an application, caused by either losing the physical device or the login/password master access. Keybox allows for the automation of the verification process of an individual's identity, enabling self-certification in applications using a Keybox-powered network. A user can regain access to their secured data records by controlling the self-certify process for each record they have created, allowing them to set the challenges themselves for the access recovery for each specific record or the whole device or account.

  

## 4 - COMPLIANCE WITH GDPR : Proof of Data Territoriality + No Personally Identifiable Data

 
### Demonstrating Auditable GDPR Compliance to Regulators

 
Whilst regulations have evolved and may continue to change, Keybox allows clients to demonstrate adoption of best practices with regards data security as a data processor through data fragmentation and territoriality.


## 5 - DATA THEFT OBSTRUCTION : Protecting Against Stolen Access

 
### Stolen Laptop

  

All data security processes have the challenge of failure at the point of consumption end, e.g. if an open laptop is stolen. Keybox has functionality to allow new keys to be reissued as soon as an attack is detected – an effective “freeze” on the account, with authenticated recovery available. Thus, after a first breach, further damage is limited.

  

## 6 - KEY MANAGEMENT : Access Control

### Crypto Currency Exchanges

  
Keybox can secure private keys with permissions over access control. Crypto exchanges request you send your crypto keys to their wallet. Keybox allows you to give the exchange permission to access your private key only under certain conditions to generate the signature needed for them to transact for you on a public network.

# Frequently Asked Questions

1.  How do we describe Keybox?

		Decentralised data security solution with active access permissions layer.

2.  What is Shamir Secret Sharing? Where is it used?

		It is a form of encryption which uses multiple parts of data instead of one large chunk. It is used on the device (not on the ledger or Keybox) to generate those multipart of data encryption.

3.  What is Activeledger and why is it different from other public (or private?) blockchains?

		Activeledger is a multiprocessing transaction ledger which has been designed for enterprise first integration. It is capable of territoriality and running a differential consensus within its smart contracts (allowing data to be fragmented and stored different fragments.)

4.  What is the difference between secret sharing and fragmenting? What is the difference between hashing and fragmenting?

		Secret Sharing vs. Fragmenting: The data in secret sharing are unique to each other. When you’re fragmenting something, there is some data overlap somewhere.

		Hashing vs. Fragmenting/Sharing: Hashed data is one way only. For example here is a credit card number hashed: e4816c29f3aa34390b27e5901b1a0d7b61323e431de3e4cb2187848f1cb8b1ac

5.  How secure is this secret sharing compared to a hashing process, can you refer to some research?

		A really simple answer is secret sharing is infinitely more insecure because it's 2 way. However, as we need to retrieve the original data for our clients, this is a strength instead of insecurity. A more relevant comparison would be secret sharing vs. ppk/passphrase encryption.

6.  Describe the steps to store data within Keybox.

		See Workflow Diagram as an example.

7.  Describe the steps to reform the data with Keybox.

		See Workflow Diagram as an example.

8.  Why is the technology unique?

		The biggest problem with secret sharing is “where and who do you trust with each secret part.” This is a key reason for it not to be adopted. However, this problem can be resolved with the current research into DLT. While each part of this technology is not unique, the combining of them creates a new unique technology (just like bitcoin.)

9.  What are the “secrets”?

		This was the term given when the algorithm was designed because they wanted to “share a secret.”

10.  Does Keybox depend on other vendors?

			Keybox Core is currently on dependent on Activeledger. This may increase during its development phase for best practice in terms of API/UI/2 Factor Authentication; however, it is easily possible to be dependent on Activeledger and the computer language runtime.

11.  Why aren’t public blockchains not suited for this (yet)?

			2 part answer. First, if all the data is somehow “on-chain” then you haven’t secured anything, just made it slightly inconvenient to find and collect. Second is if you were to only put a representational reference on a public ledger you still lose the consensus on where and how the original data is secured.

12.  Is the data replicated anywhere or simply fragmented across multiple nodes?

			It depends on the model used. On the POC it is fragmented across multiple nodes and kept in consensus by the Smart contracts and policies applied.

13.  What are the nodes? Where are they?

			Currently, the demo is running on the Activeledger global testnet. They are located in USA, UK, EU, Hong Kong. This network of computers would not be used in a production environment in which case a production grade

14.  Can we store an unlimited amount of data?

			Activeledger doesn’t impose any data restrictions. Only restrictions are the typical bandwidth and storage limitations in the infrastructure.

15.  How is the backup system working? What happens if some nodes fail?

			Activeledger has a restore mechanism in a post error iteration. However, depending on the model used this may not help. This is why Keybox will operate a health checker smart contract where if it detects the threshold is getting too close to losing the data, it will trigger an automated recombine process and issue a brand-new set of shares. This will be fully automated and audited by those contracts.

16.  How much of the data is needed to retrieve 100 %? Can we lose data?

			This is configurable. The demo uses a 60% setting of the network which is then rounded, so its threshold is 2 parts needed out of 4. This setting combined with the health check above is how we reduce the risk of losing data.

17.  Is there dependency on miners?

			No. However, I believe there is a business model which could bring in the equivalent of miners for extended data security

18.  Can you explain the consensus model?

			Configurable Practical Byzantine Fault Tolerance. Activeledger network has to agree upon inputs, outputs, valid transactional data and signatures to reach the commit phase to store state. It is also possible to have additional consensus delegated to within a smart contract.

19.  How can I see the smart contract on the back-end?

			Either via file access on the node host or by knowing their Activity stream id and using the API. Smart contracts are self-hosted on Activeledger. You can see an encoded versioned of a Keybox contract here: http://testnet-uk.activeledger.io:5261/api/stream/a9dc9b6085e05ea1765a72c163c2f7d00bf0566214ccc9416966ad7ef7258038

20.  How does access to the data, permissions, 2FA, private keys etc. work?

			In the demo this is done directly with the Activeledger API (Activecore). In production, Keybox will have its own API which has its own additional authentication for security practices. Some 2FA requests will come directly from the ledger to prevent man-in-the-middle type attacks. (The ledger can send the SMS)

21.  Can we store an unlimited amount of data without compromising speed?

			Yes, if we can exclude bandwidth related restrictions.

22.  Can we store an unlimited amount of data without compromising safety?

			Yes, as we are storing the equivalent of “junk” data and protection the intelligence which converts it from being junk.

23.  Can we retrieve large amounts of data? What are the limitations in terms of latency?

			Activeledger lookups can be measured in 10ms, so latency is not impacted; bandwidth availability, however, will reduce the download times, but this is true of any remote system.

24.  Is data on the Blockchain?

			Yes, with all-out data models everything is stored on the blockchain either across “Virtual Networks” or using Volatile memory. All data will be processed and available within smart contracts.

25.  Describe the potential delivery mechanisms for Keybox (SDK, API, Gateway, Platform, WeTransfer model, DropBox model etc.)

			See Workflow Diagram as an example. To add to that, it will mostly be API driven but delivered by an SDK for easier integration, as it will be powered by a series of data handshakes wrapped up in signed Activeledger transactions.
  

TO GAIN ACCESS TO THE KEYBOX API, PLEASE CONTACT FRANCESCO@KEYBOX.CO 
 
GENERAL ENQUIRIES TO INFO@KEYBOX.CO

```
© Keybox Ltd. 2019 All rights reserved. 
```
```
Disclaimer: all data provided is for information purposes only and may not form the basis of any agreement
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM0OTM3NzQwNCw1Njc0NDU2NjYsLTMxMD
g1OTA3NCwtMTg5NDIzMDUwMiwxMDU4MzI4ODA3LDE3MzQ4NTI0
MzcsLTE2NzgwMjI3MDksLTE3MTU2OTEwMjMsLTMyMjIzMDg0Ni
wxMTI4Njk3MzYwLC03OTkyMDI4NTgsNDA4NjIwNTQsLTEzMzIy
NDA3NSwtMTcxMjY1NzY2OCwtMTAxMDAzMzUzMywtMTMxMTM3Nz
E4OSwxMjA3MTk4MTk0XX0=
-->