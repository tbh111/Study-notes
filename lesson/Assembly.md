# 汇编部分

## 操作数符号表示

```markdown
DST：目的操作数
SRC：源操作数
TARGET：循环、转移和调用指令目标地址
reg(8/16)：寄存器操作数(字节/字)
mem(8/16/32)：存储器操作数(字节/字/双字)
acc：累加器(AL/AX)
seg_reg：段寄存器
imm(8/16)：立即操作数(字节/字)
short/near/far_label：短/近/远标号(8/16/32位地址偏移)
```

## 常用指令

#### 数据传送类

##### 1. MOV DST, SRC

```assembly
mov mem, acc
mov acc, mem
mov	reg, mem
mov	mem, reg
mov	reg, imm
mov	mem, imm
mov seg_reg,reg16 ;CS除外
mov seg_reg,mem16 ;CS除外
mov reg16,seg_reg
mov mem16,seg_reg
```

``` Markdown
注意事项：
(1) 目的操作数不能为立即数
(2) MOV segreg, mem/reg，不能为CS
(3) 除源操作数为立即数情况外(MOV mem/reg, data)，两个操作数中必须有一个为寄存器
(4) 不允许在两个存储单元或两个段寄存器间直接传送数据
(5) 不影响标志位
(6) 注意传输位数匹配
(7) 段寄存器只能由通用寄存器或存储器赋值
```

##### 2. PUSH/POP SRC

```assembly
PUSH SRC  ;(SP) <- (SP)-2, ((SP)+1,(SP)) <- (SRC)
ex:
PUSH reg16  ;16位数高8位先入栈
PUSH seg_reg
PUSH mem16
PUSH imm  ;在8086中不支持
```
```assembly
POP DST	  ;(DST) <- ((SP)+1, (SP)), (SP) <- (SP)+2
ex:
POP reg16
POP seg_reg  ;除CS
POP mem16
```

必须以字为单位，不影响标志位