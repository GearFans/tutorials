## Gear 合约中的常用方法

### exec

```rust
gstd::exec::block_timestamp() // 获取当前时间
gstd::exec::block_height() // 获取当前区块高度
gstd::exec::program_id() // 获取当前程序的id
gstd::exec::value_available // 获取当前余额

gstd::exec::exit // 终止程序的执行

```

详细资料：https://docs.gear.rs/gstd/exec/index.html

### msg

```rust
gstd::msg::id // 获取消息 Id
gstd::msg::source //获取消息发送者的钱包地址，类似 solidity 中的msg.sender

gstd::msg::load // 获取发送给合约的消息
gstd::msg::load_bytes // 获取发送给合约的消息

gstd::msg::reply // 发送一条新信息作为对当前正在处理的信息的回复
gstd::msg::reply_bytes // 发送一条新信息作为对当前正在处理的信息的回复
gstd::msg::reply_to // 获取当前handle_reply函数被调用的初始信息的标识符

gstd::msg::send_bytes // 向合约或者用户发现新消息
gstd::msg::send // 向合约或者用户发现新消息

```

详细资料：https://docs.gear.rs/gstd/msg/index.html
