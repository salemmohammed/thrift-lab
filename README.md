# thrift-lab
Before cloning the repo make sure that thrift path is added to your PATH environment variable.

##Setting up the Environment
####Type bash in your remote terminal
````
export PATH=$PATH:/home/yaoliu/src_code/local/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:"/home/yaoliu/src_code/local/lib"
````

If you set the thrift path correctly you should be able to get following output.

```
czhou5@remote00:~$ which thrift
/home/yaoliu/src_code/local/bin/thrift
```

```
czhou5@remote00:~$ thrift --version
Thrift version 1.0.0-dev
```

___

##Running Examples
1-) Clone the repo

`git clone https://github.com/chaozhou5/thrift-lab.git`

2-) Go to thrift-lab directory

3-) Thrift files are already generated with Thrift 1.0.0-dev in cpp/gen-cpp and java/gen-java. 
If you would like to re-generate;
Go to language that you want to use;

`thrift -r --gen cpp ../tutorial.thrift` or `thrift -r --gen java ../tutorial.thrift`


###For CPP

####Sample Server Output:
```
czhou5@remote00:~/thrift-lab/cpp$ ./server
Starting the server...
Incoming connection
	SocketInfo: <Host: 127.0.0.1 Port: 38451>
	PeerHost: localhost
	PeerAddress: 127.0.0.1
	PeerPort: 38451
ping()
add(1, 1)
calculate(1, 4)
calculate(1, 2)
getStruct(1)
```

####Sample Client Output
````
czhou5@remote00:~/thrift-lab/cpp$ ./client
ping()
1 + 1 = 2
InvalidOperation: Cannot divide by 0
15 - 10 = 5
Received log: 3F5FC93B338687BC7235B1AB103F47B3
````

###For JAVA

server usage :`./server [port]`
client usage : `./client [ip] [port]`

####Sample Server Output
```
czhou5@remote00:~/thrift-lab/java$ ./server.sh 9091
Starting the simple server...
ping()
add(1,1)
calculate(1, {DIVIDE,1,0})
calculate(1, {SUBTRACT,15,10})
getStruct(1)
```

####Sample Client Output
```
czhou5@remote00:~/thrift-lab/java$ ./client.sh localhost 9091
ping()
1+1=2
Invalid operation: Cannot divide by 0
15-10=5
Check log: 5
```

###For PYTHON

You need to have the following lines in your program, be careful of current sys.path and gen-py directory:

```` 
sys.path.append('gen-py')
sys.path.insert(0, glob.glob('/home/yaoliu/src_code/thrift/lib/py/build/lib.*')[0])
````

####Sample Server Output
```
czhou5@remote00:~/thrift-lab/py$ ./server.sh
Starting the simple server...
ping()
add(1,1)
calculate(1, Work(comment=None, num1=1, num2=0, op=4))
calculate(1, Work(comment=None, num1=15, num2=10, op=2))
getStruct(1)
```

####Sample Client Output
```
czhou5@remote00:~/thrift-lab/py$ ./client.sh
ping()
1+1=2
InvalidOperation: InvalidOperation(whatOp=4, why='Cannot divide by 0')
15-10=5
Check log: 5
```
