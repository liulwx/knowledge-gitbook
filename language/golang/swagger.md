## 坑1
```golang
// Package swagger Production Management API 
// 
//     Schemes: http, https 
//     Host: localhost 
//     BasePath: /api/v1 
//     Version: 1.0.0 
// 
//     Consumes: 
//     - application/json 
// 
//     Produces: 
//     - application/json 
// 
// swagger:meta 
package swagger 

import ( 
    _ "gitlab.momenta.works/hdmap-workflow/data-store/router/server" // APIs 
) 

//go:generate swagger generate spec -o files/swagger.json 
//　这个空行不能少，否则会报　unexpected EOF 
```
