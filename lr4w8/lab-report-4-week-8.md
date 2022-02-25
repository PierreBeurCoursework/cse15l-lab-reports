# Lab Report 4 Week 8

For each snippet, a test was added both to [my implementation](https://github.com/PierreBeur/markdown-parse) of markdown-parse, and [the implementation I reviewed](https://github.com/ucsd-cse15l-w22/markdown-parse). What each test should produce was decided by using the VScode preview.


## Snippet 1

```java
@Test
public void testSnippet1() {
    ArrayList<String> actual = MarkdownParse.getLinks(
        "`[a link`](url.com)\n\n"+
        "[another link](`google.com)`\n\n"+
        "[`cod[e`](google.com)\n\n"+
        "[`code]`](ucsd.edu)"
    );
    List<String> expected = List.of("`google.com", "google.com", "ucsd.edu");
    assertEquals(expected, actual);
}
```

The JUnit output shows that the test failed when running the tests for my implementation:

```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com, ucsd.edu]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:28)
```

The JUnit output shows that the test failed when running the tests for the implementation I reviewed:

```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com, ucsd.edu]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:21)
```

A small code change that would make my program work for snippet 1 and all related cases that use inline code with backticks would be to disregard otherwise valid links whose opening bracket is within a region encapsulated by backticks.

## Snippet 2

```java
@Test
public void testSnippet2() {
    ArrayList<String> actual = MarkdownParse.getLinks(
        "[a [nested link](a.com)](b.com)\n\n"+
        "[a nested parenthesized url](a.com(()))\n\n"+
        "[some escaped \\[ brackets \\]](example.com)"
    );
    List<String> expected = List.of("a.com", "a.com(())", "example.com");
    assertEquals(expected, actual);
}
```

The JUnit output shows that the test failed when running the tests for my implementation:

```
2) testSnippet2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com, a.com((, example.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet2(MarkdownParseTest.java:39)
```

The test passed when running the tests for the implementation I reviewed.

A small code change that would make my program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets would be to add a method which loops with a stack to find a matching closing character given the index of an opening character.

## Snippet 3

```java
@Test
public void testSnippet3() {
    ArrayList<String> actual = MarkdownParse.getLinks(
        "[this title text is really long and takes up more than \n"+
        "one line\n\n"+
        "and has some line breaks](\n"+
        "    https://www.twitter.com\n"+
        ")\n\n"+
        "[this title text is really long and takes up more than \n"+
        "one line](\n"+
        "    https://ucsd-cse15l-w22.github.io/\n"+
        ")\n\n\n"+
        "[this link doesn't have a closing parenthesis](github.com\n\n"+
        "And there's still some more text after that.\n\n"+
        "[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/\n\n\n\n"+
        ")\n\n"+
        "And then there's more text"
    );
    List<String> expected = List.of("https://ucsd-cse15l-w22.github.io/");
    assertEquals(expected, actual);
}
```

The JUnit output shows that the test failed when running the tests for my implementation:

```
3) testSnippet3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://ucsd-cse15l-w22.github.io/]> but was:<[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:61)
```

The JUnit output shows that the test failed when running the tests for the implementation I reviewed:

```
2) testSnippet3(MarkdownParseTest)
java.lang.StringIndexOutOfBoundsException: String index out of range: 452
        at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:48)
        at java.base/java.lang.String.charAt(String.java:711)
        at MarkdownParse.findCloseParen(MarkdownParse.java:14)
        at MarkdownParse.getLinks(MarkdownParse.java:36)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:37)
```

A small code change that would make my program work for snippet 3 and all related cases that have newlines in brackets and parentheses would be to disregard links which have newline characters in brackets.