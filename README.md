# HuffCompress using Huffman-Coding

Huffman Coding (HC) is a technique of Compressing data to reduce its size without losing any of the details. David Huffman first developed it.

HC is generally useful to compress the data in which there are frequently occurring characters.

## Running the Program

1. **Clone the repository.**
   - The repository consists of a sample text file of size 715kB.

2. **Run the Python code `useHuffman.py` to compress & decompress the given sample file.**
   - For example, open terminal and run:
     ```sh
     python3 useHuffman.py
     ```
   - The above command will perform compression and decompression on the `sample.txt` file present in the repository.
   - Both the compressed and decompressed files will be present at the same location.

3. **To run the code for compression of any other text file:**
   - Edit the `path` variable in the `useHuffman.py` file to point to the desired text file.



## Huffman Coding algorithm

1. **Create a Priority Queue `Q` consisting of each unique character.**
2. **Sort them in ascending order of their frequencies.**
3. **For all the unique characters:**
   - Create a `newNode`.
   - Extract the minimum value from `Q` and assign it to `leftChild` of `newNode`.
   - Extract the minimum value from `Q` and assign it to `rightChild` of `newNode`.
   - Calculate the sum of these two minimum values and assign it to the value of `newNode`.
   - Insert this `newNode` into the tree.

4. **Return `rootNode`.**

## How Huffman Coding works?
Suppose the string below is to be sent over a network.

![image](https://user-images.githubusercontent.com/22562694/120909515-6c09b600-c693-11eb-8a4c-1c2c2ad2537f.png)

Each character occupies 8 bits. There are a total of 15 characters in the above string. Thus, a total of 8 * 15 = 120 bits are required to send this string.

Using the Huffman Coding technique, we can compress the string to a smaller size.

Huffman coding first creates a tree using the frequencies of the character and then generates code for each character.

Once the data is encoded, it has to be decoded. Decoding is done using the same tree.

Huffman Coding prevents any ambiguity in the decoding process using the concept of prefix code ie. a code associated with a character should not be present in the prefix of any other code. The tree created above helps in maintaining the property.

## In depth Explaination

1. Calculate the frequency of each character in the string.

![image](https://user-images.githubusercontent.com/22562694/120909529-893e8480-c693-11eb-87ae-20c9c6705d6d.png)

2. Sort the characters in increasing order of the frequency. These are stored in a priority queue Q.

![image](https://user-images.githubusercontent.com/22562694/120909537-9a879100-c693-11eb-937f-9b4870c88d6d.png)

3. Make each unique character as a leaf node.

4. Create an empty node z. Assign the minimum frequency to the left child of z and assign the second minimum frequency to the right child of z. Set the value of the z as the sum of the above two minimum frequencies.

![image](https://user-images.githubusercontent.com/22562694/120909559-bc811380-c693-11eb-85a6-597f9bd4e328.png)

5. Remove these two minimum frequencies from Q and add the sum into the list of frequencies (* denote the internal nodes in the figure above).

6. Insert node z into the tree.

7. Repeat steps 3 to 5 for all the characters.

![image](https://user-images.githubusercontent.com/22562694/120909564-d1f63d80-c693-11eb-8e6a-681dc5c09441.png)



![image](https://user-images.githubusercontent.com/22562694/120909567-dae70f00-c693-11eb-874e-bda5c6e294a3.png)



8. For each non-leaf node, assign 0 to the left edge and 1 to the right edge.

![image](https://user-images.githubusercontent.com/22562694/120909576-edf9df00-c693-11eb-8d05-eb837d93a3c0.png)


For sending the above string over a network, we have to send the tree as well as the above compressed-code. The total size is given by the table below.


| Character | Frequency | Code | Size     |
|-----------|-----------|------|----------|
| A         | 5         | 11   | 5*2 = 10 |
| B         | 1         | 100  | 1*3 = 3  |
| C         | 6         | 0    | 6*1 = 6  |
| D         | 3         | 101  | 3*3 = 9  |


 

Without encoding, the total size of the string was 120 bits. After encoding the size is reduced to 32 + 15 + 28 = 75.

Decoding the code
For decoding the code, we can take the code and traverse through the tree to find the character.

Let 101 is to be decoded, we can traverse from the root as in the figure below.

![image](https://user-images.githubusercontent.com/22562694/120909632-711b3500-c694-11eb-92b6-83da3cbfb91c.png)



