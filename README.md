# Amazon Vendor Central MCP server (Amazon Vendor Central MCP) by Kuudo

Run every Amazon Vendor Central function from your AI agents: Direct Fulfillment, Retail Procurement, Data Kiosk, Retail Analytics, and A+ Content.

[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-8A2BE2?style=flat-square)](https://modelcontextprotocol.io/) [![Registry](https://img.shields.io/badge/MCP%20Registry-io.github.KuudoAI%2Famazon--vendor--central--mcp-blue?style=flat-square)](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.KuudoAI%2Famazon-vendor-central-mcp&version=latest) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE) [![Community](https://img.shields.io/badge/Kuudo-community-D97757?style=flat-square)](https://github.com/KuudoAI/community)

Product page: https://www.kuudo.com/features/amazon-vendor-central-mcp/ · Docs: https://www.kuudo.com/docs/mcp-reference/tools/ · Pricing: https://www.kuudo.com/pricing.md

## Connect

Kuudo runs in your own cloud. The Community plan deploys one instance of each Amazon MCP server into your account, and your client connects to that deployment:

```json
{
  "mcpServers": {
    "amazon-vendor-central-mcp": {
      "url": "https://<your-host>/mcp",
      "headers": {
        "Authorization": "Bearer <your Kuudo API key>"
      }
    }
  }
}
```

Replace `<your-host>` with the hostname of your deployment and the bearer value with your Kuudo API key.

## What this repository is

This repository holds registry metadata and a catalog-only stub. Live execution runs in your Kuudo deployment. The server source is not published. The stub in `src/` answers `tools/list` with the catalog below, serves the same catalog as one resource (`kuudo://catalog/tools.json`), offers one prompt (`connect`) carrying the setup guidance, and returns an error with that guidance on any call, so registries and clients can inspect the surface without any access to Amazon.

### Inspect the catalog locally with Docker

The image runs the same catalog-only stub over stdio. It is not the live server.

```bash
docker build -t amazon-vendor-central-mcp .
docker run -i --rm amazon-vendor-central-mcp
```

Point a client at it with a stdio entry:

```json
{
  "mcpServers": {
    "amazon-vendor-central-mcp-catalog": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "amazon-vendor-central-mcp"]
    }
  }
}
```

## Tools

40 API operations exposed as 40 tools across 12 Selling Partner API resources. This catalog lists the Vendor-prefixed Selling Partner API resources. Vendor Retail Analytics, Data Kiosk, and A+ Content reach vendor data through shared Selling Partner resources your deployment also exposes. The production server's built-in setup and status tools are not listed here.

Argument schemas are not published in this catalog: every tool carries an empty object schema, and the live server in your deployment validates the real parameters on each call.

| Resource | Operations |
| --- | ---: |
| VendorDFI | 1 |
| VendorDirectFulfillmentOrders20211228 | 3 |
| VendorDirectFulfillmentOrdersV1 | 3 |
| VendorDirectFulfillmentPaymentsV1 | 1 |
| VendorDirectFulfillmentShipping20211228 | 11 |
| VendorDirectFulfillmentShippingV1 | 9 |
| VendorDirectFulfillmentTransactions20211228 | 1 |
| VendorDirectFulfillmentTransactionsV1 | 1 |
| VendorInvoicesV1 | 1 |
| VendorOrdersV1 | 4 |
| VendorShipmentsV1 | 4 |
| VendorTransactionStatusV1 | 1 |

<details>
<summary>Every operation (40)</summary>

| Tool | Access | What it does |
| --- | --- | --- |
| `VendorDFI_submitInventoryUpdate` | write | Submits inventory updates for the specified warehouse for either a partial or full feed of inventory items. |
| `VendorDirectFulfillmentOrders20211228_submitAcknowledgement` | write | Submits acknowledgements for one or more purchase orders. |
| `VendorDirectFulfillmentOrders20211228_getOrders` | read | Returns a list of purchase orders created during the time frame that you specify. |
| `VendorDirectFulfillmentOrders20211228_getOrder` | read | Returns purchase order information for the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentOrdersV1_submitAcknowledgement` | write | Submits acknowledgements for one or more purchase orders. |
| `VendorDirectFulfillmentOrdersV1_getOrders` | read | Returns a list of purchase orders created during the time frame that you specify. |
| `VendorDirectFulfillmentOrdersV1_getOrder` | read | Returns purchase order information for the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentPaymentsV1_submitInvoice` | write | Submits one or more invoices for a vendor's direct fulfillment orders. |
| `VendorDirectFulfillmentShipping20211228_createContainerLabel` | write | Creates a container (pallet) label for the associated shipment package. |
| `VendorDirectFulfillmentShipping20211228_getCustomerInvoices` | read | Returns a list of customer invoices created during a time frame that you specify. |
| `VendorDirectFulfillmentShipping20211228_getCustomerInvoice` | read | Returns a customer invoice based on the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentShipping20211228_getPackingSlips` | read | Returns a list of packing slips for the purchase orders that match the criteria specified. |
| `VendorDirectFulfillmentShipping20211228_getPackingSlip` | read | Returns a packing slip based on the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentShipping20211228_submitShipmentConfirmations` | write | Submits one or more shipment confirmations for vendor orders. |
| `VendorDirectFulfillmentShipping20211228_submitShipmentStatusUpdates` | write | This operation is only to be used by Vendor-Own-Carrier (VOC) vendors. |
| `VendorDirectFulfillmentShipping20211228_getShippingLabels` | read | Returns a list of shipping labels created during the time frame that you specify. |
| `VendorDirectFulfillmentShipping20211228_submitShippingLabelRequest` | write | Creates a shipping label for a purchase order and returns a transactionId for reference. |
| `VendorDirectFulfillmentShipping20211228_getShippingLabel` | read | Returns a shipping label for the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentShipping20211228_createShippingLabels` | write | Creates shipping labels for a purchase order and returns the labels. |
| `VendorDirectFulfillmentShippingV1_getCustomerInvoices` | read | Returns a list of customer invoices created during a time frame that you specify. |
| `VendorDirectFulfillmentShippingV1_getCustomerInvoice` | read | Returns a customer invoice based on the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentShippingV1_getPackingSlips` | read | Returns a list of packing slips for the purchase orders that match the criteria specified. |
| `VendorDirectFulfillmentShippingV1_getPackingSlip` | read | Returns a packing slip based on the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentShippingV1_submitShipmentConfirmations` | write | Submits one or more shipment confirmations for vendor orders. |
| `VendorDirectFulfillmentShippingV1_submitShipmentStatusUpdates` | write | This API call is only to be used by Vendor-Own-Carrier (VOC) vendors. |
| `VendorDirectFulfillmentShippingV1_getShippingLabels` | read | Returns a list of shipping labels created during the time frame that you specify. |
| `VendorDirectFulfillmentShippingV1_submitShippingLabelRequest` | write | Creates a shipping label for a purchase order and returns a transactionId for reference. |
| `VendorDirectFulfillmentShippingV1_getShippingLabel` | read | Returns a shipping label for the purchaseOrderNumber that you specify. |
| `VendorDirectFulfillmentTransactions20211228_getTransactionStatus` | read | Returns the status of the transaction indicated by the specified transactionId. |
| `VendorDirectFulfillmentTransactionsV1_getTransactionStatus` | read | Returns the status of the transaction indicated by the specified transactionId. |
| `VendorInvoicesV1_submitInvoices` | write | Submit new invoices to Amazon. |
| `VendorOrdersV1_submitAcknowledgement` | write | Submits acknowledgements for one or more purchase orders. |
| `VendorOrdersV1_getPurchaseOrders` | read | Returns a list of purchase orders created or changed during the time frame that you specify. |
| `VendorOrdersV1_getPurchaseOrder` | read | Returns a purchase order based on the purchaseOrderNumber value that you specify. |
| `VendorOrdersV1_getPurchaseOrdersStatus` | read | Returns purchase order statuses based on the filters that you specify. |
| `VendorShipmentsV1_SubmitShipmentConfirmations` | write | Submits one or more shipment confirmations for vendor orders. |
| `VendorShipmentsV1_GetShipmentDetails` | read | Returns the Details about Shipment, Carrier Details, status of the shipment, container details and other details related to shipment based on the filter parameters value that you specify. |
| `VendorShipmentsV1_SubmitShipments` | write | Submits one or more shipment request for vendor Orders. |
| `VendorShipmentsV1_GetShipmentLabels` | read | Returns small parcel shipment labels based on the filters that you specify. |
| `VendorTransactionStatusV1_getTransaction` | read | Returns the status of the transaction that you specify. |

</details>

## Set up your client
- [Quick Start: Activepieces MCP](https://www.kuudo.com/docs/quick-start/activepieces/)
- [Quick Start: Google Antigravity](https://www.kuudo.com/docs/quick-start/antigravity/)
- [Quick Start: ChatGPT Skills](https://www.kuudo.com/docs/quick-start/chatgpt-skills/)
- [Quick Start: ChatGPT](https://www.kuudo.com/docs/quick-start/chatgpt/)
- [Quick Start: Claude](https://www.kuudo.com/docs/quick-start/claude-ai/)
- [Quick Start: Claude Skills](https://www.kuudo.com/docs/quick-start/claude-app-skills/)
- [Quick Start: Claude Code MCP](https://www.kuudo.com/docs/quick-start/claude-code-mcp/)
- [Quick Start: Claude Cowork for Amazon Workflows](https://www.kuudo.com/docs/quick-start/claude-cowork-amazon/)
- [Quick Start: Claude Code Skills](https://www.kuudo.com/docs/quick-start/claude-skills/)
- [Quick Start: Codex Skills](https://www.kuudo.com/docs/quick-start/codex-skills/)
- [Quick Start: Codex](https://www.kuudo.com/docs/quick-start/codex/)
- [Quick Start: Hermes MCP](https://www.kuudo.com/docs/quick-start/hermes/)
- [Quick Start: Lovable](https://www.kuudo.com/docs/quick-start/lovable/)
- [Quick Start: n8n MCP](https://www.kuudo.com/docs/quick-start/n8n/)
- [Quick Start: NanoClaw MCP](https://www.kuudo.com/docs/quick-start/nanoclaw/)
- [Quick Start: OpenAI API](https://www.kuudo.com/docs/quick-start/openai-api/)
- [Quick Start: OpenClaw MCP](https://www.kuudo.com/docs/quick-start/openclaw/)
- [Quick Start: Perplexity MCP](https://www.kuudo.com/docs/quick-start/perplexity/)

## Playbooks

Operator guides grounded in Amazon's own documentation, each with the artifact the agent produces:
- [Read the ARA Sales Dashboard Without Mixing Views](https://www.kuudo.com/guides/vendor-ara-sales-dashboard/)
- [Why A+ Submissions Fail, and How to Clear Each One](https://www.kuudo.com/guides/vendor-aplus-error-resolution/)
- [A+ Content Without the Seven-Day Rejection Loop](https://www.kuudo.com/guides/vendor-aplus-content-automation/)
- [Automate Vendor Listing Quality at Catalog Scale](https://www.kuudo.com/guides/vendor-listing-quality-automation/)
- [Fix Catalog Identity Before You Write A+ Content](https://www.kuudo.com/guides/vendor-catalog-data-preflight/)
- [The ARA Report and Metric Glossary for Vendors](https://www.kuudo.com/guides/vendor-ara-reports-metric-glossary/)
- [Find ASIN Margin Leakage in the Net PPM Dashboard](https://www.kuudo.com/guides/vendor-net-ppm-margin-leakage/)
- [Dispute a PO On-Time Accuracy Chargeback](https://www.kuudo.com/guides/vendor-po-chargeback-disputes/)

## How it compares
- [Kuudo vs agentcentral for Amazon MCP](https://www.kuudo.com/compare/kuudo-vs-agentcentral/)

## Reads, writes, approvals

Read tools are safe to call freely. Write tools are guarded and can require approval before anything changes on Amazon. The full read-versus-write split is documented at https://www.kuudo.com/docs/mcp-reference/tools/.

## Kuudo

- Website: https://www.kuudo.com/
- Docs: https://www.kuudo.com/docs/
- Guides: https://www.kuudo.com/guides/
- Community, bugs, and questions: https://github.com/KuudoAI/community
- Roadmap: https://github.com/orgs/KuudoAI/projects
- Machine-readable: https://www.kuudo.com/llms.txt · https://www.kuudo.com/pricing.md

Generated from KuudoAI/marketing. Do not edit by hand; changes are overwritten on the next sync.
