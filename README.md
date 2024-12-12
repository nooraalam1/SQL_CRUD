## SQL_CRUD
# Connection

 var mysql = require('mysql2');
 var db = mysql.createConnection({
 host: "localhost",
 user: "root",
 password: "",
 database: "students_db"
 });
