# 图像数据说明 {#spec_image_data}

| 名称 | 字段 | 单位 | 字节数 | 说明 |
| :----- | :----- | :----- | :-------- | :----- |
| 帧 ID | frame_id | - | 2 | uint16_t; [0,65535] |
| 时间戳 | timestamp | 1 us | 8 | uint64_t |
| 曝光时间 | exposure_time | 1 us | 2 | uint16_t |

> 图像数据传输方式：倒序排在图像尾部。

## 图像数据包

| Name | Header | Size | FrameID | Timestamp | ExposureTime | Checksum |
| :--- | :----- | :--- | :------ | :-------- | :----------- | :------- |
| 字节数 | 1 | 1 | 2 | 8 | 2 | 1 |
| 类型 | uint8_t | uint8_t | uint16_t | uint64_t | uint16_t | uint8_t |
| 描述 | 0x3B | 0x10 （数据内容大小） | 帧 ID | 时间戳 | 曝光时间 | 校验码（数据内容所有字节异或） |

* 数据包校验不过，会丢弃该帧。
* 时间的单位精度为： 1 us 。
* 时间累计是从上电时从开始，而不是从打开时开始。