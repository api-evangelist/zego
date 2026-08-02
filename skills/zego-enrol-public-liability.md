---
name: Enrol a Zego customer on public liability cover
description: Register a customer, look up their occupation, enrol them on public liability, and issue a one-day fixed-term public liability policy via the Zego Partner API.
api: openapi/zego-partner-openapi.yml
operations: [registerCustomer, listPublicLiabilityOccupations, enrolCustomerPublicLiability, createPolicy]
---

# Enrol a Zego customer on public liability

## Prerequisites
- Partner authorization token in the `Authorization` header.
- Base URL: `https://api.zego.com`

## Steps
1. **Register the customer.** Call `registerCustomer` (`POST /v2/customer/register/`) to create the customer in Zego.
2. **Resolve the occupation.** Call `listPublicLiabilityOccupations` (`GET /v2/public-liability-occupations/`) to get the supported occupation codes and pick the matching one.
3. **Enrol on public liability.** Call `enrolCustomerPublicLiability` (`POST /v2/customer/enrol/public-liability/`) with the customer and occupation.
4. **Issue a policy.** Call `createPolicy` (`POST /v2/policy/`) to create a one-day fixed-term public liability policy.

## Rules
- Use the v2 endpoints for this flow.
- Errors are signalled by HTTP status: `400` invalid request, `401` bad/missing token.
- No idempotency-key header is documented; do not blindly retry policy creation.
