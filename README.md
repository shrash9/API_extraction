
# ** API Extraction**  

## **Overview**  
This project extracts all possible names from an undocumented autocomplete API hosted at `http://35.200.185.69:8000`. Since no official documentation is available, the API behavior was explored through systematic testing. Initially, a single-threaded approach was used to fetch data for one version, but to speed up the process, **multithreading** was implemented to extract names from all three API versions (`v1`, `v2`, `v3`) simultaneously.  

## **Approach**  

1. **API Exploration**  
   - Discovered that the `/autocomplete?query=<string>` endpoint returns name suggestions for a given prefix.  
   - Identified a rate limit (HTTP 429) and implemented retries with delays.  

2. **Single-Version Extraction (Initial Approach)**  
   - Implemented a recursive search to systematically query all alphabetical prefixes (`a–z`).  
   - If the API returned fewer than `MAX_RESULTS`, results were stored. Otherwise, deeper prefixes were explored recursively.  
   - Introduced a delay (`RATE_LIMIT_DELAY`) to handle rate limits.  

3. **Optimizing with Multithreading**  
   - To speed up extraction, **multithreading** was introduced, allowing all three API versions (`v1`, `v2`, `v3`) to be queried in parallel.  
   - Each thread handled a separate API version, ensuring efficient utilization of network requests without blocking execution.  

4. **Data Storage**  
   - Extracted names were stored in separate text files (`names_v1.txt`, `names_v2.txt`, `names_v3.txt`) for each API version.  

## **Challenges & Findings**  
- **Rate Limits:** The API enforces rate limiting, which was handled using retries and delays.  
- **Recursive Depth:** Some prefixes required deeper recursion to retrieve all names.  
- **Performance Gains:** Switching from a single-threaded to a multithreaded approach significantly reduced the overall runtime.  

## **How to Run**  
1. Install dependencies (if not already installed):  
   ```bash
   pip install requests
   ```  
2. Run the script:  
   ```bash
   python script.py
   ```  
3. Extracted names will be saved in `names_v1.txt`, `names_v2.txt`, and `names_v3.txt`.  

## **Future Improvements**  
- Implement asynchronous requests for further performance improvements.  
- Store results in a database for better analysis and retrieval.  
- Enhance error handling for more efficient retries.  
