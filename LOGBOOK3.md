# Trabalho realizado na Semana #3

## Identificação 

- CVE-2020-0688: Microsoft Exchange Validation Key Remote Code Execution Vulnerability (`1`)
- Remote code execution vulnerability were identified in Microsoft Exchange Server (`1`)
- Occurs when the server fails to properly create unique keys at install (`1`)

## Catalogação

- The National Vulnerability Database gave it a Base Score of 8.8 HIGH (`2`)
- Microsoft patched this vulnerability in Feb/2020 however, in late 2020 it was estimated that over 60% of Exchange servers were still vulnerable (`3`)
- This vulnerability was reported by an anonymous researcher working at Trend Micro’s Zero Day Initiative (`4`)
- Initially, Microsoft stated this bug was due to a memory corruption vulnerability but later revised their write-up to indicate that the vulnerability results from failing to properly create unique keys at install (`4`)

## Exploit

- Due to the use of static keys, an authenticated attacker can trick the server into deserializing maliciously crafted ViewState data. (`4`)
- Microsoft listed this with an Exploit Index of 1, which means they expected to see exploits within 30 days of the patch release (`1`)

## Ataques

- Cybersecurity firm Volexity observed multiple APT groups exploiting or attempting to exploit on-premise Exchange Servers. (`5`)

-----------------------------------------

### Bibliografia

`1` https://msrc.microsoft.com/update-guide/en-US/vulnerability/CVE-2020-0688 <br /> 
`2` https://nvd.nist.gov/vuln/detail/CVE-2020-0688#vulnCurrentDescriptionTitle <br /> 
`3` https://securityaffairs.co/wordpress/108946/hacking/vulnerable-exchange-servers.html <br /> 
`4` https://www.zerodayinitiative.com/blog/2020/2/24/cve-2020-0688-remote-code-execution-on-microsoft-exchange-server-through-fixed-cryptographic-keys <br /> 
`5` https://www.logpoint.com/en/blog/microsoft-exchange-server-rce-vulnerability/ <br /> 
