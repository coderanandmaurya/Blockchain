Let's walk through the **code** in detail to explain its functionality and concepts.

---

### **1. `Block` Class**
The `Block` class represents an individual block in the blockchain.

#### **Key Components of `Block` Class:**

```python
class Block:
    def __init__(self, index, timestamp, data, previous_hash):
        self.index = index
        self.timestamp = timestamp
        self.data = data
        self.previous_hash = previous_hash
        self.hash = self.calculate_hash()
```

- **`index`**: The block's position in the chain (e.g., 0 for the genesis block, 1 for the next block).
- **`timestamp`**: Records the time the block is created.
- **`data`**: Holds information (e.g., transactions or messages). This can be anything.
- **`previous_hash`**: Links the block to the previous block by storing its hash.
- **`hash`**: A unique identifier for the block, calculated by combining the above attributes using a hash function.

---

#### **Hash Calculation in `calculate_hash`**
This ensures the immutability of the block’s data.

```python
def calculate_hash(self):
    block_string = f"{self.index}{self.timestamp}{self.data}{self.previous_hash}"
    return hashlib.sha256(block_string.encode()).hexdigest()
```

- Concatenates the block’s attributes into a string (`block_string`).
- Uses the **SHA-256 cryptographic hash function** to generate a fixed-length hash for the block.

---

### **2. `Blockchain` Class**
The `Blockchain` class manages the chain of blocks.

#### **Key Components of `Blockchain` Class:**

```python
class Blockchain:
    def __init__(self):
        self.chain = [self.create_genesis_block()]
```

- **`chain`**: A list that holds all blocks in the blockchain. It starts with the **genesis block**.

---

#### **Genesis Block**
The first block in the blockchain, created manually as it has no "previous" block.

```python
def create_genesis_block(self):
    return Block(0, datetime.datetime.now(), "Genesis Block", "0")
```

- **Index**: 0.
- **Timestamp**: Current time when the genesis block is created.
- **Data**: `"Genesis Block"` (a predefined message).
- **Previous Hash**: `"0"` (since no block precedes it).

---

#### **Adding Blocks**
New blocks are added to the blockchain using the `add_block` method.

```python
def add_block(self, data):
    latest_block = self.get_latest_block()
    new_block = Block(
        index=latest_block.index + 1,
        timestamp=datetime.datetime.now(),
        data=data,
        previous_hash=latest_block.hash
    )
    self.chain.append(new_block)
```

- Retrieves the **latest block** in the chain (`get_latest_block`).
- Creates a new block with:
  - Incremented index.
  - Current timestamp.
  - The provided data.
  - The hash of the latest block as its `previous_hash`.
- Appends the new block to the chain.

---

#### **Verifying the Blockchain**
This ensures the blockchain's integrity by validating all links.

```python
def is_chain_valid(self):
    for i in range(1, len(self.chain)):
        current_block = self.chain[i]
        previous_block = self.chain[i - 1]

        # Check if the current block's hash is correct
        if current_block.hash != current_block.calculate_hash():
            return False

        # Check if the current block's previous hash matches the previous block's hash
        if current_block.previous_hash != previous_block.hash:
            return False

    return True
```

**Two checks for integrity:**
1. **Hash Validation**: Verifies that the block's hash matches its recalculated hash (ensures data hasn't been tampered with).
2. **Previous Hash Validation**: Confirms the block's `previous_hash` matches the hash of the preceding block (ensures links are intact).

---

### **3. Demonstration (`main` Function)**

The following section shows how to use the `Blockchain` class.

```python
if __name__ == "__main__":
    # Create a new blockchain
    my_blockchain = Blockchain()

    # Add blocks to the blockchain
    my_blockchain.add_block("First block after genesis")
    my_blockchain.add_block("Second block after genesis")
    my_blockchain.add_block("Third block after genesis")

    # Display the blockchain
    print("Blockchain:")
    print(my_blockchain)

    # Verify the blockchain's validity
    print("\nIs blockchain valid?", my_blockchain.is_chain_valid())

    # Tamper with the blockchain
    print("\nTampering with blockchain...")
    my_blockchain.chain[1].data = "Tampered data"
    print("Is blockchain valid after tampering?", my_blockchain.is_chain_valid())
```

#### **Explanation:**
1. A new blockchain is created, starting with the genesis block.
2. Blocks are added with custom data (`"First block after genesis"`, etc.).
3. The entire blockchain is displayed using the `__repr__` method.
4. The blockchain’s integrity is validated using `is_chain_valid`.
5. Tampering is demonstrated by altering a block’s data, which invalidates the blockchain.

---

### **Key Concepts Illustrated**

1. **Block Linking**: Blocks are connected using the `previous_hash`.
2. **Immutability**: The hash ensures that altering a block's data changes its hash, breaking the chain.
3. **Integrity Check**: The `is_chain_valid` method ensures all blocks are linked correctly and no data has been altered.

By running this code, you’ll see how a basic blockchain operates and how tampering with any block breaks its integrity!
