#  API  Extraction

## **Overview**  
This project extracts all possible names from an undocumented autocomplete API hosted at `http://35.200.185.69:8000`. Since no official documentation was provided, I explored its functionality through systematic testing. Initially, I used a single-threaded approach to fetch data for one version, but to improve efficiency, I implemented **multithreading** to extract names from all three API versions (`v1`, `v2`, `v3`) simultaneously in **Jupyter Notebook**.  

## **Approach**  

1. **API Exploration**  
   - Tested the `/autocomplete?query=<string>` endpoint to understand its response structure.  
   - Identified a rate limit (HTTP 429) and implemented retries with delays.  

2. **Single-Version Extraction (Initial Approach)**  
   - Queried the API with all alphabetical prefixes (`a–z`).  
   - Used recursion to explore deeper prefixes if the API returned a full list of results (`MAX_RESULTS`).  
   - Introduced a delay (`RATE_LIMIT_DELAY`) to handle rate limits.  

3. **Optimizing with Multithreading in Jupyter**  
   - Used Python’s **ThreadPoolExecutor** to query all three API versions (`v1`, `v2`, `v3`) in parallel.  
   - This significantly reduced execution time compared to the single-threaded approach.  

4. **Data Storage**  
   - Extracted names were saved in separate text files (`names_v1.txt`, `names_v2.txt`, `names_v3.txt`) for each API version.  

## **Challenges & Findings**  
- **Rate Limits:** The API enforces rate limiting, which was handled using retries and delays.  
- **Recursive Depth:** Some prefixes required deeper recursion to retrieve all names.  
- **Performance Gains:** Switching to **multithreading** improved execution speed in Jupyter.  

## **How to Run in Jupyter Notebook**  
1. Ensure `requests` is installed:  
   ```python
   !pip install requests
   ```  
2. Run the notebook cells sequentially.  
3. Extracted names will be saved as `names_v1.txt`, `names_v2.txt`, and `names_v3.txt`.  

## **Future Improvements**  
- Implement **async requests** for further performance optimization.  
- Store results in a structured format (CSV or database).  
- Improve handling of API failures and timeouts.  
