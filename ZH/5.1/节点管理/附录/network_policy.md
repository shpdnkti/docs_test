# 开通网络策略

## GSE 与直连 Agent 之间需要的网络策略


源地址|目标地址|协议|端口|用途
   --|--|--|--|--
agent|zk|TCP|2181|获取配置
agent|gse_task|TCP|48533|任务服务端口
agent|gse_data|TCP|58625|数据上报端口
agent|gse_btsvr|TCP|59173|bt传输
agent|gse_btsvr|TCP,UDP|10020|bt传输
agent|gse_btsvr|UDP|10030|bt传输
gse_btsvr|agent|TCP,UDP|60020-60030|bt传输
gse_btsvr|gse_btsvr|TCP|58930|bt传输
gse_btsvr|gse_btsvr|TCP,UDP|10020|bt传输
gse_btsvr|gse_btsvr|UDP|10030|bt传输
agent|agent|TCP,UDP|60020-60030|bt传输
agent|||监听随机端口|bt传输，可不开通
gse_btsvr|||监听随机端口|bt传输，可不开通
