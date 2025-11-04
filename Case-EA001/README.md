# **The Planet's Prestige**

Challege Link: [https://blueteamlabs.online/home/challenge/the-planets-prestige-e5beb8e545](https://blueteamlabs.online/home/challenge/the-planets-prestige-e5beb8e545)

**Scenario**

CoCanDa, a planet known as 'The Heaven of the Universe' has been having a bad year. A series of riots have taken place across the planet due to the frequent abduction of citizens, known as CoCanDians, by a mysterious force. CoCanDa’s Planetary President arranged a war-room with the best brains and military leaders to work on a solution. After the meeting concluded the President was informed his daughter had disappeared. CoCanDa agents spread across multiple planets were working day and night to locate her. Two days later and there’s no update on the situation, no demand for ransom, not even a single clue regarding the whereabouts of the missing people. On the third day a CoCanDa representative, an Army Major on Earth, received an email.

# **Email Analysis Report**

### Tools Used

1. Exiftool
2. HxD
3. Notepad++
4. https://www.garykessler.net/library/file_sigs.html
5. https://gchq.github.io/CyberChef/
6. WinRar/7zip
7. https://mxtoolbox.com/EmailHeaders.aspx
8. https://whatismyipaddress.com/ip/
9. https://www.virustotal.com/
10. SquareX File viewer online

### 1. **Basic Information**

| Field | Details |
| --- | --- |
| **Case ID** | EA001 |
| **Analyst Name** | Jaya Sai Krishna Guttula |
| **Date of Analysis** | 04-11-2025 |
| **Source of Email** | User-reported |
| **Email Received Date & Time** |  Tue, 26 Jan 2021 01:41:18 -0500 (EST) |
| **Email Subject** | A Hope to CoCanDa |
| **Sender Name & Address** | Bill & billjobs@microapple.com |
| **Reply-to** | negeja3921@pashter.com |
| **Recipient(s)** | themajoronearth@gmail.com |
| **Reported By** | Army Major |

---

### 2. **Initial Observation**

- The email was sent from an unauthorized mail server. The SPF check **failed** indicating the sender IP **93.99.104.210** is **not authorized** to send mail on behalf of **microapple.com**.
- The **“Received”** header shows the message originated from **localhost (emkei.cz)**, which is a known **fake email generator service**, confirming potential spoofing or social engineering intent.
- The **“Reply-To”** address (`negeja3921@pashter.com`) differs from the “From” address (`billjobs@microapple.com`), suggesting an attempt to redirect replies to a different malicious or attacker-controlled account.
- The email is of type **multipart/mixed**, indicating multiple parts — a **plain text body** and an **attachment**.
- The attached file **“PuzzleToCoCanDa.pdf”** is likely the malicious payload or phishing lure document.
- All components use **Content-Transfer-Encoding: base64**, a common technique to encode attachments and text, possibly used here to **obfuscate content** and **bypass filters**.
- Overall, the headers and structure strongly suggest this is a **phishing or social engineering attempt** sent from a spoofed domain using a fake email service.

---

### 3. **Header Analysis**

| Header Field | Observation |
| --- | --- |
| **Return-Path** | billjobs@microapple.com |
| **Received From** | localhost (emkei.cz [93.99.104.210]) |
| **SPF Record** | Fail |
| **DKIM Signature** | Not Present |
| **DMARC Alignment** | Not Present |
| **Originating IP** | 93.99.104.210 |
| **Geolocation of IP** | Czechia |
| **Reverse DNS / WHOIS Info** | moaningrail.gb.net |

IP Lookup

![image.png](image.png)

MxToolbox Header analyser

![image.png](image%201.png)

---

### 4. **Body & Content Analysis**

| Component | Findings |
| --- | --- |
| **Language & Tone** | Threatening |
| **Brand Impersonation** | No |
| **Grammar & Spelling** | (Errors / Poor formatting / Legitimate) |
| **Embedded Links** | Not Present |
| **Attachments** | PuzzleToCoCanDa.pdf |
| **Suspicious Indicators** | Attachment is encoded |

Body is encoded using base64

Decode Message using Cyberchef

```python
Hi TheMajorOnEarth,

The abducted CoCanDians are with me including the President’s daughter. Dont worry. They are safe in a secret location.
Send me 1 Billion CoCanDs🤑 in cash💸 with a spaceship🚀 and my autonomous bots will safely bring back your citizens.

I heard that CoCanDians have the best brains in the Universe. Solve the puzzle I sent as an attachment for the next steps.

I’m approximately 12.8 light minutes away from the sun and my advice for the puzzle is 

“Don't Trust Your Eyes”

Lol😂

See you Major. Waiting for the Cassshhhh💰
```

![image.png](image%202.png)

---

### 5. Email Domain **Analysis**

| Domain | Verdict |
| --- | --- |
| microapple.com | Legit |
| pashter.com | Malicious |

Virustotal results on microapple.com

![image.png](image%203.png)

Virustotal result on pashter.com

![image.png](image%204.png)

---

### 6. **Attachment Analysis**

Decoding the attachment

Copy the pdf contents and paste it in the cyberchef

![image.png](image%205.png)

Cyberchef detected it as a .zip file.

Save the file and extract it.

![image.png](image%206.png)

We got 3 file 2 files are normal 1 file is hidden.

Lets check the file types using HxD and GCK'S FILE SIGNATURES TABLE.

| File Name | Signature | Type | SHA256 Hash | Result |
| --- | --- | --- | --- | --- |
| DaughtersCrown | FF D8 FF E0 | JPEG, JPG | BA4F25BF16BA4BE6BC7D3276FAFEB67F9EB3C5DF042BC3A405E1AF15B921EED7 | Not malicious |
| GoodJobMajor | 25 50 44 46 | PDF | 315D429B7714CEDB6AD04AC31240145257692630457F3C88253C5BECEAC76027 | Not malicious |
| Money.xlsx | 50 4B 03 04 | .xlsx | 8DCC7E601606217F3B754766511182A916B17E9A26A94C9D887104EBA92E9BB2 | Not malicious |

Lets rename the first two file with their extensions and view the files. (use online SquareX file Viewer)

DaughtersCrown.jpeg

![image.png](image%207.png)

GoodJobMajor.pdf

![image.png](image%208.png)

Money.xlsx

Sheet 1

![image.png](image%209.png)

Sheet 3 - If you Format the cell in black you will get a base64 message

![image.png](image%2010.png)

```python
VGhlIE1hcnRpYW4gQ29sb255LCBCZXNpZGUgSW50ZXJwbGFuZXRhcnkgU3BhY2Vwb3J0Lg==

```

Decode with cyberchef

```python
The Martian Colony, Beside Interplanetary Spaceport.
```

---

### Questions & Answers

What is the email service used by the malicious actor?

**Answer:** emkei.cz

What is the Reply-To email address? 

**Answer:** negeja3921@pashter.com

What is the filetype of the received attachment which helped to continue the investigation? *(1 points)*

**Answer:** Zip

What is the name of the malicious actor? *(2 points)*

**Answer:**  Pestero Negeja

What is the location of the attacker in this Universe? *(2 points)*

**Answer:** The Martian Colony, Beside Interplanetary Spaceport.

What could be the probable C&C domain to control the attacker’s autonomous bots? *(2 points)*

**Answer:** pashter.com
