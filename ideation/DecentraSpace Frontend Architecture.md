digraph DecentraSpaceFrontend {

    rankdir=LR;
    node [shape=rectangle, style=filled, color=lightblue];

    // Main Components
    subgraph cluster_MainApp {
        label="Main App Container";
        Dashboard;
        HostingManagement;
        DomainManagement;
        StorageManagement;
        BillingCredit;
        Analytics;
        AuthModule;
        UIRouter [label="UI Router", shape=ellipse, color=orange];
    }

    // Authentication and Authorization
    subgraph cluster_Auth {
        label="Authentication Module";
        WalletConnect [label="Wallet Connect"];
        SessionHandling [label="Session Handling"];
        AccountManagement [label="Account Management"];
        AuthAPI [label="Auth API Service", color=yellow];
        AuthModule -> {WalletConnect SessionHandling AccountManagement} -> AuthAPI;
    }

    // API Service Layer
    APIService [label="API Service Layer", shape=diamond, color=lightgreen];
    AuthAPI -> APIService;

    // Main Modules and Components
    Dashboard -> {HostingManagement DomainManagement StorageManagement BillingCredit Analytics} [dir=none];
    UIRouter -> {Dashboard HostingManagement DomainManagement StorageManagement BillingCredit Analytics};
    
    // Hosting Management Module
    subgraph cluster_Hosting {
        label="Hosting Management Module";
        DeploymentManager;
        ServiceControl [label="Service Control"];
        ResourceMonitoring [label="Resource Monitoring"];
        HostingAPI [label="Hosting API Service", color=yellow];
        HostingManagement -> {DeploymentManager ServiceControl ResourceMonitoring} -> HostingAPI;
        HostingAPI -> APIService;
    }

    // Domain Management Module
    subgraph cluster_Domain {
        label="Domain Management Module";
        DomainPurchase [label="Domain Purchase & Renewal"];
        DNSSettings [label="DNS Settings"];
        OwnershipTransfers [label="Ownership Transfers"];
        DomainAPI [label="Domain API Service", color=yellow];
        DomainManagement -> {DomainPurchase DNSSettings OwnershipTransfers} -> DomainAPI;
        DomainAPI -> APIService;
    }

    // Storage Management Module
    subgraph cluster_Storage {
        label="Storage Management Module";
        FileUpload [label="File Upload Interface"];
        FileOrganization [label="File Organization"];
        AccessControl [label="Access Control"];
        StorageAPI [label="Storage API Service", color=yellow];
        StorageManagement -> {FileUpload FileOrganization AccessControl} -> StorageAPI;
        StorageAPI -> APIService;
    }

    // Billing and Credit Module
    subgraph cluster_Billing {
        label="Billing & Credit Module";
        CreditBalance [label="Credit Balance Display"];
        CreditPurchase [label="Credit Purchase"];
        BillingHistory [label="Billing History"];
        BillingAPI [label="Billing API Service", color=yellow];
        BillingCredit -> {CreditBalance CreditPurchase BillingHistory} -> BillingAPI;
        BillingAPI -> APIService;
    }

    // Analytics Module
    subgraph cluster_Analytics {
        label="Analytics Module";
        PerformanceInsights;
        UsageTracking [label="Usage Tracking"];
        ActionableInsights [label="Actionable Insights"];
        AnalyticsAPI [label="Analytics API Service", color=yellow];
        Analytics -> {PerformanceInsights UsageTracking ActionableInsights} -> AnalyticsAPI;
        AnalyticsAPI -> APIService;
    }

    // Global Components
    AuthModule -> AuthAPI;
    AuthAPI -> APIService;
    APIService -> Backend;

    // Backend Interaction
    Backend [label="Backend System", shape=ellipse, color=orange];
    APIService -> Backend;

    // Styling & State Management
    StateManagement [label="Global State (Redux/Context API)", shape=diamond, color=pink];
    Styling [label="UI Styling (Tailwind CSS/Material UI)", shape=diamond, color=pink];
    {Dashboard HostingManagement DomainManagement StorageManagement BillingCredit Analytics AuthModule} -> StateManagement;
    {Dashboard HostingManagement DomainManagement StorageManagement BillingCredit Analytics AuthModule} -> Styling;
}
