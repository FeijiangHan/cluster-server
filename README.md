# ChatServer

A cluster-based chat server and client code that utilizes Nginx for load balancing and Redis as a message middleware. The software is designed with a layered architecture and is built using the muduo network library, MySQL, and CMake.

Features:
- User registration, login, and logout
- Real-time chat and offline message delivery
- Creation and joining of chat groups
- Group chat functionality

## Environment
1. muduo network library
2. MySQL database
3. Nginx (TCP module)
4. Redis
5. CMake

Add the following configuration to `nginx.conf` in order to expose port 8000 and load balance requests between `127.0.0.1:6000` and `127.0.0.1:6002` using a round-robin algorithm:

```makefile
#ngix tcp loadbalance config
stream{
    upstream MyServer{
        server 127.0.0.1:6000 weight=1 max_fails=3 fail_timeout=30s;
        server 127.0.0.1:6002 weight=1 max_fails=3 fail_timeout=30s;
    }

    server{
        proxy_connect_timeout 1s;
        listen 8000;
        proxy_pass MyServer;
        tcp_nodelay on;
    }
}
```

## Compilation
Simply run `./autoCompile.sh` to compile the project.

## Running
Navigate to the `/bin` directory:
- To run the server: `./ChatServer 127.0.0.1 port` (replace `port` with the desired port number)
- To run the client: `./ChatClient IP 8000` (replace `IP` with the server's IP address)
