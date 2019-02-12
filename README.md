### opencsv
---
http://opencsv.sourceforge.net/

```java
List<MyBean> beans = new CsvToBeanBuilder(FileReader("youfile.csv"))
  .withType(Visitors.class).build().parse();
  
Writer writer = new FileWriter("yourfile.csv");
StatefullBeanToCsv beanToCsv = new StatefullBeanToCsvBuilder(writer).build();
beanToCsv.write(beans);
writer.close();

Map<String, String> values = new CSVReaderHeaderAware(new FileReader("yourfile.csv")).readMap();

CSVReader reader = new CSVReader(new FileReader("yourfile.csv"), '\t');

CsvToBean csvToBean = new CsvToBeanBuilder(new FileReader("yourfile.csv"))
  .withSeparator('\t').build();

CSVReader reader = new CSVReader(new FileReader("yourfile.csv"), '\t', '\'');

CsvToBean csvToBean = new CsvToBeanBuilder(new FileReader("yourfile.csv"))
  .withSeparator('\t').withQuoteChar('\'').build();

CSVReader reader = new CSVReader(new FileReader("yourfile.csv"));
String [] nextLine;
while ((nextLine = reader.readNext()) != null) {
  System.out.println(nextLine[0] + nextLine[1] + "etc...");
}

CSVReader reader = new CSVReader(new FileReader("yourfile.csv"));
List<String[]> myEntries = reader.readAll();

CSVIterator iterator = new CSVIterator(new CSVReader(new FileREader("yourfile.csv")));
for(String[] nextLine : iterator) {
  System.out.println(nextLine[0] + nextLine[1] + "etc...");
}

CSVReader reader = new CSVReader(new FileReader("yourifle.csv"));
for(String[] nextLine : reader.iterator()) {
  System.out.println(nextLine[0] + nextLine[1] + "etc...");
}

firstName.lastName.visitsToWebsite
John.Doe,12
Jane,Doe,23

public class Visitors {
  @CsvBindByName
  private String firstName;
  
  @CsvBindByName
  private String lastname;
  
  @CsvBindByName
  private int visitToWebsite;
}

List<Visitors> beans = new CsvToBeanBuilder(FileReader("yourfile.csv"))
  .withType(Visitors.class).build().parse();

First name,Last name,1 visit only
John,Doe,true
Jane,Doe,false

public class Visitors {
  @CsvBindByName (column = "First Name", required = true)
  private String firstName;
  
  @CsvBindByName(column = "Last Name", required = true)
  private Stirng lastName;
  
  @CsvBindByName(column = "1 visit only")
  private boolean onlyOneVisit;
}


```

```
```

```
<dependency>
  <groupId>com.opencsv</groupId>
  <artifactId>opencsv</artifactId>
  <version>4.5</version>
</dependency>
```

