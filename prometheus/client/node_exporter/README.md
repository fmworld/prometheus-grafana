# node exporter  

## 安装

- 安装golang环境

  ```docker
  docker pull golang
  docker run --name -v /tmp:/etc/golang -it pClient01 /bin/bash
  ```

- node exporter安装
  - 在[github](https://github.com/prometheus/node_exporter)上获取源码
  - 通过go build生成可运行软件，/go/bin/.node_exporter
  - nohup & 命令行启动后台不挂断服务
  - prometheus 配置文件，接入node_exporter
  - grafana [dashboard](https://grafana.com/grafana/dashboards) 中导入node_exporter面板，[导入方法](../../../grafana/README.md)
  - 面板内容
    - 提供了多个性能参数的面板，面板由数据展示UI、提供数据的查询语言、相关面板设置等组成
