# Grafana

## 安装

- docker install

```docker
docker pull grafana/grafana
docker run -d -p 3000:3000 --name=grafana01 grafana/grafana:latest
```

- 配置dataSource
  - 集成prometheus插件
    ![ 插件列表](./image/grafana_add_datasource.png)

  - 进入dataSource面板，选择prometheus数据源
  ![ 插件列表](./image/grafana_datasource_02.png)

- 配置dashborad面板
  - 新建dashboard面板
    ![new dashborad](./image/grafana_new_dashboard.png)
  - 新建视图面板panel
    - 选择数据源和查询数据
    - 配置视图样式
    - 配置基础面板信息
  ![panel](./image/grafana_new_panel.png)

- 导入/导出dashboard
  - 导入，在新建餐单选项中，选择import选项，进入imprt页面
  ![import menu](./image/grafana_import_menu.png)
    - 线上面板
      - 通过grafana的[dashboard仓库](https://grafana.com/grafana/dashboards)找寻目标面板，获取ID
      - 将ID填入输入框，配置页面跳转至uid和prometheus源数据的配置页面
    - 本地面板
      - 通过upload,浏览本地的面板文件
      - 选择面板文件导入，配置页面跳转至uid和prometheus源数据的配置页面
    - json字符串
      - 将面板的模板json字符串贴入编辑框
      - 点击load，配置页面跳转至uid和prometheus数据源的配置页面

    ![配置输入](./image/grafana_import_id.png)
    - 进入uid和prometheus源数据的配置页面后，填入uid和prometheus数据源，确定导入即可

    ![配置数据源](./image/grafana_import_setting.png)
  - 导出
    - 在dashboard的右上角，选择share选项

    ![menu](./image/grafana_export_menu.png)
    - 在弹出的面板中，选择export选项，即可导出文件或者json串
  
    ![menu](./image/grafana_export_item.png)

- 配置node exporter面板
  - 导入node_exporter面板(导入dashboard介绍)
    ![node exporter](./image/grafana_node_exporter.png)
  - 点击import，生成node exporter面板
    ![node数据展示](./image/grafana_node_export_data_display.png)