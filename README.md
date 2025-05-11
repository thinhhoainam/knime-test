# Pool Values REST API

A FastAPI-based REST API to manage pools of values and query quantiles with two POST endpoints: append/insert values and query quantiles. Data is stored in memory.

## Requirements
- Python 3.8+
- pip

## Installation
1. Install dependencies:
   ```bash
   pip install fastapi uvicorn pydantic numpy
   ```

## Running the API
1. Run the server:
   ```bash
   uvicorn main:app --reload
   ```
2. Access at `http://localhost:8000`. Use `http://localhost:8000/docs` for Swagger UI.

## API Endpoints

### POST `/append`
Add values to a pool.

- **Request**:
  ```json
  {
    "poolId": 123,
    "poolValues": [1, 7, 2, 6]
  }
  ```
- **Response**:
  - New pool: `{"status": "inserted"}`
  - Existing pool: `{"status": "appended"}`
- **Example**:
  ```bash
  curl -X POST "http://localhost:8000/append" -H "Content-Type: application/json" -d '{"poolId": 123, "poolValues": [1, 7, 2, 6]}'
  ```

### POST `/query`
Query a pool's quantile.

- **Request**:
  ```json
  {
    "poolId": 123,
    "percentile": 99.5
  }
  ```
- **Response**:
  ```json
  {
    "quantile": 7,
    "count": 4
  }
  ```
- **Example**:
  ```bash
  curl -X POST "http://localhost:8000/query" -H "Content-Type: application/json" -d '{"poolId": 123, "percentile": 99.5}'
  ```
- **Errors**:
  - 400: Invalid input.
  - 404: Pool not found/empty.

## Run Test
```bash
pytest
```
