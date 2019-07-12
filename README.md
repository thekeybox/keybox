# KEYBOX  WHITE PAPER

Valuable enterprise data is vulnerable to hacks, whether stored in the Cloud or on-premise. Data at rest and data transfers between organisations increase the risk of breaches. Key management and recovery remain an issue and current storage technologies rarely comply with data regulations and privacy laws (e.g. GDPR). Keybox addresses all of these issues.

>With data fragmentation, Keybox sets the new standard in data management best practice, offering enterprises of all sizes data security, control and traceability

## SECURING DATA 


Keybox stores data in encrypted fragments across multiple, decentralised private or public nodes, such that penetrating any node cannot yield any decipherable information. Authorised users recombine data from fragments using smart contract technology.

```

i. Keybox encrypts and fragments data into multiple unique parts

ii. The fragments are distributed across a decentralized network of private or public nodes

iii. Only a subset of the fragments is needed to recreate the whole

iv. The data can only be accessed through the recombination process via smart contracts

v. A redundancy threshold ensures that the failure of a node does not affect the integrity of the data

```

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

> Write Inspect Get Delete
> 
> Write
> 
> Returns: A reference

The write endpoint is used to add data to the Keybox. Data can be sent as text or as an Octet-stream. The name and extension of the file is not stored. When uploading it is recommended that both are stored with the returned reference. This can be used to correctly rename the file upon downloading.

Inspect

Receives: Reference  

Returns: Fragbits  

The inspect endpoints returns a list of the fragments created when the uploaded data was sharded.

Get

Receives: Reference  
Returns: Uploaded data  
The get function takes the stored reference and returns the un-fragmented data.

Delete

Receives: Reference  
The delete function takes the reference and deletes the fragmented data.

# USE CASES

Below are examples of where and how Keybox can be applied: for data at rest; for data in transit or sharing; for key management and recovery; for compliance and for data theft obstruction.
  

![enter image description here](https://lh3.googleusercontent.com/FxtOLWXnVseOEClFMR_0ORvVwSep7BlwTA83Zpu16z0ZHRAUX9uocLWhs-CcKrybPFja281cP5A) 

# 1 - DATA AT REST : Protecting Archive Data with Keybox

  

## Example: Enterprise customer data (Cloud-based or on premise)

  

Customer data is stolen every day from enterprises, e.g. hotels. Keybox allows sensitive data to be stored or backed up in decentralised, secure fragments. The data can be accessed instantly for business logic and may not even need to be recovered in its entirety to return specific data requests.

  

## Example: Cloud-based shared data storage solutions (e.g. Dropbox)

  

Keybox can sit as a layer between a user and their database, providing an additional security layer to deliver greater control of access.

  

## Example: Digital Asset Custody

  

Keybox is the safest way to store keys for digital assets that also allows low-latency recovery. Where hot wallets are not secure and cold storage is slow/inefficient, Keybox provides instant access with highest grade security.

Private keys can be recombined at the point of trade, or for more security, trades executed without fully recombining the key.

  

# 2 - DATA IN TRANSIT /SHARING : Sharing Data Safely with Keybox

  

## Example: Sharing Data Securely (e.g. file export, Open Banking, Compliance & Audit)

  

Large corporates frequently need auditors or regulators to access and review sensitive information. Banks need to collaborate with Fintechs. Corporates frequently need to export sensitive data. Keybox can allow authorised third party access in secure way, with specific, permissioned key access and a full audit trail.


## Example: Secure Investor Identity Verification

  

To comply with KYC/AML, investors have to provide highly sensitive documents to complete transactions (personal details, proof of wealth, residency, address). This data transfer poses a risk. Keybox can allow entities to share data access exclusively and for a limited time period to specific persons, with low risk.

  

## Example: Transaction Data Rooms

  

To complete corporate transactions, a great deal of sensitive data is stored in data rooms. Access to and transfer of this data poses a risk. Keybox can allow data sharing for a limited time period to specific entities, with low risk.

  

# 3 - DEVICE/USER KEY RECOVERY : Supporting Lost Access

  

## Example: Lost Phone

  

One of the most common mobile/online support issues is loss of access to a device or an application, caused by either losing the physical device or the login/password master access. Keybox allows for the automation of the verification process of an individual's identity, enabling self-certification in applications using a Keybox-powered network. A user can regain access to their secured data records by controlling the self-certify process for each record they have created, allowing them to set the challenges themselves for the access recovery for each specific record or the whole device or account.

  

# 4 - COMPLIANCE WITH GDPR : Proof of Data Territoriality + No Personally Identifiable Data

  

## Example: Demonstrating Auditable GDPR Compliance to Regulators

  

Whilst regulations have evolved and may continue to change, Keybox allows clients to demonstrate adoption of best practices with regards data security as a data processor through data fragmentation and territoriality.


# 5 - DATA THEFT OBSTRUCTION : Protecting Against Stolen Access

  

## Example: Stolen Laptop

  

All data security processes have the challenge of failure at the point of consumption end, e.g. if an open laptop is stolen. Keybox has functionality to allow new keys to be reissued as soon as an attack is detected – an effective “freeze” on the account, with authenticated recovery available. Thus, after a first breach, further damage is limited.

  

# 6 - KEY MANAGEMENT : Access Control

  

## Example: Crypto Currency Exchanges

  

Keybox can secure private keys with permissions over access control. Crypto exchanges request you send your crypto keys to their wallet. Keybox allows you to give the exchange permission to access your private key only under certain conditions to generate the signature needed for them to transact for you on a public network.

  

### TO GAIN ACCESS TO THE KEYBOX API, PLEASE CONTACT FRANCESCO@KEYBOX.CO

 

### GENERAL ENQUIRIES TO INFO@KEYBOX.CO

```
© Keybox Ltd. 2019 All rights reserved. 
```
```
Disclaimer: all data provided is for information purposes only and may not form the basis of any agreement
```
![enter image description here](https://lh3.googleusercontent.com/BsXES4FZtOZ-aRN9KeAOpb3DyBfSrmot-F-qRNcK2k7p0YWzpoYFSef7ivlUtpc9xnwSnnzLvdM)  



<!--stackedit_data:
eyJoaXN0b3J5IjpbNzI0MTIwNjYzLDE3MzQ4NTI0MzcsLTE2Nz
gwMjI3MDksLTE3MTU2OTEwMjMsLTMyMjIzMDg0NiwxMTI4Njk3
MzYwLC03OTkyMDI4NTgsNDA4NjIwNTQsLTEzMzIyNDA3NSwtMT
cxMjY1NzY2OCwtMTAxMDAzMzUzMywtMTMxMTM3NzE4OSwxMjA3
MTk4MTk0XX0=
-->