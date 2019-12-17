# prometheus-grafana  

### 产品开发环境部署

- node exporter
  - install
    - 在[github](https://github.com/prometheus/node_exporter)上 通过go build生成可运行软件，/go/bin/.node_exporter
    - nohup & 命令行启动后台不挂断服务
    - prometheus 配置文件，接入node_exporter
    - grafana [dashboard](https://grafana.com/grafana/dashboards) 中搜索node_exporter插件，并导入，配置datasource后保存
  - 面板内容
    - 提供了多个性能参数的面板，面板由数据展示UI、提供数据的查询语言、相关面板设置等组成
- custom exporter
  - format
    - 标注 #开头（HELP， TYPE（counter, gauge, histogram, summary, 和 untyped 类型））
    - 以行结束符 \n 作为每一行的结尾
    - 提供prometheus数据类型的数据上报
      - Counter
      - Gauge
      - Histogram
      - Summary
  - 提供相关数据访问服务（如： http server）
    - 将规定格式的数据发送给请求者，此处一般为用于pull数据的prometheus服务器
  - 示例 [完整sample](https://songjiayang.gitbooks.io/prometheus/content/exporter/sample.html)

  ``` ymal
  # HELP http_requests_total The total number of HTTP requests.
  # TYPE http_requests_total counter
  http_requests_total{method="post",code="200"} 1027 1395066363000
  http_requests_total{method="post",code="400"}    3 1395066363000

  # Escaping in label values:
  msdos_file_access_time_seconds{path="C:\\DIR\\FILE.TXT",error="Cannot find file:\n\"FILE.TXT\""} 1.458255915e9

  # Minimalistic line:
  metric_without_timestamp_and_labels 12.47

  # A weird metric from before the epoch:
  something_weird{problem="division by zero"} +Inf -3982045

  # A histogram, which has a pretty complex representation in the text format:
  # HELP http_request_duration_seconds A histogram of the request duration.
  # TYPE http_request_duration_seconds histogram
  http_request_duration_seconds_bucket{le="0.05"} 24054
  http_request_duration_seconds_bucket{le="0.1"} 33444
  http_request_duration_seconds_bucket{le="0.2"} 100392
  http_request_duration_seconds_bucket{le="0.5"} 129389
  http_request_duration_seconds_bucket{le="1"} 133988
  http_request_duration_seconds_bucket{le="+Inf"} 144320
  http_request_duration_seconds_sum 53423
  http_request_duration_seconds_count 144320

  # Finally a summary, which has a complex representation, too:
  # HELP rpc_duration_seconds A summary of the RPC duration in seconds.
  # TYPE rpc_duration_seconds summary
  rpc_duration_seconds{quantile="0.01"} 3102
  rpc_duration_seconds{quantile="0.05"} 3272
  rpc_duration_seconds{quantile="0.5"} 4773
  rpc_duration_seconds{quantile="0.9"} 9001
  rpc_duration_seconds{quantile="0.99"} 76656
  rpc_duration_seconds_sum 1.7560473e+07
  rpc_duration_seconds_count 2693
  ```

- K8s+docker环境下的数据监测
- 其他服务的探测和监测部署
