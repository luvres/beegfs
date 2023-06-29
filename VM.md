# Management 
```
VMID=19237;HOSTNAME="beegfs-mgmtd";MEMORY="2048";STORAGE="SSD";DISK="2";
BRIDGE0="vmbr0";IP0="192.168.96.37/27";GW="192.168.96.33";DNS="192.168.96.33";
BRIDGE="vmbr406";IP="10.8.33.50/28";

pct create ${VMID} \
-hostname ${HOSTNAME} \
local:vztmpl/alpine-3.18-default_20230607_amd64.tar.xz \
-cores 1 -memory ${MEMORY} -swap 0 \
-rootfs ${STORAGE}:${DISK} \
-net0 name=eth0,bridge=${BRIDGE0},ip=${IP0},gw=${GW} \
-net1 name=eth1,bridge=${BRIDGE},ip=${IP},tag=833 \
-nameserver ${DNS} \
-unprivileged 1 \
-features nesting=1,keyctl=1 \
-onboot 1 \
-ssh-public-keys ~/hci.pub
pct start ${VMID}

VMID=19237;pct exec ${VMID} -- sh -c "apk add --no-cache bash bash-completion nano nano-syntax curl openssh docker docker-compose iperf3 nmap htop \
&& echo 'PermitRootLogin yes' >>/etc/ssh/ssh_config && rc-update add sshd \
&& rc-update add docker && service sshd restart \
&& cat /usr/share/nano/*.nanorc > ~/.nanorc \
&& reboot" # 244.6M
```

### Access
```
ssh -i ~/hci.key -o StrictHostKeyChecking=no -o BatchMode=yes root@192.168.96.37

VMID=19237;pct exec ${VMID} -- bash
```

### Remove
```
VMID=19237;pct stop ${VMID};pct destroy ${VMID}
```

# Storages
```
VMID=1725117;HOSTNAME="beegfs-stg-51";MEMORY="2048";STORAGE="SSD";DISK="2";
BRIDGE0="vmbr1";IP0="172.3.51.17/28";GW="172.3.51.30";DNS="192.168.96.33";
BRIDGE="vmbr406";IP="10.8.33.57/28";

VMID=1725217;HOSTNAME="beegfs-stg-52";MEMORY="2048";STORAGE="SSD";DISK="2";
BRIDGE0="vmbr1";IP0="172.3.52.17/28";GW="172.3.51.30";DNS="192.168.96.33";
BRIDGE="vmbr406";IP="10.8.33.58/28";

VMID=1725317;HOSTNAME="beegfs-stg-53";MEMORY="2048";STORAGE="SSD";DISK="2";
BRIDGE0="vmbr1";IP0="172.3.53.17/28";GW="172.3.53.30";DNS="192.168.96.33";
BRIDGE="vmbr406";IP="10.8.33.59/28";

pct create ${VMID} \
-hostname ${HOSTNAME} \
local:vztmpl/alpine-3.18-default_20230607_amd64.tar.xz \
-cores 1 -memory ${MEMORY} -swap 0 \
-rootfs ${STORAGE}:${DISK} \
-net0 name=eth0,bridge=${BRIDGE0},ip=${IP0},gw=${GW} \
-net1 name=eth1,bridge=${BRIDGE},ip=${IP},tag=833 \
-nameserver ${DNS} \
-unprivileged 1 \
-features nesting=1,keyctl=1 \
-onboot 1 \
-ssh-public-keys ~/hci.pub
pct start ${VMID}

pct exec ${VMID} -- sh -c "apk add --no-cache bash bash-completion nano nano-syntax curl openssh docker docker-compose iperf3 nmap htop \
&& echo 'PermitRootLogin yes' >>/etc/ssh/ssh_config && rc-update add sshd \
&& rc-update add docker && service sshd restart \
&& cat /usr/share/nano/*.nanorc > ~/.nanorc \
&& reboot" # 244.6M

VMID=1725117;
VMID=1725217;
VMID=1725317;
```

### Access
```
ssh -i ~/hci.key -o StrictHostKeyChecking=no -o BatchMode=yes root@172.3.51.17
ssh -i ~/hci.key -o StrictHostKeyChecking=no -o BatchMode=yes root@172.3.52.17
ssh -i ~/hci.key -o StrictHostKeyChecking=no -o BatchMode=yes root@172.3.53.17

pct exec ${VMID} -- bash
```

### Remove
```
pct stop ${VMID};pct destroy ${VMID}
```

