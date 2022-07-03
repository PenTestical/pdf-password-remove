# Cracking PDF passwords on Windows 10

## Requirements

+ Hashcat version 6.2.5.7: https://hashcat.net/files/hashcat-6.2.5.7z
+ Perl installer: https://strawberryperl.com/
+ John The Ripper (needed for PDF conversion): https://github.com/openwall/john/archive/refs/heads/bleeding-jumbo.zip
+ WeakPass Wordlist (small, 29GB): https://download.weakpass.com/wordlists/1947/weakpass_3.7z
+ *(WeakPass Wordlist (huge, 108GB): https://download.weakpass.com/wordlists/1948/weakpass_3a.7z)*

## How to crack PDF passwords (2-steps process)

It's a 2 step process. First, we need to generate the hash value with pdf2john.pl, and then crack the hash value with hashcat:

![image](https://user-images.githubusercontent.com/57206134/177036890-bb606d5e-203a-480f-84a2-70511de45756.png)

### 1) Generate the hash value

To generate the hash value, you need perl installed. Replace "your-PDF.pdf" with the name of your PDF file:

```perl pdf2john.pl your-PDF.pdf > hash.txt```

### 2) Crack the password with hashcat

To crack the password, use the "hash.txt" file you generated. The modes (-m NUMBER) can be checked at: https://hashcat.net/wiki/doku.php?id=example_hashes

```hashcat.exe -m 10400 hash.txt weakpass_3 -r rules\best64.rules```

Read more about hashcat rules: https://hashcat.net/wiki/doku.php?id=rule_based_attack

