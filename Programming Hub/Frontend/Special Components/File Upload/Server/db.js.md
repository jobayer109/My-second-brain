```js
const { Pool } = require("pg");


const pool = new Pool({
  user: "postgres",
  host: "localhost",
  database: "cmsdb",
  password: "t@im@15.5.22#",
  port: 5432,
});
 

module.exports = pool;
```
