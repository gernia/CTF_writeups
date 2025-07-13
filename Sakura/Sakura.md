## Step 1: The SVG Picture

- the picture can be looked at in the browser
- using inspect, we can see the export filename of the svg: /home/SakuraSnowAngelAiko/Desktop/pwnedletter.png

![Pasted image 20250711213342.png](https://github.com/gernia/CTF_writeups/blob/main/Sakura/imgs/Pasted%20image%2020250711213342.png)

- **What username does the attacker go by? - SakuraSnowAngelAiko**
## Step 2: Search for Username

- search for the username on google
- we find a github and an X account
- look up username search tools on OSINT Framework -> usersearch.org and https://whatsmyname.app/
- didn't give us anything new compared to google

## Step 3: GitHub 
https://github.com/sakurasnowangelaiko

### Step 3.1: The Crypto Wallet
- we find, that sakura accidentally made her ethereum wallet address public in an old commit `stratum://0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef.Aiko:pswd@eu1.ethermine.org:4444`

- **What cryptocurrency does the attacker own a cryptocurrency wallet for? - Ethereum**
- **What is the attacker's cryptocurrency wallet address? - 0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef** 

- using etherscan.io we can look up the wallet address and can see the transactions

![Pasted image 20250712212707.png](https://github.com/gernia/CTF_writeups/blob/main/Sakura/imgs/Pasted%20image%2020250712212707.png)
- **What mining pool did the attacker receive payments from on January 23, 2021 UTC? - Ethermine**

- under token transfers we can also see which other cryptocurrency was used

- **What other cryptocurrency did the attacker exchange with using their cryptocurrency wallet? - Tether**

### Step 3.2: The E-Mail Address
- Also on GitHub, Aiko posted a PGPKey. Using `gpg --show-keys publickey` (publickey is the file containing her key), we get the associated E-Mail address.

- **What is the full email address used by the attacker? - SakuraSnowAngel83@protonmail.com**

![Pasted image 20250712212251.png](https://github.com/gernia/CTF_writeups/blob/main/Sakura/imgs/Pasted%20image%2020250712212251.png)
		
## Step 4: X
X Account: @SakuraLoverAiko
- **What is the attacker's current Twitter handle? - SakuraLoverAiko**
  
-  on this account, she says she is @AikoAbe3
  - **What is the attacker's full real name? - Aiko Abe**

### Step 4.1: DeepPaste
- Aiko shared a screenshot of the onion site DeepPaste. DeepPaste (http://deepv2w7p33xa4pwxzwi2ps4j62gfxpyp44ezjbmpttxz3owlsp4ljid.onion/ ) got removed, so I could not find her DeepPaste site (which had the address b2b37b3c106eb3f86e2340a3050968e2)
- I resorted to using the image the OSINT Dojo hosted of the DeepPaste site on github:
![OSINT Dojo DeepPaste img](https://raw.githubusercontent.com/OsintDojo/public/main/deeppaste.png)
- there we can see a Wifi called Home Wifi with the SSID DK1F-G
- we can search on WiGLE.com for this SSID and find the BSSID 84:af:ec:34:fc:f8
- **What is the BSSID for the attacker's Home WiFi? - 84:af:ec:34:fc:f8**
  
- also WiGLE shows us where the Home WiFi is located: in Hirosaki
- **What city does the attacker likely consider "home"? - Hirosaki**
  
### Step 4.2: The Flights
- Aiko shared some pictures on her X account. The first one is a view of the Washington Monument before she got on her flight
- **What airport is closest to the location the attacker shared a photo from prior to getting on their flight? - DCA (Ronald Reagan Washington National Airport)**
   
- Aiko shared a google maps satellite shot with the text "soo close to home". Because Aikos Name is Japanese, we can assume it's a shot of Japan. Looking at Japan on Google Maps, north if Tokyo in Fukushima Prefecture is a very round lake - the lake from the post
- **What lake can be seen in the map shared by the attacker as they were on their final flight home? - Lake Inawashiro**
   
- Because Aikos home is Japan, she probably flies via Tokyo. To determine which airport it is (Haneda or Narita), I looked up pictures of the Sakura lounge on google images. Searching "haneda sakura lounge entry" I found the same entryway that Aiko posted.
- **What airport did the attacker have their last layover in? - HND**
  
 ![Pasted image 20250712233034.png](https://github.com/gernia/CTF_writeups/blob/main/Sakura/imgs/Pasted%20image%2020250712233034.png)


## Remarks
- I think there was supposed to be a LinkedIn Profile to be found - I couldn't find it, I think it got removed
- similar to DeepPaste, which has also been removed 
	- http://deepv2w7p33xa4pwxzwi2ps4j62gfxpyp44ezjbmpttxz3owlsp4ljid.onion/ which is the onion link for DeepPaste (as found on here https://oniondotindex.com/deeppaste-onion-links/) leads nowhere

	
