# MedVault - Decentralized Health Record Management DApp

## Overview

MedVault is a decentralized healthcare application (DApp) built on the Cardano blockchain that enables patients to maintain complete control over their medical records. The system stores encrypted medical files off-chain (on IPFS/Arweave) while maintaining cryptographic hashes and access permissions on-chain through smart contracts. This architecture ensures data immutability, patient-controlled consent management, cross-hospital interoperability, and tamper-proof verification of medical documents.

The application supports three primary user types: patients who own and control their health data, and healthcare providers (hospitals, laboratories, insurers) who can access records only when explicitly granted permission by patients. Authentication uses a simulated Aadhaar/OTP flow for patients and wallet-based authentication for all users.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React with TypeScript for type-safe component development
- Vite as the build tool and development server
- Wouter for lightweight client-side routing
- TanStack Query (React Query) for server state management and caching
- Shadcn/ui component library built on Radix UI primitives
- Tailwind CSS with custom design tokens following Material Design principles

**Design System:**
- Hybrid approach combining Material Design (healthcare trust/clarity) with Web3 DApp patterns (transaction transparency)
- Custom color system with light/dark mode support via CSS variables
- Typography using Inter for UI text and JetBrains Mono for technical data (wallet addresses, hashes)
- Responsive grid layouts with mobile-first approach

**State Management:**
- Authentication context (`auth-context.tsx`) for user session and wallet state
- Local storage for token persistence across sessions
- React Query for server state, automatic refetching, and optimistic updates

**Key UI Patterns:**
- Dashboard views with statistics cards, recent activity, and quick actions
- File upload zones with drag-and-drop support and progress indicators
- Access grant dialogs for permission management
- Record verification interfaces showing hash comparison results
- Activity logs with filterable audit trails

### Backend Architecture

**Technology Stack:**
- Express.js server with TypeScript
- Session-based authentication with JWT tokens
- Cookie-parser for secure token management
- Multer for multipart file upload handling
- Custom storage abstraction layer for database operations

**API Design:**
- RESTful endpoints organized by resource type (patients, providers, records, grants, logs)
- Authentication middleware validating JWT tokens from headers or cookies
- Separate endpoints for patient and provider workflows
- File upload endpoints handling encryption and IPFS simulation

**Authentication Flow:**
1. Patient registration: Aadhaar number hashing → OTP generation → wallet connection → session creation
2. Provider registration: Organization details → wallet connection → session creation
3. Token-based session management with automatic expiration

**Security Measures:**
- Aadhaar numbers stored as SHA-256 hashes, never in plaintext
- AES-256 encryption for medical files (simulated for demo)
- JWT tokens with configurable secret key
- Simulated blockchain transaction hashes for audit trails
- Access permission checks before record retrieval

### Data Storage Architecture

**Database Schema (PostgreSQL via Drizzle ORM):**

**Patients Table:**
- Stores hashed Aadhaar, demographic info, and Cardano wallet address
- Public key for file encryption
- UUID primary keys for cross-table references

**Providers Table:**
- Organization details with type classification (hospital/lab/insurer)
- Verification status for trusted provider management
- Wallet address for blockchain identity

**Medical Records Table:**
- References patient via foreign key
- File metadata (name, type, size)
- SHA-256 hash of original file for verification
- IPFS CID for decentralized storage reference
- Encrypted AES key for file decryption
- Simulated blockchain transaction hash and block number
- Soft delete via `isActive` flag

**Access Grants Table:**
- Links records to grantee wallet addresses
- Expiration timestamps for time-limited access
- Revocation status tracking
- Grantee type and name for UI display

**Audit Logs Table:**
- Comprehensive activity tracking (upload, grant, revoke, view, verify, download)
- Actor identification via wallet address
- Contextual metadata stored as JSONB
- Immutable append-only design

**Sessions Table:**
- Token-based session tracking
- Separate patient/provider identification
- Expiration timestamp for automatic cleanup

**ORM Configuration:**
- Drizzle ORM with Neon serverless PostgreSQL driver
- WebSocket support for connection pooling
- Schema-first approach with TypeScript type generation
- Migration support via drizzle-kit

### External Dependencies

**Blockchain Integration (Cardano):**
- **Planned Smart Contracts:** Plutus/Aiken contracts for record registration, access control, hash verification, and audit logging
- **Current Implementation:** Simulated blockchain with generated transaction hashes and block numbers
- **Wallet Support:** Designed for Nami, Eternl, and Flint wallet integration (currently mocked)

**Decentralized Storage:**
- **IPFS/Arweave:** Intended for encrypted medical file storage
- **Current Implementation:** Simulated with generated CIDs and local storage references
- **Architecture:** Only content hashes stored on-chain, full files off-chain

**Database:**
- **Neon Serverless PostgreSQL:** Managed PostgreSQL with serverless scaling
- **Connection:** WebSocket-based pooling via `@neondatabase/serverless`
- **Environment Variable:** `DATABASE_URL` required for connection

**UI Component Libraries:**
- **Radix UI:** Headless, accessible component primitives (@radix-ui/react-*)
- **Shadcn/ui:** Pre-styled component implementations built on Radix
- **Class Variance Authority:** Type-safe component variant management
- **Lucide React:** Icon system

**Authentication & Cryptography:**
- **jsonwebtoken:** JWT token generation and validation
- **Planned:** Cardano wallet signatures for authentication
- **Planned:** AES-256 encryption with secure key management system (KMS)

**Development Tools:**
- **Vite Plugins:** Runtime error overlay, cartographer, dev banner (Replit-specific)
- **TypeScript:** Strict mode with path aliases for clean imports
- **ESBuild:** Server bundling with selective dependency bundling

**Form Management:**
- **React Hook Form:** Declarative form state management
- **Zod:** Schema validation with TypeScript type inference
- **@hookform/resolvers:** Zod integration with React Hook Form

**Date Utilities:**
- **date-fns:** Lightweight date manipulation and formatting

**File Handling:**
- **react-dropzone:** Drag-and-drop file upload interface
- **Multer:** Server-side multipart form data processing