# Sellfy Backend coding exercise

We're going to build a very simple report tool.

Before we go further, please note that it doesn’t matter if we finish the exercise: we’re looking to see how you break down a problem and turn it into executable code! We are looking for code which:

- is not AI generated
- is readable and maintainable
- is well-testable
- follows the best practices of your chosen language/platform

## Scenario
We collect payments from customers on behalf of our merchants.

In this exercise, we're going to build the reporting tool, which envovles generating a report containing aggregated data about our merchant sales.

## Available data
There is an HTTP API we can use with two endpoints to retrieve following data:

1. A list of IDs of all merchants
2. The payments for each merchant

This API returns the account number for the merchant and list of their transactions. For each transaction, it includes the amount collected (in cents) and a fee (in cents).

## Goal
We'd like to generate a report showing amount of transaction each customer has, total amount transacted, total fee amount, and merchant net revenue after our fee.

You would need to create an application that creates a CSV file in the same folder as your application, called `report.csv`

All of the major components should be testable. The CSV should have a header row with these columns:
- Account ID
- Number of transactions
- Total
- Total fee
- Net revenue

All the amounts should be converted into USD with 2 decimal points.

## Notes
- For some merchants, the total fee might equal 0. In that case, we don't want that merchant in our output.
- No two merchant could have the same account number


## Examples
Getting a list of merchants
```
GET https://raw.githubusercontent.com/Sellfy/test-assignment-backend/refs/heads/master/users.json HTTP/1.1

{
    "data": [
        "U7F9K2",
        "X3DA9Q",
        ...
    ],
    "pagination": {
        "page": 1,
        "total_pages" : 1,
        "total_items": 20
    }
}
```

Getting a list of transactions for a particular merchant
```
GET https://raw.githubusercontent.com/Sellfy/test-assignment-backend/refs/heads/master/users/B4R6Y0.json HTTP/1.1


{
  "id": "B4R6Y0",
  "account": "DY6274930648077057",
  "transactions": [
    {
      "id": "2SMDZQCBZAMD",
      "amount_in_cents": 179965,
      "fee_in_cents": 466
    },
    ....
  ]
}
```
