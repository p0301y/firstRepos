## nodejs的加密技术
- md5加密技术与bcrypt加密技术

    md5加密是采用hash算法，将一个字符串转化成16bytes的字符串存储在数据库中
    例如password对应的是"afkajfklaa678fafa..."，它的速度比较快，换句话说效率比较高
    ，但是安全性差；相比与md5,bcrypt技术就更加安全，在md5的基础上，采用了加盐“salt”算法
    生成一个随机数salt，然后在数据库中记录salt和h=(pwd + salt)，查询的时候得到用户口令p
    ，然后从数据库中查出salt，计算hash(p + salt),看是不是等于h

```javascript
comparePassword: function (_password,cb) {
        var password = bcrypt.hashSync(_password, bcrypt.genSaltSync(SALT_WORK_FACTOR));
        var isMatch = bcrypt.compareSync(_password, password)
        cb(null,isMatch)
}
```

