# katana-help
Katana is a versatile and powerful web vulnerability scanner designed for penetration testing and security assessments. To get started with Katana, you can use the help command to outline its various features and options. Here’s a basic outline of how to use the help command and some common options:


```sh
go install github.com/projectdiscovery/katana/cmd/katana@latest
```

---

### **Basic Command**
```bash
katana -h  # Shows all help options
```

---

### **Core Options & Examples**

#### **1. Input Options**
| **Option**      | **Description**                                   | **Example**                                      |
|-----------------|---------------------------------------------------|--------------------------------------------------|
| `-u`            | Target URL(s) to crawl                            | `katana -u https://example.com`                  |
| `-list`         | File containing URLs to crawl                     | `katana -list urls.txt`                          |
| `-sf`           | Filter URLs by extension (e.g., exclude images)   | `katana -u https://example.com -sf png,jpg`      |
| `-d`            | Maximum depth to crawl (default: `2`)             | `katana -u https://example.com -d 3`             |
| `-jc`           | Include JavaScript files in crawling              | `katana -u https://example.com -jc`              |
| `-headless`     | Use headless browser for JS-heavy sites           | `katana -u https://example.com -headless`        |
| `-proxy`        | Use HTTP/S proxy                                  | `katana -u https://example.com -proxy http://127.0.0.1:8080` |

---

#### **2. Output Options**
| **Option**      | **Description**                                   | **Example**                                      |
|-----------------|---------------------------------------------------|--------------------------------------------------|
| `-o`            | Save results to a file                            | `katana -u https://example.com -o output.txt`    |
| `-json`         | Output in JSON format                             | `katana -u https://example.com -json -o results.json` |
| `-silent`       | Suppress non-essential output                     | `katana -u https://example.com -silent`          |
| `-verbose`      | Show verbose output (debugging)                   | `katana -u https://example.com -verbose`         |

---

#### **3. Crawling Configuration**
| **Option**      | **Description**                                   | **Example**                                      |
|-----------------|--------------------------------------------------|--------------------------------------------------|
| `-c`            | Concurrency (parallel threads, default: `10`)    | `katana -u https://example.com -c 20`            |
| `-rl`           | Rate limit (requests per second)                 | `katana -u https://example.com -rl 5`            |
| `-timeout`      | HTTP request timeout (seconds)                   | `katana -u https://example.com -timeout 20`      |
| `-retry`        | Retry failed requests                            | `katana -u https://example.com -retry 2`         |
| `-form`         | Detect and crawl forms                           | `katana -u https://example.com -form`            |
| `-no-scope`     | Disable domain scoping (crawl all domains)       | `katana -u https://example.com -no-scope`        |

---

#### **4. Authentication**
| **Option**      | **Description**                                   | **Example**                                      |
|-----------------|---------------------------------------------------|--------------------------------------------------|
| `-auth`         | HTTP Basic Auth (username:password)              | `katana -u https://example.com -auth admin:pass` |
| `-H`            | Add custom headers                                | `katana -u https://example.com -H "Cookie: test=1"` |

---

### **Advanced Use Cases**

#### **1. Crawl with Headless Browser**
```bash
katana -u https://example.com -headless -d 3 -o crawled_urls.txt
```

#### **2. Extract JavaScript Endpoints**
```bash
katana -u https://example.com -jc -silent -o js_endpoints.txt
```

#### **3. Crawl with Forms Detection**
```bash
katana -u https://example.com -form -d 2
```

#### **4. Crawl Multiple URLs from a File**
```bash
katana -list targets.txt -c 20 -rl 10 -o all_results.txt
```

#### **5. JSON Output with Custom Headers**
```bash
katana -u https://example.com -H "User-Agent: Katana" -json -o results.json
```

---

### **Filtering & Scoping**
- **Include specific domains**:
  ```bash
  katana -u https://example.com -scope example.com,sub.example.com
  ```
- **Exclude paths**:
  ```bash
  katana -u https://example.com -exclude /logout,/admin
  ```

---

### **Troubleshooting Tips**
1. **Path Issues**:
   ```bash
   # If Katana isn't recognized:
   export PATH=$PATH:/usr/local/bin  # or $HOME/go/bin for Go installs
   ```
2. **Version Conflicts**:
   ```bash
   # Uninstall other Katana versions (if any):
   sudo apt remove katana   # For Kali's default package
   pip3 uninstall katana    # For the RedHuntLabs version
   ```

---

### **Pro Tips**
- Combine Katana with tools like **httpx** or **nuclei**:
  ```bash
  katana -u https://example.com -silent | httpx -status-code
  ```
- Use `-json` output for automated parsing:
  ```bash
  katana -u https://example.com -json | jq .url
  ```

---

(Due to technical issues, the search service is temporarily unavailable.)

Here’s a **comprehensive list of practical examples** for **ProjectDiscovery’s Katana**, covering basic to advanced use cases:

---

### **1. Basic Crawling**
#### **Crawl a single URL (depth 2)**  
```bash  
katana -u "https://example.com"  
```  

#### **Crawl with increased depth (depth 3)**  
```bash  
katana -u "https://example.com" -d 3  
```  

#### **Crawl multiple URLs from a file**  
```bash  
katana -list urls.txt -d 2  
```  

---

### **2. Output Handling**  
#### **Save results to a file**  
```bash  
katana -u "https://example.com" -o crawled_urls.txt  
```  

#### **Save results in JSON format**  
```bash  
katana -u "https://example.com" -json -o results.json  
```  

#### **Silent mode (only show results)**  
```bash  
katana -u "https://example.com" -silent  
```  

---

### **3. JavaScript & Headless Crawling**  
#### **Crawl JavaScript-heavy sites (headless browser)**  
```bash  
katana -u "https://example.com" -headless  
```  

#### **Extract JavaScript endpoints only**  
```bash  
katana -u "https://example.com" -jc -silent  
```  

#### **Headless mode with custom user agent**  
```bash  
katana -u "https://example.com" -headless -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)"  
```  

---

### **4. Scoping & Filtering**  
#### **Crawl only within the target domain**  
```bash  
katana -u "https://example.com" -scope example.com  
```  

#### **Exclude specific paths (e.g., admin/logout)**  
```bash  
katana -u "https://example.com" -exclude "/admin,/logout"  
```  

#### **Filter by file extension (exclude images)**  
```bash  
katana -u "https://example.com" -sf "jpg,png,css"  
```  

---

### **5. Authentication & Proxies**  
#### **Basic authentication**  
```bash  
katana -u "https://example.com" -auth "admin:password123"  
```  

#### **Crawl through a proxy (e.g., Burp Suite)**  
```bash  
katana -u "https://example.com" -proxy "http://127.0.0.1:8080"  
```  

#### **Add custom headers (e.g., API tokens)**  
```bash  
katana -u "https://example.com" -H "Authorization: Bearer xyz123"  
```  

---

### **6. Performance Tuning**  
#### **Increase concurrency (parallel threads)**  
```bash  
katana -u "https://example.com" -c 20  
```  

#### **Limit requests to 5 per second**  
```bash  
katana -u "https://example.com" -rl 5  
```  

#### **Set timeout for requests**  
```bash  
katana -u "https://example.com" -timeout 30  
```  

---

### **7. Advanced Use Cases**  
#### **Crawl and detect forms (for pentesting)**  
```bash  
katana -u "https://example.com" -form  
```  

#### **Crawl all subdomains (disable scoping)**  
```bash  
katana -u "https://example.com" -no-scope  
```  

#### **Retry failed requests (3 times)**  
```bash  
katana -u "https://example.com" -retry 3  
```  

---

### **8. Integration with Other Tools**  
#### **Pipe results to `httpx` for live URL checks**  
```bash  
katana -u "https://example.com" -silent | httpx -status-code -title  
```  

#### **Feed results to `nuclei` for vulnerability scanning**  
```bash  
katana -u "https://example.com" -silent | nuclei -t ~/nuclei-templates/  
```  

#### **Extract URLs and filter with `grep`**  
```bash  
katana -u "https://example.com" -silent | grep "api"  
```  

---

### **9. Real-World Recon Workflow**  
#### **Crawl + JavaScript endpoints + JSON output**  
```bash  
katana -u "https://example.com" -jc -headless -json -o example.json  
```  

#### **Crawl multiple domains with custom config**  
```bash  
katana -list domains.txt -d 3 -c 25 -rl 10 -o all_results.txt  
```  

---

### **10. Troubleshooting**  
#### **Debug crawling issues**  
```bash  
katana -u "https://example.com" -verbose  
```  

#### **Check Katana version**  
```bash  
katana -version  
```  

---

### **Bonus: Automation Scripts**  
#### **Bash script to crawl and save results daily**  
```bash  
#!/bin/bash  
katana -u "https://example.com" -o "results-$(date +%F).txt"  
```  

---

### **Key Notes**  
- 🔍 **Ethical Use**: Always get permission before crawling.  
- 🚀 **Combine Tools**: Katana pairs well with `httpx`, `nuclei`, and `gau`.  
- 💡 **Optimize Performance**: Use `-c` (concurrency) and `-rl` (rate limit) to avoid overloading servers.  

Let me know if you need help crafting a specific workflow! 😊
