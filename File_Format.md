# File Formats

![image](https://user-images.githubusercontent.com/32897934/124364130-14904300-dc5d-11eb-9729-6a43769ae204.png)

`* Row-oriented:`

![image](https://user-images.githubusercontent.com/32897934/124364651-7c945880-dc60-11eb-9685-cca315c0bca8.png)

  - Row-oriented storage is suitable for situations where the entire row of data needs to be processed simultaneously.
  - In this way, if only a small amount of data of the row needs to be accessed, the entire row needs to be read into the memory. 
  - Eg: SequenceFile, MapFile, Avro Datafile. 
  
  ![image](https://user-images.githubusercontent.com/32897934/124364866-ebbe7c80-dc61-11eb-8ee4-f5a7f250d6c4.png)


`* Column-oriented:`

![image](https://user-images.githubusercontent.com/32897934/124364658-8918b100-dc60-11eb-88a8-999496f689c8.png)

  - The entire file cut into several columns of data, and each column of data stored together:
  - Eg: Parquet, RCFile, ORCFile. 
  - The column-oriented format makes it possible to skip unneeded columns when reading data, suitable for situations where only a small portion of the rows are in the field.

![image](https://user-images.githubusercontent.com/32897934/124364872-f547e480-dc61-11eb-8ec3-32d9dc50b449.png)

`* Sequence File`

![image](https://user-images.githubusercontent.com/32897934/124364682-b9f8e600-dc60-11eb-80c5-14e2390d8c02.png)

  - The storage format differs depending on whether it is compressed, and whether it uses record compression or block compression

   **No compression:** 
   Store in order according to record length, Key length, Value degree, Key value, and Value value. The range is the number of bytes. Serialization is performed using the specified Serialization.
   **Record compression:**
   Only the value is compressed, and the compressed codec stored in the header.
   **Block compression:**
   Multiple records are compressed together to take advantage of the similarities between records and save space. The synchronization flag is added before and after the block. The minimum value of the block is io.seqfile.compress.blocksizeset by the attribute.
   
![image](https://user-images.githubusercontent.com/32897934/124364721-fb899100-dc60-11eb-9fe3-cf6c3f2f9250.png)

`* Map File`

  - MapFile is a variant of SequenceFile. 
  - It is MapFile after adding an index to SequenceFile and sorting it. 
  - The index is stored as a separate file, typically storing an index for every 128 records. 

    ```
    Derived type of MapFile
    **SetFile ** 
    A special MapFile for storing a sequence of keys of type Writable. Key is written in order.
    **ArrayFile: **
    Key is an integer representing the position in the array, and value is Writable.
    **BloomMapFile: **
    Optimized for the MapFile get() method using dynamic Bloom filters. The filter stored in memory, and only when the key value exists, the regular get() method is called to perform the read operation.
    ```

`* RC File`

![image](https://user-images.githubusercontent.com/32897934/124364852-c0d42880-dc61-11eb-9323-625c4cfaa99f.png)

Hive’s Record Columnar File, this type of file first divides the data into Row Group by row, and inside the Row Group, the data is stored in columns.

`* ORC File`

ORCFile (Optimized Record Columnar File) provides a more efficient file format than RCFile. It internally divides the data into Stripe with a default size of 250M. Each stripe includes an index, data, and Footer. The index stores the maximum and minimum values ​​of each column, as well as the position of each row in the column.
![image](https://user-images.githubusercontent.com/32897934/124364899-19a3c100-dc62-11eb-9c54-b2fafcf36038.png)

`* Parquet`

A generic column-oriented storage format based on Google’s Dremel. Especially good at handling deeply nested data.

![image](https://user-images.githubusercontent.com/32897934/124364921-6091b680-dc62-11eb-9f78-9cb580120d11.png)

![image](https://user-images.githubusercontent.com/32897934/124364927-69828800-dc62-11eb-9f43-9e6d2bccd4f1.png)

For nested structures, Parquet converts it into a flat column store, which is represented by Repeat Level and Definition Level (R and D) and uses metadata to reconstruct the record when reading the data to rebuild the entire file. Structure. 




# Serialization

![image](https://user-images.githubusercontent.com/32897934/124365130-a438f000-dc63-11eb-800e-f3f09c7ae087.png)
![image](https://user-images.githubusercontent.com/32897934/124365171-e4986e00-dc63-11eb-9bb0-3ce4886da20c.png)


 - Data serialization is a process that converts structure data manually back to the original form.
 - Serialize to translate data structures into a stream of data. Transmit this stream of data over the network or store it in DB regardless of the system architecture.
 - Isn't storing information in binary form or stream of bytes is the right approach.
 - Serialization does the same but isn't dependent on architecture.
 - Consider CSV files contains a comma (,) in between data, so while Deserialization, wrong outputs may occur. Now, if metadata is stored in XML form, a self- architected form of data storage, data can easily deserialize.
