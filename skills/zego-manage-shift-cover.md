---
name: Manage Zego shift cover for a customer
description: Activate and deactivate Zego insurance cover for a gig-economy customer by opening and closing a shift, after confirming the customer is valid.
api: openapi/zego-partner-openapi.yml
operations: [validateCustomerNumber, getCustomerStatus, startShift, endShift]
---

# Manage Zego shift cover

Use the Zego Partner API to turn a customer's insurance cover on and off around a work shift.

## Prerequisites
- A partner authorization token issued by the Zego Partnerships Manager. Send it in the `Authorization` header on every request.
- Base URL: `https://api.zego.com`

## Steps
1. **Validate the customer.** Call `validateCustomerNumber` (`GET /v1/validate/customer-number/{customerNumber}`) to confirm the Zego customer number exists. A `404` means the number is unknown — stop.
2. **Check status (optional).** Call `getCustomerStatus` (`GET /v1/user/status/`) to confirm the customer's current insurance status before starting cover.
3. **Start cover.** Call `startShift` (`POST /v1/shift/login/`) to begin the shift and activate cover.
4. **End cover.** When the shift finishes, call `endShift` (`POST /v1/shift/logout/`) to deactivate cover.

## Rules
- Errors are signalled by HTTP status: `400` invalid request, `401` bad/missing token, `404` not found.
- No idempotency-key header is documented; avoid blind retries on writes.
- For many customers at once, use `startBatchShifts` / `endBatchShifts` instead of the single-customer calls.
