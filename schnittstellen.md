# Schnittstellen Spezifikation

# Frontend
 - IndexJSX
 - Robin macht das schon :)

# Backend

## Authentication-Service

### POST `/`

#### Headers

#### Parameters

#### Response
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
