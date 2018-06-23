# Google protobuF sample maven project

Protocol buffers are Google’s language-neutral, platform-neutral, extensible mechanism for serializing structured data – think XML, but smaller, faster, and simpler. You define how you want your data to be structured once, then you can use special generated source code to easily write and read your structured data to and from a variety of data streams and using a variety of languages.

To serialize/deserialize any object , this is one best format. We first define a metadata of the object in a .proto file and then with corresponding java object that are generated from this proto file, we can serialize/deseailze a object.

Follow below 3 steps ..

1> pom.xml
```XML
<phase>generate-sources</phase>
<goals>
<goal>run</goal>
</goals>
<configuration>
<protocVersion>2.6.1</protocVersion> <!– 2.4.1, 2.5.0, 2.6.1, 3.2.0 –>
<inputDirectories>
<include>src/main/proto</include>
</inputDirectories>
<cleanOutputFolder>false</cleanOutputFolder>
</configuration>
</execution>
</executions>
</plugin>
</plugins>
</build>
```
2>  Now create a file   in src/main/proto/addressbook.proto , with following contents.

```proto
syntax = “proto2”;
   
   package tutorial;
   
   option java_package = “com.example.tutorial”;
   option java_outer_classname = “AddressBookProtos”;
   
   message Person {
   required string name = 1;
   required int32 id = 2;
   optional string email = 3;
   
   enum PhoneType {
   MOBILE = 0;
   HOME = 1;
   WORK = 2;
   }
   
   message PhoneNumber {
   required string number = 1;
   optional PhoneType type = 2 [default = HOME];
   }
   
   repeated PhoneNumber phones = 4;
   }
   
   message AddressBook {
   repeated Person people = 1;
   }
```
With above file, mvn clean install will created corresponding java POJO file for above meta information.

3> Now time is for testing. We have two files AddPerson.java which will add a person object and serialize it and ListPeople.java to read from file and list it in output.

