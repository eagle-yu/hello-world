
测试
服务器
H:\>python udp_remote.py server 127.0.0.1   也可是用“”表示可以接收任意地址和端口
Listening at ('127.0.0.1', 1060)
Pretending to drop packet from ('127.0.0.1', 64769)
Pretending to drop packet from ('127.0.0.1', 64769)
The client at ('127.0.0.1', 64769) says 'This is another message'

客户端
H:\>python udp_remote.py client 127.0.0.1    当参数为127.0.0.1时，与服务器的地址相同
Client socket name is ('127.0.0.1', 64769)
Waiting up to 0.1 seconds for a reply
Waiting up to 0.2 seconds for a reply
Waiting up to 0.4 seconds for a reply
The server says 'Your data was 23 bytes long'

H:\>python udp_remote.py client 192.168.1.101   该地址为要连接的服务器的地址，由于服务器绑定地址为127.0.0.1（当不是“”时），所以客户端一直收不到服务器的响应
Client socket name is ('192.168.0.10', 63606)
Waiting up to 0.1 seconds for a reply
Waiting up to 0.2 seconds for a reply
Waiting up to 0.4 seconds for a reply
Waiting up to 0.8 seconds for a reply
Waiting up to 1.6 seconds for a reply
Traceback (most recent call last):
  File "udp_remote.py", line 32, in client
    data = sock.recv(MAX_BYTES)
socket.timeout: timed out

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "udp_remote.py", line 53, in <module>
    function(args.host, args.p)
  File "udp_remote.py", line 36, in client
    raise RuntimeError('I think the server is down') from exc
RuntimeError: I think the server is down

如果在同一台机器运行服务器监听的地址127.0.0.1，那么再次运行使用127.0.0.1时会报错（提示该 接口已使用）,而如果第二次调用使用的通配符，同样会报错，因为通配符（""也就是任意地址）包含第一次调用 的地址127.0.0.1
