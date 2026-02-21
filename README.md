# Email Discovery & Validation Automation (Excel → Email Guessing → SMTP/IMAP Bounce Validation)

## Overview
This project is an end-to-end automation workflow that helps generate likely corporate email addresses for contacts and validate which ones are deliverable at scale. It combines two scripts into a single pipeline: (1) an email pattern generator that creates multiple email guesses using common naming conventions, and (2) an email validation engine that sends test emails, monitors bounce-back responses via Gmail (Inbox/Spam), and classifies emails as valid or invalid. The workflow is designed to reduce manual effort in contact discovery and outreach preparation by producing an enriched and validated email list in a structured Excel format.

## Problem Statement
In many outreach and prospecting workflows, the biggest challenge is that direct email addresses are unavailable. Often only the person’s name and company website/domain are known. Manually generating possible email formats and then confirming if they work is slow, repetitive, and inconsistent—especially when dealing with large lists. A scalable and repeatable workflow was needed to:
- Generate realistic corporate email candidates using standard naming patterns
- Validate deliverability using bounce detection without manually checking each email
- Output results in a structured format suitable for outreach and tracking

## Solution
The project implements a two-stage automation pipeline.

### Stage 1: Email Guessing (Excel-Based Lead Enrichment)
1. Reads input from an Excel sheet containing:
   - Full name
   - Domain (optional)
   - Website (optional, used to derive domain when missing)
2. Normalises the input:
   - Splits names into first and last name where possible (supports multi-part names)
   - Derives and cleans domains from website URLs (removes `www` if present)
3. Generates multiple email candidates using common corporate patterns:
   - `firstname@domain`
   - `lastname@domain`
   - `firstname.lastname@domain`
   - `firstinitiallastname@domain`
   - `firstnamelastinitial@domain`
   - `firstnamelastname@domain`
4. Writes all guesses into a structured Excel output sheet with dedicated columns for each pattern.

### Stage 2: Email Validation (SMTP Send + IMAP Bounce Detection)
1. Reads a list of email IDs to validate from an Excel file using Pandas.
2. Sends test emails to each candidate email using Gmail SMTP:
   - Uses environment variables for credentials (no hardcoding of passwords in code)
   - Adds delays between sends to reduce throttling risk
3. Waits for a defined period and then checks Gmail for bounce-back responses using IMAP:
   - Reads Inbox and Spam to capture delivery failure notifications
   - Extracts and searches bounce messages for patterns like:
     - `Final-Recipient: RFC822; <email>`
     - `Action: failed`
4. Classifies each email as valid/invalid based on bounce presence.
5. Optionally cleans up Gmail folders (Inbox/Spam/Sent) by deleting test messages to keep the mailbox tidy.

## Tech Stack
- Python
- openpyxl (Excel read/write automation)
- pandas (Excel reading and list handling)
- SMTP (smtplib) for sending emails
- IMAP (imaplib) for reading Inbox/Spam/Sent folders
- email / EmailMessage for message parsing and composition
- Environment variables for credentials management

## Outcome
This project converts a manual contact discovery task into a scalable automation pipeline. It produces a structured Excel output containing multiple email guesses per person and validates which emails are likely deliverable based on bounce detection. The result is an outreach-ready and prioritised list that reduces time spent on trial-and-error email searches and improves efficiency in recruitment, business development, or networking workflows.

## Notes / Considerations
- This validation approach is based on bounce-back detection and does not guarantee that a “valid” email belongs to the intended person—only that the address is deliverable.
- Sending test emails should be used responsibly and in compliance with organisational policies and applicable regulations.
- Gmail rate limits may apply; delays and batching are recommended for larger runs.

## Potential Enhancements
- Write validation results back into Excel alongside each guess (Valid/Invalid/Unknown)
- Add pattern ranking and confidence scoring (e.g., prioritise firstname.lastname)
- Add retry logic, rate limiting, and robust error handling for SMTP/IMAP calls
- Support multiple email providers (Outlook/Office365 IMAP/SMTP)
- Integrate an optional third-party email verification API for stronger validation
- Store results in SQL for historical tracking and deduplication
