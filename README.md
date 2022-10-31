Upon building the jar using `mvn clean package -DskipTests=true`<br/> and running the jar via `flink run target/myproject-0.1.jar`, I see the following error:

```java
 The program finished with the following exception:

org.apache.flink.client.program.ProgramInvocationException: The main method caused an error: Failed to execute job 'Flink Java API Skeleton'.
        at org.apache.flink.client.program.PackagedProgram.callMainMethod(PackagedProgram.java:372)
        at org.apache.flink.client.program.PackagedProgram.invokeInteractiveModeForExecution(PackagedProgram.java:222)
        at org.apache.flink.client.ClientUtils.executeProgram(ClientUtils.java:114)
        at org.apache.flink.client.cli.CliFrontend.executeProgram(CliFrontend.java:836)
        at org.apache.flink.client.cli.CliFrontend.run(CliFrontend.java:247)
        at org.apache.flink.client.cli.CliFrontend.parseAndRun(CliFrontend.java:1078)
        at org.apache.flink.client.cli.CliFrontend.lambda$main$10(CliFrontend.java:1156)
        at org.apache.flink.runtime.security.contexts.NoOpSecurityContext.runSecured(NoOpSecurityContext.java:28)
        at org.apache.flink.client.cli.CliFrontend.main(CliFrontend.java:1156)
Caused by: org.apache.flink.util.FlinkException: Failed to execute job 'Flink Java API Skeleton'.
        at org.apache.flink.streaming.api.environment.StreamExecutionEnvironment.executeAsync(StreamExecutionEnvironment.java:2108)
        at org.apache.flink.client.program.StreamContextEnvironment.executeAsync(StreamContextEnvironment.java:188)
        at org.apache.flink.client.program.StreamContextEnvironment.execute(StreamContextEnvironment.java:119)
        at org.apache.flink.streaming.api.environment.StreamExecutionEnvironment.execute(StreamExecutionEnvironment.java:1969)
        at org.flink.myproject.DataStreamJob.main(DataStreamJob.java:100)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:566)
        at org.apache.flink.client.program.PackagedProgram.callMainMethod(PackagedProgram.java:355)
        ... 8 more
Caused by: java.lang.RuntimeException: org.apache.flink.runtime.client.JobInitializationException: Could not start the JobMaster.
        at org.apache.flink.util.ExceptionUtils.rethrow(ExceptionUtils.java:319)
        at org.apache.flink.util.function.FunctionUtils.lambda$uncheckedFunction$2(FunctionUtils.java:75)
        at java.base/java.util.concurrent.CompletableFuture$UniApply.tryFire(CompletableFuture.java:642)
        at java.base/java.util.concurrent.CompletableFuture$Completion.exec(CompletableFuture.java:479)
        at java.base/java.util.concurrent.ForkJoinTask.doExec(ForkJoinTask.java:290)
        at java.base/java.util.concurrent.ForkJoinPool$WorkQueue.topLevelExec(ForkJoinPool.java:1020)
        at java.base/java.util.concurrent.ForkJoinPool.scan(ForkJoinPool.java:1656)
        at java.base/java.util.concurrent.ForkJoinPool.runWorker(ForkJoinPool.java:1594)
        at java.base/java.util.concurrent.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:183)
Caused by: org.apache.flink.runtime.client.JobInitializationException: Could not start the JobMaster.
        at org.apache.flink.runtime.jobmaster.DefaultJobMasterServiceProcess.lambda$new$0(DefaultJobMasterServiceProcess.java:97)
        at java.base/java.util.concurrent.CompletableFuture.uniWhenComplete(Unknown Source)
        at java.base/java.util.concurrent.CompletableFuture$UniWhenComplete.tryFire(Unknown Source)
        at java.base/java.util.concurrent.CompletableFuture.postComplete(Unknown Source)
        at java.base/java.util.concurrent.CompletableFuture$AsyncSupply.run(Unknown Source)
        at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source)
        at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source)
        at java.base/java.lang.Thread.run(Unknown Source)
Caused by: java.util.concurrent.CompletionException: java.lang.RuntimeException: org.apache.flink.runtime.JobException: Cannot instantiate the coordinator for operator Source: kafka-datasource
        at java.base/java.util.concurrent.CompletableFuture.encodeThrowable(Unknown Source)
        at java.base/java.util.concurrent.CompletableFuture.completeThrowable(Unknown Source)
        ... 4 more
Caused by: java.lang.RuntimeException: org.apache.flink.runtime.JobException: Cannot instantiate the coordinator for operator Source: kafka-datasource
        at org.apache.flink.util.ExceptionUtils.rethrow(ExceptionUtils.java:319)
        at org.apache.flink.util.function.FunctionUtils.lambda$uncheckedSupplier$4(FunctionUtils.java:114)
        ... 4 more
Caused by: org.apache.flink.runtime.JobException: Cannot instantiate the coordinator for operator Source: kafka-datasource
        at org.apache.flink.runtime.executiongraph.ExecutionJobVertex.initialize(ExecutionJobVertex.java:229)
        at org.apache.flink.runtime.executiongraph.DefaultExecutionGraph.initializeJobVertex(DefaultExecutionGraph.java:849)
        at org.apache.flink.runtime.executiongraph.DefaultExecutionGraph.initializeJobVertices(DefaultExecutionGraph.java:839)
        at org.apache.flink.runtime.executiongraph.DefaultExecutionGraph.attachJobGraph(DefaultExecutionGraph.java:798)
        at org.apache.flink.runtime.executiongraph.DefaultExecutionGraph.attachJobGraph(DefaultExecutionGraph.java:780)
        at org.apache.flink.runtime.executiongraph.DefaultExecutionGraphBuilder.buildGraph(DefaultExecutionGraphBuilder.java:194)
        at org.apache.flink.runtime.scheduler.DefaultExecutionGraphFactory.createAndRestoreExecutionGraph(DefaultExecutionGraphFactory.java:149)
        at org.apache.flink.runtime.scheduler.SchedulerBase.createAndRestoreExecutionGraph(SchedulerBase.java:363)
        at org.apache.flink.runtime.scheduler.SchedulerBase.<init>(SchedulerBase.java:208)
        at org.apache.flink.runtime.scheduler.DefaultScheduler.<init>(DefaultScheduler.java:191)
        at org.apache.flink.runtime.scheduler.DefaultScheduler.<init>(DefaultScheduler.java:139)
        at org.apache.flink.runtime.scheduler.DefaultSchedulerFactory.createInstance(DefaultSchedulerFactory.java:135)
        at org.apache.flink.runtime.jobmaster.DefaultSlotPoolServiceSchedulerFactory.createScheduler(DefaultSlotPoolServiceSchedulerFactory.java:115)
        at org.apache.flink.runtime.jobmaster.JobMaster.createScheduler(JobMaster.java:345)
        at org.apache.flink.runtime.jobmaster.JobMaster.<init>(JobMaster.java:322)
        at org.apache.flink.runtime.jobmaster.factories.DefaultJobMasterServiceFactory.internalCreateJobMasterService(DefaultJobMasterServiceFactory.java:106)
        at org.apache.flink.runtime.jobmaster.factories.DefaultJobMasterServiceFactory.lambda$createJobMasterService$0(DefaultJobMasterServiceFactory.java:94)
        at org.apache.flink.util.function.FunctionUtils.lambda$uncheckedSupplier$4(FunctionUtils.java:112)
        ... 4 more
Caused by: java.lang.ClassCastException: cannot assign instance of org.apache.kafka.clients.consumer.OffsetResetStrategy to field org.apache.flink.connector.kafka.source.enumerator.initializer.ReaderHandledOffsetsInitializer.offsetResetStrategy of type org.apache.kafka.clients.consumer.OffsetResetStrategy in instance of org.apache.flink.connector.kafka.source.enumerator.initializer.ReaderHandledOffsetsInitializer
        at java.base/java.io.ObjectStreamClass$FieldReflector.setObjFieldValues(Unknown Source)
        at java.base/java.io.ObjectStreamClass$FieldReflector.checkObjectFieldValueTypes(Unknown Source)
        at java.base/java.io.ObjectStreamClass.checkObjFieldValueTypes(Unknown Source)
        at java.base/java.io.ObjectInputStream.defaultCheckFieldValues(Unknown Source)
        at java.base/java.io.ObjectInputStream.readSerialData(Unknown Source)
        at java.base/java.io.ObjectInputStream.readOrdinaryObject(Unknown Source)
        at java.base/java.io.ObjectInputStream.readObject0(Unknown Source)
        at java.base/java.io.ObjectInputStream.defaultReadFields(Unknown Source)
        at java.base/java.io.ObjectInputStream.readSerialData(Unknown Source)
        at java.base/java.io.ObjectInputStream.readOrdinaryObject(Unknown Source)
        at java.base/java.io.ObjectInputStream.readObject0(Unknown Source)
        at java.base/java.io.ObjectInputStream.defaultReadFields(Unknown Source)
        at java.base/java.io.ObjectInputStream.readSerialData(Unknown Source)
        at java.base/java.io.ObjectInputStream.readOrdinaryObject(Unknown Source)
        at java.base/java.io.ObjectInputStream.readObject0(Unknown Source)
        at java.base/java.io.ObjectInputStream.readObject(Unknown Source)
        at java.base/java.io.ObjectInputStream.readObject(Unknown Source)
        at org.apache.flink.util.InstantiationUtil.deserializeObject(InstantiationUtil.java:617)
        at org.apache.flink.util.InstantiationUtil.deserializeObject(InstantiationUtil.java:602)
        at org.apache.flink.util.InstantiationUtil.deserializeObject(InstantiationUtil.java:589)
        at org.apache.flink.util.SerializedValue.deserializeValue(SerializedValue.java:67)
        at org.apache.flink.runtime.operators.coordination.OperatorCoordinatorHolder.create(OperatorCoordinatorHolder.java:433)
        at org.apache.flink.runtime.executiongraph.ExecutionJobVertex.initialize(ExecutionJobVertex.java:223)
        ... 21 more

```

A similar issue is logged to [stackoverflow](https://stackoverflow.com/questions/72266646/flink-application-classcastexception).<br/>

As per the docs: <br/>
>
> However, there are cases when the inverted classloading causes problems (=
see below, =E2=80=9CX cannot be cast to X=E2=80=9D). For user code classloa=
ding, you can revert back to Java=E2=80=99s default mode by configuring the=
ClassLoader resolution order via classloader.resolve-order in the Flink co=
nfig to parent-first (from Flink=E2=80=99s default child-first).

Have added the config as follows:
```java
Configuration configuration = new Configuration();
configuration.set(CLASSLOADER_RESOLVE_ORDER,"parent-first");
final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment(configuration);
```
Still seeing the job fail due to the aforementioned class cast issue.