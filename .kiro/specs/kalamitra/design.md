# KalaMitra System Design

## Overview

KalaMitra is a comprehensive digital platform that connects Indian artisans with global buyers, leveraging advanced AI technologies and immersive experiences to preserve and promote cultural heritage while enabling economic empowerment. The system architecture is designed for scalability, cultural authenticity, and seamless user experience across multiple touchpoints.

## System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend Layer                           │
├─────────────────────────────────────────────────────────────────┤
│  Web App (React/Next.js)  │  Mobile App (React Native)        │
│  3D Bazaar (Three.js)     │  AR Components (AR.js/WebXR)      │
└─────────────────────────────────────────────────────────────────┘
                                    │
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway Layer                         │
├─────────────────────────────────────────────────────────────────┤
│              Load Balancer & Rate Limiting                     │
│              Authentication & Authorization                     │
│              Request Routing & Validation                      │
└─────────────────────────────────────────────────────────────────┘
                                    │
┌─────────────────────────────────────────────────────────────────┐
│                    Microservices Layer                         │
├─────────────────────────────────────────────────────────────────┤
│ User Service │ Product Service │ Auction Service │ Chat Service │
│ Payment Svc  │ AI Services     │ Media Service   │ Analytics    │
│ Notification │ Search Service  │ 3D/AR Service   │ Admin Portal │
└─────────────────────────────────────────────────────────────────┘
                                    │
┌─────────────────────────────────────────────────────────────────┐
│                      Data Layer                                │
├─────────────────────────────────────────────────────────────────┤
│ PostgreSQL │ Redis Cache │ S3 Storage │ OpenSearch │ Vector DB │
│ (Primary)  │ (Sessions)  │ (Media)    │ (Search)   │ (AI/ML)   │
└─────────────────────────────────────────────────────────────────┘
```

### Technology Stack

#### Frontend Technologies
- **Web Application**: React 18+ with Next.js 14 for SSR/SSG
- **Mobile Application**: React Native with Expo for cross-platform development
- **3D Visualization**: Three.js for 3D bazaar and product rendering
- **AR Integration**: WebXR API with AR.js for product visualization
- **State Management**: Redux Toolkit with RTK Query for API integration
- **Styling**: Tailwind CSS with custom cultural design tokens
- **Animation**: Framer Motion for smooth cultural-themed transitions

#### Backend Technologies
- **Runtime**: Node.js with TypeScript for type safety
- **Framework**: Express.js with Helmet for security
- **Authentication**: Supabase Auth with JWT tokens
- **Database**: PostgreSQL with Prisma ORM
- **Caching**: Redis for session management and performance
- **Message Queue**: Bull Queue with Redis for background jobs
- **File Storage**: AWS S3 with CloudFront CDN
- **Real-time**: Socket.io for live auctions and chat

#### AWS AI/ML Services
- **AWS Bedrock**: Claude/Titan models for content generation
- **Amazon Rekognition**: Image analysis and auto-tagging
- **Amazon Transcribe**: Voice-to-text conversion
- **Amazon Polly**: Text-to-speech for story narration
- **Amazon Translate**: Multi-language support
- **Amazon OpenSearch**: Semantic search and recommendations
- **AWS Lambda**: Serverless AI microservices
- **AWS App Runner**: Container hosting for AI services

## Core System Components

### 1. Authentication & Authorization System

#### Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Auth Service  │    │   Supabase      │
│                 │    │                 │    │   Auth          │
│ Login/Register  ├────┤ JWT Validation  ├────┤                 │
│ OAuth Flows     │    │ Role Management │    │ User Storage    │
│ Route Guards    │    │ Session Mgmt    │    │ OAuth Providers │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

#### Implementation Details
- **Multi-Provider Authentication**: Email/password, Google OAuth 2.0, Microsoft OAuth 2.0
- **Role-Based Access Control (RBAC)**: Artisan and Buyer roles with granular permissions
- **JWT Token Management**: Access tokens (15min) and refresh tokens (7 days)
- **Session Security**: Redis-based session storage with automatic cleanup
- **Middleware Protection**: Route-level authentication and authorization checks

### 2. Virtual Stall Management System

#### Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   3D Renderer   │    │  Stall Service  │    │   Media Store   │
│                 │    │                 │    │                 │
│ Three.js Scene  ├────┤ Stall Config    ├────┤ 3D Assets       │
│ Cultural Themes │    │ Public URLs     │    │ Textures        │
│ Customization   │    │ Analytics       │    │ Cultural Media  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

#### Implementation Details
- **3D Environment**: Three.js-based customizable stalls with cultural architecture
- **Asset Management**: Optimized 3D models, textures, and cultural design elements
- **Real-time Updates**: WebSocket connections for live stall modifications
- **Public Sharing**: SEO-optimized public URLs with social media integration
- **Performance Optimization**: Level-of-detail (LOD) rendering and asset streaming

### 3. Product Management System

#### Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Product UI    │    │ Product Service │    │   AI Services   │
│                 │    │                 │    │                 │
│ CRUD Interface  ├────┤ Catalog Mgmt    ├────┤ Image Enhancement│
│ Media Upload    │    │ Inventory Track │    │ Auto-tagging    │
│ Digital Products│    │ Pricing Engine  │    │ Story Generation│
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

#### Implementation Details
- **Dual Product Types**: Physical products with inventory and digital products with licensing
- **AI-Enhanced Uploads**: Automatic image enhancement and cultural categorization
- **Inventory Management**: Real-time stock tracking with low-stock alerts
- **Digital Rights Management**: Licensing terms and download tracking for digital products
- **Bulk Operations**: CSV import/export for large product catalogs

### 4. Search & Discovery System

#### Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Search UI     │    │  Search Service │    │   OpenSearch    │
│                 │    │                 │    │                 │
│ Voice Input     ├────┤ Query Processing├────┤ Vector Search   │
│ Filters         │    │ Result Ranking  │    │ Cultural Index  │
│ Recommendations │    │ Personalization │    │ Analytics       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

#### Implementation Details
- **Semantic Search**: Vector embeddings for meaning-based product discovery
- **Voice Integration**: Amazon Transcribe for multilingual voice queries
- **Advanced Filtering**: Category, price, region, cultural significance, artisan filters
- **Personalized Results**: ML-based ranking considering user preferences and behavior
- **Cultural Context**: Heritage-aware search with cultural significance scoring

### 5. AI & ML Services

#### Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   AI Gateway    │    │  ML Pipeline    │    │  AWS Bedrock    │
│                 │    │                 │    │                 │
│ Request Router  ├────┤ Model Ensemble  ├────┤ Claude/Titan    │
│ Rate Limiting   │    │ Feature Store   │    │ Custom Models   │
│ Result Caching  │    │ A/B Testing     │    │ Knowledge Base  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

#### AI Service Components
- **Story Generation**: Cultural heritage narratives using Claude models
- **Image Enhancement**: Automatic quality improvement and cultural context detection
- **Recommendation Engine**: Collaborative and content-based filtering
- **Price Optimization**: Dynamic pricing suggestions based on market analysis
- **Chatbot (RAG)**: Retrieval-Augmented Generation for shopping assistance
- **Translation Services**: Real-time multilingual support for Indian languages

## Data Architecture

### Database Schema Design

#### Core Entities
```sql
-- Users table with role-based access
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR UNIQUE NOT NULL,
    role user_role NOT NULL, -- 'artisan' | 'buyer'
    profile_data JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Artisan stalls with 3D configuration
CREATE TABLE stalls (
    id UUID PRIMARY KEY,
    artisan_id UUID REFERENCES users(id),
    name VARCHAR NOT NULL,
    description TEXT,
    config_3d JSONB, -- 3D stall configuration
    public_url VARCHAR UNIQUE,
    is_active BOOLEAN DEFAULT true
);

-- Products with dual type support
CREATE TABLE products (
    id UUID PRIMARY KEY,
    artisan_id UUID REFERENCES users(id),
    stall_id UUID REFERENCES stalls(id),
    type product_type NOT NULL, -- 'physical' | 'digital'
    name VARCHAR NOT NULL,
    description TEXT,
    price DECIMAL(10,2),
    inventory_count INTEGER,
    digital_file_url VARCHAR,
    cultural_tags TEXT[],
    ai_generated_story TEXT
);

-- Auctions with real-time bidding
CREATE TABLE auctions (
    id UUID PRIMARY KEY,
    product_id UUID REFERENCES products(id),
    start_time TIMESTAMP,
    end_time TIMESTAMP,
    starting_bid DECIMAL(10,2),
    current_bid DECIMAL(10,2),
    winner_id UUID REFERENCES users(id),
    status auction_status -- 'pending' | 'active' | 'ended'
);
```

## Security Architecture

### Security Layers

#### 1. Network Security
- **API Gateway**: Rate limiting and DDoS protection
- **WAF (Web Application Firewall)**: SQL injection and XSS prevention
- **SSL/TLS**: End-to-end encryption for all communications
- **VPC**: Isolated network environment for backend services

#### 2. Application Security
- **Input Validation**: Comprehensive sanitization and validation
- **OWASP Compliance**: Following OWASP Top 10 security practices
- **Dependency Scanning**: Regular vulnerability assessments
- **Code Analysis**: Static and dynamic security testing

#### 3. Data Security
- **Encryption at Rest**: AES-256 encryption for sensitive data
- **Encryption in Transit**: TLS 1.3 for all data transmission
- **PII Protection**: Tokenization of personally identifiable information
- **Audit Logging**: Comprehensive security event logging

## Performance & Scalability

### Performance Targets
- **Response Time**: < 200ms for API calls, < 2s for page loads
- **Throughput**: 10,000 requests/second peak capacity
- **Availability**: 99.9% uptime with graceful degradation
- **Scalability**: Support for 100,000 concurrent users

### Caching Strategy
- **Redis Cache**: Session storage, product catalog, search results
- **CDN**: Global content delivery with CloudFront
- **Application Cache**: In-memory caching for frequently accessed data
- **Database Optimization**: Read replicas and connection pooling

## Deployment Architecture

### Container Strategy
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Development   │    │    Staging      │    │   Production    │
│                 │    │                 │    │                 │
│ Docker Compose  ├────┤ AWS ECS         ├────┤ AWS ECS/EKS     │
│ Local Testing   │    │ Integration     │    │ Auto-scaling    │
│ Hot Reload      │    │ E2E Testing     │    │ Load Balancing  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### CI/CD Pipeline
- **Source Control**: Git with feature branch workflow
- **Build Process**: Docker multi-stage builds for optimization
- **Testing**: Unit, integration, and E2E automated testing
- **Deployment**: Blue-green deployment with rollback capabilities
- **Monitoring**: Comprehensive logging and performance monitoring

## Correctness Properties

### Property 1: Authentication Integrity
**Validates: Requirements 1.1, 1.2, 1.3**
For all authentication attempts, the system must maintain user identity integrity and session security.

### Property 2: Product Catalog Consistency
**Validates: Requirements 3.1, 3.2, 3.3**
All product operations (create, update, delete) must maintain data consistency across all system components.

### Property 3: Auction Fairness
**Validates: Requirements 6.1, 6.2, 6.3**
All auction operations must ensure fair bidding, accurate timing, and proper winner determination.

### Property 4: Search Result Accuracy
**Validates: Requirements 4.1, 4.2, 19.1**
Search queries must return relevant results based on semantic meaning and cultural context.

### Property 5: Payment Transaction Safety
**Validates: Requirements 12.1, 12.2**
All financial transactions must be secure, atomic, and properly recorded with audit trails.

### Property 6: Real-time Communication Reliability
**Validates: Requirements 10.1, 10.2**
All real-time features (chat, auctions, notifications) must deliver messages reliably and in order.

### Property 7: Cultural Content Authenticity
**Validates: Requirements 11.1, 23.1**
All cultural content and design elements must maintain authenticity and respectful representation.

### Property 8: Performance Under Load
**Validates: Requirements 18.1, 18.3**
The system must maintain performance standards under varying load conditions.

## Testing Framework

### Property-Based Testing Setup
- **Framework**: fast-check for JavaScript/TypeScript property-based testing
- **Test Categories**: Unit properties, integration properties, end-to-end properties
- **Coverage**: All correctness properties with comprehensive test generators
- **Automation**: Continuous property testing in CI/CD pipeline

### Test Implementation Strategy
- **Generators**: Smart test data generators for cultural products, user interactions
- **Shrinking**: Automatic minimal counterexample generation for failed properties
- **Regression**: Property-based regression testing for all major features
- **Performance**: Load testing with property validation under stress conditions

## Monitoring & Observability

### Metrics Collection
- **Application Metrics**: Response times, error rates, throughput
- **Business Metrics**: User engagement, transaction volumes, cultural content usage
- **Infrastructure Metrics**: CPU, memory, network, storage utilization
- **Security Metrics**: Authentication failures, suspicious activities, data access patterns

### Alerting Strategy
- **Critical Alerts**: System outages, security breaches, payment failures
- **Warning Alerts**: Performance degradation, high error rates, capacity thresholds
- **Info Alerts**: Deployment notifications, scheduled maintenance, feature usage
- **Cultural Alerts**: Content moderation flags, cultural sensitivity issues

This design provides a comprehensive foundation for building KalaMitra as a scalable, secure, and culturally authentic platform that serves both artisans and buyers while preserving and promoting Indian cultural heritage through technology.