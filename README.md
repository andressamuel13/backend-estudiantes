### opciones activas:

- target: procurar ser lo más cercano a la versión LTS de EcmaScript. (2020 en este caso)
    - Antes:
        
        ![image.png](attachment:0a69051b-225c-44e4-8bc9-c6a1d1d652c4:image.png)
        
    - Después:
        
        ![image.png](attachment:8c01047e-3b00-4b55-9fa4-63233a3bffd5:image.png)
        
- outDir: la ruta o carpeta de compilación del código ts, debe estar dentro de una carpeta aislada del código principal de ts, para prevenir desorden.
    - Antes: outDir comentado.
        
        ![image.png](attachment:6a4c54e7-79da-45b5-bd43-503047903f56:image.png)
        
    - Después: se debe des comentar esta sección y especificar la ruda o carpeta donde se va a transpilar el código ts.
        
        ![image.png](attachment:d0a68839-8b9a-44a3-9b9e-9ae0bbc4a7c4:image.png)
        
- Si no se van a usar las opciones comentadas, es buena práctica dejarlas des comentadas para mejorar legibilidad.
    - Antes:
    - 
        
        ![image.png](attachment:b778a53d-76a1-493c-b6cc-a06a85198719:image.png)
        
    - ahora:
        
        ```json
        {
          "compilerOptions": {
            "target": "es2020",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */
            "module": "commonjs",                                /* Specify what module code is generated. */
            "outDir": "./dist",                                   /* Specify an output folder for all emitted files. */                      /* Specify the output directory for generated declaration files. */
            "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */
            "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */
            "strict": true,                                      /* Enable all strict type-checking options. */                 /* Disable error reporting for unreachable code. */
            "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */
          }
        }
        ```
        
    

### package.json

- caret:
    
    ```json
    {
      "name": "prochr",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@types/bcryptjs": "^3.0.0", // <- Posible problema
        "@types/dotenv": "^8.2.3", // <- Posible problema
        "@types/express": "^5.0.1", // <- Posible problema
        "@types/jsonwebtoken": "^9.0.9", // <- Posible problema
        "ts-node-dev": "^2.0.0", // <- Posible problema
        "typescript": "^5.8.3" // <- Posible problema
      },
      "dependencies": {
        "mysql2": "^3.14.1" // <- Posible problema
      }
    }
    ```
    

- caret: Es recomendable quitar el caret (^) de cada dependencia para prevenir errores futuros por conflictos con las mismas.
    
    ```json
    {
      "name": "prochr",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@types/bcryptjs": "3.0.0", // <- Corrección
        "@types/dotenv": "8.2.3", // <- Corrección
        "@types/express": "5.0.1", // <- Corrección
        "@types/jsonwebtoken": "9.0.9", // <- Corrección
        "ts-node-dev": "2.0.0", // <- Corrección
        "typescript": "5.8.3" // <- Corrección
      },
      "dependencies": {
        "mysql2": "3.14.1" // <- Corrección
      }
    }
    
    ```
    

- type:
    
    ![image.png](attachment:7146089f-96df-4ade-989c-c1dfbb888d1d:image.png)
    
- type: el tipo debe corresponder con el tipo que se va a usar, en este caso, el proyecto está escrito en commonjs, por lo que module genera errores (para este caso o la cambiamos o la eliminamos, yo opté por eliminarla).

- antes:
    
    ```
    {
      "name": "prochr",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "type": "module",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@types/bcryptjs": "^3.0.0",
        "@types/dotenv": "^8.2.3",
        "@types/express": "^5.0.1",
        "@types/jsonwebtoken": "^9.0.9",
        "ts-node-dev": "^2.0.0",
        "typescript": "^5.8.3"
      },
      "dependencies": {
        "mysql2": "^3.14.1"
      }
    }
    
    ```
    

- ahora:
    
    ```
    {
      "name": "prochr",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@types/bcryptjs": "3.0.0",
        "@types/dotenv": "8.2.3",
        "@types/express": "5.0.1",
        "@types/jsonwebtoken": "9.0.9",
        "ts-node-dev": "2.0.0",
        "typescript": "5.8.3"
      },
      "dependencies": {
        "mysql2": "3.14.1"
      }
    }
    
    ```
    

## Instalación de dependencias:

- express: ya que no se le especifica al sistema qué tiene que instalar, el mismo, no puede saber que tiene que instalar express ni las dependencias de tipos de express.
    1. Instalación de express para js:
        
        ```bash
        npm install express
        ```
        
    2. Instalación de los tipos para ts:
        
        ```bash
        npm install --save-dev @types/express
        ```
        
    
- Esto, generará cambios en `package-log.json` y en `package.json`, por lo que ahora, quedaría así:
    
    ```json
    {
      "name": "prochr",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "",
      "license": "ISC",
      "devDependencies": {
        "@types/bcryptjs": "3.0.0",
        "@types/dotenv": "8.2.3",
        "@types/express": "5.0.1",
        "@types/jsonwebtoken": "9.0.9",
        "ts-node-dev": "2.0.0",
        "typescript": "5.8.3"
      },
      "dependencies": {
        "express": "5.1.0",
        "mysql2": "3.14.1"
      }
    }
    ```
    

## Ejecución:

- Antes:
    - Comando `tsc -w`:
        
        ```bash
        [12:23:33 p.m.] Starting compilation in watch mode...
        
        app.ts:1:21 - error TS2307: Cannot find module 'express' or its corresponding type declarations.
        
        1 import express from 'express';
                              ~~~~~~~~~
        
        app.ts:2:20 - error TS2307: Cannot find module 'dotenv' or its corresponding type declarations.
        
        2 import dotenv from 'dotenv';
                             ~~~~~~~~
        
        app.ts:11:14 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        11 const port = process.env.PORT || 3000;
                        ~~~~~~~
        
        config/conecction.ts:1:20 - error TS2307: Cannot find module 'mysql2/promise' or its corresponding type declarations.
        
        1 import mysql2 from 'mysql2/promise';
                             ~~~~~~~~~~~~~~~~
        
        config/conecction.ts:2:20 - error TS2307: Cannot find module 'dotenv' or its corresponding type declarations.
        
        2 import dotenv from 'dotenv';
                             ~~~~~~~~
        
        config/conecction.ts:6:11 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        6     host: process.env.DB_HOST,
                    ~~~~~~~
        
        config/conecction.ts:7:11 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        7     user: process.env.DB_USER,
                    ~~~~~~~
        
        config/conecction.ts:8:15 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        8     password: process.env.DB_PASSWORD,
                        ~~~~~~~
        
        config/conecction.ts:9:15 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        9     database: process.env.DB_DATABASE,
                        ~~~~~~~
        
        config/conecction.ts:10:19 - error TS2580: Cannot find name 'process'. Do you need to install type definitions for node? Try `npm i --save-dev @types/node`.
        
        10     port : Number(process.env.DB_PORT),
                             ~~~~~~~
        
        controllers/student.controller.ts:1:35 - error TS2307: Cannot find module 'express' or its corresponding type declarations.
        
        1 import { Request, Response } from "express";
                                            ~~~~~~~~~
        
        Helpers/generateHash.ts:1:20 - error TS2307: Cannot find module 'bcryptjs' or its corresponding type declarations.
        
        1 import bcrypt from "bcryptjs";
                             ~~~~~~~~~~
        
        Helpers/generateToken.ts:1:17 - error TS2307: Cannot find module 'jsonwebtoken' or its corresponding type declarations.
        
        1 import jwt from 'jsonwebtoken';
                          ~~~~~~~~~~~~~~
        
        routes/student.routes.ts:1:24 - error TS2307: Cannot find module 'express' or its corresponding type declarations.
        
        1 import { Router } from "express";
                                 ~~~~~~~~~
        
        [12:23:34 p.m.] Found 14 errors. Watching for file changes.
        
        ```
        
    - Comando `node app.js`:
        
        ```bash
        file:///C:/Users/Zamch/Desktop/qqq/coding/backend-students/app.js:5
        Object.defineProperty(exports, "__esModule", { value: true });
                              ^
        
        ReferenceError: exports is not defined in ES module scope
        This file is being treated as an ES module because it has a '.js' file extension and 'C:\Users\Zamch\Desktop\qqq\coding\backend-students\package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
            at file:///C:/Users/Zamch/Desktop/qqq/coding/backend-students/app.js:5:23
            at ModuleJob.run (node:internal/modules/esm/module_job:274:25)
            at async onImport.tracePromise.__proto__ (node:internal/modules/esm/loader:644:26)
            at async asyncRunEntryPointWithESMLoader (node:internal/modules/run_main:116:5)    
        
        Node.js v22.15.0
        PS C:\Users\Zamch\Desktop\qqq\coding\backend-students> 
        ```
        

- Ahora:
    - Comando `tsc -w`:
        
        ```bash
        [12:27:14 p.m.] Starting compilation in watch mode...
        
        [12:27:15 p.m.] Found 0 errors. Watching for file changes.
        ```
        
    - Comando `node app.js`:
        
        ```bash
        Server is running on port 3000
        ```
