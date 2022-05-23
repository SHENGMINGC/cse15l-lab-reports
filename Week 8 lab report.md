[Link to my repo](https://github.com/SHENGMINGC/Josh)

[Link to the repo I reviewed](https://github.com/AlexVazquez19/markdown-parser-echidnas)

# Test1
Expected output:
```
"`google.com","google.com","ucsd.edu"
```

Tester Code: 


```
@Test
public void testSnippet1() throws IOException {
    assertEquals(List.of("`google.com","google.com","ucsd.edu"),MarkdownParse.getLinks(Files.readString(Path.of("snippet-1.md"))));
}
```

My implementation:

```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:147)
```

Partner's implementation:
```
1) testSnippet1(MarkdownParseTest)
java.lang.AssertionError: expected:<[`google.com, google.com, ucsd.edu]> but was:<[url.com, `google.com, google.com]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet1(MarkdownParseTest.java:67)
```

Thoughts: I thinnk a small change can not fix this bug because it would require some meticulous casework to handle those abnormal braket behaviors. The best way, in my opinion, is to develop a general approach that can handle most edge cases. 


# Test2
Expected output:
```
"a.com","a.com(())","example.com"
```

Tester Code: 

```
@Test
public void testSnippet2() throws IOException {
    assertEquals(List.of("a.com","a.com(())","example.com"), MarkdownParse.getLinks(Files.readString(Path.of("snippet-2.md"))));
}
```

My implementation:

```
2) testSnippet2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet2(MarkdownParseTest.java:153)
```

Partner's implementation:
```
2) testSnippet2(MarkdownParseTest)
java.lang.AssertionError: expected:<[a.com, a.com(()), example.com]> but was:<[a.com((]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet2(MarkdownParseTest.java:73)
```

Thoughts: Again, both of our codes determine a link based on a wishful rule that is susceptible to bizzare cases. 
Maybe we can improve this particular bug by adding one more edge case in our codes, but we can not guarantee that our codes are bug free. 

# Test3
Expected output:
```
"https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"
```

Tester Code: 

```
@Test
public void testSnippet3() throws IOException {
    assertEquals(List.of("https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"),
    MarkdownParse.getLinks(Files.readString(Path.of("snippet-3.md"))));
}

```

My implementation:

```
3) testSnippet3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]> but was:<[
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:159)
```

Partner's implementation:
```
3) testSnippet3(MarkdownParseTest)
java.lang.AssertionError: expected:<[https://www.twitter.com, https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule, https://cse.ucsd.edu/]> but was:<[https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at MarkdownParseTest.testSnippet3(MarkdownParseTest.java:79)
```

Thoughts: The bug here is that my code returns the empty spaces along with the link when there are empty spaces between the open parentheses. This maybe the easiest bug to fix among all three, because I only need to locate those empty spaces in my if-condition and exclude them before I return the link. However, the bigger problem as mentions in Test 2 is far from solved.

