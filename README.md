# Conflict-of-Interest-Detector
Detect conflicts of interest and hidden bias in online articles using AI-powered analysis. Quickly scan webpages for disclosures, sponsorships, and funding statements with clear, readable summaries.

<img width="532" height="307" alt="Screenshot 2026-06-16 171720" src="https://github.com/user-attachments/assets/f0307674-fae7-49c4-a283-d12fc43ded6a" />

<img width="535" height="310" alt="Screenshot 2026-06-16 171748" src="https://github.com/user-attachments/assets/25881bc7-4ce9-4cc3-860a-0a07263b973a" />

<img width="532" height="366" alt="Screenshot 2026-06-16 171814" src="https://github.com/user-attachments/assets/83ddf824-9e77-4c09-a1a3-cd78ae18f14e" />

<img width="957" height="457" alt="Screenshot 2026-06-16 171943" src="https://github.com/user-attachments/assets/887593c7-2a1c-4069-ac23-f5a44265002b" />

<img width="1906" height="942" alt="Animation" src="https://github.com/user-attachments/assets/ba73cad3-d47d-488c-acac-6c79dc2c4edb" />


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
