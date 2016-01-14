# SQLCipher-For-FMDB
FMDB 创建加密数据库的时候需要用到这两个文件   
如果想使用FMDB 创建一个加密的数据库，就需要用到这两个文件了。   
具体用法如下：   
第一步：导入 FMDB   
第二步：导入SQLCipher的两个文件   
第三步：设置 Build Settings -> Other C Flags:   
-DSQLITE_HAS_CODEC   
-DSQLITE_THREADSAFE   
-DSQLCIPHER_CRYPTO_CC   
-DSQLITE_TEMP_STORE=2   
第四步：设置 Build Setting -> Other Link Flags:    
输入这个：-framework "Security"      带着引号复制进去   
第五步：修改 FMDB 的文件：   
在 FMDatabase.m文件里面有两个方法: -open   -openWithFlag:，修改如下：   
if(err != SQLITE_OK){   
  NSLog(@"error opening!:%d", err);   
}else if(err == SQLITE_OK){//   
  [self setKey:@"数据库密码"];//   
}//上面这三行是新加的代码   
   
然后运行，创建的数据库就是加密的数据库了   

