cmake_minimum_required(VERSION 2.8.11)   # <-- target_include_directories() needs 2.8.11
project(rsmb C)

set(BINDIR bin)
set(SBINDIR sbin)
set(LIBDIR lib${LIB_SUFFIX})

set(SOURCES Bridge.c Filter.c Log.c MQTTPacketOut.c MQTTProtocolOut.c MQTTSProtocol.c Protocol.c StackTrace.c Tree.c)
set(SOURCES ${SOURCES} Broker.c Heap.c Messages.c MQTTProtocol.c MQTTSPacket.c MQTTSProtocolOut.c SocketBuffer.c SubsEngine.c Users.c)
set(SOURCES ${SOURCES} Clients.c LinkedList.c MQTTPacket.c MQTTProtocolClient.c MQTTSPacketSerialize.c Persistence.c Socket.c Topics.c)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Os -g")
ADD_DEFINITIONS(-DREVERSED)

configure_file(Messages.1.3.0.2 Messages.1.3.0.2 COPYONLY)

add_executable(broker_mqtts ${SOURCES})
target_compile_definitions(broker_mqtts PRIVATE -DMQTTS)
install(TARGETS broker_mqtts RUNTIME DESTINATION ${BINDIR} LIBRARY DESTINATION ${LIBDIR})

add_executable(broker_mqtt ${SOURCES})
install(TARGETS broker_mqtt RUNTIME DESTINATION ${BINDIR} LIBRARY DESTINATION ${LIBDIR})

