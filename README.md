# Connection

    var mysql = require('mysql2');
    var db = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "",
    database: "students_db"
    });

# Fetch
    app.get('/fetch', (req, res) => {
    const q = "SELECT * from students"
    db.query(q,(err,data)=>{
    if(err) return res.json(err)
    return res.json(data) 
    })
    })
