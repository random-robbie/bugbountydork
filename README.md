# bugbountydork

Bug Bounty Dork — based on [GoogD0rker](https://github.com/ZephrFish/GoogD0rker) by ZephrFish.

A simple Python script that runs a series of Google dorks against a target domain and writes the results to text files so you can review them and (hopefully) spot a vulnerability or exposed asset.

## Requirements

- Python 3
- The [`googlesearch`](https://pypi.org/project/googlesearch/) package:

```bash
pip install googlesearch
```

## Usage

```bash
python3 main.py -d example.com
```

The `-d` argument is required; if omitted, the script prints the usage hint and exits.

## What it does

For each dork below, the script clears the `.google-cookie` file, queries Google (up to 50 results), prints the URLs to the terminal, and appends them to an output file in the current directory:

| Output file | Dork target |
| --- | --- |
| `loginpage.txt` | Login pages and WordPress/plugin/upload/download paths |
| `backdoor.txt` | Shells, backdoors and common sensitive file names (`shadow`, `passwd`, `boot.ini`) |
| `setup_files.txt` | `readme`, `license`, `install`, `setup` and `config` files |
| `wordpress.txt` | WordPress plugins, uploads and downloads |
| `openredirect.txt` | Potential open redirect parameters (`redir`, `url`, `redirect`, `return`, `src=http`, `r=http`) |
| `extentions.txt` | Files by extension (`cgi`, `php`, `asp`, `aspx`, `jsp`, `jspx`, `swf`, `fla`, `xml`) |
| `documents.txt` | Documents by extension (`doc`, `docx`, `csv`, `pdf`, `txt`, `log`, `bak`) |
| `struts.txt` | Apache Struts file extensions (`action`, `struts`, `do`) |
| `pastebin.txt` | Pastebin posts mentioning the domain |
| `linkedin.txt` | Employees on LinkedIn |
| `subdomains.txt` | Subdomains |
| `sub-subdomains.txt` | Sub-subdomains |
| `phpinfo.txt` | Exposed `phpinfo.php` files |
| `sensitive.txt` | `.htaccess`, `phpinfo.php` and exposed `/.git` directories |

## Example

```console
$ python3 main.py -d example.com
Finding Login Pages for example.com
Finding Backdoors for example.com
Finding Install / Setup files for example.com
...
```

Each result file is appended to, so re-running against the same domain accumulates results — delete the files first if you want a clean run.

## Notes

- A `503` error from Google means it has rate-limited your IP — switch IP (a VPS from [DigitalOcean](https://www.digitalocean.com/?refcode=e22bbff5f6f1&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) works well) and try again.
- All dorks are scoped with `site:` except the Pastebin, LinkedIn and phpinfo lookups, so results stay on target.

## Disclaimer / Authorised use

This tool is for authorised security testing and responsible disclosure only. Do not use it against systems you do not have permission to test.

## Author

Robbie Wiggins — [What-Security](https://www.what-security.co.uk) · [GitHub](https://github.com/random-robbie)
