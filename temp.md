```
 
 ██╗   ██╗ ██████╗ ██╗   ██╗██████╗     ████████╗███████╗ █████╗ ███╗   ███╗
 ╚██╗ ██╔╝██╔═══██╗██║   ██║██╔══██╗    ╚══██╔══╝██╔════╝██╔══██╗████╗ ████║
  ╚████╔╝ ██║   ██║██║   ██║██████╔╝       ██║   █████╗  ███████║██╔████╔██║
   ╚██╔╝  ██║   ██║██║   ██║██╔══██╗       ██║   ██╔══╝  ██╔══██║██║╚██╔╝██║
    ██║   ╚██████╔╝╚██████╔╝██║  ██║       ██║   ███████╗██║  ██║██║ ╚═╝ ██║
    ╚═╝    ╚═════╝  ╚═════╝ ╚═╝  ╚═╝       ╚═╝   ╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝
 
                       [ RAD 2.0 CTF — Write-Up ]
                   ================================
                    Team    :  Your Team  🇮🇳
                    Rank    :  7th Place
                    Points  :  3050
                    Date    :  March 14, 2025
                   ================================
```
 
---

| # | Challenge | Category | Points | Time Solved |
|---|-----------|----------|--------|-------------|
| 1 | Docking at Cyberzee Station | Welcome | 50 | Mar 14, 11:31 AM |
| 2 | The Astronaut Registry | Welcome | 50 | Mar 14, 11:34 AM |
| 3 | Echo Signal | Forensics | 100 | Mar 14, 11:36 AM |
| 4 | Signal from the Deep Space Telescope | Welcome | 50 | Mar 14, 11:45 AM |
| 5 | Corrupted Signal from Gargantua | Forensics | 100 | Mar 14, 11:49 AM |
| 6 | Event Horizon Authentication | Web | 150 | Mar 14, 11:54 AM |
| 7 | Tesseract Relay | Reverse | 250 | Mar 14, 11:56 AM |
| 8 | Hidden in Plain Sight | Crypto | 100 | Mar 14, 11:59 AM |
| 9 | Singularity Protocol | Reverse | 100 | Mar 14, 12:08 PM |
| 10 | Wormhole Access | Welcome | 50 | Mar 14, 12:10 PM |
| 11 | Singularity Echo | Crypto | 400 | Mar 14, 12:13 PM |
| 12 | Fragments Beyond Gargantua | MISC | 100 | Mar 14, 12:30 PM |
| 13 | Murph's First Signal | Steganography | 100 | Mar 14, 12:37 PM |
| 14 | Event Horizon Relay | Steganography | 200 | Mar 14, 1:35 PM |
| 15 | Sixty-Three Steps to Nowhere | MISC | 350 | Mar 14, 1:36 PM |
| 16 | Robots | OSINT | 100 | Mar 14, 1:55 PM |
| 17 | Murphy's Echo | Forensics | 250 | Mar 14, 2:01 PM |
| 18 | Timestamp Whisper | Forensics | 200 | Mar 14, 2:06 PM |
| 19 | Echo Beyond the Horizon | Web | 100 | Mar 14, 2:17 PM |
| 20 | Gargantua Relay Station | Web | 300 | Mar 14, 2:54 PM |

---

## Write-Ups

---

### 1. Docking at Cyberzee Station

| Field | Detail |
|-------|--------|
| **Points** | 50 |
| **Category** | Welcome |

**Description:**
> Join the Cyberzee Discord server and access the RAD sector. Mission Control will send a signal containing the flag.

**How we solved it:**

Pretty straightforward one to kick things off. We joined the Cyberzee Discord, headed over to the RAD sector channel, and the flag was just sitting there in a message from Mission Control. No tricks, just making sure you're actually part of the community.

---
### 1.5. Sixty-Three Steps to Nowhere
 
| Field | Detail |
|-------|--------|
| **Points** | 350 |
| **Category** | MISC |
 
**Description:**
> A piece was left wandering on a board it never understood. It never stood still, never repeated itself, and yet somehow returned home. Every tile remembers the moment it was touched. Follow the wanderer's footsteps in the only order that makes sense. Sixty-three steps were taken. The sixty-fourth was inevitable.
 
**How we solved it:**
 
This one was genuinely one of our favourites from the whole CTF. The riddle is poetic but every line is a direct clue if you read it carefully.
 
*"A piece was left wandering on a board it never understood"* — there's a knight (♘) sitting on `d4` in the provided grid. *"Never stood still, never repeated itself, and yet somehow returned home"* — that's a closed Knight's Tour: visit every single square on an 8×8 board exactly once using only L-shaped knight moves, then land back where you started. *"Sixty-three steps were taken, the sixty-fourth was inevitable"* — 64 squares, 63 moves, the last one closes the loop back to `d4`.
 
So the grid has a character on every square. The challenge is figuring out *which* Knight's Tour path, when followed, spells out something readable. There's only one that makes coherent leetspeak English.
 
We started at the knight on `d4` and traced the path square by square. One thing that tripped us up briefly — the character on `a4` has a tiny top serif which makes it look like a lowercase `l`, but it's actually the number `1`. The hint **D4_closed_loop** confirmed the mechanic perfectly and nudged us toward that correction.
 
Tracing all 63 steps and collecting the characters in order:
 
- `d4` → `f5(R)` → `d6(A)` → `e8(D)` → `c7({)` → `a8(k)` → `b6(n)` → `a4(1)` → `b2(g)` → `d1(h)` → `f2(t)` → `h1(_)` → ...continuing through all 64 squares...→ `f3(a)` → back to `d4(})`
 
The full string collected along the path spelled out the flag. A satisfying puzzle — pure chess logic meets CTF encoding.
 Stringing all these visited squares together yields the final flag.


RAD{knlght_t0ur_p4th_8x8_ch3ss_gr1d_m4p_63_sq_v1s1t_fl4g_h3r3_a}


**Key technique:** Closed Knight's Tour path tracing on an 8×8 character grid, leetspeak decoding.
 
---

### 2. Timestamp Whisper

| Field | Detail |
|-------|--------|
| **Points** | 200 |
| **Category** | Forensics |

**Description:**
> A deep-space probe relays telemetry through a ground station. Normal network traffic looks fine, but command acknowledgments are missing. Intel suggests a covert channel hidden in timing jitter rather than payloads. Analyze the capture and recover the hidden transmission.

**How we solved it:**

The description made it pretty clear this wasn't about what was inside the packets — it was about *when* they arrived. Timing-based covert channels work by encoding bits into the gaps between packets rather than the data itself, which is why payload inspection turns up nothing.

We loaded the capture into Wireshark first just to get a feel for it, then wrote a quick Scapy script to pull out the inter-packet time deltas. Two values kept showing up — roughly 49 ms and 50 ms. That 1 ms difference was the signal: 49 ms mapped to `0`, 50 ms mapped to `1`.

From there it was just collecting the bits, grouping them into bytes, and decoding as ASCII. The hidden message came right out.

**Key technique:** Side-channel extraction via inter-packet timing deltas.

---

### 3. Murph's First Signal

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | Steganography |

**Description:**
> An image recovered from Murph's bookshelf. Something's hidden inside the pixels.

**How we solved it:**

First thing we did was the usual boring checklist — `exiftool` for metadata, `strings` to see if anything was just appended to the file. Nothing came up on either. So the data was clearly hidden at the bit level inside the image itself.

Threw it at `zsteg` which goes through all the bit planes and color channels looking for hidden data. It found something embedded in one of the LSB layers and pulled out the flag directly. Honestly one of the quicker ones once you know the right tool to reach for.

**Key technique:** LSB steganography extraction via `zsteg`.

---

### 4. Corrupted Signal from Gargantua

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | Forensics |

**Description:**
> A mysterious transmission was received from a probe near Gargantua. The signal appears corrupted and the file cannot be opened normally. Something in the data seems to be missing or damaged.

**How we solved it:**

File won't open? First instinct is always to check the header in a hex editor. Sure enough, the PNG magic bytes were messed up — but what made this slightly trickier than a standard header repair was that *two* regions were corrupted. The first few bytes were wrong, but so were the void bytes further into the magic sequence, which is easy to miss if you just fix the obvious part and move on.

Once we patched both sections back to what a valid PNG header should look like, the file opened fine and the flag was right there in the image.

**Key technique:** PNG magic byte restoration — both leading bytes and void bytes.

---

### 5. Event Horizon Authentication

| Field | Detail |
|-------|--------|
| **Points** | 150 |
| **Category** | Web |

**Description:**
> The login credentials were constantly changing every 3 seconds. Time behaves differently near the horizon. If you want access, you'll have to stop time… or move faster than it.

**How we solved it:**

We opened the page and immediately saw the problem — the credentials were cycling every 3 seconds, way too fast to type manually. The hint about "moving faster than time" was basically pointing at automation.

Popped open DevTools and watched the Network tab. The site was making requests to an API endpoint that returned fresh credentials before they got displayed on screen. So the credentials were available a moment before you could even see them — we just needed to intercept them at that stage.

We set up Burp Suite to catch the credential response, grabbed the username and password, and fired the login request straight from Burp Repeater before the next rotation kicked in. Server accepted them and returned the flag.

**Key technique:** Burp Suite interception, race-condition-aware credential capture.

---

### 6. Hidden in Plain Sight

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | Crypto |

**Description:**
> A strange encoded string was recovered. Sometimes the simplest layers hide the real secret. Decode the message and uncover the hidden flag.

**How we solved it:**

Looked like Base64 right away, so we ran it through a decoder. Got back another Base64 string. Ran it again. Another one. Third time was the charm — the flag came out clean.

Triple-nested Base64 is a classic CTF move. Chained three "From Base64" steps in CyberChef and that was it.

**Key technique:** Triple-layer Base64 decoding via CyberChef.

---

### 7. Robots

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | OSINT |

**Description:**
> In Interstellar, Christopher Nolan built fully functional practical robot props instead of using CGI. Identify the special effects company that built the TARS robot.
>
> **Flag Format:** `RAD{Company Name}` — first letter of each word capitalised, spaces included.

**How we solved it:**

Bit of a trivia/OSINT challenge. We searched around the production details for *Interstellar* and quickly landed on the answer — the TARS and CASE robots were physical props built by **Legacy Effects**, the Hollywood practical effects studio behind a ton of big productions. Formatted it per the flag instructions and that was that.

**Key technique:** OSINT via web search into film production credits.

---

### 8. Echo Signal

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | Forensics |

**Description:**
> The Endurance spacecraft intercepted a strange transmission. The signal doesn't appear to be a normal image and seems to be encoded in an unusual format. Analyze the signal and recover what was sent.

**How we solved it:**

We got a `.wav` file. Playing it back gave us those distinctive screechy, warbling tones that anyone who's done radio stuff before would recognise instantly — it's SSTV (Slow-Scan Television). It's been used since the early days of space exploration to beam images over radio.

Identified the mode as **Robot 36** based on the audio characteristics, then decoded it using `qsstv`. The output was an image with the flag in it.

**Key technique:** SSTV Robot 36 decoding via `qsstv`.

---

### 9. The Lazarus Leak

| Field | Detail |
|-------|--------|
| **Points** | 250 |
| **Category** | OSINT / Steganography |

**Description:**
> A corrupted archive appeared online containing fragments of a Lazarus probe transmission. The leak was spread across multiple platforms by someone who wanted the information preserved.

**How we solved it:**

The challenge gave us the username `dr-mann-archive` and basically said "go find the pieces." So we started hunting across platforms.

Found the first fragment on **Reddit** in a post under that account. Second one was buried in a **GitHub** repo. Third showed up on **Instagram** in the bio or a post caption. Three parts down, but the flag wasn't complete yet.

The fourth piece ended up being hidden in the EXIF metadata of an image file — just a single `!` character sitting in the metadata, recoverable with `exiftool`. Easy to miss if you don't think to check there. Put all four pieces together in order and the flag was complete.

**Key technique:** Multi-platform OSINT username hunt + EXIF metadata extraction via `exiftool`.

---

### 10. The Astronaut Registry

| Field | Detail |
|-------|--------|
| **Points** | 50 |
| **Category** | Welcome |

**Description:**
> Locate Cyberzee's LinkedIn page and inspect the latest broadcast discussion.

**How we solved it:**

Found the Cyberzee LinkedIn page, opened their latest post, and scrolled through the comments. Mission Control had dropped the flag there. Simple one but you had to know where to look.

**Key technique:** LinkedIn OSINT / Welcome challenge.

---

### 11. Singularity Protocol

| Field | Detail |
|-------|--------|
| **Points** | 100 |
| **Category** | Reverse Engineering |

**Description:**
> Every session: new constants. A new cipher. The VM ran forward. You must run it backward — in real time, on an equation you've never seen before.

**How we solved it:**

The description sounds way scarier than the actual solution. The flag wasn't stored anywhere in the binary — it was being built in memory while the program ran. On top of that, the binary had a `ptrace` check to detect debuggers and bail out before anything useful happened.

First step was patching out that `ptrace` call so we could actually attach without the process killing itself. Once that was done we used `ltrace` to watch the library calls during execution and `r2` to set breakpoints and inspect memory at the right moments. We dumped `var_278`, `var_2a8`, and the `tp` region — that last one had the fully assembled flag sitting in it at runtime.

**Key technique:** Anti-debug bypass via `ptrace` patch, runtime memory dumping with `ltrace` + Radare2.

---

*Write-up by **Your Team** · RAD 2.0 CTF · 7th Place · 3050 Points*
