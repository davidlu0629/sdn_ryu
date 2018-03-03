# sdn_ryu
# simple comments to operate mininet and RYU controller    
mininet: sudo mn --topo single,3 --mac --controller remote --switch ovsk    
RYU: cd /home/ubuntu/ryu && ./bin/ryu-manager --verbose ryu/app/simple_switch_13.py    
# RYU code structure (under /ryu/ folder)    
### app/: app run on top of the controller  
### base/: base class for RYU app, RyuApp class app_manager.py is inheried in a new application  
### controller/: include files you need to deal with OpenFlow functions  
### lib/: include parser of different protocol headers  
### ofproto/: include OpenFlow protocol  
### topology/: included files are related to topology discovery  
# Basic functions for controller  
傳送(L2Forwarding)->接收switch到controller的封包(EventOFPPacketIn)->輸出controller到switch的封包(OFPPacketOut)  
->對應進入的封包產生rule->送rule給switch  

ex:  
```python
@set_ev_cls(ofp_event.EventOFPSwitchFeatures, CONFIG_DISPATCHER)    
def switch_features_handler(self, ev):    
    datapath = ev.msg.datapath    
    ofproto = datapath.ofproto    
    parser = datapath.ofproto_parser    
```    
>ev.msg: 儲存對應事件的OpenFlow訊息類別實體    
>底下有msg.datapath, datapath當中常用的有: id(DPID), ofproto, ofproto_parser(parser)    

http://sdnhub.org/tutorials/ryu/    
simple_switch_13解析:https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html    
實作教學:https://github.com/OSE-Lab/Learning-SDN/tree/master/Controller/Ryu/ShortestPath    

  常用指令:    
  mininet: sudo mn --topo single,3 --mac --controller remote --switch ovsk    
  controller: cd /home/ubuntu/ryu && ./bin/ryu-manager --verbose ryu/app/simple_switch_13.py    
  other: sudo ovs-vsctl set bridge s1 protocols=OpenFlow13    
  sudo wireshark &    
  in mininet:   
  to inspect the rule in the switch(s1): ovs-ofctl -O openflow13 dump-flows s1    
  check packet get in the host(h1): tcpdump -en -i h1-eth0
  
  

