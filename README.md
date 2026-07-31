# অপারেটিং সিস্টেম — একদম গোড়া থেকে, বাংলায়

> A complete, free Operating Systems course in Bengali — theory, hand-drawn diagrams, and hands-on C projects.

**🌐 [os.najmulislam.dev](https://os.najmulislam.dev)**

OS কীভাবে কাজ করে — process, memory, concurrency, file system — সব বাংলায়, ডায়াগ্রাম আর হাতে-কলমে C প্রজেক্ট সহ। শূন্য থেকে শুরু করে নিজের kernel পরিবর্তন করা পর্যন্ত একটা সম্পূর্ণ পথ।

কোর্সটা সাজানো হয়েছে **OSTEP**-এর তিন স্তম্ভ ঘিরে — Virtualization · Concurrency · Persistence।

---

## কেন এই কোর্স

- **শুধু পড়া নয়, বানানো** — প্রতিটা ধারণার সাথে C-তে বাস্তবায়ন। একটা মডিউল "শেষ" ততক্ষণ নয়, যতক্ষণ না তার প্রজেক্টটা কাজ করছে।
- **নিজের আঁকা ডায়াগ্রাম** — paging, context switch, deadlock, inode — প্রতিটা কঠিন ধারণা SVG ডায়াগ্রামে বোঝানো, কপি করা ছবি নয়।
- **বাংলায়, কিন্তু পরিভাষা ঠিক রেখে** — ব্যাখ্যা বাংলায়, টেকনিক্যাল টার্ম (syscall, page fault, inode) ইংরেজিতেই, যাতে ইংরেজি বই-ডকুমেন্টেশনে গিয়ে আটকে না যান।

## শুরু কোথা থেকে

নতুন হলে **[রোডম্যাপ](https://os.najmulislam.dev/plan.html)** দিয়ে শুরু করুন — কী কোন ক্রমে শিখবেন, কোন রিসোর্স, কত সময় লাগবে, সব এক জায়গায়। তারপর মডিউল ১।

## মডিউল

| # | মডিউল | যা শিখবেন | প্রজেক্ট |
|---|---|---|---|
| ০১ | [ভিত্তি](https://os.najmulislam.dev/module1.html) | kernel vs user space, system call, interrupt ও trap, OS-এর স্থাপত্য, boot process | `strace` দিয়ে syscall বিশ্লেষণ |
| ০২ | [Process ও Scheduling](https://os.najmulislam.dev/module2.html) | process জীবনচক্র, fork/exec/wait, context switch, scheduling অ্যালগরিদম, thread, IPC | নিজের shell (pipe + background job সহ) |
| ০৩ | [Memory ও Virtual Memory](https://os.najmulislam.dev/module3.html) | address translation, paging, TLB, multi-level page table, page fault, swap, page replacement | নিজের `malloc` (coalescing সহ) |
| ০৪ | [Concurrency](https://os.najmulislam.dev/module4.html) | race condition, critical section, mutex, condition variable, semaphore, deadlock | producer-consumer + dining philosophers |
| ০৫ | [Storage ও File System](https://os.najmulislam.dev/module5.html) | disk, file ও directory, inode, path resolution, journaling, disk scheduling, buffer cache | toy file system (create/read/write/ls) |
| ০৬ | [নিজের OS বানানো](https://os.najmulislam.dev/module6.html) | xv6 পড়া ও চালানো, নতুন syscall যোগ, scheduler বদল, GDB debug, MIT 6.1810-র পথ | xv6 kernel hacking |

প্রতিটা মডিউল আগেরটার উপর দাঁড়িয়ে — ক্রম মেনে যাওয়াই ভালো।

## কত সময় লাগবে

| গতি | সময় |
|---|---|
| নিবিড় (full-time) | ~৩ মাস |
| ধীর (সপ্তাহে ১০ ঘণ্টা) | ~৬ মাস |

সাপ্তাহিক ছন্দ: **৪০% পড়া → ৪০% কোড → ২০% রিভিশন**।

## যা লাগবে

- **C-র প্রাথমিক জ্ঞান** — pointer, struct, array বুঝলেই যথেষ্ট
- **Linux** (বা Windows-এ WSL2, Mac-এ বেশিরভাগ কাজ চলে)
- `gcc`/`clang`, `make`, `gdb`, `strace`
- মডিউল ৬-এর জন্য বাড়তি: **QEMU** + RISC-V toolchain

সবই বিনামূল্যে ও ওপেন সোর্স।

## রিসোর্স

কোর্সটা এই রিসোর্সগুলোর উপর দাঁড়িয়ে — অল্প কিন্তু সেরা কয়েকটাতেই লেগে থাকুন:

- [**OSTEP**](https://pages.cs.wisc.edu/~remzi/OSTEP/) — বিনামূল্যে অনলাইন বই, পুরো পথের মেরুদণ্ড
- [**MIT 6.1810**](https://pdos.csail.mit.edu/6.1810/) — xv6 দিয়ে হাতে-কলমে kernel lab, video ও lab উন্মুক্ত
- [**xv6 book**](https://pdos.csail.mit.edu/6.1810/2023/xv6/book-riscv-rev3.pdf) — একটা আসল ছোট OS-এর ভাষ্য
- **CS:APP** — hardware-software সীমানা গভীরভাবে
- [**The Little Book of Semaphores**](https://greenteapress.com/wp/semaphores/) — concurrency অনুশীলনের জন্য

## লোকালি চালানো

কোনো build step, dependency বা package manager নেই — প্রতিটা পেজ একটা স্বয়ংসম্পূর্ণ HTML ফাইল। ক্লোন করে `index.html` ব্রাউজারে খুললেই হয়।

```bash
git clone https://github.com/najmulislamnajim/os.git
cd os
python -m http.server 8000   # অথবা সরাসরি index.html খুলুন
```

## ফাইল গঠন

```
index.html      কোর্স হোম — সব মডিউলের কার্ড
plan.html       সম্পূর্ণ রোডম্যাপ ও স্টাডি প্ল্যান
module1..6.html ছয়টা মডিউল
CNAME           GitHub Pages-এর কাস্টম ডোমেইন
```

## অবদান

ভুল, টাইপো, বা কোনো ব্যাখ্যা অস্পষ্ট মনে হলে [issue খুলুন](https://github.com/najmulislamnajim/os/issues) — ছোট সংশোধনও স্বাগত। নতুন কোনো বিষয় বা ডায়াগ্রাম যোগ করতে চাইলে PR পাঠানোর আগে একটা issue খুলে আলোচনা করে নিলে ভালো হয়।

## কৃতজ্ঞতা

Remzi ও Andrea Arpaci-Dusseau (OSTEP), আর MIT PDOS দলের (xv6, 6.1810) কাছে — তাঁদের উন্মুক্ত কাজ ছাড়া এই কোর্স সম্ভব হতো না।

---

কোর্সটা **উন্মুক্ত ও বিনামূল্যে**। ভালো লাগলে একটা ⭐ দিন — অন্যদের কাছে পৌঁছাতে সাহায্য করে।

তৈরি করেছেন **[Najmul Islam](https://github.com/najmulislamnajim)**
