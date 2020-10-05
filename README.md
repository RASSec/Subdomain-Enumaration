# Subdomain-Enumaration

These are Subdomain Enumaration Tools that I use, **Thanks to all the Authors for making things easy** and make sure to comment down which tools you use for Subdomain Enumaration and your methodologies


- **Using Findomain**

    [Findomain/Findomain](https://github.com/Findomain/Findomain)

    $ findomain -t target.com -o

---

- **Using jhaddix All.txt**

    $ ffuf -w JHADDIX-ALL/all.txt -u "https://FUZZ.target.com/" -v | grep "| URL |" | awk '{print $4}'

---

- **Search Subdomain using Gospider**

    [KingOfBugbounty/KingOfBugBountyTips](https://github.com/KingOfBugbounty/KingOfBugBountyTips)

    $ gospider -d 0 -s "https://target.com" -c 5 -t 100 -d 5 --blacklist jpg,jpeg,gif,css,tif,tiff,png,ttf,woff,woff2,ico,pdf,svg,txt | grep -Eo '(http|https)://[^/"]+' | anew

---

- **Using Subfinder**

    [projectdiscovery/subfinder](https://github.com/projectdiscovery/subfinder)

    $ subfinder -d target.com -o target.com_subfinder.txt

---

- **Search subdomains using jldc**

    [KingOfBugbounty/KingOfBugBountyTips](https://github.com/KingOfBugbounty/KingOfBugBountyTips)

    $ curl -s "https://jldc.me/anubis/subdomains/target.com" | grep -Po "((http|https):\/\/)?(([\w.-]*)\.([\w]*)\.([A-z]))\w+" | anew

---

- **Subdomain search Bufferover resolving domain to httpx**

    [KingOfBugbounty/KingOfBugBountyTips](https://github.com/KingOfBugbounty/KingOfBugBountyTips)

    $ curl -s https://dns.bufferover.run/dns?q=.target.com |jq -r .FDNS_A[] | sed -s 's/,/\n/g' | httpx -silent | anew

---

- **Using AssetFinder**

    [tomnomnom/assetfinder](https://github.com/tomnomnom/assetfinder)

    $ assetfinder --subs-only target.com >> target.com.txt

---

- **Using Knockpy**

    [guelfoweb/knock](https://github.com/guelfoweb/knock)

    $ knockpy.py target.com

---

- **Using Amass**

    [OWASP/Amass](https://github.com/OWASP/Amass)

    $ amass enum -d target.com -o target.com_amass.txt

---

- **Using Subbrute**

    [TheRook/subbrute](https://github.com/TheRook/subbrute)

    $ subbrute.py target.com -o target.com_Subbrute.txt

---

- **Using Sublist3r**

    [aboul3la/Sublist3r](https://github.com/aboul3la/Sublist3r)

    $ sublist3r.py -d target.com -o target.com_Sublist3r.txt

---

- **Using Sudomy**

    [Screetsec/Sudomy](https://github.com/Screetsec/Sudomy)

    $ sudomy -d target.com

---

- **Filter the Valid Subdomains Found**

    $ while read i; do digout=$(dig +short ${i//[$'\t\r\n ']}); if [[ ! -z $digout ]]; then echo ${i//[$'\t\r\n ']}; fi; done < target.com.txt > target.com_valid.txt

---

- **Python Script To Run All Tools In One Go By Me**

    $   python sub3num.py target.com 

    ```python
    #!/usr/bin/python
    from subprocess import Popen, PIPE
    import sys

    domain = sys.argv[1]
    commands = ['findomain -t '+domain+' -o;subfinder -d '+domain+' -o '+domain+'_subfinder.txt ;assetfinder --subs-only '+domain+' >> '+domain+'_assetfinder.txt;amass enum -d '+domain+' -o '+domain+'_amass.txt ;python ~/Bug-Tools/subbrute/subbrute.py '+domain+' -o '+domain+'_subbrute.txt ;python ~/Bug-Tools/Sublist3r/sublist3r.py -d '+domain+' -o '+domain+'_sublist3r.txt ;cat *.txt | sort -u >> '+domain+'_final_domains.txt ;cat '+domain+'_final_domains.txt | httprobe | httpx | sort -u >> valid_subs.txt;']
    count = 0
    processes = []
    for com in commands:
        print "Start execute commands.."
        processes.append(Popen(com, shell=True))
        count += 1
        print "[OK] command "+str(count)+" running successfully."
    else:
        print "Finish.."

    for i, process in enumerate(processes):
        process.wait()
        print "Command #{} finished".format(i)
    ```

---

💬 **Contact Me Here:**

[](https://twitter.com/AbhishekKarle3)

---

💬 **Comment down which tools you use for Subdomain Enumaration and your methodologies Here** 👇
