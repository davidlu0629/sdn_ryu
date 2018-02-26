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

http://sdnhub.org/tutorials/ryu/  
simple_switch_13解析:https://osrg.github.io/ryu-book/zh_tw/html/switching_hub.html  
