1. 异步非阻塞io
2. epoll模型
- select/poll是 一个一个问 O(n)
- epoll是一种多路复用机制，底层维护一个事件表
- 采用水平触发 每次都举手 让nginx知道，但是一直举手会浪费资源
- 边缘触发 举手了，错过就没法读了
3. 高并发  master+worker  nginx是多进程！！！  worker是处理请求的   master是读取配置文件 管理worker的
4. 内存管理极度精简！！ 复用内存池 而不是像apache一样
5. 零拷贝技术 
1️⃣ sendfile(fd, socket) 一次完成：

📦 文件 → 内核缓冲区
📬 内核直接把数据 → 送到 socket 缓冲区
🚀 最终发给网卡 → 客户端

6. 热重启  假如你修改了配置文件  执行了nginx -s reload （-s 告诉nginx执行哪个指令） 他会重新读取配置文件，逐步关闭旧的worker
7. 模块化设计 按需加载