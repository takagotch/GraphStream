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
  
  static class InternalByteDecoder extends SourceBase implements ByteDecoder {
    @Override
    public void decode(ByteBuffer buffer) {
      System.out.printf("%X%n", buffer.get());
    }
    
    @Override
    public boolean validate(ByteBuffer buffer) {
      return buffer.position() > 0;
    }
  }
  
  static class InternalByteEncoder implements ByteEncoder {
    Transport transport;
    
    @Override
    public void addTransport(Transport transport) {
      this.transport = transport;
    }
    
    @Override
    public void removeTransport(Transport transport) {
    }
    
    void send(ByteBuffer buffer) {
      buffer.rewind();
      transport.send(buffer);
    }
  }
  
  @Override
  public void graphAttributeAdded(String sourceId, long timeId, String attribute, Object value) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x01);
    
    send(buffer);
  }
  
  
  
  
  
  
  
  @Override
  public void edgeAttributeRemoved(String sourceId, long timeId, String edgeId, String attribute) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x23);
    
    send(buffer);
  }
  
  @Override
  public void nodeAdded(String sourceId, long timeId, String nodeId) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((put) 0x31);
    
    send(buffer);
  }
  
  @Override
  public void nodeRemoved(String sourceId, long timeId, String nodeId) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x32);
    
    send(buffer);
  }
  
  @Override
  public void edgeAdded(String sourceId, long timeId, String edgeId, String fromNodeId, String toNodeId, boolean directed) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x41);
    
    send(buffer);
  }
  
  @Override
  public void edgeRemoved(String sourceId, long timeId, String edgeId) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x42);
    
    send(buffer);
  }
  
  @Override
  public void graphCleared(String sourceId, long timeId) {
    ByteBuffer buffer = ByteBuffer.allocate(1);
    buffer.put((byte) 0x50);
    
    send(buffer);
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


