# hytale-ipv6-patch
A patch for Hytale Server Jar

Hytale Server dont work on Android due to access to INET6 adapter info being locked behind ROOT privilege.

So in order to launch the HytaleServer.Jar in non ROOT (SuperUser etc) Android, the IPv6 must be disabled in some way,
i tried many methods without editing the Jar file, but no success.

The file that contains the code for IPv6 implementation is: HytaleServer.jar\com\hypixel\hytale\server\core\io\transport\QUICTransport.class
After decompiling and editing the source code, i recompiled the QUICTransport.java file using Eclipse as IDE and the original HytaleServer.Jar as Lib
so all the depends are OK for recompilation.

After recompiled to a .jar file, copy all the QUICTransport .class files from the build and replace on the original HytaleServer.jar
DONE! happy Server
--------------------------------------------------------------------------------------------------------------------------------------------------------
Tested on Hytale 2026.02.19-1a311a592 Revision: 1a311a5921cb413cc899ada8941ff0b9ce1d64e1

Before using this patch be sure that its the correct solution for your situation...
How to know that this patch will fix your problem:

Find in the server log, similar to this: 
  "[io.netty.util.internal.MacAddressUtil] Failed to find a usable hardware address from the network interfaces; using random bytes:"

And also: 

"SEVERE]                 [Hytale] Unhandled exception! Thread[#48,ForkJoinPool.commonPool-worker-1,5,InnocuousForkJoinWorkerThreadGroup]
java.util.concurrent.CompletionException: io.netty.channel.ChannelException: Unable to create Channel from class class io.netty.channel.socket.nio.NioDatagramChannel
	at java.base/java.util.concurrent.CompletableFuture.wrapInCompletionException(CompletableFuture.java:323)
	at java.base/java.util.concurrent.CompletableFuture.encodeThrowable(CompletableFuture.java:359)
	at java.base/java.util.concurrent.CompletableFuture.completeThrowable(CompletableFuture.java:364)
	at java.base/java.util.concurrent.CompletableFuture$AsyncRun.run(CompletableFuture.java:1828)
	at java.base/java.util.concurrent.CompletableFuture$AsyncRun.exec(CompletableFuture.java:1817)
	at java.base/java.util.concurrent.ForkJoinTask.doExec(ForkJoinTask.java:511)
	at java.base/java.util.concurrent.ForkJoinPool$WorkQueue.topLevelExec(ForkJoinPool.java:1450)
	at java.base/java.util.concurrent.ForkJoinPool.runWorker(ForkJoinPool.java:2019)
	at java.base/java.util.concurrent.ForkJoinWorkerThread.run(ForkJoinWorkerThread.java:187)
Caused by: io.netty.channel.ChannelException: Unable to create Channel from class class io.netty.channel.socket.nio.NioDatagramChannel
	at com.hypixel.hytale.server.core.io.netty.NettyUtil$ReflectiveChannelFactory.newChannel(NettyUtil.java:275)
	at io.netty.bootstrap.AbstractBootstrap.initAndRegister(AbstractBootstrap.java:330)
	at io.netty.bootstrap.AbstractBootstrap.register(AbstractBootstrap.java:247)
	at com.hypixel.hytale.server.core.io.transport.QUICTransport.<init>(QUICTransport.java:133)
	at com.hypixel.hytale.server.core.io.ServerManager.lambda$init$0(ServerManager.java:92)
	at com.hypixel.hytale.sneakythrow.ThrowableRunnable.run(ThrowableRunnable.java:9)
	at java.base/java.util.concurrent.CompletableFuture$AsyncRun.run(CompletableFuture.java:1825)
	... 5 more
	Suppressed: java.util.concurrent.CompletionException: Rethrowing promise failure cause
		at io.netty.util.concurrent.DefaultPromise.rethrowIfFailed(DefaultPromise.java:686)
		at io.netty.util.concurrent.DefaultPromise.sync(DefaultPromise.java:420)
		at io.netty.channel.DefaultChannelPromise.sync(DefaultChannelPromise.java:119)
		at io.netty.channel.DefaultChannelPromise.sync(DefaultChannelPromise.java:30)
		... 9 more
Caused by: java.lang.reflect.InvocationTargetException
	at java.base/jdk.internal.reflect.DirectConstructorHandleAccessor.newInstance(DirectConstructorHandleAccessor.java:74)
	at java.base/java.lang.reflect.Constructor.newInstanceWithCaller(Constructor.java:499)
	at java.base/java.lang.reflect.Constructor.newInstance(Constructor.java:483)
	at com.hypixel.hytale.server.core.io.netty.NettyUtil$ReflectiveChannelFactory.newChannel(NettyUtil.java:273)
	... 11 more
Caused by: java.lang.UnsupportedOperationException: IPv6 not available
	at java.base/sun.nio.ch.DatagramChannelImpl.<init>(DatagramChannelImpl.java:190)
	at java.base/sun.nio.ch.SelectorProviderImpl.openDatagramChannel(SelectorProviderImpl.java:59)
	at io.netty.channel.socket.nio.NioDatagramChannel.newSocket(NioDatagramChannel.java:101)
	at io.netty.channel.socket.nio.NioDatagramChannel.<init>(NioDatagramChannel.java:138)
	at java.base/jdk.internal.reflect.DirectConstructorHandleAccessor.newInstance(DirectConstructorHandleAccessor.java:62)
	... 14 more"
