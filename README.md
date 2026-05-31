# Conflict-of-Interest-Detector
Detect conflicts of interest and hidden bias in online articles using AI-powered analysis. Quickly scan webpages for disclosures, sponsorships, and funding statements with clear, readable summaries.

<img width="530" height="311" alt="Screenshot 2026-05-27 204921" src="https://github.com/user-attachments/assets/e4492b30-a6a7-4006-898a-a34710f0c5f0" />
<img width="1662" height="911" alt="COI-Animation" src="https://github.com/user-attachments/assets/9f539ad4-32f8-4132-ac63-2c84099edbd1" />
<img width="533" height="310" alt="Screenshot 2026-05-27 204813" src="https://github.com/user-attachments/assets/32b8c6e9-896f-4b7e-9017-b529d0c5a26b" />
<img width="704" height="489" alt="Screenshot 2026-05-27 204835" src="https://github.com/user-attachments/assets/e57fa794-4c3a-461e-92df-c862d9ea2eb1" />
## How It Works

The Conflict of Interest Detector is a Chrome extension that uses the Anthropic LLM API to analyze online articles and research papers for potential conflicts of interest (COI) and disclosure statements.

When a user clicks **“Analyze Current Article,”** the extension scrapes the article text directly from the webpage and sends relevant content to the AI model for analysis. The model identifies possible indicators of bias, including funding disclosures, consultancy involvement, sponsorships, and financial affiliations.

Detected COI statements are automatically highlighted on the article page. Users can click highlighted sections to open interactive tooltips containing AI-generated explanations describing why the statement may represent a potential conflict of interest.
## Motivation to Build
Media consumers rarely notice conflict of interest disclosures buried in research papers and news articles and the implications aren't always clear. The COI Detector makes these disclosures impossible to miss by highlighting them directly on the page and explaining in plain language why each one matters to emphasize financial and literary transparency and awareness for all people.

## Tech Stack
- JavaScript
- HTML/CSS
- Chrome Extensions API (Manifest V3)
- Anthropic Claude API (claude-haiku-4-5)
- Cloudflare Workers
- Chrome Messaging API
- DOM manipulation and parsing

## Installation Guide
- Clone or download this repository
- Open Chrome and go to chrome://extensions
- Enable Developer Mode in the top right corner
- Click "Load unpacked"
- Select the project folder
- The extension icon will appear in your Chrome toolbar

## Project Structure

- /background.js      → API communication  
- /popup.js           → Popup logic  
- /popup.html         → Extension UI  
- /content.js         → Webpage scraping  

## Challenges and Improvements
Challenges: 
- Learning and covering all the entire Chrome Messaging Procedures and understanding what each part relays and means and how all of the different files intertwine
- Managing asynchronous JavaScript including Promises and the Chrome messaging to prevent failure
Future Improvements:
- Cross-referencing author names with public financial databases to detect undisclosed conflicts of interest beyond what appears in the article text
- Smoother UI and more pleasing design
