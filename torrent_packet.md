```
TODO  list
- SNMP Protocol
- 프로토콜 연결 순서
```

- [BT-uTP Protocol](http://www.bittorrent.org/beps/bep_0029.html)  
  
BT-uTP 통신 seeder와의 연결
---  
![syn_ack](https://user-images.githubusercontent.com/15623089/45482545-5dfc0480-b789-11e8-87ce-b335925c3d28.png)

 BT-uTP 패킷에서 192.168.43.83(peer)이 192.168.43.201(seeder)를 찾기위해서 Syn BT-uTP 패킷을 전송하고 있다.
 현재 배포중이고 접속중인 192.168.43.201(seeder)가 state BT-uTP 패킷을 192.168.43.83(peer)에게 응답하고 있다.  
  
BT-uTP 통신 peer 요청 패킷
---  
![syn](https://user-images.githubusercontent.com/15623089/45484080-ef6d7580-b78d-11e8-8cf7-f71769e88e31.png)  
  
- BT-uTP 연결(ST_SYN) 패킷 전송  
  
```
 - Version : (1)
 - Type : ST_SYN(4)
 - Connection ID : 46080
 - Windows Size : 1048576
 - Sequence number : 62808
 - ACK number : 0
```  
  
BT-uTP 패킷에서 Connection ID 46080 으로 ST_SYN(4) 요청패킷을 전송한다. 현재 Sequence number는 62808이며 응답이 오지 않은 상태라 Ack number는 0임을 확인 할 수 있다.
  
  
BT-uTP 통신 seeder 응답
---  
![state](https://user-images.githubusercontent.com/15623089/45506094-3d539f00-b7c9-11e8-919d-b36be807272e.png)  
  
- BT-uTP 상태(ST_STATE)

```
 - Version : (1)
 - Type : ST_STATE(2)
 - Connection ID : 46080
 - Windows Size : 1048576
 - Sequence number : 22347
 - ACK number : 62808
```  
  
BT-uTP 패킷에서는 Connection ID 46080 으로 ST_STATE(2) 상태 응답 패킷을 전송한다. 현재 Sequence number는 22347이며 ACK number는 62808임을 확인 할 수 있다.  
  

```
 TODO 1603 - 1624 까지 분석 필요
```
  
BT-uTP 통신 data 송/수신
---  
![utp](https://user-images.githubusercontent.com/15623089/45508095-db963380-b7ce-11e8-8eb6-9250b94d6fac.png)  
  
 BT-uTP 패킷에서 192.168.43.201(seeder)이 192.168.43.83(peer)으로 data 1085byte를 전송한다. 
 192.168.43.83(peer)가 192.168.43.201(seeder)에게 state 응답 패킷을 전송한다.  
  
BT-uTP 통신 seeder 데이터 전송
---  
  
![image](https://user-images.githubusercontent.com/15623089/45508617-3714f100-b7d0-11e8-8eaf-3e6366b184f1.png)  
  
- BT-uTP 데이터(ST_DATA)  

```
 - Version : (1)
 - Type : ST_DATA(0)
 - Connection ID : 46080
 - Windows Size : 50000
 - Sequence number : 22349
 - ACK number : 62812
```  
  
BT-uTP 패킷에서는 Connection ID 46080 으로 ST_DATA(0) 데이터 패킷을 전송한다. 현재 Sequence number는 22349이며 ACK number는 62812임을 확인 할 수 있다.  
  
```
 - 전송된 패킷은 1085byte = 이더넷(14byte) + IP 프로토콜(20byte) + UserData 프로토콜(8byte) + uTorrent 프로토콜(1043byte)
```

BT-uTP 통신 peer 응답 전송
---  
  
![image](https://user-images.githubusercontent.com/15623089/45510287-c2908100-b7d4-11e8-8014-84ebd174699c.png)
- BT-uTP 상태(ST_STATE)  

```
 - Version : (1)
 - Type : ST_STATE(2)
 - Connection ID : 46081
 - Windows Size : 48977
 - Sequence number : 62813
 - ACK number : 22349
```  
  
BT-uTP 패킷에서는 Connection ID 46081 으로 ST_STATE(2) 데이터 패킷을 전송한다. 현재 Sequence number는 62813이며 ACK number는 22349임을 확인 할 수 있다.

```
 - 응답한 패킷은 62byte = 이더넷(14byte) + IP 프로토콜(20byte) + UserData 프로토콜(8byte) + uTorrent 프로토콜(20byte)
```  
Windows Size가 48977byte으로 50000byte - (1043byte-20byte) = 48977byte로 BT-uTP프로토콜에서 이전에 받은 데이터 길이를 확인 할 수 있다.
  

- BT uTP : 패킷번호 1552 Node 0, 1 정보 요청 이게 무엇인가? 0 == "G1.txt"?? 1 == "MA.txt"??
- LSD : 패킷번호 1584
