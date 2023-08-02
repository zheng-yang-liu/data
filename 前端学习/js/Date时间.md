基础格式

```
var time = new Date()
var 任意 = new Date()
```

相关方法

| 方法          | 说明                    |
| ------------- | :---------------------- |
| getDate()     | 获取当前是几号1~31      |
| getDay()      | 获取当前的星期0为星期日 |
| getHours()    | 获取小时                |
| getMinutes()  | 获取分钟                |
| getSeconds()  | 获取秒                  |
| getMonth()    | 获取月份0为1月          |
| getFullYear() | 获取年份                |

组合获取新日期

```
time:2023年8月X日
var newTime = new Date(time.getFullYear(), time.getMonth() + 1, 1)
获取到的newTime为2023年9月1日
```

