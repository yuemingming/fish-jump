[981. 基于时间的键值存储](https://leetcode-cn.com/problems/time-based-key-value-store/)
创建一个基于时间的键值存储类 TimeMap，它支持下面两个操作：

1. set(string key, string value, int timestamp)

存储键 key、值 value，以及给定的时间戳 timestamp。
2. get(string key, int timestamp)

返回先前调用 set(key, value, timestamp_prev) 所存储的值，其中 timestamp_prev <= timestamp。
如果有多个这样的值，则返回对应最大的  timestamp_prev 的那个值。
如果没有值，则返回空字符串（""）。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/time-based-key-value-store
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
