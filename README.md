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

Let me know if you need help with a specific scenario! 😊
