# BV1Xx411R743 P14 01:08

# Python

## ubuntu终端命令

```
python3 XXXX.py
```

用python3运行xxx.py

```
python3
```

打开python3的交互模式，可用于验证某些知识点语法

```
ipython3
```

比python3交互模式高端的一种交互模式

## 创建套接字

```python
import socket
socket.socket(AddressFamily,Type)
```

 AddressFamily：协议族，IPv4、IPv6

Type：两大类，UDP还是TCP

### tcp套接字

```python
import socket

# 创建tcp的套接字
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)

# 功能......省略

# 不用的时候，关闭套接字
s.close()
```

socket.AF_INET：IPv4

socket.SOCK_STREAM：TCP



### udp套接字

```python
import socket

# 创建udp的套接字
s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 功能......省略

# 不用的时候，关闭套接字
s.close()
```

socket.SOCK_DGRAM：UDP





## 发送消息

```python
udp_socket.sendto(b"can you hear me?",('192.XXX.XXX.X', 8080))

# 或者
dest_addr = ('192.XXX.XXX.X', 8080) # 注意是个元组，ip是字符串
send_data = input("请输入要发送的数据：")
udp_socket.sendto(send_data.encode('utf-8'), dest_addr)
```

“can you hear me?”前的b，是用于类型转换，表示转成byte类型。

('192.XXX.XXX.X', 8080)是一个元组类型



dest_addr，注意是个元组，ip是字符串，端口是数字

send_data.encode('utf-8')，将send_data的编码格式转为utf-8的编码格式



### 示例

```python
from socket import *
# 1.创建udp套接字
udp_socket=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 2.准备接收方地址
# '192.XXX.XXX.X' 表示目标ip地址
# 8080表示目的端口
dest_addr = ('192.XXX.XXX.X', 8080) # 注意是个元组，ip是字符串，端口是数字

# 3.从键盘获取数据
send_data = input("请输入要发送的数据：")

# 4.发送数据到指定电脑上的指定程序中
udp_socket.sendto(send_data.encode('utf-8'), dest_addr)

#5. 关闭套接字
udp_socket.close()
```



## 接收消息

### 绑定

```
local_addr = ('',7788)
udp_socket.bind(local_addr)
```

''，表示本机的任何一个ip

必须绑定本机的ip和post，其他的不行

### 接收

```python
rece_data=udp_socket.recvfrom(1024)
```

1024为本次接收的最大字节数

接收到的是一个元组，例如：

![image-20231112172931227](D:\akkkkk\study\MyNotes\image\socket编程\image-20231112172931227.png)

#### 解析接收数据

```
recv_msg = recv_data[0]
send_addr = recv_data[1]
```

将接收到的元组recv_data进行分解

recv_data[0]为接收的数据，注意接收到的数据是byte类型，显示的话也需要用utf-8的编码方式，但如果发送方是windows则需要用gbk的编码方式

recv_data[1]为发送方的地址信息，注意地址信息也是一个元组类型

### 示例

```python
import socket
def main():
    # 1.创建套接字
    udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    # 2.绑定本地信息
    localaddr = ("", 7788) # 端口号1025~65535均可
    udp_socket.bind(localaddr)
    # 3.接收数据
    recv_data = udp_sockeet.recvfrom(1024)
    # 4.解析数据
    recv_msg = recv_data[0]
    send_addr = recv_data[1]
    # 5.打印
    print("%s:%s" % (str(send_addr), recv_msg.decode("gbk")))
    # 6.关闭套接字
    udp_socket.close()
    
if __name__ == "__main__":
    main()
```

