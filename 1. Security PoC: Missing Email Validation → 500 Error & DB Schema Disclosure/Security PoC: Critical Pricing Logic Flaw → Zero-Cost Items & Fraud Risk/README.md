##  Security PoC: Critical Pricing Logic Flaw → Zero-Cost Items & Fraud Risk

### Overview
A critical vulnerability was identified in the catalog pricing logic, where certain items could be rendered with a price of zero due to flawed backend validation. This issue originated from incorrect data synchronization between the 1C backend and the web-facing database, allowing attackers to exploit the system for large-scale fraudulent purchases.

| Metric      | Value     | Rationale                                                                 |
|-------------|-----------|---------------------------------------------------------------------------|
| Severity    | Critical  | Enables direct financial loss through unauthorized acquisition of goods. |
| CWE         | CWE-284   | Improper Access Control.                                                  |
| Risk Rating | High      | Exploitation leads to monetary loss and reputational damage.             |

---

###  Impact

- **Financial Loss**: Attackers can place orders for high-value items at zero cost.
- **Reputation Damage**: Public disclosure could erode customer trust and brand integrity.
- **Inventory Disruption**: Unauthorized orders may distort stock levels and logistics.

---

###  Affected System

- **System Type**: E-commerce platform (integrated with 1C backend)
- **Sample Endpoint**: `https://[anonymized-ecommerce-site.com]/catalog/item/[item-id]`

---

###  Steps to Reproduce

1. Intercept or export product data from 1C.
2. Modify the price field to `0.00` or leave it empty.
3. Sync the data with the web catalog.
4. Access the product page and verify the zero price.
5. Add to cart and complete checkout without being charged.

---

###  Proof of Concept

- **Reference**: `<img width="543" height="220" alt="Снимок экрана 2025-11-06 141445" src="https://github.com/user-attachments/assets/23f85b91-bfe9-4a21-b749-e68466eeb367" />
`
- **Tools Used**: Postman

---

###  Recommended Remediation

- **Backend Validation**: Reject zero or negative prices unless explicitly allowed.
- **Business Logic Enforcement**: Block checkout of zero-cost items unless part of a verified promotion.
- **Audit Logging**: Track all pricing changes and sync operations.
- **Monitoring & Alerts**: Detect and alert on anomalous pricing or order patterns.
