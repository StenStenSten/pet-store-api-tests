# API Test Summary

**Framework:** Jest + Supertest  
**Language:** JavaScript (Node.js)  
**API:** Swagger Petstore  
**Base URL:** `https://petstore.swagger.io/v2`

---

## Endpoints Tested

- `POST /pet` – Create a new pet with valid and invalid data  
- `GET /pet/{petId}` – Retrieve pet by ID (existing and non-existing)  
- `PUT /pet` – Update pet details  
- `DELETE /pet/{petId}` – Delete a pet and confirm it's removed  
- `GET /pet/findByStatus` – Filter pets by status (valid and edge cases)

---

## Test Scenarios

### Functional Tests
- Successfully create a new pet using `POST /pet`
- Retrieve a pet by its ID using `GET /pet/{petId}`
- Update the pet’s name and status with `PUT /pet`
- Delete the pet and verify deletion with `DELETE /pet/{petId}`
- Get pets by status using `GET /pet/findByStatus`

### Negative Tests
- Attempt to get a pet that doesn’t exist (expect `404 Not Found`)
- Try deleting a pet twice (second call still returns `200 OK`)
- Create a pet with missing required fields (e.g. no name or photoUrls)
- Use invalid pet ID formats (e.g. string instead of number)

### Edge Case Tests
- Create a pet with only minimal fields provided
- Send unexpected values to the `status` query (e.g. `?status=banana`)

---

## Observations

- The API accepts minimal data during pet creation (only `id`, `name`, and `photoUrls` required)
- Deleting a non-existent or already-deleted pet still returns `200 OK` instead of `404`
- Invalid input (like string IDs) doesn’t always trigger clear validation errors
- Querying pets with an invalid status value doesn’t return an error—it just returns an empty array
- **Console Warnings:**
  - "Pet not found after creation — Swagger API may not have saved it."
  - "Pet still accessible after deletion — API may not actually delete it."
- These warnings indicate the API's inconsistent behavior regarding pet persistence and deletion.


