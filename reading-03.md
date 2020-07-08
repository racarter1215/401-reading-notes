# File and Stream I/O

### This refers to the trransfer of data either to or from a storage medium. 
##### System I/O namespaces contain types that enable reading and writing both sync and asynch on data.
##### File: Ordered and name pile of bytes that have persistent storage
##### Stream: sequence of bytes that you can use to read and write a backing store, be it a disk or harddrive memory.

#### Files and directories
###### Use System.IO to interact with these
##### Commonly used file and directory classes:

##### File - provides static methods for creating, copying, deleting, moving, and opening files, and helps create a FileStream object.

##### FileInfo - provides instance methods for creating, copying, deleting, moving, and opening files, and helps create a FileStream object.

##### Directory - provides static methods for creating, moving, and enumerating through directories and subdirectories.

##### DirectoryInfo - provides instance methods for creating, moving, and enumerating through directories and subdirectories.

##### Path - provides methods and properties for processing directory strings in a cross-platform manner.

#### Streams

##### These involve: Reading, Writing, and Seeking

##### Stream Classes:

###### FileStream – for reading and writing to a file.

###### IsolatedStorageFileStream – for reading and writing to a file in isolated storage.

###### MemoryStream – for reading and writing to memory as the backing store.

###### BufferedStream – for improving performance of read and write operations.

###### NetworkStream – for reading and writing over network sockets.

###### PipeStream – for reading and writing over anonymous and named pipes.

###### CryptoStream – for linking data streams to cryptographic transformations.

#### Readers and writers

##### Commonly used classes:

###### BinaryReader and BinaryWriter – for reading and writing primitive data types as binary values.

###### StreamReader and StreamWriter – for reading and writing characters by using an encoding value to convert the characters to and from bytes.

###### StringReader and StringWriter – for reading and writing characters to and from strings.

###### TextReader and TextWriter – serve as the abstract base classes for other readers and writers that read and write characters and strings, but not binary data.

#### Asynchronous I/O Ops

##### This link has lots of info: https://docs.microsoft.com/en-us/dotnet/standard/io/asynchronous-file-i-o

#### Compression

##### This is the process of redicing the size of files or storage. Decompression takes compressed files and makes them usable

##### Classes for compression and decompression

###### ZipArchive – for creating and retrieving entries in the zip archive.

###### ZipArchiveEntry – for representing a compressed file.

###### ZipFile – for creating, extracting, and opening a compressed package.

###### ZipFileExtensions – for creating and extracting entries in a compressed package.

###### DeflateStream – for compressing and decompressing streams using the Deflate algorithm.

###### GZipStream – for compressing and decompressing streams in gzip data format.

### How to write a Text File for a .NET app

##### With Synchronous StreamWriter (since it needs to be started with a "using" it ends with a Dispose method):

##### using System;
##### using System.IO;

##### class Program
##### {
#####     static void Main(string[] args)
#####     {

#####         // Create a string array with the lines of text
#####         string[] lines = { "First line", "Second line", "Third line" };

#####         // Set a variable to the Documents path.
#####         string docPath =
#####           Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments);

#####         // Write the string array to a new file named "WriteLines.txt".
#####         using (StreamWriter outputFile = new StreamWriter(Path.Combine(docPath, "WriteLines.txt")))
#####        {
#####             foreach (string line in lines)
#####                 outputFile.WriteLine(line);
#####         }
#####     }
##### }
##### // The example creates a file named "WriteLines.txt" with the following contents:
##### // First line
##### // Second line
##### // Third line

#### Others examples exist here: https://docs.microsoft.com/en-us/dotnet/standard/io/how-to-write-text-to-a-file

### How to: Read and write to a newly created data file

 
##### Copy
##### using System;
##### using System.IO;

##### class MyStream
##### {
#####     private const string FILE_NAME = "Test.data";

#####     public static void Main()
#####     {
#####         if (File.Exists(FILE_NAME))
#####         {
#####            Console.WriteLine($"{FILE_NAME} already exists!");
#####             return;
#####         }

#####         using (FileStream fs = new FileStream(FILE_NAME, FileMode.CreateNew))
#####         {
#####             using (BinaryWriter w = new BinaryWriter(fs))
#####             {
#####                 for (int i = 0; i < 11; i++)
#####                 {
#####                     w.Write(i);
#####                 }
#####             }
#####         }

#####         using (FileStream fs = new FileStream(FILE_NAME, FileMode.Open, FileAccess.Read))
#####         {
#####             using (BinaryReader r = new BinaryReader(fs))
#####             {
#####                 for (int i = 0; i < 11; i++)
#####                 {
#####                     Console.WriteLine(r.ReadInt32());
#####                 }
#####             }
#####         }
#####     }
##### }


##### // The example creates a file named "Test.data" and writes the integers 0 through 10 to it in binary format.
##### // It then writes the contents of Test.data to the console with each integer on a separate line.