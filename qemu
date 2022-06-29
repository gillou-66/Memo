Utilisation de qemu pour ouvrir l'image du kernel embarque

##Creation d'un bridge
sudo brctl addbr br0
#Nettoyage ip de la carte reseau locale
sudo ip addr flush dev eth0
#Ajout eth0 dans bridge
sudo brctl addif br0 eth0
#Creation d'un tap interface
sudo tunctl -t tap0 -u `whoami`
#Ajout du tap0 au bridge
sudo brctl addif br0 tap0
#Verifier que tout est up
sudo ifconfig eth0 up
sudo ifconfig tap0 up
sudo ifconfig br0 up
#check proprietes bridge
sudo brctl show
#Assigner une ip a br0
sudo dhclient -v br0

##Cleanup
#Remove tap interface tap0 from bridge br0
sudo brctl delif br0 tap0
#Delete tap0
sudo tunctl -d tap0
#Remove eth0 from bridge
sudo brctl delif br0 eth0
#Bring bridge down
sudo ifconfig br0 down
#Remove bridge
sudo brctl delbr br0
#Bring eth0 up
sudo ifconfig eth0 up
#Check if an IP is assigned to eth0, if not request one
sudo dhclient -v eth0
##dhclient - Auto configuration using a DHCP server
#Release IP
sudo dhclient -v -r <interface>
#Request IP
sudo dhclient -v <interface>

##exemple lancement de qemu
sudo qemu-system-i386 -drive format=raw,file=disk.img -net nic -net tap,ifname=tap0
la carte reseau apparit bien dans la vm
