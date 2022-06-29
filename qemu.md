Utilisation de qemu pour ouvrir l'image du kernel embarque.<br/>

##Creation d'un bridge.<br/><br/>
sudo brctl addbr br0.<br/>
#Nettoyage ip de la carte reseau locale.<br/>
sudo ip addr flush dev eth0<br/>
#Ajout eth0 dans bridge<br/>
sudo brctl addif br0 eth0<br/>
#Creation d'un tap interface<br/>
sudo tunctl -t tap0 -u `whoami`<br/>
#Ajout du tap0 au bridge<br/>
sudo brctl addif br0 tap0<br/>
#Verifier que tout est up<br/>
sudo ifconfig eth0 up<br/>
sudo ifconfig tap0 up<br/>
sudo ifconfig br0 up<br/>
#check proprietes bridge<br/>
sudo brctl show<br/>
#Assigner une ip a br0<br/>
sudo dhclient -v br0<br/>

##Cleanup<br/><br/>
#Remove tap interface tap0 from bridge br0<br/>
sudo brctl delif br0 tap0<br/>
#Delete tap0<br/>
sudo tunctl -d tap0<br/>
#Remove eth0 from bridge<br/>
sudo brctl delif br0 eth0<br/>
#Bring bridge down<br/>
sudo ifconfig br0 down<br/>
#Remove bridge<br/>
sudo brctl delbr br0<br/>
#Bring eth0 up<br/>
sudo ifconfig eth0 up<br/>
#Check if an IP is assigned to eth0, if not request one<br/>
sudo dhclient -v eth0<br/>
##dhclient - Auto configuration using a DHCP server<br/><br/>
#Release IP<br/>
sudo dhclient -v -r <interface><br/>
#Request IP<br/>
sudo dhclient -v <interface><br/>

##exemple lancement de qemu<br/><br/>
sudo qemu-system-i386 -drive format=raw,file=disk.img -net nic -net tap,ifname=tap0<br/>
la carte reseau apparit bien dans la vm
