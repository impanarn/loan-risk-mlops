\# Security \& Compliance Documentation



\## Docker Image Security Scan (Trivy)

Image scanned: loan-risk-api:latest

Base image: python:3.11-slim (Debian 13.5)



\### Scan Results Summary

\- Total vulnerabilities: 58

\- CRITICAL: 5 | HIGH: 34 | MEDIUM: 16 | LOW: 3 | UNKNOWN: 0



\### Notes

\- Vulnerabilities are in base OS/system packages (debian, util-linux, tar etc.)

\- No vulnerabilities found in application code

\- Mitigation: Base image can be updated to python:3.11-slim with latest patches

\- Application code has no known CVEs



\## Secrets Management

\- All secrets stored in GitHub Secrets (DOCKERHUB\_USERNAME, DOCKERHUB\_TOKEN)

\- `.env` file excluded via `.gitignore`

\- `.env.example` provided as template



\## Data Compliance

\- Dataset: Home Credit Default Risk (public Kaggle dataset)

\- No PII stored in repository

\- Data tracked via DVC, not committed to git

