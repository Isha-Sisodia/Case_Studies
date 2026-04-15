# Zomato System Design – Quick Revision Notes

## Basic Idea

Zomato = 3 parts working together

* User → orders food
* Restaurant → prepares food
* Rider → delivers food

Main challenge:
Everything changes in real-time (traffic, orders, riders)

---

# Core Problems (Simple)

## 1. Search & Ranking

When user searches "pizza"

System checks:

* Distance
* Rating
* Offers
* User preference

Approach:

* Use city database (geo-partitioned)
* Use ML model to rank results

Keyword:
Fast + Personalized

---

## 2. Dispatch Problem

Who will deliver the order?

System decides:

* Nearest rider
* Fastest delivery
* Least workload

Uses:

* Greedy logic
* Batching (one rider, multiple orders)

Keyword:
Optimization problem

---

## 3. Peak Traffic

Example: Dinner time

Problem:

* Too many users at once

Solution:

* Cache data (Redis)
* Use queues
* Disable extra features

Keyword:
System should not crash

---

## 4. Payments

Money must be correct always

Important rules:

* No double payment
* Safe retry
* Keep records

Keyword:
Accuracy > Speed

---

# Important Technologies

* Microservices
* Redis (cache)
* Kafka (events)
* Geo-partitioning
* APIs (maps)

---

# Class Questions – Easy Answers

## Q1: City-wise data but national search?

Answer:

* Store data city-wise
* Create one global search system

So:

* Local → fast
* Global → possible

1-line answer:
Local storage + global index

---

## Q2: How to detect bad dispatch?

Look at:

* More cancellations
* Late deliveries
* Wrong ETA
* User complaints

1-line answer:
ETA error + cancellations increase

---

# Final Short Summary (Quick Revision)

* Zomato = User + Restaurant + Rider
* Main problems:

  * Search
  * Dispatch
  * Traffic
  * Payments
* Uses:

  * Caching, queues, ML
* Success depends on:

  * Speed
  * Accuracy
  * Reliability

---

# System Flow (How Everything Connects)

## Complete Order Flow

### 1. User searches food

* User opens app and searches (e.g., pizza)
* System uses search and ranking
* Looks into **city database (geo-partitioned data)**

### 2. User places order

* User selects items and confirms order
* Order stored in database
* Sent to restaurant service

### 3. Dispatch process

* System assigns a delivery partner
* Based on distance, availability, and time

### 4. Restaurant prepares food

* Restaurant accepts and prepares order
* Status updates are sent to system

### 5. Delivery tracking

* Rider picks up order
* User tracks delivery in real time using maps

### 6. Payment processing

* Payment is processed securely
* System ensures no duplicate transactions

### 7. Order completion

* Food delivered to user
* Order marked as completed

---

# How Components Connect

| Step          | System Component        |
| ------------- | ----------------------- |
| Search        | Search & Ranking        |
| Order         | Database & Services     |
| Dispatch      | Optimization Logic      |
| Tracking      | Maps & Real-time System |
| Payment       | Payment System          |
| Load Handling | Caching & Queues        |

---

# Quick Flow Summary

Search → Order → Dispatch → Delivery → Payment

---

# Memory Trick

S O D D P

* S = Search
* O = Order
* D = Dispatch
* D = Delivery
* P = Payment

---

# Key Understanding

Zomato is not a single system.

It is a combination of multiple systems working together in a pipeline:

Search + Ordering + Dispatch + Delivery + Payment

