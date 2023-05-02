Download Link: https://assignmentchef.com/product/solved-comp2140-assignment5-merkle-hash-trees
<br>
This assignment is self-contained and probably the easiest. You will write two functions.  We do not expect you to know how Blockchain works. However, by the end of this assignment, if you read the code well enough, you will learn Blockchain in detail.

You will be surprised how this Blockchain technology, considered revolutionary, is built on such simple ideas that a beginner student can code. And later in life, you can mention that you were writing blockchains in your second year of undergraduate.

A transaction is a transfer of coins from a set of addresses (i.e., senders) to another set of addresses (i.e., receivers).

Each sender or receiver is an address, which is stored in a String variable (see Transaction.java). In real life, people can create and use many addresses. We cannot know the owner of an address by just looking at the string.  A Bitcoin transaction can have many senders and receivers. This is why transactions in Figure 1 have different shape sizes. For this assignment, we simplify the transaction model to only one sender and one receiver (see Transaction.java).

A transaction has sender, receiver, and amount attributes. In Bitcoin, transactions are created by ordinary users and sent to a Peer-to-Peer network. Miners listen to the network, discover new transactions, and create blocks out of them. In this assignment, we will not have a real Peer-to-Peer network. The PeerToPeerNetwork.java simulates this and returns a random number of artificial transactions whenever someone calls the collectNewTransactions() function.

A miner is a user (anyone can choose to be a miner) who wants to create a block. The process of getting transactions, putting them into a block, and solving the Proof-of-Work puzzle is called mining a block.

Proof-of-Work (see mineTheBlock() in Blockchain.java) involves creating a string from the blockHash of the previous block, topHash of the MerkleTree, and a long integer (called nonce). Once the SHA256 hash is applied to this string, a 256-bit integer is computed. If the integer is less than a predefined difficulty, the nonce is said to satisfy the difficulty. The block is said to be mined.

Any helper function that you need (e.g., to hash SHA256) is already given in the files.

<strong>What you should implement:</strong> Implement the following algorithms and methods (you can add any necessary private helper methods):

1- buildFrom function in MerkleTree.java:

<strong>Concerns and steps:</strong>

Implement the algorithm that takes n transactions and creates a Merkle tree from them. A Merkle tree is a binary tree where leaf nodes are transactions, and interior nodes are transaction hashes (SHA256 algorithm). See figure 1.

In leaf nodes, we take a SHA256 of each transaction, and then concatenate these hashes in the next level, and take their hash again. For example, in the figure the hash “goz1erin…” is computed by

SHA256(SHA256(tx1.toString())+sha256(tx2.toString())). This is applied until we end up with one top hash in the Merkle tree.

At every level (from bottom up), output how many hashes are computed at each level:

Merkle Tree, Bottom Up, Level: 0, number of hashes: 21

Merkle Tree, Bottom Up, Level: 1, number of hashes: 11

Merkle Tree, Bottom Up, Level: 2, number of hashes: 6

Merkle Tree, Bottom Up, Level: 3, number of hashes: 3

Merkle Tree, Bottom Up, Level: 4, number of hashes: 2

Merkle Tree, Bottom Up, Level: 5, number of hashes: 1 – See the Assignment5Output.txt file for output details.

Note that by definition, SHA256(tx1.toString() +SHA256(tx2.toString()) is not equal to SHA256(tx2.toString()+ SHA256(tx1.toString()). When you are creating the Merkle tree, the transaction order is important. You should follow the transaction order defined in the block.

A blockchain does not need to store the Merkle tree, it computes the Merkle tree just to find the top hash, which is “iNu7ag1gor…” in the figure. As a result your code can either i) implement the Merkle tree and store each interior node to reach the top hash, or ii) find the tophash and not store interior nodes.  1st solution: When implementing MerkleTree with nodes, child pointers need to point to parents, because you should build the tree from bottom up, starting from transactions.

2nd solution: If you want to use the second approach, be efficient. Code can be written in 20 lines.

The current block hash is computed from SHA256(previousBlockHash+ topHash+nonce). This way, the block hash of the current block is linked to the block hash of the previous block. If anyone changes the previous block, its hash will change. We will call this event “corruption”.

2- validate() in BlockchainPOW.java

A method to validate the blockchain:

The validation starts from the second block. The first block (genesis block) is mined by the creator of the Bitcoin: Satoshi Nakamoto.

Take the list of transactions stored in a block, and create a Merkle tree from them again (use the existing BuildFrom() function in MerkleTree.java) to find the top hash.

Link the previous block and nonce (follow the order given in mineTheBlock() function in Blockchain.java. Compute the Block hash and compare it to the block hash stored in the block. if they do not match (use string1.equals(string2)), call it a corruption, and return.

<ol start="3">

 <li>Optional 1: write code to update the difficulty every 2 weeks. For this, you can runthe blockchain in a while(true) loop.</li>

 <li>Optional 2: write code to update block reward every 4 years. 5. A log file forsample output will be shared on D2L. The output of your code must follow similar steps.</li>

 <li>See the discussion forum on D2L for your questions.</li>

</ol>

<strong>Concerns.</strong> Please avoid magical numbers in your code. There should be only ONE return per method. See the programming standards (under content/course documents) file on UMLearn, and follow the suggestions. Assignments will be graded by considering these standards. Your code must not give any warnings or errors when compiled and run.

<strong>Report</strong>

Write a small report in the comments at the end of your program. Answer the following questions in terms of transaction count n. (use short sentences, ideally only one sentence):

<ol>

 <li>What is the depth of the Merkle tree in a block.</li>

 <li>If we want to detect corruption at the transaction level, how many comparisonsshould we make in the Merkle tree.</li>

 <li>Is there a way to corrupt any part of the blockchain without being detected?</li>

</ol>