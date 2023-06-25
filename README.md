# সিস্টেম ডিজাইন বাংলা

এটি একটি রিপোজিটরি যেখানে সিস্টেম ডিজাইন এর মৌলিক জিনিসগুলো নিয়ে আলোচনা করা হয়েছে।

[সিস্টেম ডিজাইন একটি বিশাল টপিক, আমাদের জিনিসগুলো বুঝতে হলে সবসময় পড়ালেখার মধ্যে থাকতে হবে।]

<p align="center">
  <img src="./images/system-design-wallpaper.png" alt="System Design Wallpaper">
</p>

### সুচিপত্র

- [Section 1: System Design](#section-1-system-design)
- [Section 2: Client Server Architecture](#section-2-client-server-architecture)
- [Section 3: Reliability](#section-3-reliability)
- [Section 4: Performance Metrics](#section-4-performance-metrics)
- [Section 5: Distributed System](#section-5-distributed-system)
- [Section 6: Proxy](#section-6-proxy)
- [Section 7: REST API](#section-7-rest-api)
- [Section 8: Scalability](#section-8-scalability)
- [Section 9: Sharding](#section-9-sharding)
- [Section 10: Database Replication](#section-10-database-replication)
- [Section 11: Caching](#section-11-caching)
- [Section 12: CAP]
  - [What is CAP]
  - [Consistency, Availability & Partitioning in Distributed System]
- [Section 13: Resources](#section-11-resources)

## Section 1: System Design

আমরা যখন কোন এপ্লিকেশন ডেভেলপ করতে যাই আমাদের একটি নির্দিষ্ট প্রকারের ডিজাইন মেনে চলতে হয়, তার কারণ হল আমাদের এপ্লিকেশনে কোন এক সময় থেকে যদি প্রচুর মানুষ ব্যবহার করা শুরু করতে থাকে, তখন আমাদের এপ্লিকেশন যাতে প্রচুর লোড ভালোভাবে নিতে পারে কোন প্রকারের কানেকশন নষ্ট বা পারফরমেন্স ডাউন হওয়া ছাড়া সেজন্য। সেই ডিজাইন কে বলা হয় সিস্টেম ডিজাইন।

(এই স্পেসিফিক সিস্টেম ডিজাইন মূলত ব্যাকএন্ড ইঞ্জিনিয়ারিং এর সাথে সম্পৃক্ত।)

## Section 2: Client Server Architecture

ক্লায়েন্ট রিকুয়েস্ট করবে সার্ভারকে কিছু স্পেসিকিফ রিসোর্স এর জন্য, সার্ভার সেই রিকুয়েস্ট পাওয়ার পর সে তার যাবতীয় প্রসেস শেষ করে ক্লায়েন্টকে রেসপন্স দিয়ে দিবে, এটি ক্লায়েন্ট সার্ভার আর্কিটেকচার।

<p align="center">
  <img src="./images/csa.png" alt="Client Server Architecture">
</p>

আমাদের সব উদাহরণ থাকবে ক্লায়েন্ট সার্ভার আর্কিটেকচারের উপর ভিত্তি করে।

## Section 3: Reliability

সিস্টেম যদি কোনো প্রকারের Fault/Error থাকার পরও ভালোভাবে কাজ করতে পারে কিংবা সিস্টেমটি যদি বন্ধ না হয়, তবে সেই সিস্টেমটি Reliable। আমাদের মনে রাখতে হবে এক বা একাধিক Fault এর কারণে সিস্টেম Failure হতে পারে।

Fault এরকম হতে পারে কোনো user সিস্টেমটি কে এমনভাবে ব্যবহার করেছে যাতে কোনো Failure হয়ে গেল, সেটা ইচ্ছাকৃত বা অনিচ্ছাকৃতভাবেও হতে পারে, তখন যদি সিস্টেমটি বন্ধ না হয়ে কোনো প্রকারের Warning message দেখালো তখন সেই সিস্টেমটিকে আমরা Reliable বলতে পারি।

🔗 [**আরও পড়ুন: রিলাইবিলিটি**](./sections/reliability/README.md)

## Section 4: Performance Metrics

### Throughput

একটি নির্দিষ্ট সময়ের ভিত্তিতে কোনো সিস্টেম যতটুকু কাজ সম্পাদন করতে পারে সেটি হচ্ছে Throughput। যেমন, প্রতি ১০ সেকেন্ড এ সিস্টেম যদি ৫০ টি API request সম্পন্ন করতে পারে তাহলে তার Throughput হবে ৫০/১০ = ৫।

### Latency

যখন রিকুয়েস্ট Client থেকে শুরু করে Server পর্যন্ত যেতে যত সময় লাগে এবং সেই Server থেকে আবার রেসপন্স যখন Client এ আসতে যত সময় লাগে সেই সময়টুকু হল Latency। Latency মূলত Network এর সময়টুকুর উপর নির্ভরশীল।

<p align="center">
  <img src="./images/latency.png" alt="Latency">
</p>

### Response Time

Response Time হল Server রিকুয়েস্ট প্রসেস করতে যত সময় নেয়, সেই সময় আর Latency এর সময়টুকুর সমষ্টি।

<p align="center">
  <img src="./images/response-time.png" alt="Response Time">
</p>

## Section 5: Distributed System

একাধিক কম্পিউটার (বা কম্পোনেন্ট) একসাথে কাজ করার ফলে কোন কাজ শেষ হয় এবং End User এর কাছে একটি কম্পিউটার (বা কম্পোনেন্ট) হিসেবে আসে, সেই সিস্টেমটি হল ডিস্ট্রিবিউটেড সিস্টেম। এই মেশিনগুলোতে শেয়ার্ড স্টেট(Shared State) থাকে, কঙ্কারেন্টলি (Concurrently) কাজ করতে পারে, প্রতিটি সিস্টেম একে অপরের সাথে Information শেয়ার করতে পারবে।

বর্তমান সময়ে Distributed System এর উদাহরণ হল YouTube।

YouTube কেন?

- সার্ভার User থেকে রিকুয়েস্ট পায় Video Upload কিংবা Video Watch করার জন্য।
- ভিডিও এনকোড।
- ডাটাবেস সিস্টেম।

এগুলো সবকিছু মিলে Distributed System YouTube তৈরি করে।

## Section 6: Proxy

ক্লায়েন্ট যখন সার্ভারকে রিকুয়েস্ট পাঠানোর সময় সরাসরি সার্ভারকে রিকুয়েস্ট না করে অন্য একটি সার্ভাররের মাধ্যমে রিকুয়েস্ট করলে, সেই প্রসেস হচ্ছে প্রক্সি এবং যে সার্ভার দিয়ে রিকুয়েস্ট করবে সেটা হচ্ছে প্রক্সি সার্ভার।

বাস্তব জীবনে প্রক্সির একটি উদাহরণ হচ্ছে NGINX।

🔗 [**আরও পড়ুন: প্রক্সি**](./sections/proxy/README.md)

## Section 7: REST Api

রেস্ট এপিআই বুঝার পূর্বে আমাদের বুঝতে হবে রেস্ট(REST) মানে কি, REST মানে হল Representational State Transfer যার মানে দাড়ায় এটি একটি আর্কিটেকচারাল স্টাইল যা ব্যবহার করা হয় স্টেট ট্রান্সফার এর জন্য। এখন REST Api হল, এক প্রকারের এপিআই কনভেনশন যা ব্যবহার করা হয় দুটি এন্ড(যেমনঃ ক্লায়েন্ট এবং সার্ভার) এর মধ্যে স্টেট ট্রান্সফার করাকে নিশ্চিত করার জন্য।

স্টেট ট্রান্সফার নিশ্চিত করতে কিছু স্পেসিফিক HTTP Methods ব্যবহার করা হয়, GET, POST, PUT, PATCH & DELETE, প্রতিটি ম্যাথোডের ব্যবহার জানতে REST Api সেকশনে ক্লিক করুন।

🔗 [**আরও পড়ুন: রেস্ট এপিআই**](./sections/rest-api/README.md)

## Section 8: Scalability

স্কেলেবিলিটি সাধারণত সিস্টেমের ক্ষমতাকে বুঝায় যখন সিস্টেমে ট্রাফিকের পরিমাণ বাড়তে থাকে। উদাহরণ বলা যেতে পারে, একটি ওয়েবসাইটের ডাটাবেসে এখন একটি নির্দিষ্ট পরিমাণ রিকুয়েস্ট করা হচ্ছে কিন্তু আজ থেকে ৫ মাস পর রিকুয়েস্ট ২ গুণ হয়ে গেল তার ঠিক আরও ৫ মাস পর রিকুয়েস্ট ৪ গুণ হয়ে গেল, একটা সময় দেখা যেতে পারে ডাটাবেস সার্ভার এত পরিমাণ রিকুয়েস্ট লোড নিতে পারছে না, এই সমস্যার সমাধানের জন্য স্কেল করাকে স্কেলেবিলিটি বলে।

স্কেলেবিলিটি সাধারণত 2 প্রকারের, ভার্টিকাল স্কেলেবিলিটি (Vertical Scalability) এবং হরাইজন্টাল স্কেলেবিলিটি (Horizontal Scalability)।

🔗 [**আরও পড়ুন: স্কেলেবিলিটি**](./sections/scalability/README.md)

## Section 9: Sharding

Horizontal Scaling কে Sharding বলে। Sharding হল ডেটা পৃথক করা। উদাহরণ বলা যায়, ডাটাবেসের ডেটা যদি বাড়তে থাকে এবং এত পরিমাণ ডেটা Store করার ক্ষমতা যদি ডাটাবেসের না থাকে তখন আরও রিসোর্স (ডাটাবেসের সংখ্যা) বৃদ্ধি করে আমরা ডেটা পৃথক করে রাখি তাহলে সেটাই Sharding।

(বিস্তারিত চলমান)

<p align="center">
  <img src="./images/sharding.png" alt="Sharding">
</p>

## Section 10: Database Replication

Database Replication এক প্রকারের Strategy, যেখানে একটি Master Database এবং একটি কিংবা একাধিক Slave Database থাকবে। Master Database এর মধ্যে Insert, Delete এবং Update এর কাজ হবে এবং Slave Database মধ্যে Master Database এর ডেটাগুলোর Copy থাকবে এবং তার মধ্যে শুধু Read Operation হবে।

<p align="center">
  <img src="./images/DB_replication.png" alt="Database Replication">
</p>

🔗 [**আরও পড়ুন: ডেটাবেস রেপ্লিকেশন**](./sections/db_replication/README.md)

## Section 11: Caching

Caching একটি কৌশল যা দ্বারা কোন Expensive Response'কে কোনো মেমোরিতে রাখা হয়, যাতে বার বার আসা সেই রেস্পন্সের রিকোয়েস্ট কে দ্রুত রেসপন্সটি দিতে পারি। মূল সার্ভারে (যেমন ডাটাবেস) হিট করার পরিবর্তে ক্যাশিং সার্ভারে রিকোয়েস্ট করবে। এতে করে যে সুবিধাটুকু হবে,

- Read API রিকোয়েস্ট Fast হবে
- Latency Reduce হবে
- Fault Tolarence এর ঝুঁকি কমবে

<p align="center">
  <img src="./images/caching1.png" alt="Caching">
</p>

(বিস্তারিত চলমান)

## Section 13: Resources

- <a href="https://github.com/donnemartin/system-design-primer" target="_blank">System Design Primer by Donne Martin (free)</a>
- <a href="https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321" target="_blank">Designing Data Intensive pplications (paid)</a>
- <a href="amazon.com/System-Design-Interview-Insiders-Guide/dp/1736049119" target="_blank">System Design Interview by Alex Xu (paid)</a>
