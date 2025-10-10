# StructuredDataLibrary

## Repository Metadata
- **Type**: JavaScript Library
- **Language(s)**: JavaScript (ES6+)
- **Framework(s)**: Vanilla JavaScript
- **Database**: None (client-side only)
- **Version**: Multiple modules (v1.2.0 - v1.7.0)

## Purpose & Context

### What This Repository Does
StructuredDataLibrary is a specialized JavaScript library developed by Happy Geeks for generating structured data (Schema.org) and enhanced e-commerce tracking events (Google Analytics 4) based on DOM query selectors. The library enables automatic extraction of product information, user interactions, and e-commerce events from HTML pages without requiring manual data layer management.

### Business Value
The library serves a dual purpose: first, it generates JSON-LD structured data for search engine optimization (SEO), enabling rich snippets in search results. Second, it provides comprehensive e-commerce event tracking for Google Analytics 4, capturing user interactions throughout the shopping journey. Built for production e-commerce environments, the library handles complex scenarios like multi-step product configurators.

### Wiser Ecosystem Role
Integrated with Wiser CMS platform and product configurators used by customers like GAMMA. The library's selector-based approach allows non-developers to configure tracking and structured data through the Wiser CMS interface.

## Architecture & Design

### Modular Architecture
Four independent modules:
1. **DataClasses** (v1.4.1) - Foundation classes for data extraction
2. **StructuredDataService** (v1.2.0) - Schema.org structured data generation
3. **EnhancedEcommerceService** (v1.6.0) - GA4 e-commerce events
4. **EnhancedEcommerceConfiguratorService** (v1.7.0) - Configurator extensions

### Core Design Patterns
- **Selector-Based Data Extraction**: Declarative approach using CSS selectors
- **Schema Composition**: Build complex structures through DataSelector and DataSchema
- **Event-Driven Architecture**: Event delegation for user interaction monitoring

### Key Classes
- **DataSelector**: Extracts individual data points from DOM elements
- **DataSchema**: Composes multiple DataSelectors into structured objects
- **StructuredDataSchema**: Extends DataSchema for Schema.org JSON-LD
- **EventDataSchema**: Specialized for GA4 event payloads
- **EnhancedEcommerceService**: Core event tracking service
- **EnhancedEcommerceConfiguratorService**: Configurator-specific tracking

## Getting Started

### Installation

```html
<!-- Always load DataClasses first -->
<script src="https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-DataClasses-1.4.1.min.js"></script>

<!-- For Schema.org structured data -->
<script src="https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-StructuredDataService-1.2.0.min.js"></script>

<!-- For GA4 e-commerce tracking -->
<script src="https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-EnhancedEcommerceService-1.6.0.min.js"></script>
```

### Basic Usage

```javascript
// Product structured data
const productSchema = new StructuredDataSchema(
    "Product",
    "product",
    ".product-container",
    true,
    [
        new DataSelector("name", ".product-title", "text", true),
        new DataSelector("price", ".product-price", "number", true)
    ]
);

const structuredData = window.structuredDataService.generateStructuredData(productSchema);
window.structuredDataService.addStructuredDataToHead(structuredData);
```

## Core Functionality

### Structured Data Generation
- Schema.org support for Product, FAQPage, BreadcrumbList, Organization, WebPage
- Automatic JSON-LD injection into page head
- Validation of mandatory fields

### Enhanced E-commerce Tracking
- GA4 event types: view_item_list, select_item, add_to_cart, purchase, etc.
- Automatic event listener management
- Data layer integration

### Configurator-Specific Features
- Multi-step navigation tracking
- Choice tracking with pricing
- Price calculation events
- Error event tracking
- Step completion monitoring

## Common Development Tasks

### Creating a New Version
1. Update version comment in source file
2. Make code changes
3. Minify the updated file
4. Create versioned file in `/versions` directory
5. Update README.md with new CDN URL
6. Commit and push to main branch
7. Wait for CDN propagation

### Testing Locally
```javascript
// Enable debug mode
window.StructuredDataLibrarySettings = { DebugMode: true };

// Inspect generated output
const data = window.structuredDataService.generateStructuredData(schema);
console.log(JSON.stringify(data, null, 2));
```

## Troubleshooting

### Structured Data Not Generating
- Verify container selector matches elements
- Check mandatory fields are present
- Enable debug mode for warnings

### Events Not in Google Analytics
- Verify dataLayer exists
- Check GTM configuration
- Test with manual push
- Disable AdBlockers temporarily

### Configurator Not Tracking Steps
- Ensure init() called after DOM updates
- Verify currentStep is updating
- Check schemas return valid data

## Original Documentation

# StructuredDataLibrary
JavaScript library for the generation of structured data and enhanced ecommerce events based on query selectors.

## DataClasses
https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-DataClasses-1.4.1.min.js

## StructuredDataService
https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-StructuredDataService-1.2.0.min.js

## EnhancedEcommerceService
https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-EnhancedEcommerceService-1.6.0.min.js

## EnhancedEcommerceConfiguratorService
https://cdn.jsdelivr.net/gh/happy-geeks/StructuredDataLibrary@main/versions/StructuredDataLibrary-EnhancedEcommerceConfiguratorService-1.7.0.min.js
