# hello-kafka - Hello World Kafka example

# EXAMPLE

```
$ docker-machine ip default
192.168.99.100
$ cd kafka-docker/
$ vi docker-compose.xml docker-compose-single-broker.yml
(Update KAFKA_ADVERTISED_HOST_NAME to match output of docker-machine ip default)
$ docker-compose up
...

$ cd hello-kafka/
$ gradle cucumber
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:jar
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:compileCucumberJava
:processCucumberResources
:cucumberClasses
:cucumber
Feature: Kafka integration
  Scenario: Hello World kafka                                                                           # kafka.feature:2
    #  docker-compose ip default
    Given kafka cluster has kafka nodes "192.168.99.100:9092" and zookeeper nodes "192.168.99.100:2181" # StepDefinitions.kafkaClusterHasNodesAndZookeeperNodes(String,String)
    When a producer sends a message to "topic-test"                                                     # StepDefinitions.aProducerSendsAMessageTo(String)
    Then a consumer receives a message from "topic-test" in group "group-test"                          # StepDefinitions.aConsumerReceivesAMessageFromInGroup(String,String)

1 Scenarios (1 passed)
3 Steps (3 passed)
0m0.893s


BUILD SUCCESSFUL

Total time: 2.67 secs
```

# REQUIREMENTS

* [Kafka](http://kafka.apache.org/) 0.8+ (e.g. https://github.com/mcandre/docker-kafka)
* [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 1.8+
* [gradle](http://gradle.org/) 2.7+

## Optional

* [Sonar](http://www.sonarqube.org/)
* [Infer](http://fbinfer.com/)
* [editorconfig-cli](https://github.com/amyboyd/editorconfig-cli) (e.g. `go get github.com/amyboyd/editorconfig-cli`)
* [flcl](https://github.com/mcandre/flcl) (e.g. `go get github.com/mcandre/flcl/...`)

# JAVADOCS

```
$ gradle javadoc
$ open build/docs/javadoc/index.html
```

# TEST + CODE COVERAGE

```
$ gradle test jacoco
$ open build/reports/jacoco/test/html/index.html
```

# LINTING

```
$ gradle check

```

## Optional: FindBugs

```
$ gradle check
$ open build/reports/findbugs/main.html
```

## Optional: Sonar

```
$ sonar start
$ gradle check sonar
$ open http://localhost:9000/
```

## Optional: Infer

```
$ infer -- gradle clean build
```

# Advanced Topics

For Kafka Connect examples, see https://github.com/mcandre/hello-kafka-connect
