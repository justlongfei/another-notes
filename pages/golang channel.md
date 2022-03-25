- #golang
- 无缓存的channel只有在receiver准备好后send才被执行
- 读取关闭的channel，会返回channel已经关闭，并返回channel变量的零值
- 已经放入channel的数据不会在channel关闭后丢失，仍然可以读取到，并且此时读取channel的状态仍然为未关闭状态（即使main已经显式调用close关闭了此channel）
- The rule of thumb：**only writers should close channels**
  只有写channel的人才应该关闭channel
- 如果缓冲大小设置为 0 或者不设置，channel 为无缓冲类型，通信成功的前提是发送者和接收者都处于就绪状态。
  `make(chan bool)`与`make(chan bool, 1)`有本质不同