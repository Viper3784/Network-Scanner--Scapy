# Network-Scanner--Scapy
A Network Scanner written in python that uses scapy.

from scapy.all import ARP, Ether, srp

def scan(ip):
    arp_request = ARP(pdst=ip)
    broadcast = Ether(dst="ff:ff:ff:ff:ff:ff")
    arp_request_broadcast = broadcast/arp_request
    answered_list = srp(arp_request_broadcast, timeout=1, verbose=False)[0]

    for sent, received in answered_list:
        print('IP: {}, MAC: {}'.format(received.psrc, received.hwsrc))

# replace '192.168.1.1/24' with your network
scan("192.168.1.1/24")
