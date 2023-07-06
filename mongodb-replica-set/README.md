## host file 設定

```
127.0.0.1 mongo1
127.0.0.1 mongo2
127.0.0.1 mongo3
```

## connect url

```
mongodb://mongo1:27017,mongo2:27027,mongo3:27037?authSource=admin&replicaSet=rs0
```
