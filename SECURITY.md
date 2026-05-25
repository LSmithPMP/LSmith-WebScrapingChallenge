# Security Policy — LSmith-WebScrapingChallenge

## Overview
Security architecture, threat model, and risk controls for the Web Scraping to Vector Database pipeline.

## Threat Model

| ID | Threat | Likelihood | Impact | Residual Risk |
|----|--------|-----------|--------|---------------|
| T1 | Unauthorized ChromaDB access | Low | High | LOW — localhost-only binding |
| T2 | Malicious URL injection | Medium | Medium | LOW — URL whitelist enforced |
| T3 | PII exposure in scraped content | Low | High | LOW — Wikipedia only, no PII |
| T4 | Rate limit abuse / IP ban | Medium | Low | LOW — 1s delay + User-Agent |
| T5 | Credential exposure via .env | Medium | High | LOW — .env in .gitignore |
| T6 | Dependency supply chain attack | Low | High | MEDIUM — pinned versions |
| T7 | Prompt injection via scraped text | Low | Medium | LOW — embeddings only, no LLM |
| T8 | Container escape (Docker) | Low | High | LOW — Codespaces isolation |

## Security Controls

### Input Validation
- URLs explicitly defined — no dynamic URL construction
- HTTP responses validated before parsing
- Scraped text length bounded by chunk size limits

### Rate Limiting & Ethical Scraping
- Mandatory 1-second delay between all HTTP requests
- Custom User-Agent header identifies the bot transparently
- Wikipedia robots.txt permits educational scraping
- No login-required or paywalled content targeted

### ChromaDB Access Controls
- Container bound to localhost:8000 only
- No external network exposure
- Production recommendation: Enable ChromaDB authentication and TLS

### Secrets Management
- All credentials stored in .env — never hardcoded
- .env excluded from version control via .gitignore
- .env.example provided with placeholder values only

### Data Privacy
- Scraping targets limited to publicly accessible non-personal content
- No PII collection, storage, or processing
- Embeddings do not reconstruct original text (one-way transformation)
- Content used for educational purposes only

## Security Checklist
- [x] URLs hardcoded — no user-controlled injection
- [x] Rate limiting implemented
- [x] .env excluded from git
- [x] ChromaDB localhost-only
- [x] No PII in scraped content
- [x] Dependencies pinned
- [x] Docker container from official image
- [ ] ChromaDB authentication (recommended for production)
- [ ] HTTPS/TLS for ChromaDB (recommended for production)

## Reporting Security Issues
Contact: Lamonte Smith — lsmith@walshcollege.edu

*Security policy version 1.0 | May 2026 | Lamonte Smith*
