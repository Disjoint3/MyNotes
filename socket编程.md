# BV1Xx411R743 P17 20:48

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

## 套接字

套接字是一个可以同时收发数据的东西

socket套接字是全双工

### ！！！注意

套接字的模块名是socket，写法不要错！！！！

```python
# 写法一
import socket
XXXX
s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 写法二
from socket import *
s=socket(AF_INET,SOCK_STREAM)
```



## udp

### 发送消息

1. **创建套接字**

   ```python
   import socket
   
   # 创建udp的套接字
   s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
   
   # 功能......省略
   
   # 不用的时候，关闭套接字
   s.close()
   ```

   socket.SOCK_DGRAM：UDP

2. **发送消息**

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

   send_data.encode('utf-8')，将send_data的编码格式转为utf-8的编码格式，windows要用gbk

   - 绑定本地信息

     ```
     udp_socket.bind(("", 7788))
     ```

3. **关闭套接字**

**示例**

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



### 接收消息

其他步骤和发送框架一致，只是在接收消息的时候有区别，此处只补充一下不同的

1. **绑定**

   ```
   local_addr = ('',7788)
   udp_socket.bind(local_addr)
   ```

   ''，表示本机的任何一个ip

   必须绑定本机的ip和post，其他的不行

2. **接收**

   ```python
   rece_data=udp_socket.recvfrom(1024)
   ```

   1024为本次接收的最大字节数

   接收到的是一个元组，例如：

   ![image-20231112172931227](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231112172931227.png)

   - 解析接收数据

   ```
   recv_msg = recv_data[0]
   send_addr = recv_data[1]
   ```

   将接收到的元组recv_data进行分解

   recv_data[0]为接收的数据，注意接收到的数据是byte类型，显示的话也需要用utf-8的编码方式，但如果发送方是windows则需要用gbk的编码方式

   recv_data[1]为发送方的地址信息，注意地址信息也是一个元组类型



### 总结

![image-20231114185044296](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231114185044296.png)

1. **创建套接字**

   ```pythonpython
   import socket
   socket.socket(AddressFamily,Type)
   ```

    AddressFamily：协议族，IPv4、IPv6

   Type：两大类，UDP还是TCP

2. **绑定接口**

   ```python
   localaddr = ("", 7890)
   ```

   这里的端口号7890指的是绑定自己的端口号，下面sendto的端口号，是对方的端口号，因此可以相同

3. **使用套接字收发数据**

   ```python
   udp_socket.sendto("XXXXX".encode("utf-8"), ("192.168.33.11", 7890))
   udp_socket.recvfrom(1024)
   ```

4. **关闭套接字**

```python
udp_socket.close()
```

### 代码示例

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

## udp应用案例：udp聊天器

**说明**

- 在一个电脑中编写1个程序，有2个功能：

  1.获取键盘数据，并将其发送给对方
  2.接收数据并显示

- 并且功能数据进行选择以上的2个功能调用

### 示例代码

![image-20231113184727045](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231113184727045.png)



## tcp

- ### 创建tcp套接字


```python
import socket

# 创建tcp的套接字
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)

```

socket.AF_INET：IPv4

socket.SOCK_STREAM：TCP

###  客户端构建

1. **socket创建套接字**

2. **链接服务器**

   (ip,端口)，依旧是个元组

3. **发送数据**

   与udp不同，输入的信息不需要再特意加上对方的ip地址，可以理解为tcp的绑定在连接服务器阶段已经完成了

4. **关闭socket**

#### 代码示例

```python
import socket

def main():
    # 1.创建tcp的套接字
    tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # 2.链接服务器
    server_ip = input("请输入要链接的服务器ip：")
    server_port = int(input("请输入要连接的服务器port："))
    server_addr = (server_ip, server_port)
    tcp_socket.connet(server_addr)
    
    # 3.发送数据/接收数据
    send_data = input("请输入要发送的数据：")
    tcp_socket.send(send_data.encode("gbk"))
    
    # 4.关闭套接字
    tcp_socket.close()
    
 if __name__ == "__main__":
    main()
```



### 服务端构建

1. **socket创建套接字**

2. **bind绑定ip和port**

3. **listen使套接字变为被动链接**

   监听套接字负责等待有新的客户端进行连接

   tcp_server_socket_listen(128)的128，一般默认写128，可能会影响到并发数量的多少，但最终还是由客户端决定

4. **accept等待客户端链接**

   accept产生的新的套接字用来为客户端服务

5. **recv/send接收发送数据**

6. **关闭socket**

#### 代码示例

```python
import socket

def main():
    # 1.创建套接字socket（买个手机）
    tcp_server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # 2.绑定本地信息 bind（插入手机卡）
    tcp_server_socket.bind(("", 7890))
    
    # 3.让默认套接字由主动成为被动 listen（将手机设置为正确的响铃模式）
    tcp_server_socket_listen(128)
    
    # 4.等待客户端的链接 accept（等待别人的电话到来）
    new_client_socket, client_addr = tcp_server_socket.accept()
    print("-----2-------")  #test
    print(client_addr)
    
    # 接收客户端发送过来的请求
    recv_data = new_client_socket.recv(1024)
    print(recv_data)
    
    # 回送一部分数据给客户端
    new_client_socket.send("hhahahahha------ok-------".encode("gbk"))
    
    # 关闭套接字
    new_client_socket.close()
    tcp_server_socket.close()
```

### 服务端升级

#### 为多个客户端服务

服务器先运行

如果将监听套接字关闭（即tcp_server_socket），会导致不能再次等待新客户端的到来，即xxxx.accept就会失败

如果关闭accept返回的套接字（即new_client_socket），意味着不会在为这个客户端服务

##### 示例

![image-20231115113154293](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231115113154293.png)



#### 并且多次服务一个客户端

如果recv解堵塞，有两种可能，一是客户端发来数据，二是客户端调用了close

因此，客户端是否还需要服务，可以判断recv_data是否为空。客户端无法发送空的消息，因此当recv_data为空时，表示客户端已经断开了连接。

##### 代码示例

![image-20231115131744790](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231115131744790.png)

### 总结

1.tcp服务器一般情况下都需要绑定，否则客户端找不到这个服务器

2.tcp客户端一般不绑定，因为是主动链接服务器，所以只要确定好服务器的ipport等信息就好，本地客户端可以随机

3.tcp服务器中通过listen可以将socket创建出来的主动套接字变为被动的，这是做tcp服务器时必须要做的

4.当客户端需要链接服务器时，就需要使用connect进行链接，udp是不需要链接的而是直接发送，但是tcp必须先链接，只有链接成功才能通信

5.当一个tcp客户端连接服务器时，服务器端会有1个新的套接字，这个套接字用来标记这个客户端，单独为这个客户端服务

6.listen后的套接字是被动套接字，用来接收新的客户端的链接请求的，而accept返回的新套接字是标记这个新客户端的

7.关闭listen后的套接字意味着被动套接字关闭了，会导致新的客户端不能够链接服务器，但是之前已经链接成功的客户端正常通信。

8.关闭accept返回的套接字意味着这个客户端已经服务完毕8.

9.当客户端的套接字调用close后，服务器端会recv解堵塞，并且返回的长度为0，因此服务器可以通过返回数据的长度来区别客户端是否已经下线



## tcp应用案例：文件下载器

### 客户端

1. 创建socket

2. 获取服务器ip和port

3. 链接服务器

4. 获取下载文件名字

5. 将文件名字发送到服务器

6. 接收文件中的数据

   1024表示1024B，也就是1K，1024*1024那就是1M

7. 保存接收到的数据到一个文件中

8. 关闭socket



#### 补充：with as

一般情况下，我们可以用以下方式读取文件，并对文件进行读写操作。

```python
f = open("xxxxx")

try:
    f.write()/read()
except:
    f.close()
```

也可以写成以下形式：

```python
with open("xxxxx") as f:
    f.read()/f.write()
```

用with as 可以不手动写close，这是因为他保证了调用文件，发现异常后会自动关闭文件，即with as 即使发现异常，也可以调用打开然后自动关闭。

适用于写文件的时候，读文件的时候不太适用

#### 示例代码

![image-20231115142350563](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231115142350563.png)

### 服务器

1. 创建socket

2. 绑定本地信息bind

3. 让默认套接字由主动变被动 listen

4. 等待客户端链接

5. 接收客户端发过来的、要下载的文件名

   

6. 发送文件的数据给客户端

   

7. 关闭套接字

#### 代码示例

![image-20231115142457249](https://cdn.jsdelivr.net/gh/Disjoint3/ImgHost@main/HisPic/MyNotes_PythonSocketimage-20231115142457249.png)



## 端口扫描











