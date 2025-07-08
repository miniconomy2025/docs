# 🚚 Bulk Logistics Considerations for YOU 🫵🫵🫵

This document outlines the specifications for the `/logistics` endpoint you are required to expose for processing pickups and deliveries.

## Endpoint: `/logistics`

To facilitate communication for pickups and deliveries, please expose a `/logistics` endpoint. This endpoint will receive a POST request with the following JSON payload.

### JSON Payload Structure

{
  "id": "string | number",
  "type": "string",
  "items": [
    {
      "name": "string",
      "quantity": "number"
    }
  ]
}


## Field Descriptions

### 1. `id` (string | number)

The identifier for the transaction. Its meaning depends on the `type` of operation:

* **For Pickups:** This will be the **Order ID** agreed upon by the parties involved in the purchase.

* **For Deliveries:** This will be the **Pickup Request ID** that we (Bulk Logistics) issued to you upon confirming the pickup request.

### 2. `type` (string)

A simple string indicating the nature of the operation. The possible values are:

* `'PICKUP'`

* `'DELIVERY'`

### 3. `items` (Array)

An array of objects, where each object represents an item being picked up or delivered.

#### Item Object

| Key | Type | Description |
| --- | --- | --- |
| `name` | string | The name of the item. |
| `quantity` | number | The quantity of the item. |