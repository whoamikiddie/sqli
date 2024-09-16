
---

# Blind SQL Injection Detection with juNgl3FuRy

## Overview

This guide outlines the process to detect blind SQL injection vulnerabilities using a combination of tools:

1. **URL Crawling**: Use `waybackurls` or `gau` to crawl and collect URLs from the target domain.
2. **Pattern Matching**: Utilize `gf` for pattern matching to identify potential SQL injection parameters.
3. **Parameter Extraction**: Extract parameters from the collected URLs with `paramspider`.
4. **Blind SQL Injection Testing**: Use the `juNgl3FuRy` tool to find blind SQL injection vulnerabilities.

## Prerequisites

- **waybackurls**: Tool for extracting URLs from the Wayback Machine.
- **gf**: A tool for pattern matching and filtering URLs.
- **paramspider**: A tool for extracting parameters from URLs.
- **juNgl3FuRy**: A tool used to find blind SQL injection vulnerabilities.

Ensure that all tools are installed and properly configured on your system.

## Instructions

### 1. Crawling URLs

Use `waybackurls` or `gau` to collect URLs from the target domain.

#### Using `waybackurls`

```bash
waybackurls domain.com | gf sqli > sqli.txt
```

- `waybackurls domain.com`: Fetches all URLs from the Wayback Machine for the specified domain.
- `gf sqli`: Filters URLs for potential SQL injection vulnerabilities.
- `> sqli.txt`: Outputs the filtered URLs to `sqli.txt`.

#### Using `gau`

Alternatively, you can use `gau`:

```bash
gau domain.com | gf sqli > sqli.txt
```

- `gau domain.com`: Fetches all URLs from public sources for the specified domain.
- `gf sqli`: Filters URLs for potential SQL injection vulnerabilities.
- `> sqli.txt`: Outputs the filtered URLs to `sqli.txt`.

### 2. Extracting Parameters

Run `paramspider` to extract parameters from the collected URLs.

```bash
paramspider -d domain.com
```

- `-d domain.com`: Specifies the domain to extract parameters from.

### 3. Processing Parameters

Process the extracted parameters to prepare for SQL injection testing.

```bash
cat results/domain.com.txt | sed 's/=.*/=/' > output.txt
```

- `cat results/domain.com.txt`: Reads the extracted parameters.
- `sed 's/=.*/=/'`: Normalizes the parameters by removing values.
- `> output.txt`: Outputs the processed parameters to `output.txt`.

### 4. Testing for Blind SQL Injection

Use the `juNgl3FuRy` tool to find blind SQL injection vulnerabilities in the parameters.

```bash
python3 sqliscanner.py -u http://example.com?param= -p payloads/xor.txt 
```

- `-u http://example.com?param=`: Specifies the target URL with a parameter to test.
- `-w output.txt`: Uses the processed parameters file for testing.

## Conclusion

After following these steps, `juNgl3FuRy` will help you identify potential blind SQL injection vulnerabilities in the target application. 

**Happy Day, Happy Hacking...🌱🌱🌱!!!**


