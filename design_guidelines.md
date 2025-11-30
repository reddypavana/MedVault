# Design Guidelines: Decentralized Health Record Management DApp

## Design Approach

**Hybrid Approach**: Material Design principles for healthcare trust + Web3 DApp patterns from Uniswap/Aave for blockchain interactions.

### Rationale
Healthcare applications demand clarity, professionalism, and trust. Combined with Web3's need for transparent transaction states and wallet connectivity, this requires a clean, information-dense interface with strong visual hierarchy and reassuring design patterns.

## Typography System

**Font Families**:
- Primary: Inter (via Google Fonts) - clean, professional, excellent for dense information
- Monospace: JetBrains Mono - for wallet addresses, file hashes, technical data

**Hierarchy**:
- H1: 2.5rem/font-bold - Page titles ("Patient Dashboard", "Medical Records")
- H2: 2rem/font-semibold - Section headers ("Your Records", "Access Permissions")
- H3: 1.5rem/font-semibold - Card titles, modal headers
- Body Large: 1.125rem/font-normal - Primary content, descriptions
- Body: 1rem/font-normal - Standard text, form labels
- Small: 0.875rem/font-medium - Metadata, timestamps, secondary info
- Tiny: 0.75rem/font-normal - Helper text, captions
- Monospace: 0.875rem - Wallet addresses (truncated with ellipsis), IPFS CIDs, file hashes

## Layout System

**Spacing Primitives**: Tailwind units of 2, 4, 6, 8, 12, 16 (keep rhythm tight for professional feel)
- Component padding: p-6 or p-8
- Section spacing: gap-6 or gap-8
- Card margins: mb-6
- Form field spacing: space-y-4

**Container Strategy**:
- max-w-7xl for main dashboard layouts
- max-w-2xl for focused forms (upload, authentication)
- max-w-4xl for modal dialogs
- Full-width tables with horizontal scroll on mobile

**Grid Patterns**:
- Record cards: grid-cols-1 md:grid-cols-2 lg:grid-cols-3
- Metrics/stats: grid-cols-2 lg:grid-cols-4
- Two-column forms: grid-cols-1 md:grid-cols-2

## Component Library

### Navigation
**Top Navigation Bar**:
- Fixed header with wallet connection status (right-aligned)
- Logo/brand left-aligned
- Role indicator badge (Patient/Hospital)
- Wallet address display with copy button (truncated: 0x1234...5678)
- Connection status indicator (green dot for connected)

**Role-Based Sidebar**:
- Patient: Dashboard, Upload Record, My Records, Access Management, Activity Log
- Hospital: Dashboard, Verify Records, Access Requests, Audit Trail
- Active state: subtle background with left border accent
- Icons from Heroicons (outline style)

### Cards & Containers

**Medical Record Card**:
- Elevated shadow (shadow-md)
- Rounded corners (rounded-lg)
- Header: File name + type badge
- Body: IPFS CID (monospace, truncated), upload date, file size
- Footer: Action buttons (View, Share, Revoke) + verification badge
- Hover: subtle lift (shadow-lg transition)

**Access Permission Card**:
- Hospital/provider name as header
- Granted wallet address (monospace, copy button)
- Expiry timestamp with countdown indicator
- Revoke button (destructive action style)
- Status badge (Active/Expired/Revoked)

**Wallet Connection Card**:
- Large card for wallet selection (Nami, Eternl logos)
- Connection status with pulse animation when connecting
- Disconnect option when connected
- Balance display (ADA amount)

### Forms & Inputs

**Upload Flow**:
- Large drag-and-drop zone with dashed border
- File preview with thumbnail (PDF icon, image preview)
- Progress bar during encryption and IPFS upload
- Metadata form: filename, type dropdown, description textarea
- Clear two-step process: "1. Upload & Encrypt" → "2. Register On-Chain"

**Access Grant Form**:
- Record selector (dropdown with file names)
- Wallet address input with validation (monospace)
- Expiry duration selector (radio buttons: 1 day, 1 week, 1 month, custom)
- Preview panel showing what will be granted
- Primary CTA: "Grant Access" with transaction fee estimate

**Authentication (Aadhaar Simulation)**:
- Clean centered form (max-w-md)
- Aadhaar number input (12 digits, formatted with spaces)
- OTP input (6-digit code, large input boxes)
- Trust indicators: lock icon, "Secure Verification" text
- Loading state during verification

### Data Display

**Access History Table**:
- Responsive table with sticky header
- Columns: Timestamp, Actor (wallet), Action, Record ID, Status
- Sortable columns with arrow indicators
- Row hover highlighting
- Pagination controls (bottom right)
- Export button (top right)

**Transaction Status Display**:
- Toast notifications (top-right corner)
- Inline progress indicators for multi-step operations
- Transaction hash with Cardano explorer link
- Block confirmation counter (simulated)

**Verification Result**:
- Large status indicator (checkmark or X icon)
- "Verified" or "Tampered" message (bold, large)
- Hash comparison display (expected vs actual, monospace)
- Metadata comparison table

### Buttons & Actions

**Primary Actions**: 
- Full button with substantial padding (px-6 py-3)
- Examples: "Upload Record", "Grant Access", "Connect Wallet"

**Secondary Actions**: 
- Outline style
- Examples: "Cancel", "View Details"

**Destructive Actions**: 
- Clear visual distinction for revoke/delete
- Examples: "Revoke Access", "Delete Record"

**Icon Buttons**: 
- Copy wallet address, View details, Download file
- Tooltip on hover with action description

### Modals & Overlays

**Transaction Confirmation Modal**:
- Clear action summary
- Gas/fee estimate (simulated)
- "Confirm" and "Cancel" buttons (prominent)
- Cannot dismiss while processing

**Record Details Modal**:
- Full record metadata display
- IPFS CID with external link
- Access history for this record
- Download encrypted file button
- Verification section

### Status Indicators

**Badges**:
- Record type: Lab Report, Prescription, Scan, etc. (small, rounded-full)
- Verification status: Verified (green), Unverified (yellow), Tampered (red)
- Access status: Active, Expired, Revoked
- Role badge: Patient, Hospital, Lab, Insurer

**Loading States**:
- Skeleton loaders for card grids while fetching
- Spinner for inline actions
- Progress bars for file uploads/encryption
- Pulsing animation for blockchain transaction pending

### Feedback & Notifications

**Toast Messages**:
- Success: "Record uploaded successfully"
- Error: "Failed to grant access" with reason
- Warning: "This access will expire in 24 hours"
- Info: "Transaction pending on blockchain"

**Empty States**:
- "No records uploaded yet" with Upload CTA
- "No access granted" with informative illustration
- "No activity logged" with timestamp

## Page Layouts

**Patient Dashboard**:
- Hero section: Wallet status + quick stats (Total Records, Active Grants, Recent Activity)
- Grid of recent medical records (3 columns on desktop)
- Access management section below
- Activity timeline on right sidebar (on large screens)

**Upload Page**:
- Centered layout (max-w-2xl)
- Clear three-step process indicator at top
- Large upload zone
- Form below
- Preview panel on right (on desktop)

**Hospital Verification Page**:
- Two-column layout: Upload zone (left) + Results (right)
- Large dropzone for file upload
- Hash computation displayed in monospace
- Comparison table with on-chain data
- Clear pass/fail visual feedback

**Access Management Page**:
- Filter controls (top): By status, by provider, date range
- Grid of access permission cards
- Bulk revoke option
- Quick grant access button (top-right)

## Images

**No Hero Images**: This is a utility-focused healthcare application. Replace traditional hero sections with functional dashboards and clear CTAs.

**Illustrations/Icons**:
- Medical-themed icons for record types (syringe for lab, pill for prescription, scan lines for imaging)
- Empty state illustrations: friendly doctor illustration for "no records", lock for "secure"
- Wallet provider logos: Nami, Eternl (actual logos from CDN/assets)
- Trust badges: encryption icon, blockchain verified icon, healthcare compliance icons

**Placeholder Elements**:
- Document thumbnails: PDF icon, image preview for scans
- Avatar placeholders for patient/hospital (initials in circle)

## Animation Principles

**Minimal and Purposeful**:
- Transaction pending: subtle pulse on status indicator
- Toast notifications: slide-in from top-right, auto-dismiss
- Card hover: slight elevation (transform: translateY(-2px))
- Modal: fade-in backdrop, scale-in content
- NO scroll-triggered animations
- NO decorative animations in data-dense areas

## Healthcare-Specific Patterns

**Trust Signals**:
- Encryption badge always visible on sensitive data
- "Verified on Cardano" badge with blockchain icon
- Audit trail always accessible
- Clear data ownership messaging ("You control this record")

**Error Prevention**:
- Confirmation dialogs for destructive actions (Revoke, Delete)
- Input validation with helpful error messages
- Disabled states with explanatory tooltips
- Multi-step processes with clear progress indicators

**Privacy First**:
- Wallet addresses truncated by default (click to reveal full)
- File previews only show metadata, not content
- Access logs clearly show who accessed what and when
- PII never displayed in URLs or shareable links