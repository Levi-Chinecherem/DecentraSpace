
## DecentraSpace Backend Architecture

The backend is designed as a REST API-driven architecture with all critical business logic, services, and integrations encapsulated in well-defined modules. Each module is accessible via endpoints, enabling easy consumption by any frontend, ensuring flexibility for future expansions across various frontend clients.

### Core Backend Modules and Responsibilities

#### 1. **User Management and Authentication**
   - **Web3 Wallet Authentication**: Authentication via wallet signature requests to verify the user’s identity without centralized credentials.
   - **Account Tier Management**: Manages user subscription tiers (Free, Paid), enforcing tier-based restrictions directly from the backend.
   - **Admin Panel API**: Admin access for user and policy management, such as adjusting free-tier duration or changing account statuses.
   
   **Endpoints**:
   - `/auth/login/`: Authenticate users via wallet signature.
   - `/auth/tier/`: Retrieve and update account tier (admin only).
   - `/auth/manage/`: Admin endpoints for user management.

#### 2. **GitHub Integration**
   - **Account Linking & Management**: Allows users to link GitHub accounts, limited by tier. Paid users can link up to three accounts; additional links incur charges.
   - **Continuous Deployment**: Deploy directly from GitHub repositories with webhooks for automated deployment.
   - **Unlink/Re-Link GitHub Accounts**: Allows dynamic re-assignment of linked GitHub accounts.

   **Endpoints**:
   - `/github/link/`: Link a GitHub account.
   - `/github/unlink/`: Unlink an existing GitHub account.
   - `/github/deploy/`: Trigger a deployment for a linked repository.

### 3. **Billing and Credit System**
   - **Payment Options**: Users can purchase credits through decentralized means using Polygon tokens or through centralized card-based payment systems like Paystack, enabling global access, especially for African countries.
   - **Pay-As-You-Go Billing**: Tracks user credits and deducts them for paid services in real-time, whether paid via cryptocurrency or card.
   - **Service-Specific Billing**: Each service (hosting, domain, database) deducts credits based on consumption, including service pause/resume states.
   - **Credit Balance and Usage Reports**: Detailed reporting on credit consumption for user reference and transparency.

   **Endpoints**:
   - `/billing/balance/`: Get the user’s current credit balance.
   - `/billing/deduct/`: Deduct credits for a specific service usage.
   - `/billing/history/`: Retrieve credit usage history.
   - `/billing/recharge/`: Recharge credits using either Polygon tokens or centralized payment methods.
   - `/billing/payment-methods/`: List available payment methods (cryptocurrency, credit card) and their details.

#### 4. **Decentralized Storage and File Management**
   - **IPFS & Arweave Integration**: Direct interaction with IPFS and Arweave to store user-uploaded files, providing decentralized access to assets.
   - **Folder Structure & Organization**: Paid users can organize files into folders (images, videos, documents) for easier management, all with unique access links.
   - **Service-Specific Pause/Resume**: Each file storage service can be individually paused and resumed, with credits deducted only for active services.

   **Endpoints**:
   - `/storage/upload/`: Upload files to IPFS or Arweave.
   - `/storage/folder/`: Create and manage file folders.
   - `/storage/manage/`: Pause or resume storage services.

#### 5. **Domain Name and DNS Management**
   - **Domain Purchase & Renewal**: Enables domain name purchases and renewals (traditional and decentralized DNS).
   - **Domain Linking & Verification**: Verifies user ownership and links custom domains to hosted sites.
   - **Decentralized DNS Support**: Allows linking blockchain-based domains (e.g., ENS, Handshake) with hosted content.

   **Endpoints**:
   - `/domain/purchase/`: Purchase a domain name.
   - `/domain/link/`: Link a domain to a hosting service.
   - `/domain/unlink/`: Unlink or release a domain.

#### 6. **Site Hosting and Deployment Management**
   - **Static & Dynamic Hosting Services**: Supports hosting for static and dynamic sites, depending on user tier.
   - **Deployment Monitoring**: Tracks deployment status and monitors site uptime, accessible via analytics endpoints.
   - **Service Expiration Control**: Free-tier sites are automatically marked for expiration after six months unless upgraded.

   **Endpoints**:
   - `/hosting/deploy/`: Deploy a new site (GitHub or manual upload).
   - `/hosting/status/`: Check the deployment and hosting status.
   - `/hosting/expire/`: Check or set site expiration date (admin only).

#### 7. **Smart Contract and Blockchain Integration**
   - **Credit Management Contracts**: Smart contracts manage credit balances and service deductions, with event listening for service deactivation when credits run out.
   - **Domain Ownership Verification**: Uses blockchain-based verification for domain ownership, ensuring that only verified owners can link domains.
   - **Event Listeners for Credit Monitoring**: Real-time listening to credit-related events (e.g., "Credit Depleted") to notify or pause user services.

   **Endpoints**:
   - `/blockchain/credit/`: Interact with smart contracts for credit deduction or recharge.
   - `/blockchain/ownership/`: Verify domain ownership.
   - `/blockchain/listener/`: Endpoint to receive blockchain events.

#### 8. **Analytics and Performance Monitoring**
   - **User-Specific Site Analytics**: Collects data on site performance (traffic, uptime, load times) and provides visual analytics through the frontend.
   - **Credit Usage Analytics**: Detailed breakdowns of credit usage by service for transparency and budget management.
   - **System Health and Monitoring**: Tracks backend system health, with reports available for administrators to ensure uptime.

   **Endpoints**:
   - `/analytics/site/`: Fetch performance metrics for a user’s site.
   - `/analytics/credit/`: Fetch credit usage analytics.
   - `/analytics/system/`: Admin-only system health metrics.

---

### Backend Workflow and Logic Summary

1. **User Authentication**:
   - Wallet-based login provides an access token, allowing users to interact with DecentraSpace APIs securely.
   
2. **Service Management**:
   - Each service endpoint (storage, hosting, domain) checks for sufficient credit before processing requests.
   - Pausing or resuming services updates both the backend database and blockchain (if needed), with charges applied only for active services.

3. **Data & File Storage**:
   - Upon file upload, the system sends data to IPFS/Arweave and returns a content hash or URL for decentralized access.
   
4. **Domain Management**:
   - Domain verification ensures blockchain ownership matches the wallet address of the user requesting the link.
   
5. **Deployment Process**:
   - GitHub or manual uploads trigger deployment services, with site monitoring data updated post-deployment.

6. **Billing**:
   - Smart contracts handle credit deductions, activating or suspending services based on credit balances and user requests.

7. **Analytics**:
   - Performance and credit usage data are stored in the backend, periodically refreshed, and served to the frontend for detailed insights.

By maintaining all core logic on the backend, DecentraSpace becomes a versatile, fully managed API-based service provider, capable of supporting diverse frontends with minimal adjustments. This will also enable easy adaptation if new frontend platforms or use cases arise. Shall we proceed with setting up the initial backend structure?