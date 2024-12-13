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
# Client
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

# Client
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
