# Connection-MSSQL-con-NodeJS
Connecting mssql database with nodeJS

## Con el packete mssql

```
import sql from 'mssql'

const config = {
  user: process.env.DB_USER,
  password: process.env.DB_PWD,
  database: process.env.DB_NAME,
  server: 'localhost',
  pool: {
    max: 10,
    min: 0,
    idleTimeoutMillis: 30000
  },
  options: {
    encrypt: true, // for azure
    trustServerCertificate: true // change to true for local dev / self-signed certs
  }
}

sql.connect(config).then(async () => {
  return await sql.query`select * from Personas`
}).then(result => {
  console.dir(result)
}).catch(err => {
  console.dir('err: ', err)
})
```

## Con Sequelize

```
const config = {
  server: 'localhost',
  user: process.env.DB_USER ?? '',
  password: process.env.DB_PWD ?? '',
  database: process.env.DB_NAME ?? ''
}
const sequelize = new Sequelize(config.database, config.user, config.password, {
  host: config.server,
  dialect: 'mssql'
})
```
