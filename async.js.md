## Async 简介
由于 JavaScript 的异步特性，使用 JS 执行很多操作时都会使用到回调函数。如果代码的逻辑稍微复杂一些，就很容易掉入 **Callback Hell**，如下面的代码：
```JS
var title = 'It is a new post';

connection.beginTransaction(function(err) {
  if (err) { throw err; }
  connection.query('INSERT INTO posts SET title=?', title, function(err, result) {
    if (err) {
      return connection.rollback(function() {
        throw err;
      });
    }

    var log = 'Post ' + result.insertId + ' added';

    connection.query('INSERT INTO log SET data=?', log, function(err, result) {
      if (err) {
        return connection.rollback(function() {
          throw err;
        });
      }
      connection.commit(function(err) {
        if (err) {
          return connection.rollback(function() {
            throw err;
          });
        }
        console.log('success!');
      });
    });
  });
});
```
AsyncJS 可以解决回调层级过深的问题。
### async.each
async.each并不能保证执行成功一条SQL语句后再去执行下一条，所以如果有一条执行失败，不会影响到其他语句的执行。
```JS
var sqls = [
  "INSERT INTO log SET data='data1'",
  "INSERT INTO log SET data='data2'",
  "INSERT INTO log SET data='data3'"
];

async.each(sqls, function(item, callback) { // callback 是 async.each 的第三个参数定义的方法
  // 遍历每条SQL并执行
  connection.query(item, function(err, results) {
    if(err) {
      // 异常后调用callback并传入err
      callback(err);
    } else {
    console.log(item + "执行成功");
      // 执行完成后也要调用callback，不需要参数
      callback();
    }
  });
}, 
function(err) { // 第一个参数必须为 err
  // 所有SQL执行完成后回调
  if(err) {
    console.log(err);
  } else {
    console.log("SQL全部执行成功");
  }
});
```
----
### async.eachSeries
如果想要实现执行成功上一条语句后再开始执行数组中下一条语句，可以使用eachSeries函数：
```JS
var sqls = [
  "INSERT INTO log SET data='data1'",
  "INSERT INTO log SET data='data2'",
  "INSERT INTO log SET data='data3'"
];

async.eachSeries(sqls, function(item, callback) {
  // 遍历每条SQL并执行
  connection.query(item, function(err, results) {
    if(err) {
      // 异常后调用callback并传入err
      callback(err);
    } else {
      console.log(item + "执行成功");
      // 执行完成后也要调用callback，不需要参数
      callback();
    }
  });
}, function(err) {
  // 所有SQL执行完成后回调
  if(err) {
    console.log(err);
  } else {
    console.log("SQL全部执行成功");
  }
});
```
----
### async.forEachOf
类似于async.each，区别是可以接收Object类型参数，并且会在第二个参数回调函数中传入遍历到的每一项的key，更适合批量执行查询语句并返回结果：
```JS
var sqls = {
  table_a: "select count(*) from table_a",
  table_b: "select count(*) from table_b",
  table_c: "select count(*) from table_c"
};

// 用于存放查询结果
var counts = {};

async.forEachOf(sqls, function(value, key, callback) {
  // 遍历每条SQL并执行
  connection.query(value, function(err, results) {
    if(err) {
      callback(err);
    } else {
      counts[key] = results[0]['count(*)'];
      callback();
    }
  });
}, function(err) {
  // 所有SQL执行完成后回调
  if(err) {
    console.log(err);
  } else {
    console.log(counts);
  }
});
// 结果： { table_a: 26, table_b: 3, table_c: 2 }
```
----
### async.map
上面的async.forEachOf获取多条Select语句的查询结果的代码可以使用async.map函数简化成这样:
```JS
var sqls = {
  table_a: "select count(*) from table_a",
  table_b: "select count(*) from table_b",
  table_c: "select count(*) from table_c"
};

async.map(sqls, function(item, callback) {
  connection.query(item, function(err, results) {
    callback(err, results[0]['count(*)']);
  });
}, function(err, results) {
  if(err) {
    console.log(err);
  } else {
    console.log(results);
  }
});
```
----
### async.series
#### async.series按顺序执行多条任务
```JS
var title = 'It is a new post';

// 用于在posts插入成功后保存自动生成的ID
var postId = null;

// function数组，需要执行的任务列表，每个function都有一个参数callback函数并且要调用
var tasks = [function(callback) {
  // 开启事务
  connection.beginTransaction(function(err) {
    callback(err);
  });
}, function(callback) {
  // 插入posts
  connection.query('INSERT INTO posts SET title=?', title, function(err, result) {
    postId = result.insertId;
    callback(err);
  });
}, function(callback) {
  // 插入log
  var log = 'Post ' + postId + ' added';
  connection.query('INSERT INTO log SET data=?', log, function(err, result) {
    callback(err);
  });
}, function(callback) {
  // 提交事务
  connection.commit(function(err) {
    callback(err);
  });
}];

async.series(tasks, function(err, results) {
  if(err) {
    console.log(err);
    connection.rollback(); // 发生错误事务回滚
  }
  connection.end();
});
```
#### 按顺序获取多条SQL的结果
```JS
// tasks是一个Object
var tasks = {
  table_a: function(callback) {
    connection.query('select count(*) from table_a', function(err, result) {
      callback(err, result[0]['count(*)']); // 将结果传入callback
    });
  },
  table_b: function(callback) {
    connection.query('select count(*) from table_b', function(err, result) {
      callback(err, result[0]['count(*)']);
    });
  },
  table_c: function(callback) {
    connection.query('select count(*) from table_c', function (err, result) {
      callback(err, result[0]['count(*)']);
    });
  }
};

async.series(tasks, function(err, results) {
  if(err) {
    console.log(err);
  } else {
    console.log(results);
  }
  connection.end();
});
```
----
### async.waterfall
按顺序执行多条任务并且下一条任务可获取上一条任务的执行结果
```JS
var title = 'It is a new post';

var tasks = [function(callback) {
  connection.beginTransaction(function(err) {
    callback(err);
  });
}, function(callback) {
  connection.query('INSERT INTO posts SET title=?', title, function(err, result) {
    callback(err, result.insertId); // 生成的ID会传给下一个任务
  });
}, function(insertId, callback) {
  // 接收到上一条任务生成的ID
  var log = 'Post ' + insertId + ' added';
  connection.query('INSERT INTO log SET data=?', log, function(err, result) {
    callback(err);
  });
}, function(callback) {
  connection.commit(function(err) {
    callback(err);
  });
}];

async.waterfall(tasks, function(err, results) {
  if(err) {
    console.log(err);
    connection.rollback(); // 发生错误事务回滚
  }
  connection.end();
});
```
----