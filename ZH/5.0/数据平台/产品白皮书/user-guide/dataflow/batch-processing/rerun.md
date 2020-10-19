## 关于补算

### 如何进行补算

* 单击画布工作台上的补算功能

    ![](../../../assets/dataflow/dataflow_batch_busuan.png)

* 配置补算任务

    ![](../../../assets/dataflow/dataflow_batch_busuan_config.png)

    节点名称：当前任务中需要进行补算的离线计算节点，支持同时选择多个节点

    开始时间：补算任务的调度开始时间

    截止时间：补算任务的调度截止时间

    补算依赖该节点的所有下游节点：选中后，会对依赖该节点选定时间内的的数据的计算任务一起进行补算

* 提交，等待管理员审批。

    ![](../../../assets/dataflow/dataflow_batch_busuan_shenpi.png)

* 审批通过后，点击执行，启动补算任务

    ![](../../../assets/dataflow/dataflow_batch_busuan_qidong.png)

* 任务执行之后，在页面右上角查看本次补算执行的进度，也可以在运行信息里查看任务运行的结果

    ![](../../../assets/dataflow/dataflow_batch_busuan_zhixing.png)

### 补算的注意事项

* 补算时间只能选择过去时间

* 如果补算的时间的任务正在运行，则补算任务无法提交，请等待任务执行完毕后再尝试提交

* 如果补算所依赖的节点的任务不存在，则补算任务将跳过执行

* 如果补算的任务之前执行过且成功，则会造成数据重复，请谨慎选择补算时间
