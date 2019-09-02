### graphstream
---
https://github.com/graphstream/gs-core

http://graphstream-project.org/

```java
// src-test/org/graphstream/binary/test/ExampleByteProxy.java

public class ExampleByteProxy {
  public static void main(String... args) throws Exception {
    ByteProxy proxy = new ByteProxy(new ByteFactory() {
      @Override
      public ByteEncoder createByteEncoder() {
        return new InternalByteEncoder();
      }
      
      @Override
      public ByteDecoder createByteDecoder() {
        return new InternalByteDecoder();
      }
    }, 10000);
    
    DefaultGraph g = new DefaultGraph("g");
    g.addSink(proxy);
    
    proxy.setReplayable(g);
    proxy.start();
    
    int idx = 0;
    
    while(true) {
      String a = String.format();
      String b = String.format();
      
      g.addNode(a);
      g.addNode(b);
      g.addEdge("edge-" + a + "-" + b, a, b);
      
      Thread.sleep(1000);
    }
  }
  
  
  
  
  
  
  
  
  
  
  @Override
  public void stepBegins(String sourceId, long timeId, double step) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x60);
    
    send(buffer);
  }
}


```

```
```

```
```


