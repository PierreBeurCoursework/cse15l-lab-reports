# Lab Report 4 Week 8

[My implementation](https://github.com/PierreBeur/markdown-parse)

[The implementation I reviewed](https://github.com/ucsd-cse15l-w22/markdown-parse)

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

For your implementation, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

For the implementation you reviewed, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks? If yes, describe the code change. If not, describe why it would be a more involved change.

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

For your implementation, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

For the implementation you reviewed, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets? If yes, describe the code change. If not, describe why it would be a more involved change.

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

For your implementation, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

For the implementation you reviewed, the corresponding output when running the tests; if it passed, say so. If it didn’t pass, show the specific part of the JUnit output that shows the test failure.

Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses? If yes, describe the code change. If not, describe why it would be a more involved change.