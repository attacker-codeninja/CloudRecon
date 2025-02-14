# CloudRecon
CloudRecon tool

# Install
** You must have CGO enabled, and may have to install gcc to run CloudRecon**
```sh
sudo apt install gcc
```

```sh
go install github.com/g0ldencybersec/CloudRecon@latest
```

# Description
**CloudRecon** 


CloudRecon is a suite of tools for red teamers and bug hunters to find ephemeral and development assets in their campaigns and hunts. 

Often, target organizations stand up cloud infrastructure that is not tied to their ASN or related to known infrastructure. Many times these assets are development sites, IT product portals, etc. Sometimes they don't have domains at all but many still need HTTPs.

CloudRecon is a suite of tools to scan IP addresses or CIDRs (ex: cloud providers IPs) and find these hidden gems for testers, by inspecting those SSL certificates.

The tool suite is three parts in GO:

Scrape - A LIVE running tool to inspect the ranges for a keywork in SSL certs CN and SN fields in real time.

Store - a tool to retrieve IPs certs and download all their Orgs, CNs, and SANs. So you can have your OWN cert.sh database.

Retr - a tool to parse and search through the downloaded certs for keywords.

# Usage
**MAIN**
```sh
Usage: CloudRecon scrape|store|retr [options]

  -h    Show the program usage message

Subcommands: 

        cloudrecon scrape - Scrape given IPs and output CNs & SANs to stdout
        cloudrecon store - Scrape and collect Orgs,CNs,SANs in local db file
        cloudrecon retr - Query local DB file for results
```
**SCRAPE**
```sh
scrape [options] -i <IPs/CIDRs or File>
  -c int
        How many goroutines running concurrently (default 100)
  -h    print usage!
  -i string
        Either IPs & CIDRs separated by commas, or a file with IPs/CIDRs on each line (default "NONE")
  -p string
        TLS ports to check for certificates (default "443")
  -t int
        Timeout for TLS handshake (default 4)
```

**STORE**
```sh
store [options] -i <IPs/CIDRs or File>
  -c int
        How many goroutines running concurrently (default 100)
  -db string
        String of the DB you want to connect to and save certs! (default "certificates.db")
  -h    print usage!
  -i string
        Either IPs & CIDRs separated by commas, or a file with IPs/CIDRs on each line (default "NONE")
  -p string
        TLS ports to check for certificates (default "443")
  -t int
        Timeout for TLS handshake (default 4)
```

**RETR**
```sh
retr [options]
  -all
        Return all the rows in the DB
  -cn string
        String to search for in common name column, returns like-results (default "NONE")
  -db string
        String of the DB you want to connect to and save certs! (default "certificates.db")
  -h    print usage!
  -ip string
        String to search for in IP column, returns like-results (default "NONE")
  -num
        Return the Number of rows (results) in the DB (By IP)
  -org string
        String to search for in Organization column, returns like-results (default "NONE")
  -san string
        String to search for in common name column, returns like-results (default "NONE")
```
