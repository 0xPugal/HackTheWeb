# SubDomain Enumeration
+ Passive Enumerationn
+ Active Enumeration
+ Permutation Enumeration

## Passive Technique 
+ **[Subfinder](https://github.com/projectdiscovery/subfinder)** 
    ```
    subfinder -d target.com -all -pc provider-config.yaml
    ```
   - Feed your api keys in subfinder config file to get more subs - [refer here](https://muhdaffa.medium.com/maximizing-the-potential-of-the-subfinder-562fc7e7e9e4)
 
+ **[Amass](https://github.com/OWASP/Amass)** 
    ```
    amass enum -d target.com -config config.ini
    ```
   - Use API keys in amass config file for better results - [refer here](https://hakluke.medium.com/haklukes-guide-to-amass-how-to-use-amass-more-effectively-for-bug-bounties-7c37570b83f7)
 
+ **[Assetfinder](https://github.com/tomnomnom/assetfinder)** 
    ```
    assetfinder --subs-only target.com
    ```
 
+ **[Findomain](https://github.com/Findomain/Findomain)** 
    ```
    findomain -t target.com -q 
    ```
 
+ **[Gau](https://github.com/lc/gau)** 
    ```
    gau -subs target.com | unfurl domains | sort -u 
    ```

+ **[Waybackurls](https://github.com/tomnomnom/waybackurls)** 
    ```
    waybackurls target.com | unfurl domains | sort -u
    ```

+ **[CTFR](https://github.com/UnaPibaGeek/ctfr)** 
    ```
    ctfr -d target.com
    ```

-------------------------------------------------------------------------------------------------------------------------------------

## Active Technique
+ **[PureDns](https://github.com/d3mondev/puredns)** 
    ```
    puredns bruteforce wordlists.txt target.com -r resolvers.txt
    ```

+ **[ShuffleDns](https://github.com/projectdiscovery/shuffledns)** 
    ```
    shuffledns -d target.com -w wordlist.txt -r resolvers.txt
    ```

    ### Wordlist for DNS bruteforcing
    + **[Assetnote_Best-DNS-wordlist](https://wordlists-cdn.assetnote.io/data/manual/best-dns-wordlist.txt)**(9M) 

    + **[Jhaddix_all.txt](https://gist.github.com/jhaddix/f64c97d0863a78454e44c2f7119c2a6a)**(1M)

    ### Resolvers
    + **[Fresh Resolver](https://github.com/BonJarber/fresh-resolvers)**

    + **[Trickest_Resolver](https://raw.githubusercontent.com/trickest/resolvers/main/resolvers-trusted.txt)**

------------------------------------------------------------------------------------------------------------------------------------------

## Permutation Scanning
+ **[Gotator](https://github.com/Josue87/gotator)** 
    ```
    gotator -sub subdomains.txt -silent -perm permutations.txt
    ```

+ **[Dmut](https://github.com/bp0lr/dmut)** 
    ```
    cat subdomains.txt | dmut -d permutations.txt -w 100 --dns-errorLimit 10 --use-pb --verbose -s resolvers.txt
    ```
    
    ### Permuntation wordlist
    + **[goaltdns_wordlist](https://github.com/subfinder/goaltdns/blob/master/words.txt)**
    
    + **[dmut_words](https://raw.githubusercontent.com/bp0lr/dmut/main/words.txt)**
    
------------------------------------------------------------------------------------------------------------------------------------------------

## One-Liners
+ **BufferOver.run**
    ```
    curl -s https://dns.bufferover.run/dns?q=.target.com | jq -r .FDNS_A[] | cut -d',' -f2 | sort -u 
    ```
    
+ **Riddler.io**
    ```
    curl -s "https://riddler.io/search/exportcsv?q=pld:target.com" | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u 
    ```
    
+ **Nmap**
    ```
    nmap --script hostmap-crtsh.nse target.com
    ```

+ **CertSpotter**
    ```
    curl -s "https://certspotter.com/api/v1/issuances?domain=target.com&include_subdomains=true&expand=dns_names" | jq .[].dns_names | grep -Po "(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
    ```
    
+ **Archive**
    ```
    curl -s "http://web.archive.org/cdx/search/cdx?url=*.target.com/*&output=text&fl=original&collapse=urlkey" | sed -e 's_https*://__' -e "s/\/.*//" | sort -u
    ```
    
+ **Crt.sh**
    ```
    curl -s "https://crt.sh/?q=%25.target.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u
    ```
    
+ **JLDC**
    ```
    curl -s "https://jldc.me/anubis/subdomains/target.com" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | sort -u
    ```
    
+ **ThreatMiner**
    ```
    curl -s "https://api.threatminer.org/v2/domain.php?q=target.com&rt=5" | jq -r '.results[]' |grep -o "\w.*target.com" | sort -u
    ```
    
+ **Anubis**
    ```
    curl -s "https://jldc.me/anubis/subdomains/target.com" | jq -r '.' | grep -o "\w.*target.com"
    ```
    
+ **Threat Crowd**
    ```
    curl -s "https://www.threatcrowd.org/searchApi/v2/domain/report/?domain=target.com" | jq -r '.subdomains' | grep -o "\w.*target.com"
    ```
    
+ **Hacker Target**
    ```
    curl -s "https://api.hackertarget.com/hostsearch/?q=target.com"
    ```