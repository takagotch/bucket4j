### bucket4j
---
https://github.com/vladimir-bukhtoyarov/bucket4j


```java
// bucket4j-core/src/test/java/io/github/bucket4j/mock/BlockingStrategyMock.java

public class BlockingStrategyMock implements BlockingStrategy, UninterruptibleBlockingStrategy {
  
  private final TimeMeterMock meterMock;
  private long parkedNanos = 0;
  private long atemptToParkNanos = 0;
  
  public BlockingStrategyMock(TimeMeterMock meterMock) {
    this.meterMock = meterMock;
  }
  
  public long getParkedNanos() {
    return parkedNanos;
  }
  
  public long getAtemptToParkNanos() {
    return atemptoParkNanos;
  }
  
  @Override
  public void park(long nanosToPark) throws InterruptedException {
    atemptToParkNanos += nanosToPark;
    if (Thread.interrupted()) {
      throw new InterruptedException();
    }
    parkedNanos += nanosToPark;
    meterMock.addTime(nanosToPark);
  }
  
  @Override
  public void parkUniterruptibly(long nanosToPark) {
    atemptToParkNanos += nanosToPark;
    parkedNanos += nanosToPark;
    meterMock.addTime(nanosToPark);
  }
}

```

```sh
mvn clean install
```

```
```


