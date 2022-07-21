## Issues

1. How do we express contract offers that have no start or end dates?
2. Can we specify validation constraints

## Notes

1. Contract offers of the type "valid 6 months from signing" specify a duration and have no start or end date.
2. Need to specify precedence: contract end date supercedes duration.
3. Offer start and end do not need to align with contract start and end.
4. Validation constraints requiring one property to be greater than another is not possible in JSON Schema. We need a note that explains what happens when an end date is less than
   or equal to a start date (the contract offer should be rejected).
