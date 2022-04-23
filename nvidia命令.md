## nvidia-smi 命令

查看当前显卡使用情况

`nvidia-smi`

<div align="left"><img src="images/nvidia.png" height=300></div>

定时刷新显示：

> 有时候GPU利用率在上下浮动，这是使用定时刷新命令比较好

- `watch -n 1 nvidia-smi` 每隔1秒刷新一次显示

- `nvidia-smi -l 1` 每隔1秒刷新一次显示

建议使用后者

