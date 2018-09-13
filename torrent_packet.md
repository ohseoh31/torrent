
TODO list
```
- SNMP Protocol

```

- [BT-uTP Protocol](http://www.bittorrent.org/beps/bep_0029.html)
</br>

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
 - type : ST_SYN(4)
 - Connection ID : 46080
 - Windows Size : 1048576
 - Sequence number : 62808
 - ACK number : 0
```  
  
BT-uTP 패킷에서 Connection ID 46080 으로 ST_SYN(4) 요청패킷을 전송한다. 현재 Sequence number는 62808이며 응답이 오지 않은 상태라 Ack number는 0임을 확인 할 수 있다.
  
  
BT-uTP 통신 seeder 응답
---  
![state](https://user-images.githubusercontent.com/15623089/45506094-3d539f00-b7c9-11e8-919d-b36be807272e.png)  
  
- BT-uTP 상태(ST_

```
 - Version : (1)
 - type : ST_STATE(2)
 - Connection ID : 46080
 - Windows Size : 1048576
 - Sequence number : 22347
 - ACK number : 62808
```  
  
BT-uTP 패킷에서는 Connection ID 46080 으로 ST_STATE(2) 상태 응답 패킷을 전송한다. 현재 Sequence number는 22347이며 ACK number는 62808임을 확인 할 수 있다.  
  
TODO
```
 1603 - 1624 까지 분석 필요
```
  
BT-uTP 통신 seeder data 전송
---  

