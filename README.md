# CPRAS Procurement Platform Documentation
This repository serves as a centralized resource for API and relevant documentation for the CPRAS Procurement Platform. It includes endpoints for creating projects, lots, specifications, social values, and importing data. The repository may be used for temporary or permanent reference, depending on project needs.



# **API ENDPOINTS**

## **Overview**
This document outlines the API endpoints for interacting with the procurement platform. The endpoints cover procurement project management, supplier hub lots, and specifications/social values. Each endpoint includes details about the HTTP method, URL, required form data, and usage notes.

### **Authentication Strategy**
The API uses a Bearer Token for authentication. This token must be included in the ```Authorization``` header for all requests.

```json
Authorization: Bearer <access_token>
```

### **How to Use**
1. Retrieve the Access Token:
  - Obtain a valid ```access_token``` from the authentication system.
2. Include the Token in Requests:
  - Add the ```Authorization``` header with the Bearer Token in your API requests.
3. Example Request:
```json
curl -X GET "https://staging.api.cpras.co.uk/api/procurement_projects" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```
4. Postman example
- In Postman, under the "Authorization" tab:
  - Set the Type to ```Bearer Token```.
  - Paste the token into the Token field.
    
Header Format:

## **1. Procurement Project**

### **a. Create Procurement Project**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/procurement_projects`
- **Form Data**:
  - `type` (string)
  - `name` (string)
  - `description` (string)
  - `status` (string, default: `PEN`)
  - `main_description` (string)
  - `common_description` (string)
  - `my_files_description` (string)
  - `qa_description` (string)
  - `my_questions_description` (string)
  - `spec_description` (string)

#### Sample Response:
```json
{
    "procurement_projects": {
        "type": "FMK",
        "name": "Sample Post Project",
        "description": "Sample Description",
        "status": "PEN",
        "user_id": 1,
        "id": 56
    },
    "message": "Procurement Project has been created successfully"
}
```
---

### **b. Import Procurement Projects**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/procurement_projects/import_projects`
- **Form Data**:
  - `file` (file)

Sample response:
```json
{
    "message": "Successfully imported 1 new projects",
    "status": 1
}
```
---

## **2. Supplier Hub Lots**

### **a. Create Supplier Hub Lot**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/supplierhub-lots`
- **Form Data**:
  - `name` (string)
  - `short_description` (string)
  - `long_description` (string)
  - `pin_notice_id` (integer, optional, null if `itt_framework_id` is provided)
  - `itt_framework_id` (integer, optional, null if `pin_notice_id` is provided)

Sample response:
```json
{
    "lot": {
        "id": 34,
        "name": "Sample Post Lot",
        "is_archived": false,
        "pin_notice_id": "21",
        "created_at": "2024-11-27T04:07:44.000000Z",
        "updated_at": "2024-11-27T04:07:44.000000Z",
        "short_description": "Sample Short Description",
        "long_description": "Sample Long Description",
        "user": {
            "id": 1,
            "name": "jasonadmin",
            "company_name": "Test Company 1 edited"
        },
        "pin_pricing_setting": {
            "supplierhub_lot_id": 34,
            "transaction_volume": 100000,
            "total_usage_cost": 80,
            "total_setup_cost": 20,
            "direction": ">=",
            "transaction_type": "value",
            "preferred_years": 10,
            "id": 7
        }
    }
}
```

---

### **b. Import Supplier Hub Lots**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/supplierhub-lots/import_supplierhublots`
- **Form Data**:
  - `file` (file)
  - `pin_notice_id` (integer, optional, null if `itt_framework_id` is provided)
  - `itt_framework_id` (integer, optional, null if `pin_notice_id` is provided)

Sample response:
```json
{
    "message": "Successfully imported 1 new supplier hub lots",
    "status": 1
}
```

---

## **3. Supplier Hub Specification/Social Values**

### **a. Create Specification/Social Value**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/supplierhub-specs`
- **Form Data**:
  - `name` (string)
  - `type` (string)
  - `unit` (string)
  - `direction` (string)
  - `threshold_value` (number)
  - `kind` (integer, `0` for specification, `1` for social values)
  - `supplierhub_lot_id` (integer, ID of the supplier hub lot)

Sample response:
```json
{
    "success": true
}
```
---

### **b. Import Specifications/Social Values**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/supplierhub-specs/import`
- **Form Data**:
  - `file` (file)
  - `kind` (integer, `0` for specification, `1` for social values)
  - `lot_id` (integer, ID of the supplier hub lot)

Sample response:
```json
{
    "status": 1,
    "success": true
}

```
---

## **4. Supplier Hub File**

### **a. Create Supplier Hub File**
- **Method**: `POST`
- **Endpoint**: `https://staging.api.cpras.co.uk/api/supplier-hub/files`
- **Form Data**:
  - `files[]` (array of files)
  - `file_names[]` (array of corresponding file names)
  - `uploaded_by` (integer, user ID of the uploader with supplier hub admin role)
  - `type` (integer, `1` for common file)
  - `pin_notice_id` (integer, optional, null if `itt_framework_id` is provided)
  - `itt_framework_id` (integer, optional, null if `pin_notice_id` is provided)
  - `supplierhub_lot_id` (integer, optional, ID of the supplier hub lot)

Sample response:
```json
{
    "message": "Supplier has been created successfully"
}
```
