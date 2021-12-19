---
title: jd 命令入门
date: 2021-12-19 00:26:33
tags: linux
---

## jq 命令
轻松操作在命令行shell中操作json数据，可以对数据映射、过滤、转换

1. 格式化JSON
```
cat data.json | jq
```

2. [index] 取数组的第一个
```
cat data.json | jq '.resources[0]'
```

3. 管道符号 ｜ 可以通过管道符号层层过滤

```
cat data.json | jq '.resources[0]' | jq '.id'
```

4. 返回数组所有数据 []

```
cat data.json | jq ".resources" | jq ".[] | { id: .id}"
```

5. 自定义key,并以数组形式显示,命令用[]扩起来即可
```
cat data.json | jq ".resources" | jq "[.[] | { _id: .id}]"
```

## 例如

1. 格式化JSON
```
➜ cat data.json
{"resources":[{"id":3,"device_id":1,"config_file_name":"/usr/local/appdata/data/zddi/f5-backup/2021-10-18_09-30-29.f5.config","sync_start_time":1634520568,"sync_end_time":1634520629,"ctime":1634520629,"error_file_state":10,"state":20},{"id":2,"device_id":1,"config_file_name":"/usr/local/appdata/data/zddi/f5-backup/2021-10-15_16-18-07.f5.config","sync_start_time":1634285832,"sync_end_time":1634285887,"ctime":1634285887,"error_file_state":10,"state":10},{"id":1,"device_id":1,"config_file_name":"/usr/local/appdata/data/zddi/f5-backup/2021-10-15_14-04-45.f5.config","sync_start_time":1634277830,"sync_end_time":1634277885,"ctime":1634277885,"error_file_state":10,"state":10}],"page_num":"1","page_size":"30","total_size":3,"min_time":1633046400000,"max_time":1634601599000}

learning-notes/jq on  every [?]
➜ cat data.json | jq
{
  "resources": [
    {
      "id": 3,
      "device_id": 1,
      "config_file_name": "/usr/local/appdata/data/zddi/f5-backup/2021-10-18_09-30-29.f5.config",
      "sync_start_time": 1634520568,
      "sync_end_time": 1634520629,
      "ctime": 1634520629,
      "error_file_state": 10,
      "state": 20
    },
    {
      "id": 2,
      "device_id": 1,
      "config_file_name": "/usr/local/appdata/data/zddi/f5-backup/2021-10-15_16-18-07.f5.config",
      "sync_start_time": 1634285832,
      "sync_end_time": 1634285887,
      "ctime": 1634285887,
      "error_file_state": 10,
      "state": 10
    },
    {
      "id": 1,
      "device_id": 1,
      "config_file_name": "/usr/local/appdata/data/zddi/f5-backup/2021-10-15_14-04-45.f5.config",
      "sync_start_time": 1634277830,
      "sync_end_time": 1634277885,
      "ctime": 1634277885,
      "error_file_state": 10,
      "state": 10
    }
  ],
  "page_num": "1",
  "page_size": "30",
  "total_size": 3,
  "min_time": 1633046400000,
  "max_time": 1634601599000
}

```
2. [index] 取数组的第一个
```
➜ cat data.json | jq '.resources[0]'
{
  "id": 3,
  "device_id": 1,
  "config_file_name": "/usr/local/appdata/data/zddi/f5-backup/2021-10-18_09-30-29.f5.config",
  "sync_start_time": 1634520568,
  "sync_end_time": 1634520629,
  "ctime": 1634520629,
  "error_file_state": 10,
  "state": 20
}
```

4. 返回数组所有数据 []
```
learning-notes/jq on  every [?]
➜ cat data.json | jq ".resources" | jq ".[] | { id: .id}"
{
  "id": 3
}
{
  "id": 2
}
{
  "id": 1
}

```
5. 自定义key,并以数组形式显示,命令用[]扩起来即可
```
learning-notes/jq on  every [?]
➜ cat data.json | jq ".resources" | jq "[.[] | { _id: .id}]"
[
  {
    "_id": 3
  },
  {
    "_id": 2
  },
  {
    "_id": 1
  }
]
```
手册
http://alingse.github.io/jq-manual-cn/manual/v1.5/#Basicfilters
