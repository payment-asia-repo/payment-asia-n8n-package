# n8n-nodes-paymentasia

This is an n8n community node. It lets you use Payment Asia in your n8n workflows.

Payment Asia is a payment gateway service that supports multiple payment methods including Alipay, WeChat Pay, Credit Cards, FPS, Octopus, PayMe, and CUP (China UnionPay).

[n8n](https://n8n.io/) is a [fair-code licensed](https://docs.n8n.io/sustainable-use-license/) workflow automation platform.

[Installation](#installation)
[Operations](#operations)
[Credentials](#credentials)
[Compatibility](#compatibility)
[Usage](#usage)
[Resources](#resources)
[Version history](#version-history)

## Installation

Follow the [installation guide](https://docs.n8n.io/integrations/community-nodes/installation/) in the n8n community nodes documentation.

## Operations

This node supports the following operations:

### Payment Resource

| Operation                      | Description                                                                                                                                        |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Create Payment**             | Create a new payment transaction with support for multiple payment methods (Alipay, Credit Card, CUP, FPS, Octopus, PayMe, WeChat Pay, UserDefine) |
| **Payment Query**              | Query payment details by merchant reference                                                                                                        |
| **Settlement**                 | Retrieve settlement transactions for a specific date                                                                                               |
| **Direct Credit Card Payment** | Create payment with direct credit card details (requires PCI compliance)                                                                           |

### Create Payment Parameters

| Parameter          | Required | Description                                                                              |
| ------------------ | -------- | ---------------------------------------------------------------------------------------- |
| Amount             | Yes      | Payment amount in the smallest currency unit                                             |
| Currency           | Yes      | Three-letter ISO currency code (e.g., HKD, USD, EUR)                                     |
| Merchant Reference | Yes      | Unique identifier for the order in your system                                           |
| Payment Method     | Yes      | Payment method to use (Alipay, CreditCard, CUP, Fps, Octopus, PayMe, UserDefine, Wechat) |
| Return URL         | No       | URL to redirect the customer after payment completion                                    |
| Customer Email     | No       | Customer email address                                                                   |
| Notify URL         | No       | For receiving datafeed after payment                                                     |
| Subject            | No       | The name or keywords of the order                                                        |

### Direct Credit Card Payment Parameters

| Parameter          | Required | Description                     |
| ------------------ | -------- | ------------------------------- |
| Amount             | Yes      | Payment amount                  |
| Currency           | Yes      | Three-letter ISO currency code  |
| Merchant Reference | Yes      | Unique identifier for the order |
| Card Number        | Yes      | Credit card number              |
| Card Expiry Year   | Yes      | Card expiry year (YYYY format)  |
| Card Expiry Month  | Yes      | Card expiry month (MM format)   |
| CVV                | Yes      | Card verification value         |

> **Note**: Direct Credit Card Payment requires PCI DSS compliance.

## Credentials

To use this node, you need to authenticate with Payment Asia API using an API Key.

### Prerequisites

1. **Register for a Payment Asia Merchant Account**
   - Visit [Payment Asia Onboarding](https://application.pa-sys.com/knMDz9YbO0) to sign up
   - Complete the merchant application process
   - Wait for account approval

2. **Obtain Your API Key**
   - Log in to the [Payment Asia Merchant Portal](https://merchant.pa-sys.com/)
   - Navigate to **Settings** or **API Settings** section
   - Find your **API Key** (API 金鑰)
   - Copy the API Key for use in n8n

### Configure Credentials in n8n

1. Go to **Settings** > **Credentials** in your n8n instance
2. Click **Add Credential**
3. Search for and select **Payment Asia API**
4. Enter your **API Key** (API 金鑰)
5. Click **Save**

The credential uses the `X-API-KEY` header for authentication with the Payment Asia API.

## Compatibility

- Tested with n8n version 1.0+
- Requires n8n-workflow peer dependency

## Usage

### Creating a Payment

1. Add the **Paymentasia** node to your workflow
2. Select **Payment** as the resource
3. Select **Create Payment** as the operation
4. Configure the payment details:
   - Set the amount and currency
   - Provide a unique merchant reference
   - Select the payment method
   - Optionally set return URL and customer details
5. Execute the node to create the payment request

### Querying a Payment

1. Select **Payment Query** operation
2. Enter the merchant reference used during payment creation
3. The node will return the current payment status and details

### Getting Settlement Transactions

1. Select **Settlement** operation
2. Enter the settlement date
3. Optionally specify a page number for pagination
4. The node will return all settlement transactions for that date

## Resources

- [n8n community nodes documentation](https://docs.n8n.io/integrations/#community-nodes)
- [Payment Asia API Documentation](https://merchant.pa-sys.com/services/online-payments/api-documents)
- [Payment Asia Merchant Portal](https://merchant.pa-sys.com/)

## Version history

### 2.0.2

- Initial release with Payment Asia integration
- Support for Create Payment, Payment Query, Settlement, and Direct Credit Card Payment operations
- Multiple payment method support (Alipay, WeChat Pay, Credit Card, FPS, Octopus, PayMe, CUP)
