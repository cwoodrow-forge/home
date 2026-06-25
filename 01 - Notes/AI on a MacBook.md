---
categories:
  - "[[Reference Guides]]"
subjects:
  - "[[Technology]]"
type: guide
description: "Article: solo developer implemented Google's AI memory-compression paper in llama.cpp, achieving 3.7x speed on a standard MacBook."
created: 2026-06-18
---
A Random Developer Just Crushed Google’s Billion-Dollar AI Trick in 7 Days And It Runs on a Regular MacBook

Google dropped a huge paper in March 2026 about a new way to make AI models use way less memory. It was so good that memory chip stocks took a hit around the world.  

Then… Google shipped zero code. Nothing.

Enter Tom Turney, a solo developer. He read the paper, grabbed Claude (the AI coding helper), and built the whole thing himself in just one week. He dropped it straight into llama.cpp, the free tool everyone uses for running big AI models.

Result? It’s 3.7 times faster. On a MacBook’s built-in graphics chip, it hits 2,747 tokens per second. That’s blazing fast.

But Tom didn’t stop there. He added his own smart improvements:





Skips 90% of slow memory steps when the chat gets long





Keeps important parts precise and compresses the rest harder





Old messages automatically use less memory over time

Now a massive 35-billion-parameter AI model runs smoothly on a normal MacBook with 4.6 times less memory needed for the thinking part.

The GitHub repo? 613 stars in days. Google still hasn’t released their own version.

This is the new reality in AI: big companies publish the ideas, but one smart solo dev + free AI tools can ship the working code faster than entire teams at Google.

Open source is eating the world. Solo builders are winning. The gap between paper and actually works on your laptop just got tiny.

Reference 

https://substack.com/@gencay/note/c-252916457?r=7wkgcg&utm_medium=ios&utm_source=notes-share-action