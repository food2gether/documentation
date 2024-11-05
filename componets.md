# Frontend
 - IndexJSX
 - Robin macht das schon :)

# Backend
 - Login/Auth Service
    -  POST `/` -> POST https://food2gether.com/api/login
       Parameter: name: String, password: String
       Return: success: boolean, token: String
 - Account Service
   -   :/create
   -   :/edit
   -   :/delete
   -   :/get (search)
 - Session Service (Order eigener Service??)
   -   GET `/:sessionId`
   -   PUT `/:sessionId`
   -   POST `/:sessionId`
   -   DELETE `/:sessionId`
   -   GET `/:sessionId/order`
   -   PUT `/:sessionId/order`
   -   POST `/:sessionId/order`
   -   DELETE `/:sessionId/order`
 - Restaurant Service
   -   :/get (search)
   -   :/create
   -   :/edit
   -   :/delete
   -   :/:id/menu/add
   -   :/:id/menu/edit
   -   :/:id/menu/delete
   -   :/:id/menu/get
