## TCP
要使用代码来描述TCP的三次握手过程，实际上我们无法直接用高级编程语言（如Python、Java或JavaScript）直接实现TCP协议栈中的低层握手过程，
因为这些语言的网络库通常已经封装了TCP连接的建立过程。但是，我们可以编写伪代码或概念性的代码来模拟这个过程，帮助理解参数的传递和验证。

### 伪代码模拟

```python
class Handshake:
    def __init__(self, client_seq, server_seq):
        self.client_seq = client_seq
        self.server_seq = server_seq
        self.client_state = "CLOSED"
        self.server_state = "CLOSED"

    def first_handshake(self):
        # 客户端发起连接请求
        self.client_seq += 1  # 客户端序列号加1
        print(f"客户端发送SYN: seq={self.client_seq}")
        self.client_state = "SYN_SENT"
        return self.client_seq

    def second_handshake(self, client_syn):
        # 服务器接收到客户端的SYN，回复SYN+ACK
        self.server_seq += 1  # 服务器序列号加1
        print(f"服务器回复SYN+ACK: seq={self.server_seq}, ack={client_syn + 1}")
        self.server_state = "SYN_RCVD"
        return self.server_seq, client_syn + 1  # 返回服务器序列号和对客户端序列号的确认

    def third_handshake(self, server_syn_ack):
        # 客户端收到服务器的SYN+ACK，发送ACK确认
        print(f"客户端发送ACK: ack={server_syn_ack[0] + 1}")
        self.client_state = "ESTABLISHED"
        return server_syn_ack[1]  # 确认服务器的序列号，表示连接建立完成

# 模拟过程
handshaker = Handshake(client_seq=0, server_seq=0)

# 第一次握手
client_syn = handshaker.first_handshake()

# 第二次握手
server_syn_ack = handshaker.second_handshake(client_syn)

# 第三次握手
handshaker.third_handshake(server_syn_ack)
```

这段伪代码模拟了TCP三次握手的关键步骤，展示了序列号（seq）和确认号（ack）是如何随着每个握手阶段而变化的。
请注意，实际的TCP握手涉及到操作系统内核中的网络栈处理以及底层的网络通信，远比这段示例复杂。
此代码仅为帮助理解三次握手的概念性演示，并未涉及真实的网络IO操作。
