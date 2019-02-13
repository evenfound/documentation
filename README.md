# EVEN network basic protocol

## 1.1. Technology choice

The basis for the stable functioning of a distributed network is a logically coherent protocol that enables three essential tasks to be solved: protection of confidentiality, distribution and storage of data. In historical terms, trust in products or services is earned in the course of their lifetime. Physical or electronic records accompany every object and confirm its origin, purpose, quantity and history. Creation, support and confirmation of all this information adds a significant 'trust tax', as expressed in the man hours expended by banks, accountants, lawyers, auditors and control services quality among others control services. At the same time, important information is frequently lost, becomes inaccessible or occasionally deliberately hidden.

The fourth industrial revolution continues to blur the lines between the physical and digital worlds, and blockchain significantly alleviates the authenticity and value of data necessary to support objects and services along the whole cost chain. Furthermore, blockchain introduces a compatible transaction layer in which the parties being not acquainted with each other can exchange financial and physical values in real time. 

Blockchain builds a wallet into machines, which allows to balance profits and losses and conduct transactions with other machines automatically. New business models geared towards interaction between machines and forms of exchanging assets between them are emerging almost on a daily basis. However, as for scaling computing resource requirements and the cost of transactions, modern blockchain technologies have serious limitations.

In this respect a new and viable means of solving familiar problems will be distribution ledger technology (DLT), which is getting stronger in the real sector of the economy. What is more, this technology can also be applied in such traditionally conservative businesses as oil and gas extraction. Practice shows that DLT can be successfully implemented wherever large volume of information databases are available and immutable.

One of the basic models successfully implemented in DLT projects (IOTA, Byteball) today is DAG; this is the technology of distributed ledgers that differ from Blockchains in the structure of their records and asynchrony. 

In classical blockchain technology transactions are intially grouped into a block, after which in the course of time this block is added to a chain of other such blocks. In this system the capacity and transaction time are limited by the block's size and the time needed to generate a new block.

![Screenshot](/img/1.png)
 
In the DAG model (Directed Acyclic Graph) each transaction is immediately added to a graph compiled from many transactions recorded not consecutively, but simultaneously. Here there are no blocks, and therefore there are no problems with size.

![Screenshot](2.png)

Within this structure users themselves support the network. Before sending a transaction no fewer than one and generally two preceding transactions need to be confirmed. That is exactly why there are no miners or masternodes here.

The advantages of this solution:

- transactions speed
- no commission (or minute)
- more scalable compared to blockchain.

However, the obvious advantages of this model are per se offset by the following shortcomings:
DAG shortcomings:

- Scalability issues (blockchain needs to be synchronised each time when adding a new transaction).
- With few network participants transactions confirmation can take long, and if there are none they may not be confirmed at all.

The existing shortcomings, as practice has shown, seriously undermine the advantages of blockchain technology when it comes to decentralization. For instance, in IOTA the Coordinator node is used to manage Tangle forks, and is essentially a validation server. 

Are there ways to solve this problem and somehow elegantly remove the existing shortcomings and make a virtue of them?

Analysis of existing approaches in implementing DLT and the DAG algorithm in particular suggests that there is such a solution. When studying for example IOTA network transaction graphs, it is easy to see that the graph's evolution time axis is directed from right to left. As it should be.  the graph is directed and acyclic, a new transaction is a content-oriented message and thus does not know its place within the network's topology and hope for the good will of the coordinator. If it does not work out (as often happens), the transaction may not be confirmed at all. 

Our solution allows change the evolution time direction in DAG and get maximum decentralization, shifts the transaction from content-oriented to topological-oriented and uses ranking algorithm. At the same time all the model's advantages are fully present.

**What is the essence of modernization?**

*1. Just as in classical DAG, a new message that in much the same way is formed from a chain of connected transactions with links to hash headings of their transactions as a trunk fork, providing balance, and as brunch links from one of several transactions connected in the message which the node has obtained for validation in the private inbox of the distributed storage;*

*2. Using the ranking algorithm described below, the node forms a list of two versions of the transmission: in the first instance with the necessary binds to the trunk and brunch graph, and in the second it sends the MAM algorithm validated messages;*

*3. The node may be passive and not do anything, neither in validating and processing messages, but then this will affect its ranking, and in order to implement its own processing transactions it will have to pay a commission for the network to provide the necessary validation message packet.*

Here the question arises: how to create topologies in a crypto-protected decentralized network? How can content-oriented messages become the addressed parcel keeping confidentiality?

This problem can be solved using the basic IPFS protocol. The term 'decentralisation' has acquired a new meaning with the advent of crypto-currencies and blockchain technology. There emerged many new projects that simply have no equivalents. The InterPlanetary File System (IPFS) is one illustrative example. What are the features of the new technology and what opportunities does it open up? 

IPFS combines sharding and decentralised file storage. Yes, many companies are developing solutions for file storage, in particular through Sia and supported by Google Storj. However, IPFS works under a different principle, more precisely bringing about a symbiosis of these technologies.

The project started as a protocol in Ethereum in 2016. This blockchain that was selected because it is friendly to new developments and innovations. Bitcoin could not boast of anything similar. How wise this decision was remains unknown for now.

A Wiki definition provides the answer to the main question: IPFS is a peer-to-peer distributed file system that connects all computing devices as a single system of files. In a sense the IPFS is similar to the World Wide Web. IPFS could be seen as a single BitTorrent swarm, exchanging objects within one Git repository. In other words, IPFS provides a high-throughput, content-addressed block storage model, with content-addressed hyperlinks. **_This forms a generalized directed tree graph._** IPFS combines a distributed hash table, a decentralised block exchange and also a self-certifying namespace. At the same time IPFS does not have a point of failure, and the nodes do not have to trust each other. The filesystem can be accessed in a variety of ways, including

- via FUSE and
- over HTTP.

A local file may be added to IPFS file system, which makes it accessible to the whole world. Files are identified by their multihashes, which makes caching easier. They are distributed through a protocol based on BitTorrent protocol. Users browsing through content help other network users access content. IPFS has a name service called IPNS, a global namespace based on open keys that is compatible with other namespaces and DNS, onion, bit etc. into the IPNS.

From the technology definition, especially with reference to forming DAG graphs, and it really does use the DAG algorithm, we can easily understand the proximity of the technologies and and opportunity for their blending when implementing the properties needed for the basic protocol.

## 1.2 Possibility levels of client applications and the subnet.

Let us first of all add some details on how EVEN network basic protocol works using IPFS and how virtual voting occurs.

Each client application (node service) connected to EVEN network is identified in the IPFS network by a unique hash address supplied by it. Each server has local storage divided into two sections — inbox and outbox — which are also uniquely identified by a hash as confidential, but at the same time they are physically situated on the service host. 

When processing, the server working in normal operation receives in its inbox a series of messages requiring confirmation. Without going into the details of cryptography, which will be discussed below, the service confirms the received messages, marks their validation with its nonce under the HashCach algorithm and its IPFS hash address, and transfers them to the outbox. The same operation is carried out by the other network services that have received the same packets. But before this can be done, each service sends out messages from its inbox to addressees in an order of priority structured after asessing the ranking of visible services, and the need to send them, in other words implementing the Gossip protocol, whether the service needs this information or not. This is achieved by checking whether there is a hash message in the addressee's inbox. This is how the distribution storage is filled with validated messages at such speed.

When creating its own transactions, the sequence of operations remains the same except that the service, in addition to validating the inbox messages, forms its own, indicating the trunk links, a link to the last incoming transaction and the previous one for balance, and branch from one to several links confirming the inbox message.

The node service that does not wish to participate in the confirmation process may ignore incoming messages and not perform message validation, but in this case its ranking will be zero, and in order to carry out its transactions, the owner of the wallet will have to pay the network a commission to receive the necessary quantity of branch messages.

Here it will be appropriate to describe the virtual voting algorithm BFT. Here we can clearly see the basic reason why the IPFS was included in the basic algorithm model. Validated messages posted by node services in their own outbox are generally accessible to be read in a distribution network, as is the node service wallet when calculating the balance, assessing the number of links to hash services of nodes they have validated while constructing a transaction tree, and estimate the consensus needed for decision making.

Bearing in mind the main advantage of DLT — the speed of carrying out transactions — doubts may arise about the possibility of implementing the network's basic algorithm. But the key factor guarantying the speed margin is its ranking calculation. How does this work?

The node service that performs the network's needs as effectively as it can, and which thus supports its stability and productivity, factoring in its steadily rising ranking (see above) is ranked in the first lines in the mailing list. Correspondingly, using the same algorithm, this service forms its own mailing list, the top of which includes services that are equally effective. Thus, since the ranking is changeable, the network dynamically forms a virtual subnetwork of effective services, on the basis of whose votes quicker virtual voting can be constructed. The key word here is **_dynamic_**. The network for preventing the monopolisation of consensus should automatically control the balance of the participants of leader subnetworks.

## 1.3 The algorithm for the ranking calculation and a few simple formulae.

The algorithm for the ranking calculation has a synthetic character and its main purpose is the dynamic ranking calculation of the node service with a simultaneous compensating this calculation under technical and information indicators.

The function value is immeasurable and has a physical meaning as a relative share of the input of a specific node into the total ranking of the network node. The continuous function calculation for node **_R_** rating value at the moment of time **_t - R(t)_** is challenged by the fact that in the current discrete system its current value does not exist. In other words, we can say that the value of the function is correct at moments that coincide with changes in the system, in the node network, for instance. `t_(-n),t_0...t_∞`. This modality,  based on an analysis of indicators on which the function value in discrete moments in a selected historical period depends, and the presumption that the total network ranking may depend on market moods, allows for the presumption that a transient *polynomial forecasting* of its value on the basis of statistical network data is possible.

In each period of calculating the work of the network the node ranking value depends on several parameters:

*1. The relative node capacity input into the total capacity of the network.

Here it is worth mentioning that most information exchange and data verification algorithms in a distributed network provide for an equal involvement of its active members in this process.   Thus the **_capacity_**  of a specific node, as a full participant, impacts the average time for processing information. Its relative value depends on the total computing capacity of the **_P_**  network, which can be represented as the sum of discrete values of the network node capacity:

	P = ∑_(i=0)^M Pi(T=〖tj)〗_                                                                             (1.1)

Where **_M_**  is the number of nodes in the network, *Pi* the computing power of the *i* node at discrete moment *T* -  from the *j* event.

At the same time the **_relative node capacity input_** into the total computing capacity of the network looks like this:

	P_o  =〖P_i (T=〖t_j)〗_ 〗_ /P                                                                         (1.2)

**Note:** *It is evident that an increase in the total capacity of the node network with its constant value at a specific node leads to the reduction of the value of its relative weight in the system, which must be factored in when considering the impact on the resulting indicator.

*2.  Of the relative speed on the network's operation.

The value *V_N* determined by the number of confirmed packets of data transfer over a unit of time in the network in which the node operates will obviously impact on its ranking. Bearing in mind that this method yields a relative value, it would be feasible to normalize this parameter *V_o* either towards the middle of its network value or to the maximum value. This choice can be made by experimental means, by calculating the level of indeterminacy of the value of the node ranking function.


*3.  Of the relative input of the node into the information exchange — activity.

A relative share of the input of a specific node into information exchange  *K_o* characterizes its activity. It depends on the total value of the volume of information exchange — the number of units of information К, transferred in the distribution network over an interval of time by active network participants calculated statistically, and the volume of the input of the *K_i  i* node into this exchange.

Here it should be noted that a substantial impact on this indicator is made by *1* and *2* above, which allows us to assume its integral nature. In other words, its value in a discrete period of time of a *j* event is the value of the figure's area limited by the function of the change in the total information exchange over a period of time *Δt* depending on the speed of the change of the *i* node input, which is determined by the derivative from the function of the change in relative values *1* and *2*:


                                  (1.3)

K_o=K_i/K ∫_(t_(j-1))^(t_j)  ((V_o (t)+P_o (t))dt)/2                                                 (1.4)
On examining the dependency schedule it can be assumed that the endless increase in node capacity does not entail an endless increase in the relative input share and the principle of its distribution, for instance, on a polynomial prognosis, will be of an exponential character, which can be used to offset its impact on distribution, factoring in the weight of the following indicators.
4.  Setting totals.

Considering one of the basic requirements of a peer-to-peer network which excludes an increasing domination of its separate members in the operational information exchange, with the aim of preventing its centralization of data this indicator can be used as an offsetting influence of technical indicators 1, 2 and 3. Prefacing the description, the approach resides essentially in the fact that the calculation of the node ranking at the moment of time t is made by calculating the average value of the natural logarithm from the relative amount of settings and the logarithmically reverse function from the value of the relative input of the node into the information exchange. In other words, the number of S settings over the j period of events is lograrithmically inverse to the relative input into the information exchange.
Picture here, I'll do it tomorrow.

This dependency demonstrates the offsetting deliberateness of calculating the node ranking from absolutely different weight categories. In other words, with the maximum possible increase in computing resources, network quality and activity and with the same maximum setting totals, the node ranking will remain no greater than at the average level. With other defined values, higher or lower rankings that do not contradict logic are possible. 
Thus 

S_o=1/(∑_(i=0)^N S_i ) S_i (T=t_j)                                        1.5
Where the settings total of the i node over the period of the j event is the value of the settings total of the i node over the time of the j event.
Note: It will be appropriate to explain that the time of event j is the time interval from the last event in the network in which the latest values required in this method of indicators were obtained.

5. Accuracy of historical information, that is, of 'rumors'


In systems with a distributed confirmation of transactions, in order to implement most consensus algorithms information on past events in the network is used.
But factoring in the fact that by no means all modes can physically be situated in the network, their blockchains form blank spots whereby the other nodes when there is a request to restore missing data on calculating the consensus algorithm are forced to lose the computing resource for the request for non-existent data.
In order to reduce the likelihood of such an outcome and thereby maintain the exchange speed indicators in the network at the required level, it is essential to include in the ranking calculation the accuracy of information I_o as a ratio of the number of blank spots in the blockchain to the total amount of information units in it. As opposed to parameter 3, this parameter is formed not in relation to the whole network but on the node's own resources.
Formally, it can be considered as a weight multiplicative coefficient with a calculation of the final node ranking.

Description of the method

Factoring in these indicators and based on a hypothesis, the first stage of the ranking calculation at the moment of time t over the time of the event j looks as follows:

R_j=I_0   (lnS_o+(ln K_0)/(K_0-1))/2                                                1.6

At this stage, as already stated, we obtain the discrete value ranking over the time of the event j.
A more refined task of the modality is in having with high probability an accurate ranking value in this uninterrupted period Δt  from the moment event j. ends.
For illustration purposes let us construct a graph of relative dependencies outlined above.
 
The diagram shows the dependency of a relative value of a node ranking with regard to others in the network which is measured along the vertical axis from the point where the schedules of the two functions intersect: K, which characterises the relative technical provision of the service and its network parameters, is the hash rate and ping time, and S is the relative balance. The ranking value is at its maximum at the point of intersection, in other words when achieving a balance of two indicators, that is, their mutual offsetting. To put it another way, to raise one's ranking having bought up all tokens or created a super powerful pool of computing capabilities is impossible, the ranking will be offset. In theory this is possible, but this is when there is one node service in the network.
If we depict the graph another way:
 
you can see the average calculation of the ranking value as an average value of indicators K and S on the synthetic curve of the values.
(The original application for demonstrating how the algorithm works can be downloaded from GitHub repository link — https://github.com/evenfound/even-network/tree/master/r-score-demo).

1.4. Structure of transactions and messages

Let us turn to classic examples for understanding the information assets transmitting process in a basic protocol. Alice has the initial number A_SECRET_SEED, which contains 100 units in 4 different addresses, and the total balances provide this value:

seed : A_SECRET_SEED 
address[0] : QGHFGFQSGQFS …… AAA, balance : 10 
address[1] : QGHFGFQSGQFS …… BBB, balance : 5 
address[2] : QGHFGFQSGQFS …… CCC, balance : 25 
address[3] : QGHFGFQSGQFS …… DDD, balance : 60 
address[4] : QGHFGFQSGQFS …… EEE, balance : 0

Bob doesn't have anything in his wallets:

seed : B_SECRET_SEED 
address[0] : AHGSHFSJHFSJ…… QQQ, balance : 0 
address[1] : AHGSHFSJHFSJ…… VVV, balance : 0

Alice decides to send Bob 80 information units at the address AHGSHFSJHFSJ…… QQQ .. A message in the EVEN basic protocol is a connected hash with an index of three types of transaction: input, output and meta-transactions. For our scenario it is initially essential to prepare an output transaction, which means that we want to send to Bob's address 80 information units:


 
Draw up a transaction to Bob's address of 80 information units
Next we will need to draw up an input transaction. In this scenario all four addresses will have to be used which contain ( 10 + 5 + 25 + 60 > 80) information units to perform the output value to the sum of 80.


    
Four output transactions which send units to Bob's address
Next we will need to draw up an input transaction. In this scenario all four addresses will have to be used which contain (10 + 5 + 25 + 60 > 80) information units to perform the output value to the sum of 80. An input transaction should contain the transaction signature, which means that it is essential to add an additional meta-transaction to transfer the signature, it must be added:





    
Adding to the meta-transaction message to transfer the signature
Drawing up the message has not been completed: the packet is unbalanced. Thus four transactions have been formed for 100 information units: 10 + 5 + 25 + 60 = 100 inputs and 80 outputs, with 20 information units remaining that should be returned to the sender's wallet. For this an additional transaction needs to be created. The wallet creates a new address to receive an output transaction for the remainder marked 'unspend':

 

After this the balanced packet is received and the conclusion of the message can be begun. For this it is essential to fill out consecutively the transaction indexes, the last index and generate the packet's hash function with the help of the hash function SHA-3. 


   
   
Filling out the indexes
After this the balanced packet is received and the conclusion of the message can be started. For this it is essential to fill out consecutively the transaction indexes, the last index and generate the packet's hash function with the help of the hash function SHA-3. 
The hash function uses a sponge algorithm that will consecutively absorb the transactions, checking each element one by one (the order is important) and then will generate the result. In addition, at the stage of receiving the hash the function will check whether the packet hash is safe or not. If it is not, it will change the obsolete tag of the u-head transaction (a transaction with the index 0) and again generate a hash. After the message hash has been received, it is essential to continue filling out the transactions and receive the following set:

   
   
Filling out the message hashes
Next it is essential to sign the input transactions with the private key of the corresponding address. For this you can receive the address private key from the key generator with the help of A_SECRET_SEED of the wallet. Using the address secret key, it becomes possible to use the signature fragment generator with the private key and the packet hash in order to receive the transaction signature.

 
Using the key generator to receive the signature fragment generator.
  
 

Filling in the signature with the appropriate signature fragment generator for each input transaction.
After this all parts of the message are ready.
Next the chain of its own transactions is connected, through an indication in the trunk field of the hash value of the last input transaction, and the chain of transactions received in the inbox of unconfirmed transactions is connected, through an indication of the hashes of the head transaction messages. Below is the connection scheme draft.
 

Scheme of DAG branches connection..
  .
After this the message is ready to be sent.

