# Product Description of Credit tCard

### Introduction
** Summary **
-------------
The Accounts API lets you retrieve account and transaction data for Citi Customers who have authorized your app. In most cases, you'll want to request a summary of all accounts first, which will return basic account information and account IDs. Once you have this information, you can request additional account details and/or transactions. The API can return information for cards, checking, savings, loans, line of credit and brokerage accounts. The API can also provide encrypted PII data such as Account Routing Number (decryption guide can be found [here](https://sandbox.developerhub.citi.com/decryption_guide)).We are working hard to extend this API to return additional types of accounts. Stay tuned for more!
> ENDPOINTS ON THIS PAGE
> -----------------------
1. Retrieve details of all accounts
2. Retrieve routing number(clear text) and encrypted account number of a specific account
3. Retrieve transactions

> GET /v2/accounts/details	Retrieve details of all accounts
> 
> GET /v2/accounts/{accountId}/encrypt/accountRoutingNumber	Retrieve routing number(clear text) and encrypted account number of a specific account
> 
> GET /v2/accounts/{accountId}/transactions	Retrieve transactions
>
## Retrieve details of all accounts
### /v2/accounts/details
### Description
---------------
Returns account details for all accounts held by Citi customers who have authorized your app. For example, if a customer has multiple credit card accounts, the accounts will be returned in the array creditCardAccountsDetails within accountGroupDetails.
Currently, the API supports cards, checking & savings, loans, line of credit, brokerage and retirement accounts.
**EXAMPLE REQUEST**

```
curl --request GET \

  --url https://sandbox.apihub.citi.com/gcb/api/v2/accounts/details \
  --header 'accept: REPLACE_THIS_VALUE' \
  --header 'authorization: REPLACE_THIS_VALUE' \
  --header 'client_id: REPLACE_THIS_VALUE' \
  --header 'uuid: REPLACE_THIS_VALUE'
  
  ```
  ## Header Parameters
  
 |Authorization|String|
 |---|---|
 |             |The most recent Authorization token. This will have the format Bearer + {space} + {accessToken}. Example: Bearer KGNsaWVudF9pZDpjbGllbnRfc2VjcmV0KQ==.|
  |UUID|String|
  |             |128 bit random UUID generated uniquely for every request|
  |Accept|String|
  |             | Content-Type that are acceptable for the response|
  |client_id|String|
  |             | client_id generated during consumer onboarding|
  
  ## Responses
  
  **200    OK**
  
  Successful operation
  
  ## Example Response for GET /v2/accounts/details
  
  ```
  {
  "accountGroupDetails": [
    {
      "accountGroup": "CHECKING",
      "checkingAccountsDetails": [
        {
          "productName": "Business Checking",
          "accountNickname": "My checking account",
          "accountDescription": "Business Checking - 9594",
          "balanceType": "ASSET",
          "displayAccountNumber": "XXXXXX9594",
          "accountId": "da549a7cc86472ee05272c7bd0a4483f57174f2110e7ad961a267995031fda66c6d5475de467a65739750107b621e5a01be7cc0dc085a825fa384795904293f6",
          "currencyCode": "USD",
          "accountStatus": "ACTIVE",
          "currentBalance": 10000.25,
          "availableBalance": 15000.25
        }
      ],
      "savingsAccountsDetails": [
        {
          "productName": "Citi Gold Savings Account",
          "accountNickname": "Personal Savings Account",
          "accountDescription": "Citi Gold Savings Account - 2033",
          "balanceType": "ASSET",
          "displayAccountNumber": "XXXXXX2033",
          "accountId": "da549a7cc86472ee05272c7bd0a4483f57174f2110e7ad961a267995031fda66c6d5475de467a65739750107b621e5a01be7cc0dc085a825fa384795904293f6",
          "currencyCode": "USD",
          "accountStatus": "ACTIVE",
          "currentBalance": 10000.25,
          "availableBalance": 15000.25,
          "maturityDate": "2020-06-03",
          "maturityTerm": "2 years"
        }
      ],
      "creditCardAccountsDetails": [
        {
          "productName": "Citi Rewards+? Card",
          "accountDescription": "Citi Rewards+? Card - 7899",
          "balanceType": "LIABILITY",
          "displayAccountNumber": "XXXXXXXXXXXX7899",
          "accountId": "8035a60debb671e89bd451c9ad0f283e8f1b8868dd4dc65520ceb7bdfeb4142999f574c9db37917ef0edfae296745142543e3ad2bc034887f37212ecbde83ee0",
          "currencyCode": "USD",
          "accountStatus": "ACTIVE",
          "availableCredit": 15000,
          "creditLimit": 20000,
          "purchasesAPR": 23.45,
          "minimumDueAmount": 1500,
          "paymentDueDate": "2017-03-27",
          "currentBalance": 10000.25,
          "lastStatementBalance": 5000.25,
          "lastStatementDate": "2019-02-27",
          "advancesAPR": 23.45,
          "cashAdvanceLimit": 5000,
          "cashAdvanceAvailableAmount": 2500,
          "lastPaymentAmount": 1500.25,
          "lastPaymentDate": "2019-06-12",
          "ctdPurchaseBalanceAmount": 300.25,
          "purchaseSpendLimitAmount": 2000,
          "remainingPurchaseSpendAmount": 1699.75
        }
      ],
      "loanAccountsDetails": [
        {
          "productName": "Personal Loan",
          "balanceType": "LIABILITY",
          "displayAccountNumber": "XXXXX1035",
          "accountDescription": "Personal Loan-1035",
          "accountNickname": "My personal loan",
          "accountId": "d8cf4b23b3a7f74fd441e93697c15fe2fe8714afdfa1d1dc619b1d2ccda41edfa965598333d790b1e2de05a4c55176094a0cc632ff4ddbe9704f10e787fa64f9",
          "currencyCode": "USD",
          "currentBalanceAmount": 10000,
          "creditAvailableAmount": 9000,
          "paymentDueAmount": 400,
          "paymentDueDate": "2017-03-27",
          "autoPayFlag": true,
          "lastPaymentAmount": 500,
          "lastPaymentDate": "2015-06-12"
        }
      ],
      "lineOfCreditAccountsDetails": [
        {
          "productName": "Checking Plus Line of Credit",
          "balanceType": "LIABILITY",
          "displayAccountNumber": "XXXXX1035",
          "accountDescription": "Checking Plus Line of Credit-1035",
          "accountNickname": "Checking plus account",
          "accountId": "da549a7cc86472ee05272c7bd0a4483f57174f2110e7ad961a267995031fda66c6d5475de467a65739750107b621e5a01be7cc0dc085a825fa384795904293f6",
          "currencyCode": "USD",
          "accountStatus": "ACTIVE",
          "creditAvailableAmount": 9000,
          "currentBalanceAmount": 10000,
          "paymentDueAmount": 5000,
          "lastPaymentAmount": 4000
        }
      ],
      "brokerageAccountsDetails": [
        {
          "accountId": "da549a7cc86472ee05272c7bd0a4483f57174f2110e7ad961a267995031fda66c6d5475de467a65739750107b621e5a01be7cc0dc085a825fa384795904293f6",
          "displayAccountNumber": "XXXXX1035",
          "accountRegistrationType": "RETAIL",
          "accountTradingCapableFlag": true,
          "balanceType": "ASSET",
          "productName": "Brokerage IRA",
          "accountDescription": "Brokerage IRA-1035",
          "brokerageAccountTransactionTypes": [
            "CASH"
          ],
          "accountHoldings": [
            {
              "currencyCode": "USD",
              "cusip": "140194101",
              "holdingCategory": "Equities",
              "quantity": 100,
              "securityName": "American Funds Capital Income Builder.",
              "asOfDateTime": "2020-01-21T18:28:00.000+0000",
              "assetClass": "EQUITY",
              "symbol": "CAIFX",
              "price": 32.41,
              "totalValueAmount": 324.1,
              "changeInPercent": -0.1,
              "changeInPrice": -0.015,
              "changeInValue": -10,
              "previousPrice": 31
            }
          ],
          "totalPortfolioBalanceAmount": "3643150.72"
        }
      ],
      "retirementAccountsDetails": [
        {
          "productName": "Rollover IRA",
          "balanceType": "ASSET",
          "displayAccountNumber": "XXX2766",
          "accountDescription": "Rollover IRA-2766",
          "accountId": "bd0fbd58e6e3d2fec034a0f4d8a41f8f0533b7f93a02a11d3fa80f7a66c62ebdd77d0dd67787d4e4f0e4949116937f429748535d1698ae0bab6e7122e884bb02",
          "accountValue": 9000.15,
          "accountStatus": "ACTIVE",
          "asOfDateTime": "2020-04-10",
          "retirementPlanComponents": [
            {
              "componentName": "Variable CD-2766",
              "currencyCode": "USD",
              "currentTerms": "2 years",
              "totalValueAmount": 4676.36,
              "interestPaidYTD": 324.12,
              "nextMaturityDate": "2020-06-03"
            }
          ]
        }
      ],
      "totalCurrentBalance": {
        "localCurrencyCode": "USD",
        "localCurrencyBalanceAmount": 8900.12
      },
      "totalAvailableBalance": {
        "localCurrencyCode": "USD",
        "localCurrencyBalanceAmount": 8900.12
      }
    }
  ],
  "customer": {
    "customerId": "bd12a6d89815aed77be876225b9a2c7f6648f0af82e84198f49d1b7e51a23fae1621936bc1addf5fdceca25c3aae5f92071fb1d6218dae32ca83b199c29962ee"
  }
}
  
  ```
  

### Definitions
-----------------
accountGroupDetails

accountGroup type : string

Account group is a classification of accounts according to their common characteristics. Values include: CHECKING, SAVINGS, CREDITCARD, LOAN, LINEOFCREDIT, BROKERAGE AND RETIREMENT

![Capture](https://user-images.githubusercontent.com/119153191/204854179-accd1ce6-1858-4f32-86cf-69919b779db1.JPG)
