#指定编译器
CC = g++  #也可以是CC = gcc
#指定编译参数
CFLAGS = -std=c++11
 
#指定头文件路径，此处用于指定非标准库的头文件路径
INC = -I./ -I /usr/include
 
#指定要链接的动态库或静态库 -L是指定动态库路径，非标准的动态库需要此参数
#LIBS = -lm -ldl -L/mylibs/xxx -lxxx
 
#把上面放一起
CXXFLAGS = ${CFLAGS} ${INC} #${LIBS}
 
#指定生成可执行文件名称
EXEC = MainUsbServer.out
 
#指定由哪些文件来生成可执行文件
OBJS = MouseDevice.o KeyboardDevice.o UsbEmulator.o IPResolver.o VUsbServer.o main.o 

KeyboardDevice:KeyboardDevice.cpp KeyboardDevice.h
	${CC} -c KeyboardDevice.cpp

MouseDevice:MouseDevice.cpp MouseDevice.h
	${CC} -c MouseDevice.cpp

IPResolver:IPResolver.cpp IPResolver.h
	${CC} -c IPResolver.cpp

UsbEmulator:UsbEmulator.cpp UsbEmulator.h
	${CC} -c UsbEmulator.cpp

VUsbServer:VUsbServer.cpp VUsbServer.h
	${CC} -c VUsbServer.cpp  -lssl -lcrypto -ldl -pthread
	#${CC}  -o VUsbServer.o VUsbServer.cpp -lssl -lcrypto -ldl -pthread
Main:main.cpp 
	${CC} -c main.cpp

RaspVirtualUsbServer: 
	${CC} -o RaspVirtualUsbServer main.o VUsbServer.o UsbEmulator.o IPResolver.o MouseDevice.o KeyboardDevice.o  -lssl -lcrypto -ldl -pthread

#https://blog.csdn.net/XN6666/article/details/81113931
#https://github.com/facebook/Surround360/issues/3
 
 .cpp.o:
	$(CC) $(CFLAGS) -c $<
#make执行动作
${EXEC} : ${OBJS}
	${CC} -o $@ $^
 
#make all 动作
all:KeyboardDevice MouseDevice IPResolver UsbEmulator VUsbServer Main RaspVirtualUsbServer


#make clean动作
clean:
	rm -rf ${OBJS}
 
#中间文件的生成
%.o:%.c
	$(CC) $(CXXFLAGS) $(INC) -o $@ -c $<

# StringTest:StringTest.o String.o
#   g++ -o StringTest StringTest.o String.o

# StringTest.o:StringTest.cpp String.h
#   g++ -c StringTest.cpp
# String.o:String.cpp String.h
#   g++ -c String.cpp
# clean :
#   rm StringTest StringTest.o String.o

#https://blog.csdn.net/XN6666/article/details/81113931

