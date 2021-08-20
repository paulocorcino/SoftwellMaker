**javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)
Using TLS receive a Handshake failure with the error No appropriate protocol**

SYMPTOM

```
Root Exception stack trace:
javax.net.ssl.SSLHandshakeException: No appropriate protocol (protocol is disabled or cipher suites are inappropriate)
at sun.security.ssl.Handshaker.activate(Handshaker.java:503)
at sun.security.ssl.SSLSocketImpl.kickstartHandshake(SSLSocketImpl.java:1482)
at sun.security.ssl.SSLSocketImpl.performInitialHandshake(SSLSocketImpl.java:1351)
+ 3 more (set debug level logging or '-Dmule.verbose.exceptions=true' for everything)
```

CAUSE
It is a possible problem due to missed AES 256 ciphers on java.

SOLUTION

Please perform the following actions to resolve this issue (the instructions listed here assumes that you are using JDK 8):
Download the JCE file from Java's official website, and unzip the file, and you should see the JCE jars.
Go to your JDK installation directory, and you should find your current JCE jars in $JAVA_HOME/jre/lib/security.
Backup the JCE jars to a different location.
Remove the current JCE jars and replace it with the JCE jars which you just downloaded.
Restart your Java/Runtime. If you are using Studio to run your application, you may need to restart your Studio so that the JVM will pick up the new JCE jars.

At same folder edit file java.security and locate parameter ``jdk.tls.disabledAlgorithms`` remove their attribute the values ``TLSv1, TLSv1.1``.

