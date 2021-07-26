# সিস্টেম ডিজাইন বাংলা

এটি একটি রিপোজিটরি যেখানে সেস্টেম ডিজাইন এর মৌলিক জিনিসগুলো নিয়ে আলোচনা করা হয়েছে।

### সুচিপত্র

<summary><b>সুচিপত্র দেখুন</b></summary>

- [Section 1: System Design](#section-1-system-design)
- [Section 2: Client Server Architecture](#section-2-client-server-architecture)
- [Section 3: Proxy](#section-3-proxy)
- [Section 4: Rest API]
  - [What is Rest API]
  - [Constraints of Rest API]
  - [Request]
  - [Response]
- [Section 5: Scalability]
  - [What is Scalability]
  - [Vertical and Horizontal Scaling]
  - [Advantages of Vertical and Horizontal Scaling]
- [Section 6: Replication]
  - [What is Replication]
  - [Synchronous and Asynchronous Replication]
  - [Advantage of Synchronous Replication]
  - [Advantage of Asynchronous Replication]
- [Section 7: CAP]
  - [What is CAP]
  - [Consistency, Availability & Partitioning in Distributed System]

## Section 1: System Design

আমরা যখন কোন এপ্লিকেশন ডেভেলপ করতে যাই আমাদের একটি নিদিষ্ট প্রকারের ডিজাইন মেনে চলতে হয়, তার কারণ হল আমাদের এপ্লিকেশনে কোন এক সময় থেকে যদি প্রচুর মানুষ ব্যবহার করা শুরু করতে থাকে, তখন আমাদের এপ্লিকেশন যাতে প্রচুর লোড ভালোভাবে নিতে পারে কোন প্রকারের কানেকশন নষ্ট বা পারফরমেন্স ডাউন হওয়া ছাড়া সেজন্য। সেই ডিজাইন কে বলা হয় সিস্টেম ডিজাইন। 

(এই স্পেসিফিক সিস্টেম ডিজাইন মূলত ব্যাকএন্ড ইঞ্জিনিয়ারিং এর সাথে সম্পৃক্ত।) 

## Section 2: Client Server Architecture

ক্লায়েন্ট রিকুয়েস্ট করবে সার্ভারকে কিছু স্পেসিকিফ রিসোর্স এর জন্য, সার্ভার সেই রিকুয়েস্ট পাওয়ার পর সে তার যাবতীয় প্রসেস শেষ করে ক্লায়েন্টকে রেসপন্স দিয়ে দিবে, এটি ক্লায়েন্ট সার্ভার আর্কিটেকচার।

<p align="center">
  <img src="./images/csa.png" alt="Client Server Architecture">
</p>

## Section 3: Proxy

ক্লায়েন্ট যখন সার্ভারকে রিকুয়েস্ট পাঠানোর সময় সরাসরি সার্ভারকে রিকুয়েস্ট না করে অন্য একটি সার্ভাররের মাধ্যমে রিকুয়েস্ট করলে, সেই প্রসেস হচ্ছে প্রক্সি এবং যে সার্ভার দিয়ে রিকুয়েস্ট করবে সেটা হচ্ছে প্রক্সি সার্ভার।

বাস্তব জীবনে প্রক্সির একটি উদাহরণ হচ্ছে NGINX।

🔗 [**আরও পড়ুন: প্রক্সি**](./sections/proxy/README.md)