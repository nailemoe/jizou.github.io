## 如何定义自己的事务

通常情况下， 事务是以 case 提交的动作来管理的。
如果在提交 case 前，调用 commit，会导致 case 提交失败。因为调用 commit 时，也会把 case 信息也提交了。包括 case 的锁。

可以通过自定义一个 transaction 的 scope 来管理独立的 transaction。

标记 transaction 开始

```Java
((PegaDatabase)tools.getThread().getDatabase()).setCurrentTransaction(<TransactionName>);
```

标记 transaction 结束

```Java
try{
  ((PegaDatabase)tools.getThread().getDatabase()).assertTransactionComplete();
}catch(Exception e){
  // error handling
}
```
