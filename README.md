# Reproducer for quarkus-kafka multi-emitter bug

* Requires java 17

This is slightly modified quickstart for [kafka-avro-schema](https://github.com/quarkusio/quarkus-quickstarts/tree/main/kafka-avro-schema-quickstart).
Uses up-to-date version of quarkus - 999-SNAPSHOT.

In `MovieResource` class, there are two emitters declared.
Which should be OK, but produces exception:
```
MovieResourceTest.testHelloEndpoint » Runtime java.lang.RuntimeException: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
	[error]: Build step io.quarkus.smallrye.reactivemessaging.deployment.SmallRyeReactiveMessagingProcessor#build threw an exception: jakarta.enterprise.inject.spi.DeploymentException: Emitter configuration for channel `movies` is different than previous configuration : QuarkusEmitterConfiguration{name='movies', emitterType=io.quarkus.smallrye.reactivemessaging.runtime.EmitterFactoryForLiteral@346bfea5, overflowBufferStrategy=BUFFER, overflowBufferSize=-1, broadcast=false, numberOfSubscriberBeforeConnecting=-1}
	at io.quarkus.smallrye.reactivemessaging.deployment.SmallRyeReactiveMessagingProcessor.build(SmallRyeReactiveMessagingProcessor.java:302)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:568)
	at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:849)
	at io.quarkus.builder.BuildContext.run(BuildContext.java:256)
	at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
	at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2513)
	at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1538)
	at java.base/java.lang.Thread.run(Thread.java:840)
	at org.jboss.threads.JBossThread.run(JBossThread.java:501)
```

## How to run

- Install [quarkus](https://github.com/quarkusio/quarkus) version 999-SNAPSHOT using `mvn clean install`
- Run reproducer using `mvn clean verify`
