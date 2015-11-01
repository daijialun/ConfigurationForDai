# Protobuf

- default value。bool的默认值是false，数值的默认值是0，enum的默认值是其第一个元素，string的默认值是空字符串

- tag id. id 1-15占用1个字节，16到2047占用两个字节。所以1-15要留个频繁使用的字段，不要刚开始定义字段的是时候都分配出去

     tag值最小是1, 最大是(2^29 - 1)即536,870,911,但是要避开19000到19999，这是protobuf内置的类型要用到的tag id
     
- enum可以有alias。enum的值不能为负数。

             enum EnumAllowingAlias {
                 option allow_alias = true;
                 UNKNOWN = 0;
                 STARTED = 1;   
                 RUNNING = 1;
             }
             
- 当协议更新的时候，如果某个字段过时了，就可以更改field的name，如"OBSOLETE_xxx"，以告诉使用者不要在使用这个field

- 如下几个类型是兼容的：

    - int32 uint32 int64 uint64 bool    
    - sint32 siint64
    - C string bytes （字符类型是UTF8）
    - D fixed32 sfixed32 fixed64 sfixed64
    - E optional repeated
    - F default([default = value])value也可以被修改
    
- protobuf对repeated压缩不够好，所以尽量在后面加上[packed = true]                      