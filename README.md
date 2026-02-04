# SellerCloud SKU Search - n8n Workflow

A reusable n8n sub-workflow for searching and validating SKUs in SellerCloud. Perfect for automation workflows that need to verify product existence before proceeding with operations.

<img width="2020" height="500" alt="image" src="https://github.com/user-attachments/assets/beb474ce-6850-4049-85bf-fc9e4780831b" />

## Use Cases

- **SKU Validation**: Verify if a SKU exists in SellerCloud before creating listings on other platforms
- **Data Synchronization**: Check product availability before syncing inventory across systems
- **Quality Control**: Validate SKUs during data import or migration processes
- **Conditional Workflows**: Branch your automation based on whether products exist in SellerCloud

## What It Does

1. Accepts a SKU as input
2. Authenticates with SellerCloud API
3. Searches for the SKU in your catalog
4. Returns structured data:
   - `sku`: The searched SKU
   - `productName`: Product name if found
   - `existsInSellerCloud`: Boolean (true/false)

## Workflow Structure

```
Input SKU → Get Auth Token → Merge Data → Search SKU → Validate Match → Return Results
```

## Prerequisites

- SellerCloud account with API access
- SellerCloud API credentials (username and password)

## Installation

### 1. Import the Workflow

1. Download `Seller_Cloud_SKU_search_n8n.json` from this repository
2. In your n8n instance, go to **Workflows** → **Import from File**
3. Select the downloaded JSON file
4. Click **Import**

### 2. Configure Credentials

You'll need to update two nodes with your SellerCloud credentials:

#### **Seller Cloud Token Credentials** Node
Replace the placeholder values:
```json
{
  "Username": "your-sellercloud-email@company.com",
  "Password": "your-password-here"
}
```

Update the URL:
```
https://YOUR-COMPANY-NAME.api.sellercloud.us/rest/api/token
```

#### **SKU Results** Node
Update the URL:
```
https://YOUR-COMPANY-NAME.api.sellercloud.us/rest/api/Catalog/GetProductsInView
```

Replace `YOUR-COMPANY-NAME` with your actual SellerCloud subdomain.

## Usage

### As a Sub-Workflow

This workflow is designed to be called from other workflows using the **Execute Workflow** node.

**Example main workflow structure:**
```
Trigger → Execute Workflow (this SKU search) → IF condition → Continue processing
```
<img width="1668" height="613" alt="image" src="https://github.com/user-attachments/assets/7f884659-d52f-49b9-959b-93c90686f817" />

### Standalone Testing

1. Open the workflow in n8n
2. Update the **Input SKU** node with a test SKU value
3. Click **Execute Workflow**
4. Check the output from **Return Data** node

## Configuration Options

### Modify the Input
Change the **Input SKU** node to accept dynamic values from your main workflow instead of the hardcoded placeholder.

### Add Error Handling
Consider adding error handling nodes to manage API failures gracefully.

### Customize Return Data
Modify the **Return Data** code node to include additional fields from the SellerCloud response (e.g., price, quantity, status).

## Security Notes

⚠️ **Important Security Considerations:**

1. **Never commit credentials**: This repository has placeholder values only
2. **Use n8n credentials**: Instead of hardcoding, consider using n8n's credential system
3. **Environment variables**: For self-hosted n8n, use environment variables for sensitive data
4. **API permissions**: Ensure your SellerCloud API user has minimal required permissions

## Troubleshooting

### Authentication Fails
- Verify your SellerCloud username and password
- Check that your company subdomain is correct
- Ensure API access is enabled for your account

### No Results Returned
- Verify the SKU exists in SellerCloud
- Check that the SKU format matches exactly (case-sensitive)
- Review the SellerCloud API response in the execution log

### Workflow Execution Errors
- Enable n8n's execution logging
- Check the individual node outputs
- Verify network connectivity to SellerCloud API


## License

MIT License - Feel free to use and modify for your automation needs.

## Acknowledgments

Built for automating SellerCloud workflows with n8n. Special thanks to the n8n community for the excellent automation platform.

**Note**: This is a sub-workflow component. It's most powerful when integrated into larger automation processes for e-commerce operations, inventory management, or multi-platform listing synchronization.
