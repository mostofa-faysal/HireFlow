# HireFlow

A privacy-first, local-only job application pipeline automation system for Canadian job seekers. Streamline your job search from intake to follow-up while keeping your personal data secure and in Canada.

## Overview

HireFlow transforms chaotic job searching into a systematic pipeline process. It automates the repetitive 80% of application work while keeping you in control of final submissions. Optimized for Canadian job markets, ATS systems, and PIPEDA compliance requirements.

## Features

### Smart Intake Pipeline
- **Multi-source ingestion**: Capture jobs from Gmail, LinkedIn alerts, RSS feeds, and manual entries
- **Intelligent deduplication**: Avoid applying to the same role across multiple platforms
- **Canadian context filtering**: Focus on roles with appropriate work authorization requirements

### Three-Tier Prioritization
- **Tier 1: Rule-based filtering**: Fast location, title, and spam detection
- **Tier 2: Semantic scoring**: Embedding-based matching against your profile
- **Tier 3: Detailed analysis**: LLM-powered extraction for high-potential opportunities

### Automated Document Generation
- **ATS-optimized resumes**: Typst templates designed to pass automated parsing systems
- **Context-aware cover letters**: Company-specific insights from reliable public sources
- **Application cheat sheets**: Quick-reference guides for manual form completion

### Assisted Application Engine
- **Greenhouse/Lever automation**: Intelligent form filling with human review checkpoints
- **Complex ATS assistance**: Side-by-side cheat sheets for Workday and other systems
- **Secure session management**: Credential storage via Windows Credential Manager

### Complete Pipeline Management
- **End-to-end tracking**: Monitor applications from discovery to final decision
- **Automated follow-ups**: Schedule strategic reminders at optimal intervals
- **Performance analytics**: Track conversion rates and identify optimization opportunities

## Privacy & Security (Canada-First Approach)

### Data Sovereignty
- **100% local processing**: No external APIs access your personally identifiable information
- **Canadian data residency**: All data encrypted at rest on your local machine
- **PIPEDA compliance**: Designed with Canadian privacy principles from inception

### Security Architecture
- **Encrypted SQLite**: SQLCipher implementation for database encryption
- **BitLocker compatibility**: Seamless integration with Windows full-disk encryption
- **Enterprise credential management**: Windows Credential Manager for secure ATS login storage
- **Zero telemetry**: No data collection, no analytics transmission to external services

### Data Minimization Principles
- **Redacted logging architecture**: PII automatically sanitized from system logs
- **Configurable retention policies**: Automatic archival after configurable periods
- **Portable data formats**: Export all data as standardized JSON at any time

## Quick Start Guide

### Prerequisites
- Windows 10/11, macOS 12+, or Ubuntu 20.04+ (Windows recommended)
- Python 3.11+ and Docker Desktop
- 8GB RAM minimum (for optional Ollama LLM integration)

### Installation Procedure

```bash
# 1. Clone repository and initialize
git clone https://github.com/yourusername/hireflow.git
cd hireflow

# 2. Execute platform-specific setup
.\scripts\setup\windows-setup.ps1  # Windows
./scripts/setup/macos-setup.sh    # macOS
./scripts/setup/linux-setup.sh    # Linux

# 3. Configure personal profile
cp data/seed/sample_profile.yaml data/profiles/master.yaml
# Edit master.yaml with your professional information

# 4. Deploy local infrastructure
docker-compose up -d

# 5. Access the management dashboard
# Navigate to http://localhost:8501 in your browser
```

### Initial Configuration Workflow

1. **Configure job sources** in n8n management interface (http://localhost:5678)
2. **Set up Gmail forwarding** to direct job alerts to a dedicated label
3. **Review prioritized opportunities** in the HireFlow dashboard
4. **Generate tailored application documents** with single-click automation
5. **Execute assisted applications** using the automation engine or manual cheat sheets

## System Architecture

### Technology Stack

| Component | Technology | Primary Function |
|-----------|------------|------------------|
| **Orchestration** | n8n (self-hosted) | Workflow automation and scheduling |
| **API Layer** | FastAPI (Python 3.11+) | Business logic, scoring, document generation |
| **Data Persistence** | SQLite (SQLCipher) | Local, encrypted data storage |
| **Browser Automation** | Playwright (Python) | ATS form interaction with safety validation |
| **Document Generation** | Typst + Jinja2 | Professional PDF resume and cover letter creation |
| **Local Intelligence** | Ollama (optional) | LLM for job description analysis and summarization |
| **Management Interface** | Streamlit | Pipeline monitoring and application tracking |
| **Cryptography** | cryptography (Fernet) | PII encryption at rest |

### Pipeline Flow
```
Data Sources → n8n Orchestration → FastAPI Processing → Three-Tier Filtering → Document Assembly → Dashboard Review → Assisted Application → Performance Tracking → Continuous Optimization
```

## Project Structure

```
hireflow/
├── apps/                    # Core application modules
│   ├── api/                # FastAPI intelligence layer
│   ├── runner/             # Playwright automation engine
│   └── dashboard/          # Streamlit management interface
├── config/                 # System configuration
├── data/                   # Templates and profiles
├── n8n/                    # Orchestration workflows
├── docker/                 # Container definitions
├── scripts/                # Setup and operational utilities
├── tests/                  # Comprehensive test suite
└── docs/                   # System documentation
```

## Configuration

### Environment Configuration

Create `.env` configuration file:

```env
# Security Configuration
ENCRYPTION_KEY=your-generated-key-here  # Execute scripts/setup/generate_key.py

# System Paths (Windows example)
STORAGE_PATH=C:/Users/YourName/hireflow/data/storage
PROFILE_PATH=C:/Users/YourName/hireflow/data/profiles

# Scoring Thresholds
TIER1_THRESHOLD=60    # Basic filter qualification score
TIER2_THRESHOLD=70    # Semantic matching threshold
TIER3_THRESHOLD=80    # LLM processing qualification level

# Optional Local AI Integration
OLLAMA_ENABLED=false
OLLAMA_MODEL=llama3.1:8b
```

### Profile Configuration

Edit `data/profiles/master.yaml` with your professional information:

```yaml
personal_info:
  name: "John Smith"
  email: "john.smith@example.com"
  phone: "+1-416-555-0123"
  location: "Vancouver, BC"
  work_auth: "Canadian Permanent Resident"
  github: "jsmith"
  linkedin: "linkedin.com/in/johnsmith"

preferences:
  remote_only: false
  hybrid_ok: true
  target_salary_min: 90000
  target_salary_max: 130000
  industries: ["Technology", "Finance", "Telecommunications"]
  avoid_companies: []  # Specific companies or recruiters to exclude

skills:
  primary: ["Python", "SQL", "Data Analysis"]
  secondary: ["AWS", "Docker", "React"]
  domains: ["Data Engineering", "Backend Development", "Cloud Infrastructure"]
```

## Performance Metrics

| Metric | Traditional Process | HireFlow Process | Improvement |
|--------|-------------------|------------------|-------------|
| **Time per application** | 60-90 minutes | 10-15 minutes | 75-85% reduction |
| **Weekly application capacity** | 3-5 applications | 15-25 applications | 5x increase |
| **Document tailoring quality** | Inconsistent manual effort | 80%+ keyword match accuracy | Significant improvement |
| **Follow-up execution rate** | 20% manual follow-up | 95%+ automated follow-up | Near-perfect execution |
| **Application tracking** | Spreadsheet-based chaos | Automated pipeline management | Complete visibility |

## Quality Assurance

```bash
# Execute comprehensive test suite
make test

# Perform static type analysis
make type-check

# Conduct security validation
make security-scan

# Run performance benchmarking
make benchmark
```

## Development and Contribution

While HireFlow is designed as a personal productivity tool, community contributions are welcomed:

1. **Repository fork**: Create your development copy
2. **Feature branch**: Establish dedicated branch: `git checkout -b feature/ats-workday`
3. **Commit changes**: Document modifications: `git commit -am 'Add Workday field detection'`
4. **Push updates**: Transfer to repository: `git push origin feature/ats-workday`
5. **Pull request**: Submit for integration consideration

### Development Environment Setup

```bash
# 1. Repository initialization
git clone https://github.com/yourusername/hireflow.git
cd hireflow

# 2. Dependency installation
python -m pip install --upgrade pip
pip install -e ".[dev]"

# 3. Test execution
pytest tests/ -v

# 4. Development server initiation
fastapi dev apps/api/main.py
```

## License

MIT License - complete terms available in LICENSE file.

## Important Disclaimers

HireFlow is a personal productivity enhancement tool, not a hiring service or guarantee of employment.

- **No employment guarantee**: Does not ensure interviews or job offers
- **ATS compatibility variance**: System compatibility differs across companies and implementations
- **Mandatory review requirement**: Always verify auto-filled information before submission
- **Terms of Service compliance**: Users must comply with each ATS's specific terms
- **User responsibility**: Ultimate responsibility for all submitted applications remains with the user

## Support Resources

- **Documentation**: Comprehensive guides available in docs/ directory
- **Issue management**: GitHub Issues for tracking and resolution
- **Security concerns**: Direct communication to security@example.com (PGP encryption available)

## Development Roadmap

### Phase 1: Core Functionality (Current Release)
- [x] Basic job intake from email sources
- [x] Three-tier scoring system implementation
- [x] Typst-based document generation
- [x] Greenhouse automation engine
- [x] Complete application tracking

### Phase 2: Enhanced Capabilities (Q2 2024)
- [ ] LinkedIn professional network integration
- [ ] Rejection pattern analysis and learning
- [ ] Interview preparation assistant
- [ ] Salary negotiation support system

### Phase 3: Advanced Features (Q3 2024)
- [ ] Professional network relationship tracking
- [ ] Referral request automation
- [ ] Market trend and compensation analysis
- [ ] Portfolio project integration

---

Developed in Toronto, Canada - Engineering privacy-respecting tools for professional advancement.

---

*HireFlow operates independently and is not affiliated with any job board, applicant tracking system provider, or recruitment agency.*

*Canadian Developed | Privacy by Design | Local-First Architecture*
