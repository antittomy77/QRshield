QRShield
OPCODE IMPACT 2026 | Hackathon Submission
Team ID: [Enter Team ID]
QRShield is a privacy-conscious prototype that analyses QR-code contents and URLs for suspicious characteristics before the user visits the destination. It provides explainable findings rather than treating a single warning sign as proof of a scam.
Project status: Initial prototype. External threat-intelligence verification and reliability testing are planned future improvements. A "No obvious risk detected" result does not guarantee that a URL is safe.
1. Problem Statement
QR codes can hide their destination until scanned, making it difficult for people to judge where a link will lead. Scammers may use QR codes to direct people to deceptive login pages, impersonation sites, or other harmful destinations. Users need a simple way to inspect a QR code or URL before opening it and understand why a destination may be suspicious.
2. Solution Title
QRShield --- Explainable QR Scam Detection
3. Solution Description
QRShield lets users upload a QR-code image or enter a URL manually. It decodes QR content locally and analyses HTTP/HTTPS URLs using transparent, explainable security rules without automatically visiting the destination. The application reports a risk category, describes the indicators it found, and offers a recommended next step. A simulated .test URL provides a safe example for demonstrations. Independent threat-intelligence checks and a reliability-testing module are planned for later development.
4. Architecture Diagram
The following diagram describes the intended initial workflow.
flowchart TD
    A[User] --> B{Choose input}
    B --> C[Upload QR image]
    B --> D[Enter URL]
    C --> E[Decode QR locally with OpenCV]
    E --> F{Is content an HTTP/HTTPS URL?}
    F -- Yes --> G[Validate and parse URL]
    F -- No --> H[Display decoded non-URL content safely]
    D --> G
    G --> I[Run explainable local security rules]
    I --> J[Generate findings and risk assessment]
    J --> K[Display report and recommended action]
    K --> L[User decides what to do next]
Workflow explanation: The user uploads a QR image or enters a URL. QRShield decodes the image locally, validates URL input, and checks URL characteristics using local rules. It then displays findings and a risk assessment. The application does not need to open the submitted destination to perform these checks.
If you later create a diagram image, save it as docs/architecture.png and replace the Mermaid diagram with ![Architecture Diagram](docs/architecture.png).
5. Technology Stack
Frontend: Streamlit
Backend: Python
Database: Not required for the initial prototype
QR decoding: OpenCV
QR-code generation: qrcode and Pillow
URL and domain analysis: Python URL parsing and a public-suffix-aware library such as tldextract
Security analysis: Explainable, rule-based URL checks
External threat intelligence: Not enabled in the initial version; planned future improvement
6. Quick Start Guide
Prerequisites
Windows, macOS, or Linux
Python 3.10 or later, using a version supported by the installed dependencies
Internet access to install packages
Git (optional, for cloning the repository)
Installation & Execution --- Windows PowerShell
Open PowerShell in the QRShield project folder.
# Create a virtual environment
py -m venv .venv

# Activate it
.\.venv\Scripts\Activate.ps1

# Install dependencies
python -m pip install --upgrade pip
pip install -r requirements.txt

# Run the application
streamlit run app.py
Streamlit will show a local address, usually http://localhost:8501. Open that address in your browser.
If PowerShell blocks virtual-environment activation, use the environment's Python directly:
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m streamlit run app.py
Other operating systems
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
Basic usage
Start QRShield.
Upload a QR-code image or enter a URL.
Run the analysis.
Review the risk category, findings, and recommended action.
For the simulated demonstration, use the sample QR containing http://account-login.test/verify?source=demo. This is a reserved test-domain example; do not visit it.
Safety note: QRShield is an advisory prototype. Local URL patterns can produce false positives and false negatives. A URL that receives no warnings may still be unsafe. The initial version does not perform an independent reputation lookup unless that feature is implemented and explicitly enabled.
7. Output Screenshots
Add screenshots of the running application to the docs/ folder.
�
Suggested screenshots: - Main page showing QR upload and URL input - Analysis report showing the risk category and explanations - Safe simulated QR demonstration
If docs/output.png does not exist yet, capture a screenshot after running the application and save it at that path. Do not present mock results as real analysis output.
8. Future Scope
Add optional threat-intelligence lookups, with clear status and privacy disclosure.
Build a reliability tester using labelled benign and threat URLs.
Measure precision, recall, false-positive rate, and false-negative rate on a documented evaluation set.
Improve domain-impersonation detection and URL normalisation.
Add automated tests for QR decoding, malformed URLs, and edge cases.
Improve accessibility and mobile-friendly layout.
9. Team Contributions
Antit Tomy 
Aswajith C A 
Adithyan Vinoy 
Abhinav Ramesh 
10. Tools Used
Tool / Platform                  Purpose / Why Used
Python                           Core application logic and URL analysis
Streamlit                        Interactive web interface
OpenCV                           Decode QR-code images locally
qrcode / Pillow                Generate QR-code images for safe demonstrations
tldextract or equivalent       Identify domain boundaries using public-suffix data
Git and GitHub                   Version control and collaboration
Antigravity (AI coding           Assist with drafting and refining assistant)                       code; generated code should be reviewed and tested by the team
Limitations and Responsible Use
QRShield does not guarantee that a URL is safe or malicious.
A local heuristic is an indicator, not proof of a threat.
The initial prototype does not automatically visit or fetch submitted URLs.
External reputation results, if added, may be incomplete or unavailable.
Avoid committing private or sensitive URLs to a public repository.
License
Add a license before publishing if your team intends to permit reuse. Until a license is added, do not assume others have permission to reuse the code.