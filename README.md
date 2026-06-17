# Conflict-of-Interest-Detector
Detect conflicts of interest and hidden bias in online articles using AI-powered analysis. Quickly scan webpages for disclosures, sponsorships, and funding statements with clear, readable summaries.

<img width="530" height="311" alt="Screenshot 2026-05-27 204921" src="https://github.com/user-attachments/assets/e4492b30-a6a7-4006-898a-a34710f0c5f0" />
<img width="1662" height="911" alt="COI-Animation" src="https://github.com/user-attachments/assets/9f539ad4-32f8-4132-ac63-2c84099edbd1" />
<img width="533" height="310" alt="Screenshot 2026-05-27 204813" src="https://github.com/user-attachments/assets/32b8c6e9-896f-4b7e-9017-b529d0c5a26b" />
<img width="704" height="489" alt="Screenshot 2026-05-27 204835" src="https://github.com/user-attachments/assets/e57fa794-4c3a-461e-92df-c862d9ea2eb1" />
## How It Works

The Conflict of Interest Detector is a Chrome extension that uses the Anthropic LLM API to analyze online articles and research papers for potential conflicts of interest (COI) and disclosure statements.

When a user clicks **“Analyze Current Article,”** the extension scrapes the article text directly from the webpage and sends relevant content to the AI model for analysis. The model identifies possible indicators of bias, including funding disclosures, consultancy involvement, sponsorships, and financial affiliations.

The biggest part of this entire project is something that I would call **"The Highlight Engine."** The highlights were effectively the most difficult and time consuming part of the entire coding process and it was well worth it. Firstly, the text from the article and the text that the Claude API sends back both have to be normalized to assure that they both are the same so when highlighting there is no errors. Then another problem arises, since many articles can have several different text nodes for one sentence which makes it very difficult to highlight. The solution is using a DOM range paired with TreeWalker API which effectively splits part of the COI statement from all of the various text nodes. Then because the article text and API text were both normalized the normalized map is what allows the code to translate a match position back to the live DOM to find start and end points which a statement is in. Finally, using DOM ranges the COI statements are essentially 'bookmarked' so that even when the page changes the statements are still intact and highlighted.

## Motivation to Build
Communities rarely notice conflict of interest disclosures buried in research papers and news articles and the implications aren't always clear. The Conflict of Interest Detector makes these disclosures impossible to miss by highlighting them directly on the page and explaining in plain language why each one matters to emphasize financial and literary transparency and awareness for all people.

## Tech Stack
- JavaScript
- HTML/CSS
- Chrome Extensions API (Manifest V3)
- Anthropic Claude API (claude-haiku-4-5)
- Cloudflare Workers
- Chrome Messaging API
- DOM manipulation and parsing
- TreeWalker API for complex sites
- DOM Range API for cross-element highlighting

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
- Learning TreeWalker API paired with DOM Range API to get through cross element highlighting which was the most difficult and time consuming part of the entire project
- Debugging unnecessarily long lags (upward of 10 seconds) and ended up reducing highlight rendering from ~11 seconds to under 1 millisecond by restructuring the engine to build the page map once and reuse live DOM Ranges.
- Debugging the problem of the amount of statements detected versus the amount that were getting highlighted not matching up by using Cross Element Highlighting
Future Improvements:
- Cross-referencing author names with public financial databases to detect undisclosed conflicts of interest beyond what appears in the article text
