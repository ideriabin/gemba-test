> "Feel free to use any tools, any presentation materials, any flow to present. No restrictions. What should be covered — systems design, principles and design decisions, important concerns, assumptions, architecture significant requirements and use cases.If you need clarifications, feel free to ask either replying to this email or starting a session with it tomorrow. Thanks and good luck!
>
> P.S You won't be evaluated based on the completeness but ability to design, explain the decision and communicate them.- Ilya"

# System Design Challenge: National Real Estate Platform

**Duration:** 60 minutes (30 min presentation + 30 min Q&A)
**Preparation Time:** 24 hours
**Level:** Senior to Staff Engineer

## Business Context

You are the lead architect for HomeFinder, a comprehensive real estate platform competing with Zillow, Redfin, and Realtor.com. The platform helps users buy, sell, and rent properties while providing market insights, connecting with agents, and offering integrated financial services like mortgage pre-approval and home valuation.

## Functional Requirements

### Core Platform Features

- **Property Search:** Advanced search with filters for price, location, property type, amenities, and school districts
- **Property Details:** High-resolution photos, virtual tours, floor plans, neighborhood data, and market analytics
- **Valuation Engine:** Automated home value estimates (AVM) with confidence intervals and market trends
- **Agent Marketplace:** Connect buyers/sellers with real estate agents, reviews, and transaction history
- **Mortgage Integration:** Pre-approval process, rate comparisons, and loan application workflow

### Data Integration Requirements

- **MLS Integration:** Real-time sync with 800+ Multiple Listing Services across the US
- **Public Records:** Property history, tax records, deed transfers, and permit data from county databases
- **Financial Services:** Integration with mortgage lenders, credit bureaus, and title companies
- **Third-Party Data:** School ratings, crime statistics, walkability scores, and demographic data

### Advanced Features

- **Price Prediction:** Machine learning models for property value forecasting and market trend analysis
- **Saved Searches & Alerts:** Personalized property recommendations and instant notifications for new listings
- **Virtual Tours:** 3D property tours, drone footage, and augmented reality features
- **Market Analytics:** Neighborhood insights, price trends, inventory levels, and days-on-market statistics

## Non-Functional Requirements

### Scale

- **Users:** 100 million monthly active users across all 50 US states
- **Properties:** 200 million property records (active listings + off-market properties)
- **Real Estate Agents:** 2 million agent profiles with transaction history
- **Data Updates:** 1 million property updates daily from MLS feeds

### Performance

- **Search Response:** Property search results in <200ms (95th percentile)
- **Map Rendering:** Interactive property maps load in <300ms with 1000+ pins
- **Image Loading:** High-resolution property photos load in <1 second
- **Valuation Calculation:** Home value estimates generated in <5 seconds

### Reliability & Compliance

- **Availability:** 99.95% uptime (critical during weekends when most browsing occurs)
- **Data Accuracy:** Property information must be 99.9% accurate and up-to-date
- **Privacy Compliance:** CCPA, state privacy laws, and real estate disclosure requirements
- **Financial Compliance:** TILA-RESPA, fair lending practices, and anti-discrimination laws

## Technical Constraints

### Data Complexity

- **MLS Variations:** 800+ different MLS systems with unique data formats and update frequencies
- **Data Quality:** Inconsistent property descriptions, missing information, and duplicate listings
- **Historical Data:** 30+ years of property transaction history requiring efficient storage and retrieval
- **Geographic Coverage:** Nationwide coverage with varying data availability by region

### Real Estate Industry Challenges

- **Agent Relationships:** Complex business relationships with brokerages and franchise networks
- **Legal Requirements:** State-specific real estate laws and disclosure requirements
- **Market Sensitivity:** Property values are highly sensitive to economic and local factors
- **Seasonal Patterns:** Traffic spikes during spring/summer buying seasons

## Key Design Challenges

- Build vs. Buy Analysis
- Data Architecture Challenges
- Event-Driven Architecture

## Deliverables

### 30-Minute Presentation

For each section below (High-Level Architecture, Deep Dive, and Scaling & Performance), please select one option only to present in detail.

#### High-Level Architecture (8 minutes)
Choose one:
- System overview and data flow architecture
- MLS integration strategy and data processing pipeline
- Search and recommendation engine design

#### Deep Dive: Choose 1 Area or Propose Another (15 minutes)
- Property search engine with geospatial indexing
- Multi-level caching strategy for property data and search results
- Event-driven notification system for saved searches

#### Scaling & Performance (7 minutes)
Choose one:
- Handling seasonal traffic spikes (spring home buying season)
- Geographic distribution and data locality optimization
- Cost optimization for large-scale data storage and processing

## Evaluation Criteria

- Technical Design
- System Thinking
- Communication
- Innovation
