# Luo & Company Official Website — Structure & Architecture

This document provides a comprehensive overview of the Luo & Company marine spare parts website structure, built with **Next.js 14 + TypeScript + Tailwind CSS** (frontend showcase only).  
The production backend (PHP + MySQL) is kept in the private repository.

---

## System Architecture Diagram (Mermaid)

```mermaid
graph TB
    %% User Access Layer
    User[User Access] --> CDN[Cloudflare CDN]
    CDN --> Pages[Cloudflare Pages]
    
    %% Frontend Application Layer
    Pages --> App[Next.js 14 App Router]
    
    %% Page Routing Structure
    App --> Layout[Root Layout<br/>layout.tsx]
    Layout --> Navigation[Navigation Bar<br/>Navigation.tsx]
    Layout --> Footer[Footer<br/>Footer.tsx]
    
    %% Main Pages
    App --> Home[Homepage<br/>page.tsx]
    App --> About[About Us<br/>about/page.tsx]
    App --> Products[Products Center<br/>products/page.tsx]
    App --> Contact[Contact Us<br/>contact/page.tsx]
    App --> Admin[Admin Panel<br/>admin/page.tsx]
    
    %% Product System
    Products --> ProductData[Product Data<br/>lib/products/]
    ProductData --> Categories[Product Categories<br/>categories.ts]
    ProductData --> ProductTypes[Product Types<br/>types.ts]
    ProductData --> ProductFiles[Product Data Files<br/>Category-specific Data]
    
    %% API Routes
    App --> API[API Routes<br/>app/api/]
    API --> ContactAPI[Contact Form<br/>contact/route.ts]
    API --> QuoteAPI[Quote Request<br/>quote/route.ts]
    API --> AdminAPI[Admin Interface<br/>admin/products/route.ts]
    API --> FileAPI[File Operations<br/>admin/file-operations/route.ts]
    
    %% Component System
    App --> Components[Component Library<br/>components/]
    Components --> QuoteModal[Quote Modal<br/>QuoteModal.tsx]
    Components --> ScrollButton[Scroll to Top<br/>ScrollToTopButton.tsx]
    Components --> AdminComponents[Admin Components<br/>admin/]
    
    %% Admin Components
    AdminComponents --> ProductList[Product List<br/>ProductList.tsx]
    AdminComponents --> ProductForm[Product Form<br/>ProductForm.tsx]
    AdminComponents --> CategoryFilter[Category Filter<br/>CategoryFilter.tsx]
    AdminComponents --> CommandModal[Command Modal<br/>CommandModal.tsx]
    
    %% Styling System
    App --> Styles[Styling System]
    Styles --> Tailwind[Tailwind CSS]
    Styles --> Globals[Global Styles<br/>globals.css]
    Styles --> DesignSystem[Design System<br/>Marine Industry Theme]
    
    %% Static Assets
    App --> Static[Static Assets<br/>public/]
    Static --> Images[Image Assets<br/>images/]
    Static --> Logos[Logo Files<br/>logo/]
    Static --> Certificates[Certificate Images<br/>certificate/]
    
    %% Image Categories
    Images --> CategoryImages[Category Images<br/>categories/]
    Images --> ProductImages[Product Images<br/>products/]
    Images --> CompanyImages[Company Images<br/>img/]
    
    %% Product Image Subcategories
    ProductImages --> PowerSystem[Power System<br/>power-system/]
    ProductImages --> DeckMachinery[Deck Machinery<br/>deck-machinery/]
    ProductImages --> MarineValves[Marine Valves<br/>marine-valves/]
    ProductImages --> AnchoringMachinery[Anchoring Machinery<br/>anchoring-machinery/]
    ProductImages --> OtherCategories[Other Categories...]
    
    %% Data Flow
    ProductData --> ProductSearch[Product Search]
    ProductData --> ProductFilter[Product Filter]
    ProductData --> ProductDisplay[Product Display]
    
    %% Feature Modules
    ContactAPI --> EmailService[Email Service<br/>Resend]
    QuoteAPI --> QuoteSystem[Quote System]
    AdminAPI --> ProductManagement[Product Management]
    
    %% Deployment and Build
    App --> Build[Build System]
    Build --> NextBuild[Next.js Build]
    Build --> CloudflareBuild[Cloudflare Pages Build]
    
    %% Development Tools
    App --> Scripts[Development Scripts<br/>scripts/]
    Scripts --> AdminCLI[Admin CLI<br/>admin-cli.js]
    Scripts --> ProductMigration[Product Migration<br/>migrate-products.js]
    Scripts --> ImageProcessing[Image Processing<br/>process-images.js]
    
    %% Documentation System
    App --> Documentation[Documentation System<br/>doc/]
    Documentation --> ProjectDoc[Project Documentation<br/>PROJECT_DOCUMENTATION.md]
    Documentation --> APIDoc[API Documentation<br/>API_DOCUMENTATION.md]
    Documentation --> DeploymentDoc[Deployment Guide<br/>DEPLOYMENT_GUIDE.md]
    Documentation --> ContactDoc[Contact Form Setup<br/>CONTACT_FORM_SETUP.md]
    
    %% Style Definitions
    classDef pageClass fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef apiClass fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef componentClass fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef dataClass fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef staticClass fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    %% Apply Styles
    class Home,About,Products,Contact,Admin pageClass
    class ContactAPI,QuoteAPI,AdminAPI,FileAPI apiClass
    class Navigation,Footer,QuoteModal,ScrollButton,AdminComponents componentClass
    class ProductData,Categories,ProductTypes,ProductFiles dataClass
    class Static,Images,Logos,Certificates staticClass