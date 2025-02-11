---
title: addReturnTracking mutation | Commerce Web APIs
---

# addReturnTracking mutation

The `addReturnTracking` mutation adds customer-entered shipping tracking information to the specified return request. Use the `available_shipping_carriers` object in the [`customer` query](../../customer/queries/customer.md) to retrieve valid `carrier_uid` values.

## Syntax

```graphql
mutation: {
    addReturnTracking(input: AddReturnTrackingInput!): AddReturnTrackingOutput
}
```

## Example usage

The following example adds the shipping carrier and a tracking number for the specified return request.

**Request:**

```graphql
mutation{
  addReturnTracking(input: {
    return_uid: "Mw=="
    carrier_uid: "dXBzLTE="
    tracking_number: "1Z9876543"
  }){
    return_shipping_tracking {
      uid
      carrier {
        uid
        label
      }
      tracking_number
    }
  }
}
```

**Response:**

```json
{
  "data": {
    "addReturnTracking": {
      "return_shipping_tracking": {
        "uid": "Mw==",
        "carrier": {
          "uid": "dXBzLTE=",
          "label": "United Parcel Service"
        },
        "tracking_number": "1Z9876543"
      }
    }
  }
}
```

## Input attributes

The `AddReturnTrackingInput` object must contain the following attributes:

Attribute |  Data Type | Description
--- | --- | ---
`carrier_uid`| ID! | The unique ID of a `ReturnShippingCarrier` object
`return_uid` | ID! | The unique ID of a `Return` object
`tracking_number` | String! | The shipping tracking number for this return request

## Output attributes

The `AddReturnTrackingOutput` object contains the following attributes.

Attribute |  Data Type | Description
--- | --- | ---
`return` | [Return](#return-object) | Contains details about the modified return
`return_shipping_tracking` | [ReturnShippingTracking](#returnshippingtracking-attributes) | Contains details about shipping for a return

### Return object

import Return from '/src/pages/_includes/graphql/return.md'

<Return />

## Related topics

*  [`requestReturn` mutation](request-return.md)
*  [`addReturnComment` mutation](add-return-comment.md)
*  [`removeReturnTracking` mutation](remove-return-tracking.md)
