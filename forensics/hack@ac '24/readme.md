## Hack Me :)
**Description:** Hack me if you can :) <br><br>
This challenge was classified as a forensics challenge, and I was quite excited to see that it was a pcap file. I love Wireshark.<br><br>
A brief overview of the network tells us that this is a capture of traffic on a wireless network, specifically a 802.11 wireless network. We know this from checking the Protocol column! You see 802.11 and EAPOL.  

If you want to further inspect this, click onto a network packet and observe that the Encapsulation type is IEE 802.11 Wireless LAN! <br><br>
<img width="878" alt="image" src="https://github.com/jj2202/silly-writeups/assets/153341066/83c28ec5-e81b-4655-890e-df91d38f82b9">

From the presence of the EAPOL packets, we are hinted towards the fact there is a key we need to crack in order to find the flag. We have the handshake packets required to crack the key.
Thankfully, we can use the Aircrack-ng suite to do this.

**Command:** aircrack-ng router.pcap-01.cap -w /usr/share/wordlists/rockyou.txt <br><br>
I used the rockyou wordlist because there's not any hints I could find in the capture that would prompt me to make a personalised wordlist for the challenge. <br><br>
<img width="443" alt="image" src="https://github.com/jj2202/silly-writeups/assets/153341066/d01d016c-c488-4f62-8689-bddc34bddd01">

The key is **trin1179**. (It takes a while... Is this really the fastest way.)<br><br>
Now, we can use this key to decrypt the traffic! Epic.<br>
Apply it by following these steps: Edit --> Preferences --> Protocols --> Scroll to IEEE802.11 --> Decryption > Edit <br><br>
Click Ok to Apply.<br><br>
<img width="713" alt="image" src="https://github.com/jj2202/silly-writeups/assets/153341066/df100b6c-0eeb-488a-8406-dae12edc281c"><br><br>
We have applied this decryption key because now when we check the Protocol Hierarchy, we can see many more protocols than previously! (If you checked, it was just a load of nothing.) <br><br>
<img width="765" alt="image" src="https://github.com/jj2202/silly-writeups/assets/153341066/ad170e07-4810-403d-9841-545c077bebaa"><br><br>
There's HTTP in here. Let's see if there's any HTTP Objects we can export then: File --> Export Objects --> HTTP 

Oh, epic. There's a .txt file called flag.txt <br>
Flag: ***ACSI{0mGGGG!!!!_H0w_d1d_y0u_H@cK_mY_w1fI????}***  <br><br>
<img width="749" alt="image" src="https://github.com/jj2202/silly-writeups/assets/153341066/ef23a8c3-7cc2-4be7-8483-3448cc0215b8"><br><br>

---

You can try it for yourself if you want to. :) Download it from the HACK@AC '24 repository :3 [Here](https://github.com/Coding-Competition-Team/hackac-2024/tree/main/forensics/Hack%20me)<br>
You will have to delete the key though.<br><br>

-------- **Epic References**
<br>What is Aircrack-ng / How do you use Aircrack-ng - https://www.aircrack-ng.org/doku.php?id=aircrack-ng
