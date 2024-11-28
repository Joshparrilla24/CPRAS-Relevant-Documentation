# CPRAS Procurement Platform Documentation
This repository serves as a centralized resource for API and relevant documentation for the CPRAS Procurement Platform. It includes endpoints for creating projects, lots, specifications, social values, and importing data. The repository may be used for temporary or permanent reference, depending on project needs.



# **API ENDPOINTS**

## **Overview**
This document outlines the API endpoints for interacting with the procurement platform. The endpoints cover procurement project management, supplier hub lots, and specifications/social values. Each endpoint includes details about the HTTP method, URL, required form data, and usage notes.


User Token:
```json

eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiI5IiwianRpIjoiOGE0NjIyMjM3ZjVmZDc4OTYxOTc3NDk4NDFhMDk4MWNiNTk4ODZjOWFkY2I4NjBjYzUyZDdlNGYyNDVmMWQ5NTUwNTIxZjI0YTQyNmZhNTkiLCJpYXQiOjE3Mjc5NTQ3MTkuMTI3NzM1LCJuYmYiOjE3Mjc5NTQ3MTkuMTI3NzQzLCJleHAiOjE3NTk0OTA3MTkuMTA4NjcyLCJzdWIiOiIxODEiLCJzY29wZXMiOltdfQ.Q6PTDvgxvSBlVWzbpEz-8HxwQ-2A0HJxxX7U5Ibl0wGSQ1Z9OtRV6yFOhIAB0khNlqBlrZ81pWeJac4QasXshni_Ed-XjeqhjcGojlvQwfyA2eMsVc_Pmpco3hyUEKMipGE12tpvLwY4okGXtsI1FghnQJQm5g1cTPTZdI1YhmnTkDP_egXk9EEEJzstfWcbXt6XHsJhIiACaKH6n8uCYzJRJMXLPxNCfuOkv9XQzpr5iW-d6HYRTayfixoG9GTyrI8K8hXFeeKHugA3FMjNbb8CckMxZn-iYIyqQtThpwsLPdFmKE3eRldF91gP6Q2jS0atvCK5HY68pvN1PFzM9naV6jD7jiVpe1CYCP-4t_B_yER5PrWyUAuer7NErsA0RpYYeRLzXiKiCtyfRisVJRbmhWpVKSnawcBqoSj65o9PzitBBQM7oy5c_iPYpJQ6I0af4r0z02ufbAVkjFuxi7S_W1EetshTxt4m5G2L-doBiH44fY9jUE7Vx2BXa7F0-lgX5nEGffb1Ko69mKaSYSO3qV_-zZprLrMZPnmn_uV_WXkO0_Z-5qFxDBMark-j-0hV2rJEv5tVLH192hxrI7ok0lIpAEaICJwioIhm5idi6TTIw8yPNLEZw5O18firfU8lh7eYOl363rRME7y4zL-9pfvos0oqW-Fau61FUxg
```

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
