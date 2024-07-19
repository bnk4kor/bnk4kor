---

# Java 11 to Java 17 Cheat Sheet

## Java 11 (September 2018)

### Local-Variable Syntax for Lambda Parameters
**Before Java 11:**
```java
(x, y) -> x + y;
```
**Java 11:**
```java
(var x, var y) -> x + y;
```

### New String Methods
- **isBlank()**: Checks if a string is empty or contains only white space.
- **lines()**: Converts a string into a stream of lines.
- **strip()**: Removes leading and trailing white space.
- **repeat(int)**: Repeats the string a given number of times.

**Example:**
```java
String str = "  Hello World  ";
System.out.println(str.isBlank()); // false
System.out.println(str.strip()); // "Hello World"
System.out.println("Java\nis\nfun".lines().collect(Collectors.toList())); // [Java, is, fun]
System.out.println("Hello".repeat(3)); // "HelloHelloHello"
```

### HTTP Client
**Before Java 11:**
```java
HttpURLConnection con = (HttpURLConnection) new URL("https://example.com").openConnection();
con.setRequestMethod("GET");
BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer content = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    content.append(inputLine);
}
in.close();
```
**Java 11:**
```java
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://example.com"))
    .build();
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

### File Methods
- **writeString(Path, CharSequence)**
- **readString(Path)**

**Example:**
```java
Path path = Paths.get("file.txt");
Files.writeString(path, "Hello, World!");
String content = Files.readString(path);
System.out.println(content); // "Hello, World!"
```

## Java 12 (March 2019)

### Switch Expressions
**Before Java 12:**
```java
int numLetters;
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        numLetters = 6;
        break;
    case TUESDAY:
        numLetters = 7;
        break;
    case THURSDAY:
    case SATURDAY:
        numLetters = 8;
        break;
    case WEDNESDAY:
        numLetters = 9;
        break;
    default:
        throw new IllegalStateException("Unexpected value: " + day);
}
```
**Java 12:**
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY -> 7;
    case THURSDAY, SATURDAY -> 8;
    case WEDNESDAY -> 9;
    default -> throw new IllegalStateException("Unexpected value: " + day);
};
```

## Java 13 (September 2019)

### Text Blocks
**Before Java 13:**
```java
String html = "<html>\n" +
    "    <body>\n" +
    "        <p>Hello, world</p>\n" +
    "    </body>\n" +
    "</html>";
```
**Java 13:**
```java
String html = """
    <html>
        <body>
            <p>Hello, world</p>
        </body>
    </html>
    """;
```

## Java 14 (March 2020)

### Helpful NullPointerExceptions
**Before Java 14:**
- Generic `NullPointerException` without detailed context.

**Java 14:**
- Provides detailed information about which variable was `null`.

### Pattern Matching for `instanceof`
**Before Java 14:**
```java
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s);
}
```
**Java 14:**
```java
if (obj instanceof String s) {
    System.out.println(s);
}
```

## Java 15 (September 2020)

### Text Blocks (Standard)
- Now officially part of the language.

## Java 16 (March 2021)

### Records
**Before Java 16:**
```java
public class Point {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() { return x; }
    public int getY() { return y; }

    @Override
    public boolean equals(Object o) { ... }
    @Override
    public int hashCode() { ... }
    @Override
    public String toString() { ... }
}
```
**Java 16:**
```java
public record Point(int x, int y) {}
```

### Stream.toList()
**Before Java 16:**
```java
List<String> list = stream.collect(Collectors.toList());
```
**Java 16:**
```java
List<String> list = stream.toList();
```

## Java 17 (September 2021)

### Sealed Classes
**Before Java 17:**
- Use interfaces and abstract classes without enforced hierarchy control.

**Java 17:**
```java
public abstract sealed class Shape 
    permits Circle, Square {
}

public final class Circle extends Shape {
    // Implementation
}

public final class Square extends Shape {
    // Implementation
}
```

### Pattern Matching for `switch`
**Before Java 17:**
```java
if (obj instanceof String) {
    String s = (String) obj;
    // use s
}
```
**Java 17:**
```java
switch (obj) {
    case Integer i -> System.out.println("int " + i);
    case Long l    -> System.out.println("long " + l);
    case Double d  -> System.out.println("double " + d);
    case String s  -> System.out.println("String " + s);
    default        -> System.out.println(obj);
}
```

---

This cheat sheet highlights the key out-of-the-box features introduced in Java 11 to Java 17, showing both the new and old ways of doing things to help developers quickly adopt these improvements.
