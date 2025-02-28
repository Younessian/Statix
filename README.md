# Statix - HTTP Status Monitoring Tool

Statix is a Bash script that utilizes [httpx](https://github.com/projectdiscovery/httpx) to monitor the status of subdomains and detect changes between runs.

## Features
- Runs HTTPX to check the status codes and titles of subdomains.
- Stores previous results for comparison.
- Detects added, removed, or changed subdomains based on HTTPX output.
- Provides a simple and easy-to-use interface with customizable input files and output directories.

## Prerequisites
Before using Statix, make sure you have:
- **Bash** (Linux/macOS)
- **httpx** installed. You can install it using:
  ```bash
  go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
  ```

## Installation
Clone this repository and navigate to the directory:
```bash
git clone https://github.com/Younessian/Statix.git
cd Statix
chmod +x statix
```
To use Statix globally, move it to your `/usr/local/bin` directory:
```bash
sudo mv statix /usr/local/bin/
```

## Usage
Run the script with the following options:
```bash
statix [options]
```

### Options
| Option | Description |
|--------|-------------|
| `-h`, `--help` | Display the help message |
| `-f FILE`, `--file FILE` | Specify the subdomains file (default: `Subdomains`) |
| `-d DIR`, `--directory DIR` | Specify the directory to save previous results (default: `previous_results/statix`) |

### Example
```bash
statix -f subdomains.txt -d /path/to/results/
```

## How It Works
1. The script reads the subdomains file and checks if it exists.
2. Runs `httpx` on the subdomains to fetch status codes and page titles.
3. Saves the results in `previous_results/statix/httpx_current.tmp`.
4. Compares the current results with previous ones:
   - Identifies newly added subdomains.
   - Detects removed subdomains.
   - Finds status changes in existing subdomains.
5. Outputs the detected changes and updates the stored results.

## Example Output
```
Running HTTPX for Status Monitoring...
Comparing HTTPX results with previous runs...
Status changes detected!
Newly added entries:
example.com [200 OK]
Removed entries:
old.example.com [404 Not Found]
Changed entries:
sub.example.com [200 OK] > [301 Moved Permanently]
```

## Troubleshooting
- If `httpx` is not installed, install it using Go.
- Ensure your subdomains file is not empty.
- Check that the results directory has proper write permissions.

## Contribution
Feel free to submit issues or pull requests to improve Statix!

