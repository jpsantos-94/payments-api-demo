# Payments API Demo

## Overview
A working test-mode payment flow on Stripe, demonstrating creation,
confirmation, failure handling, event delivery and safe retries.

## The flow
1. Create a customer
2. Create and confirm a PaymentIntent (success)
3. Show the decline path
4. Prove idempotency on a retry

## Example calls

$ curl -i https://api.stripe.com/v1/payment_intents   -u $STRIPE_KEY:   -d amount=5000   -d currency=eur   -d "payment_method_types[]=card"   -d payment_method=pm_card_visa   -d confirm=true

$ curl https://api.stripe.com/v1/customers?limit=2 -u $STRIPE_KEY:

$ curl -v https://api.stripe.com/v1/payment_intents   -u $STRIPE_KEY: -H "Idempotency-Key: demo-key-004"  -d amount=2000   -d currency=eur   -d "payment_method_types[]=card"   -d payment_method=pm_card_visa   -d confirm=true

$ curl https://api.stripe.com/v1/payment_intents   -u $STRIPE_KEY:   -d amount=2000   -d currency=eur   -d "payment_method_types[]=card"   -d payment_method=pm_card_authenticationRequired   -d confirm=true

## Key concepts shown
- Idempotency keys (no double charges)
- Webhooks (event-driven reconciliation)
- SCA / 3D Secure (requires_action)

## Why it matters in payments
Two or three sentences on double-charge prevention, real-time
reconciliation and the regulatory dimension.
