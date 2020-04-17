# ComBridge是一个通信桥接实现的通信库  

目前实现了InputStream和OutputStream桥接到LocalServerSocket的过程 

使用方法：  

LocalComBridgeAdapter是负责上述映射过程的实现类，在需要进行转发时，需要先开启服务
    LocalComBridgeAdapter.startServer(String name)  
其中，namespace参数必须独一无二，我们提供了默认的命名空间：
    "DXL.COM.ASL"

服务开启后，你可以进行设置IO引用：  
    LocalComBridgeAdapter.setOutputStream(OS);
    LocalComBridgeAdapter.setInputStream(IS);
设置完成后，如果IO引用不为空，转发将会自动开始工作，你可以在其他任意地方连接此LocalServerSocket进行数据传输！  
  
注意，不需要转发时，应当关闭SocketClient：  
    LocalComBridgeAdapter.stopClient();
  
退出APP时，应当关闭服务：  
    LocalComBridgeAdapter.stopServer();
  
针对设备的验证，我们提供了检查抽象类：
    DeviceChecker
    你需要实现其中的：boolean checkDevice() 与 void close()两个方法
    以提供完整的验证过程！
    
 针对UsbDeviceConnection与UsbEndpoint到Inputstream与OutputStream的转换  
 我们提供了BulkInputStream与BulkOutputStream两个封装类，你只需要实例化并且传入对应的链接与端点即可。
 例如：
    inputStream = new BulkInputStream(mCon, mEpIn);
    outputStream = new BulkOutputStream(mCon, mEpOut);
    
 祝你使用顺利：）
