# docker删除所有none镜像

在docker反复build后，会存留很多none镜像，下面命令一键删除所有none镜像

```
docker rmi `docker images | grep  '<none>' | awk '{print $3}'`
```

```
docker rmi -f $(docker images | grep none | awk '{print $3}')
```
