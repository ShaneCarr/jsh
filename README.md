Jshell with External Libraries
@see https://github.com/johnpoth/jshell-maven-plugin

## Install

```bash
$ git clone git@github.com:appkr/jsh
$ cd jsh
~/jsh $ mvn package
```

## Run

```bash
~/jsh $ mvn jshell:run
```

## Example

```bash
$ jsh
jshell> import com.fasterxml.jackson.databind.*;

jshell> var om = new ObjectMapper();
om ==> com.fasterxml.jackson.databind.ObjectMapper@6b57696f

jshell> var list = new ArrayList<String>(Arrays.asList("foo", "bar")) 
list ==> [foo, bar]

jshell> om.writeValueAsString(list);
$4 ==> "[\"foo\",\"bar\"]"

jshell> import org.apache.commons.lang3.RandomStringUtils;

jshell> RandomStringUtils.randomAlphanumeric(11)
$6 ==> "RJsQrNWp1pp"
```

## Add dependency and make it runnable in jshell

```xml
<!--pom.xml-->
  <dependencies>
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.11</version>
    </dependency>
    <!--...-->
  </dependencies>
```

```java
// startup.jsh
import org.apache.commons.lang3.*;
import com.fasterxml.jackson.databind.*;
```

```bash
~/jsh $ mvn package
~/jsh $ mvn jshell:run -Djshell.scripts="startup.jsh"
```


## example

```bash

jshell> public record Group(String description, String displayName, Boolean mailEnabled, String mailNickname, Boolean securityEnabled) implements Serializable { }
|  created record Group
jshell> import com.fasterxml.jackson.databind.*;
jshell> var om = new ObjectMapper();
om ==> com.fasterxml.jackson.databind.ObjectMapper@1a968a59
jshell> Group g = new Group("desc", "name", true, "nick", false)
g ==> Group[description=desc, displayName=name, mailEna ... ck, securityEnabled=false]
jshell> g
g ==> Group[description=desc, displayName=name, mailEnabled=true, mailNickname=nick, securityEnabled=false]
jshell> g
g ==> Group[description=desc, displayName=name, mailEnabled=true, mailNickname=nick, securityEnabled=false]
jshell> om.write
writeTree(                         writeValue(                        writeValueAsBytes(                 writeValueAsString(                writer(                            writerFor(                         writerWithDefaultPrettyPrinter()
writerWithType(                    writerWithView(
jshell> om.writeValueAs
writeValueAsBytes(    writeValueAsString(
jshell> om.writeValueAsString(g)
$7 ==> "{\"description\":\"desc\",\"displayName\":\"name\",\"mailEnabled\":true,\"mailNickname\":\"nick\",\"securityEnabled\":false}"

jshell>
```