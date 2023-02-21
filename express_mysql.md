```javascript

const express = require("express"); // express 모듈 로드
const app = express(); // express 서버 객체 생성
const port = '8080'; // 포트번호

/* post response 처리 필수 함수 */
app.use(express.json());
app.use(express.urlencoded({extended: true}));

const mysql = require('mysql2');  // mysql 모듈 로드
let connection = mysql.createConnection({  // mysql 접속 설정
  host: 'localhost',
  port: '3306',
  user: 'root',
  password: '1234',
  database: 'warehouse'
}); // DB 커넥션 생성

connection.connect();   // DB 접속

app.listen(port, () => {
  console.log(`Listening Port ${port}`);
});

app.post('/', (req, resp) => {  
  let sql = "INSERT INTO `s`(`SNO`,`SNAME`,`STATUS`,`CITY`) VALUES ('S" + req.body.sno + "','" + req.body.sname + "', " + parseInt(Math.random() * 10) + ",'" + req.body.city + "')";

  connection.query(sql, function (err, results, fields) {
    if (err) {
      console.log(err);
    }
    console.log(results);
  });
});

```
