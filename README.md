# Java Stream API Questions with Solution

- [String Questions](#string-questions)
- [Integer Questions](#integer-questions)

## String Questions

<details>
  <summary>Count total number of characters in a string</summary>

```java
public static void main(String[] args)
{
    String str = "hello world";

    long count = str.chars().count();

    System.out.println(count);
}
```

</details>

<details>
 <summary>Convert the entire string to uppercase</summary>

```java
public static void main(String[] args)
{
    String str = "hello world";

    String upperCaseStr = str.chars()
            .mapToObj(Character::toString)
            .map(String::toUpperCase)
            .collect(Collectors.joining());

    System.out.println(upperCaseStr);
}
```

</details>

<details>
  <summary>Convert the entire string to lowercase</summary>

```java
  public static void main(String[] args)
{
    String str = "HELLO WORLD";

    String lowerCaseStr = str.chars()
            .mapToObj(Character::toString)
            .map(String::toLowerCase)
            .collect(Collectors.joining());

    System.out.println(lowerCaseStr);
}
```

</details>

<details>
  <summary>Count the number of occurrences of a specific character (e.g., 'l')</summary>

#### solution-1

```java
  public static void main(String[] args)
{
    String str = "Hello Lost World";

    long count = str.chars()
            .filter(ch -> ch == 'L' || ch == 'l')
            .count();

    System.out.println(count);
}
```

#### solution-2

```java
  public static void main(String[] args)
{
    String str = "Hello Lost World";

    long count = str.chars()
            .mapToObj(Character::toLowerCase)
            .filter(ch -> ch == 'l')
            .count();

    System.out.println(count);
}
```

</details>

<details>
<summary>Reverse the order of the characters in the string</summary>

#### solution-1

```java
public static void main(String[] args)
{
    String str = "hello world";

    String reverseStr = str.chars()
            .mapToObj(Character::toString)
            .reduce((str1, str2) -> str2 + str1)
            .orElseThrow();

    System.out.println(reverseStr);
}
```

#### solution-2

```java
public static void main(String[] args)
{
    String str = "hello world";

    String reverseStr = IntStream.range(0, str.length())
            .mapToObj(i -> String.valueOf(str.charAt(str.length() - i - 1)))
            .collect(Collectors.joining());

    System.out.println(reverseStr);
}
```

</details>

<details>
<summary>Reverse the order of the words in the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String newStr = Arrays.stream(str.split("\\s+"))
              .reduce((string, string2) -> string2 + " " + string)
              .orElseThrow();

      System.out.println(newStr);
  }
```

</details>

<details>
<summary>Reverse the characters of each word in a given string while keeping the order of words intact</summary>

```java
  public static void main(String[] args)
  {
      String str = "hello world";

      String newStr = Stream.of(str.split("\\s+"))
              .map(val -> new StringBuilder(val).reverse())
              .collect(Collectors.joining(" "));

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Replace all occurrences of a specific word with another word</summary>

```java
  public static void main(String[] args)
  {
      String str = "Banana is tasty, but some people prefer Banana pie.";

      String newStr = Stream.of(str.split("\\s+"))
              .map(val -> val.equalsIgnoreCase("Banana") ? "Apple" : val)
              .collect(Collectors.joining(" "));

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Capitalize the first character of each word in the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "The quick brown fox jumps over the lazy dog";

      String newStr = Stream.of(str.split("\\s+"))
              .map(val -> Character.toUpperCase(val.charAt(0)) + val.substring(1))
              .collect(Collectors.joining(" "));

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Remove all non-alphabetic characters from a string</summary>

```java
  public static void main(String[] args)
  {
      String str = "Th3 qu!ck br0wn f0x jump$ 0ver the l4zy d0g";

      String sanitizeStr = str.chars()
              .filter(Character::isLetter)
              .mapToObj(Character::toString)
              .collect(Collectors.joining());

      System.out.println(sanitizeStr);
  }
```

</details>

<details>
  <summary>Extract all the unique characters from the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "hello world";

      String newStr = str.chars()
              .mapToObj(Character::toString)
              .distinct().collect(Collectors.joining());

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Filter out all the vowels from the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "The quick brown fox jumps over the lazy dog";
      String vowels = "aeiou";

      String newStr = str.chars()
              .mapToObj(Character::toString)
              .filter(val -> !vowels.contains(val))
              .collect(Collectors.joining());

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Find the first non-repeating character in the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String newStr = str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
              .entrySet().stream()
              .filter(entry -> entry.getValue() == 1)
              .map(Map.Entry::getKey)
              .findFirst().orElseThrow();

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Find the all non-repeating characters in the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      List<String> map = str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
              .entrySet().stream()
              .filter(entry -> entry.getValue() == 1)
              .map(Map.Entry::getKey)
              .collect(Collectors.toList());

      System.out.println(map);
  }
```

</details>

<details>
  <summary>Group characters by their frequency of occurrence</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      Map<String, Long> map = str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

      System.out.println(map);
  }
```

</details>

<details>
  <summary>count the occurrences of each character and then sorts these characters based on their counts in ascending order</summary>

#### solution-1
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      Map<String, Long> map = str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
              .entrySet().stream()
              .sorted(Map.Entry.comparingByValue())
              .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue, (e1, e2) -> e1, LinkedHashMap::new));

      System.out.println(map);
  }
```

#### solution-2
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      Map<String, Long> map = new LinkedHashMap<>();
      str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))
              .entrySet().stream()
              .sorted(Map.Entry.comparingByValue())
              .forEachOrdered(entry -> map.put(entry.getKey(), entry.getValue()));

      System.out.println(map);
  }
```

</details>

<details>
  <summary>Split the string into an array of words</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String[] arr = Arrays.stream(str.split("\\s+"))
              .toArray(String[]::new);

      System.out.println(Arrays.toString(arr));
  }
```

</details>

<details>
  <summary>Sort the words in the string alphabetically (ascending or descending)</summary>

#### ascending
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String[] arr = Arrays.stream(str.split("\\s+"))
              .sorted()
              .toArray(String[]::new);

      System.out.println(Arrays.toString(arr));
  }
```

#### descending
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String[] arr = Arrays.stream(str.split("\\s+"))
              .sorted(Comparator.reverseOrder())
              .toArray(String[]::new);

      System.out.println(Arrays.toString(arr));
  }
```

</details>

<details>
  <summary>Filter out words with a specific length (e.g., only words with 5 letters)</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over the lazy dog";

      String[] arr = Arrays.stream(str.split("\\s+"))
              .filter(val -> val.length() == 5)
              .toArray(String[]::new);

      System.out.println(Arrays.toString(arr));
  }
```

</details>

<details>
  <summary>Find the longest or shortest word in the string</summary>

```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over a lazy dog";

      String longestWord = Arrays.stream(str.split("\\s+"))
              .max(Comparator.comparing(String::length)).orElseThrow();

      String shortestWord = Arrays.stream(str.split("\\s+"))
              .min(Comparator.comparing(String::length)).orElseThrow();

      System.out.println(longestWord);
      System.out.println(shortestWord);
  }
```

</details>

<details>
  <summary>Join all the words in the string with a specific delimiter (e.g., "-")</summary>

#### solution-1
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over a lazy dog";

      String newStr = Arrays.stream(str.split("\\s+"))
              .collect(Collectors.joining("-"));

      System.out.println(newStr);
  }
```

#### solution-2
```java
  public static void main(String[] args)
  {
      String str = "the quick brown fox jumps over a lazy dog";

      String newStr = Arrays.stream(str.split("\\s+"))
              .reduce((string, string2) -> string + "-" + string2)
              .orElseThrow();

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Print only the even-indexed characters in uppercase</summary>

```java
  public static void main(String[] args)
  {
      String str = "The quick brown fox jumps over the lazy dog";

      String newStr = IntStream.range(0, str.length())
              .filter(i -> i % 2 == 0)
              .mapToObj(str::charAt)
              .map(Character::toUpperCase)
              .map(String::valueOf)
              .collect(Collectors.joining());

      System.out.println(newStr);
  }
```

</details>

<details>
  <summary>Check if a string is a palindrome</summary>

#### solution-1
```java
  public static void main(String[] args)
  {
      String str = "level";

      boolean isPalindrome = str.chars()
              .mapToObj(Character::toString)
              .reduce((val, val2) -> val2 + val)
              .orElseThrow().equals(str);
      
      System.out.println(isPalindrome);
  }
```

#### solution-2
```java
  public static void main(String[] args)
  {
      String str = "level";

      boolean isPalindrome = IntStream.range(0, str.length() / 2)
              .noneMatch(i -> str.charAt(i) != str.charAt(str.length() - i - 1));

      System.out.println(isPalindrome);
  }
```

</details>

<details>
  <summary>Find all the substrings of a specific length (e.g., all 3-letter substrings)</summary>

```java
  public static void main(String[] args)
    {
        String str = "hellWorld";
        int subStrLength = 3;
  
        IntStream.range(0, str.length() - subStrLength + 1)
                .mapToObj(i -> str.substring(i, subStrLength + i))
                .forEach(System.out::println);
    }
```

</details>

<details>
  <summary>Map each character of "hello world" to its uppercase version</summary>

```java
  public static void main(String[] args)
  {
      String str = "helloWorld";

      Map<String, String> map = str.chars()
              .mapToObj(Character::toString)
              .collect(Collectors.toMap(
                      Function.identity(),
                      String::toUpperCase,
                      (string, string2) -> string2 // Merge function to handle duplicates (keep the first occurrence)
              ));

      System.out.println(map);
  }
```

</details>

<details>
  <summary>Calculate the average length of each word in the string</summary>

```java
    public static void main(String[] args)
    {
        String str = "the quick brown fox jumps over the lazy dog";

        System.out.println(Stream.of(str.split("\\s+"))
                .collect(Collectors.averagingInt(String::length)));
    }
```

</details>

## Integer Questions
