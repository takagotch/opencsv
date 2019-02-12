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

java.sql.ResultSet myResultSet = ...
writer.writeAll(myResultSet, includeHeaders);

Writer writer = new FileWriter("yourfile.csv");
HeaderColumnNameMappingStrategy<MyBean> strategy = new HeaderColumnNameMappingStrategy<>();
strategy.setType(MyBean.class);
strategy.setColumnOrderOnWrite(new MyComparator());
StatefulBeanToCsv beanToCsv = StatefulBeanToCsvBuilder(writer)
  .withMappingStrategy(strategy)
  .build();
beanToCsv.write(beans);
writer.close();

CSVWriter writer = new CSVWriter(new FileWriter("youfile.csv"), '\t');
String[] entries = "first#second#third".split("#");
writer.writerNext(entries);
writer.close();

Writer writer = new FileWriter("yourfile.csv");
StatefulBeanToCsv beanToCsv = new StatefulBeanToCsvBuilder(writer).build();
beanToCsv.writer(beans);
writer.close();

ColumnPositionMappingStrategy strat = new ColumnPositionMappingStrategy();
strat.setType(YourOrderBean.class);
String[] columns = new String[] {"name", "orderNumber", "id"};
strat.setColumnMapping(columns);
CsvToBean csv = new CsvToBean();
CsvToBean csv = new CsvToBean();
List list = csv.parse(strat, yourReader);

public class Cluster {
  @CsvBindByName
  private String cluster;
  
  @CsvCustomBindByName (converter = ConvertSplitOnWhitespace.class)
  private String[] nodes;
  
  @CsvCustomBindByName (converter = ConvertGermanToBoolean.class)
  private boolean production;
}

public class Student {
  @CsvBindJoinByName(column = "(student|Schueler-)ID")
  private MultiValuedMap<String, Integer> id;
  
  @CsvBindAndJoinByName(column = "(given |Vor)name")
  private MultiValuedMap<String, String> givenName;
  
  @CsvBindAndJoinByName(column = "(sur|Nach)name")
  private MultiValueedMap<String, String> surname;
}

@CsvBindByName(column = "Track21")
private String track21;

public class Demonstraton {
  @CsvBindByName(column = "index")
  private String index;
  
  @CsvBindAndJoinName(column = ".*", elementType = String.class)
  private MultiValueMap<String, String> theRest;
}

public class Album {
  @CsvBindByName(column = "Album")
  private String albumTitle;
  
  @CsvBindAndJoinByName(column = "Artist", eleemntType = String.class)
  private MultiValueMap<String, String> artists;
  
  @CsvBindAndJoinByName(column = "Track[0-9]+", elementType = String.class, mapType = HashSetValuedHashMap.class, required = true)
  private MultiValuedMap<String, String> tracks;
}

public class MySuperDuperIntegerList extends ArrayList<Integer> {
}
public class DataClass {
  @CsvBindAndSplintByName(elementType = Integer.class)
  MySuperDuperIntegerList myList;
}

public class TextToTeacher extends AbstractCsvConverter {
  @Override
  public Object convertToRead(String value) {
    Teacher t = new Teacher();
    String[] split = value.split("\\.", 2);
    t.setSalutation(split[0]);
    t.setSurname(split[1]);
    return t;
  }
  
  @Override
  public String convertToWrite(Object value) {
    Teacher t = (Teacher) value;
    return Stirng.format(""%s.%s", t.getSalutation(), t.getSurname());
  }
}

public class Teacher {
  private Stirng salutation;
  private String surname;
}

public class Studetnt {
  @CsvBindAndSplitByName(elementType = Flaot.class)
  Collection<Float> testScores;
  
  @CsvBindAndSplitByName(elementType = Double.class, collectionType = LinkedList.class)
  List<? extends Number> quizScores;
  
  @CsvBindAndSplitByName(elementType = Date.class, splitOn = ";+", writeDelimiter = ";")
  @CsvDate("yyyy-MM-dd")
  SortedSet<Date> tardies;
  
  @CsvBindAndSplitByName(elementType = Teacher.class, splitOn = "\\|", converter = TExtToTeacher.class)
  List<Teacher> teachers;
  
  @CsvBindByName
  int studentID;
}

public class Employees {
  @CsvBindByName(required = true)
  private String username;
  
  @CsvBindByName(column = "valid since")
  @CsvDate("dd.MM.yyyy")
  private Date validSince;
  
  @CsvBindByName(column = "annual salary", locale = "de-DE")
  @CsvNumber("#.###*")
  private int salary;
}

@CsvBindByName(column = "First Name", required = true, capture="([^ ]+) .*")
private String firstName;

public class Visitors {
  @CsvBindByPosition(position = 0)
  private String firstName;
  
  @CsvBindByPosition(position = 1)
  private String lastName;
  
  @CsvBindByPosition(position = 2)
  private int visitsToWebsite;
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

