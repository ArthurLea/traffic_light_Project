1、按键程序（收获）
2、串口程序、电路图（收获）
3、CRC循环校验（总结）


自动模式,默认各方向均为20s,同时开始以南北方向为准，南北为绿，东西为红
手动模式,操作者自己设置南北东西方向上的绿灯时间
注意：南北方向上的绿灯时间和东西方向上的红灯时间相同
      东西方向上的绿灯时间和南北方向上的红灯时间相同

车流量的检测：
	1、理论计算法：
		单位时间内通过某路段的车辆：车流量=单位时间*车速/（车距+车身长）
	2、模拟计算法：
		单位时间内（一个红绿灯循环周期）内通过交通十字路口某方向上的的车辆数：

    采用算数平均值来进行统计，具体为：
	1、在一个循环周期中，分别测量出东南西北方向上的模拟车流量数目分别为nums_from_eas、nums_from_sou、nums_from_wes、nums_from_nor,
	2、然后再分别存储于car_num[0]、car_num[1]、car_num[2]、car_num[3];
	3、分别计算南北、东西方向上的车辆数，然后除以循环周期数，得到模拟车流量存储于sou_nor_nums，eas_wes_nums
	4、当车辆数达到某个设定的极限后，重置车辆数和循环周期数

实际应用时，发送装置计算出CRC值并随数据一同发送给接收装置，接收装置对收到的数据重新计算CRC并与收到的
CRC相比较，若两个CRC值不同，则说明数据通讯出现错误。
命令字格式：最长为16个字节(并带有CRC两位校验)
命令开头('$') 数据长度('8') 主命令 次命令|数据1 数据2 数据3 数据4 结束标记（'F'）        CRC1 CRC2 
