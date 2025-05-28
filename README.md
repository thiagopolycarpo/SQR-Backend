# SQR - Backend API (Node.js + Express)

This project was developed based on the **technical test**, which required the creation of a **RESTful API** to simulate production control in an industrial environment.

The API allows querying production orders, viewing records submitted by users, and registering new production records, with specific validation rules.

---

## Implemented Endpoints

### `GET /api/orders/GetOrders`
Returns a list of Production Orders with their respective products and materials.

#### Example Response:
```json
{
  "orders": [
    {
      "order": "111",
      "quantity": 100.00,
      "productCode": "abc",
      "productDescription": "Product ABC",
      "image": "0x000001",
      "cycleTime": 30.3,
      "materials": [
        { "materialCode": "aaa", "materialDescription": "Material A" },
        { "materialCode": "bbb", "materialDescription": "Material B" }
      ]
    }
  ]
}
```

### `GET /api/orders/GetProduction?email=user@example.com`
Returns the list of production records registered by a user based on their email.

#### Example Response:
```json
{
  "productions": [
    {
      "order": "111",
      "date": "2023-11-10T10:30:00Z",
      "quantity": 50,
      "materialCode": "aaa",
      "cycleTime": 28.5
    }
  ]
}
```

### `POST /api/orders/SetProduction`
Registers a new production record.

#### Request Body:
```json
{
  "email": "user@example.com",
  "order": "111",
  "productionDate": "2023-11-10",
  "productionTime": "10:30:00",
  "quantity": 50,
  "materialCode": "aaa",
  "cycleTime": 28.5
}
```

#### Validations:
- The email must exist in the system.
- The order must be registered.
- The production date must be within the allowed period.
- The quantity must be > 0 and <= the order quantity.
- The material must be listed in the order.
- The cycle time must be > 0. If it is less than the standard cycle time, an alert is returned.

#### Example Response:
```json
{
  "status": 200,
  "type": "S",
  "description": "Production record registered successfully."
}
```

## 🛠️ Technologies Used
- Node.js
- Express
- Docker
- Swagger (Automatic documentation)
- Postman (Collections available)
- Local data mock (JSON)

## How to Run Locally
> Requirements: Docker or Node.js installed

### Using Docker
```bash
docker build -t sqr-backend .
docker run -p 3000:3000 sqr-backend
```

### Manually (dev mode)
```bash
npm install
npm run dev
```

The API will be available at `http://localhost:3000`.

## Swagger Documentation
After running the project, access:

`http://localhost:3000/api-docs`

## Postman Tests
A test collection is available in this repository:

`SQR_Postman_Collection.json` (add this file here)

## Notes
- Data is simulated with JSON mocks to facilitate testing.
- This backend is compatible with the Angular and React frontends available in the main repository.
