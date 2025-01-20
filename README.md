# Connection

    var mysql = require('mysql2');
    var db = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "",
    database: "students_db"
    });

# Fetch (Server)
    app.get('/fetch', (req, res) => {
    const q = "SELECT * from students"
    db.query(q,(err,data)=>{
    if(err) return res.json(err)
    return res.json(data) 
    })
    })
# Fetch (Client)
    const [data, setData] = useState([])
    useEffect(() => {
        axios.get('http://localhost:3000/fetch')
            .then(res => setData(res.data))
            .catch(err => console.log(err))
    }, [])

# Create (Server)
    app.post('/create',(req,res)=>{
    const {id, name, roll, fees, classs,medium} = req.body
    const q = 'INSERT INTO students(id, name, roll, fees, class, medium) VALUES (?,?,?,?,?,?)'
    db.query(q, [id, name, roll, fees, classs, medium],(err,data)=>{
    if(err) return res.json(err)
    return res.json(data) 
    })
    })

#  Create (Client)
    const handleSubmit = (e) => {
        e.preventDefault()
        const id = e.target.id.value;
        const name = e.target.name.value;
        const roll = e.target.roll.value;
        const fees = e.target.fees.value;
        const classs = e.target.classs.value;
        const medium = e.target.medium.value;
        console.log(id, name, roll, fees, classs, medium)
        const values = { id, name, roll, fees, classs, medium }
        axios.post('http://localhost:3000/create', values)
            .then(res => console.log(res.data))
            .catch(err => console.log(err))
    }
# Delete (Server)
    app.delete('/cartItems', (req, res) => {
    const { email, id } = req.query; 
    const sqlQuery = "DELETE FROM cart WHERE email = ? AND _id = ?";
    db.query(sqlQuery, [email, id], (err, result) => {
      if (err) {
        console.log(err)
          return res.status(500).send('Error deleting cart item');
      }
      res.status(200).send('Cart item deleted successfully');
    });
    });

# Delete (Client)
    function handleDelete(x){
    
    const id = x._id;       
    axios.delete(`http://localhost:3000/cartItems?email=${user?.email}&&id=${id}`) 
    then(res => console.log(res.data))
    .catch(err => console.log(err));         
        
    }





# Add Unique Email To DB
    app.post('/userInfo',(req,res)=>{
    const {name,email} = req.body
    const q ="INSERT INTO user_info (name, email) SELECT ?, ? WHERE NOT EXISTS (SELECT 1 FROM user_info WHERE email = ?)";
    db.query(q, [name,email,email],(err,data)=>{
    if(err) return res.json(err)
    return res.json(data) 
    })
    })
