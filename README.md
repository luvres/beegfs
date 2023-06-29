# BeeGFS

hsttps://doc.beegfs.io/latest/advanced_topics/containers.html

### Management
```
curl https://raw.githubusercontent.com/luvres/beegfs/main/beegfs-management.yaml | docker-compose -f - up -d
```

### Storages
```
curl https://raw.githubusercontent.com/luvres/beegfs/main/beegfs-storage.yaml | docker-compose -f - up -d
```

### Pay attention to the variables with the interface(s) that BeeGFS must use for communication and the IP that must be used for the BeeGFS management service.
```
connInterfacesList=eth1 and sysMgmtdHost=10.8.33.50
```





curl https://raw.githubusercontent.com/luvres/beegfs/main/docker-compose.yaml | docker-compose -f - up -d

curl https://raw.githubusercontent.com/luvres/beegfs/main/docker-compose.yaml | docker-compose -f - down



