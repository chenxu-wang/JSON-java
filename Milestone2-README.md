### Milestone2 Assignment

Group member: Zicheng Shan, Chenxu Wang

####Two toJsonObject() methods are added in src/main/java/org.json/XML.java
1. JSONObject toJSONObject(Reader reader, JSONPointer path) (At 760 Line)
    - Extract smaller sub-objects on a certain key path
    - Main method:   
      - Traverse the tag names in the xml file according to the path given by JSONPointer until the last one. 
      - Then call the parse() function to write the subobject to the target object.
2. JSONObject toJSONObject(Reader reader, JSONPointer path, JSONObject replacement) (At 840 Line)
    - Replace a sub-object on a certain key path with another JSON object that user constructed
    - Main Method: 
      - Call toJSONObject() to convert xml to JSONObject
      - Find the target object recursively and use put method to replace sub-object

#### Unit Tests are added in src/test/java/org.json.junit/MileStone2Test.java
* The unit tests are based on the small test file which is provided in the assignment description (https://www.ics.uci.edu/~lopes/teaching/swe262p/M2Test.java).

1. For toJSONObject(Reader reader, JSONPointer path) we tested with "/contact/address/street/" and "/contact/address/nick/"
   - "/contact/address/street/" gives a certain path and should return "{\"street\":\"Ave of Nowhere\"}".
   - "/contact/address/nick/" gives a nonexistent path and should throw an exception "Misshaped element at 200 [character 10 line 9]".
   - We also tested it with a jsonArray, and all of them are passed.

2. For toJSONObject(Reader reader, JSONPointer path, JSONObject replacement) we tested with "/contact/address/street/" and "/contact/address/nick/" and replace them by "\<street>Ave of the Arts\</street>\n"
   - "/contact/address/street/" gives a certain path and should return"{\"contact\":{\"nick\":\"Crista\",\"address\":{\"zipcode\":92614,\"street\":{\"street\":\"Ave of the Arts\"}},\"name\":\"Crista Lopes\"}}".
   - "/contact/address/nick/" gives a nonexistent path and should throw an exception JSONObject[\"nick\"] not found.".
   - Both of them are passed.

   
#### Performance comparison
* Based on the average running time between in-library and outside. And their performance is better in library.
* For example, in toJSONObject(Reader reader, JSONPointer path) 
* file size: 210.4MB
  numebr of lines: 2855718
  running time: in-library = 6782250 ns; outside = 4737288375 ns

#### build script
* The built jar file is in JSON-java/build/libs/.



