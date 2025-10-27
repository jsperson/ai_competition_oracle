# 🏆 2025 Wichita Regional AI Prompt Competition - Winning Portfolio

**Winner:** Top Prize - Oracle Track
**Competition:** [2025 Wichita Regional AI Prompt Championship](https://www.aipromptchamp.com)
**Date:** October 2025

This repository contains the complete winning portfolio for the Oracle track of the 2025 Wichita Regional AI Prompt Competition. The challenge required designing a comprehensive solution for the Kansas Department of Labor to help citizens upskill and change careers through a unified platform.

---

## 🎯 Project Overview: LaunchKS

**LaunchKS** is a unified digital platform designed to connect Kansas citizens to personalized upskilling and career change pathways. The solution addresses a critical workforce paradox: Kansas has 70,000+ job openings while hundreds of thousands of adults struggle to navigate fragmented workforce development resources.

### The Challenge

The competition presented an Oracle track challenge focused on:
- **Problem Definition:** Clearly define a workforce development problem and solution
- **Research Integration:** Identify and integrate local community partners and resources
- **Impact Estimation:** Quantify the value and impact for Kansas
- **Deliverables:** Create a pitch deck, business plan, and technical walkthrough

### The Solution

LaunchKS provides:
1. **AI-Powered Pathway Matching** - Personalized career recommendations based on skills, interests, and constraints
2. **One-Stop Program Hub** - Aggregated training programs from WSU Tech, Butler CC, Newman University, and more
3. **Barrier Navigator** - Transportation, childcare, and financial assistance coordination
4. **Partner Integration** - Direct API connections to KansasWorks, training providers, and employers
5. **Progress Tracking** - Milestone-based journey with coaching and support

### Key Impact Projections

**Year 1:**
- 5,000 users complete assessments
- 1,500 enrollments in training programs
- 750 job placements
- $37.5M in increased earnings

**Year 3:**
- 25,000 users
- 10,000 enrollments
- 5,000 job placements
- $250M in increased earnings
- $12.5M/year in increased tax revenue

---

## 📁 Repository Contents

### 1. Prompts Directory (`/prompts/`)

Contains the master prompts and challenge specifications used during the competition:

- **`master_challenge.md`** - The Oracle track master prompt with retrieval and synthesis strategies, citation standards, and execution protocols
- **`additional_info.md`** - Supplementary requirements including research scope, community partners, time constraints, and deliverable specifications
- **`ColorScheme.txt`** - Branding color scheme for visual materials

### 2. Deliverables

#### **`LaunchKS_PitchDeck.pptx`**
A 15-slide pitch deck covering:
- Problem statement (workforce paradox in Kansas)
- Target market (273,000+ adults with some college, no degree)
- Solution features and user journey
- Community partner integration strategy
- Impact projections and revenue model
- Technology stack and competitive advantages
- Implementation roadmap

All statistics cited from verified sources including U.S. Census Bureau, Kansas Department of Labor, BLS, and local workforce organizations.

#### **`LaunchKS_Business_Plan.md`**
Comprehensive 52KB business plan including:
- Executive summary with financial projections
- Detailed problem statement with market research
- Solution architecture and features
- Target market analysis and segmentation
- Community partner integration steps
- Go-to-market strategy
- Financial model (B2G contracts, B2B partnerships, performance-based payments)
- Risk analysis and mitigation strategies
- Team structure and governance

**Key Research Sources:**
- KansasWorks.com (27 workforce centers, 70,000+ job openings)
- Workforce Alliance of South Central Kansas (6-county coverage)
- WSU Tech Wichita Promise (tuition-free programs)
- Kansas Registered Apprenticeship (1,500+ occupations)
- U.S. Census Bureau (demographic and education data)
- Bureau of Labor Statistics (unemployment rates)
- Greater Wichita Partnership (employer and industry data)

#### **`LaunchKS_Technical_Walkthrough.md`**
Detailed 66KB technical implementation guide covering:
- System architecture (microservices, cloud-native design)
- Technology stack justification
  - Frontend: React.js, Next.js, TypeScript, Tailwind CSS
  - Backend: Node.js, Python (FastAPI)
  - Database: PostgreSQL, MongoDB, Redis, Elasticsearch
  - AI/ML: TensorFlow, scikit-learn for pathway matching
  - Infrastructure: AWS GovCloud for compliance
- Core components and data models
- AI/ML pipeline for career pathway recommendations
- Integration architecture with partner APIs
- Security and compliance (SOC 2 Type II, FERPA, WCAG 2.1)
- Deployment strategy and scalability plans
- Development workflow and implementation roadmap

### 3. Supporting Files

#### **`pitch_deck_content.md`**
Raw markdown content for the pitch deck with detailed slide-by-slide outline, talking points, and full citation list.

#### **`create_slides.py`**
Python automation script using `python-pptx` library to generate the PowerPoint presentation programmatically from structured content.

---

## 🔍 Methodology: The Oracle Approach

This project exemplified the Oracle track's core competencies:

### 1. Surgical Information Extraction
- Researched 20+ community partner organizations
- Extracted labor market data from government sources
- Identified 1,500+ apprenticeship occupations
- Mapped 27 KansasWorks workforce centers statewide

### 2. Citation Excellence
Every claim in all deliverables includes precise source attribution:
```
[Claim] [Source: Organization/Document, Date]
```
Examples:
- "70,000+ job openings across the state [Source: KansasWorks.com, 2025]"
- "273,000+ Kansas adults have some college but no degree [Source: U.S. Census Bureau, 2024]"

### 3. Noise Filtering
- Distinguished between state-level and regional programs
- Verified current vs. outdated program information
- Cross-referenced data across multiple authoritative sources
- Prioritized active community partners with DOL relationships

### 4. Synthesis Mastery
- Connected workforce development infrastructure gaps to specific solutions
- Integrated data from education, labor, commerce, and community organizations
- Translated research findings into actionable business and technical plans
- Aligned solution features with documented barriers (transportation, childcare, digital access)

---

## 🚀 Quick Start

### Viewing the Deliverables

1. **Pitch Deck:** Open `LaunchKS_PitchDeck.pptx` in PowerPoint, Google Slides, or LibreOffice
2. **Business Plan:** Read `LaunchKS_Business_Plan.md` in any markdown viewer
3. **Technical Walkthrough:** Read `LaunchKS_Technical_Walkthrough.md` in any markdown viewer

### Regenerating the Pitch Deck

```bash
# Install dependencies
pip install python-pptx

# Run the script
python create_slides.py
```

---

## 📊 Research Sources

This project synthesized information from:

**Government & Labor:**
- Kansas Department of Labor (KansasWorks.com)
- Kansas Department of Commerce
- Bureau of Labor Statistics (BLS)
- U.S. Census Bureau

**Workforce Development:**
- Workforce Alliance of South Central Kansas
- Kansas Labor Information Center
- Kansas Registered Apprenticeship Program

**Education & Training:**
- WSU Tech (Wichita Promise)
- Butler Community College
- Newman University
- Wichita Public Library

**Economic Development:**
- Greater Wichita Partnership
- Wichita Regional Chamber of Commerce

**Community & Research:**
- Kansas University Transportation Research
- National Skills Coalition
- Kansas Reflector

---

## 🏅 Competition Success Factors

### What Made This Submission Stand Out

1. **Comprehensive Research:** Deep dive into Kansas-specific data, not generic solutions
2. **Real Integration Paths:** Specific API integration steps with named community partners
3. **Quantified Impact:** Detailed economic projections with transparent assumptions
4. **Implementation Ready:** Technical walkthrough that could guide actual development
5. **Citation Rigor:** Every factual claim backed by authoritative sources
6. **Problem-Solution Fit:** Direct mapping between researched barriers and proposed features
7. **Local Context:** Understanding of Kansas workforce ecosystem (Wichita Promise, WASCK, etc.)

### Oracle Track Principles Applied

- ✅ **"Cite or die"** - 100+ inline citations across all deliverables
- ✅ **"The noise is the challenge"** - Filtered 20+ organizations to identify most relevant partners
- ✅ **"Precision over poetry"** - Specific statistics and concrete implementation steps
- ✅ **"Trust but verify"** - Cross-referenced labor market data across multiple sources
- ✅ **Accuracy over speed** - Spent time validating partner information and program details

---

## 📝 License & Usage

This portfolio was created for the 2025 Wichita Regional AI Prompt Competition. The concepts, research, and proposals are provided as reference for educational and competitive purposes.

**Competition:** [AI Prompt Championship](https://www.aipromptchamp.com)
**Track:** Oracle (Advanced Retrieval & Synthesis)
**Result:** 🥇 Top Prize Winner

---

## 🙏 Acknowledgments

- **Competition Organizers:** Wichita Regional AI Prompt Championship team
- **Research Sources:** All Kansas workforce development organizations cited in deliverables
- **AI Tools:** Claude AI for research synthesis and content generation
- **Community:** Kansas Department of Labor and local workforce development partners

---

**Generated with AI-assisted research and prompt engineering**
**Competition Date:** October 2025
**Repository Created:** October 2025
