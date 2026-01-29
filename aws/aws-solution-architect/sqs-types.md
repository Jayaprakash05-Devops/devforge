# AWS SQS Queue Types and Patterns

This document explains common **Amazon SQS queue types, configurations, and usage patterns**, with simple examples for each. These are frequently tested in AWS exams and widely used in real-world architectures.

---

## 1. Standard Queue

**Description**
- Default SQS queue type
- Nearly unlimited throughput
- At-least-once delivery
- Messages may be delivered out of order
- Duplicate messages are possible

**Use Case**
- High-throughput, best-effort ordering workloads

**Example**
- Collecting application logs or user activity events

---

## 2. FIFO Queue

**Description**
- First-In-First-Out message delivery
- Exactly-once processing
- Maintains message order
- Requires `MessageGroupId`
- Lower throughput compared to Standard queues

**Use Case**
- Workflows requiring strict ordering and no duplicates

**Example**
- Processing financial transactions or inventory updates

---

## 3. Dead-Letter Queue (DLQ)

**Description**
- A separate SQS queue for messages that fail processing
- Configured using a redrive policy
- Messages are moved after exceeding `maxReceiveCount`

**Use Case**
- Isolating failed or "poison pill" messages for debugging

**Example**
- Order processing message fails 5 times and is sent to DLQ

---

## 4. Delay Queue

**Description**
- Delays delivery of all messages in the queue (0–15 minutes)
- Delay can also be set per message

**Use Case**
- Deferred or retry-based processing

**Example**
- Retry payment processing after a 5-minute delay

---

## 5. Temporary Queue (Ephemeral Pattern)

**Description**
- Not an official SQS queue type
- Short-lived queue created and deleted dynamically
- Used for one-time or session-based workflows

**Use Case**
- Temporary batch jobs or request-response patterns

**Example**
- Create a queue for a batch job, process messages, then delete it

---

## 6. Visibility Timeout

**Description**
- Time period during which a received message is hidden
- Prevents multiple consumers from processing the same message
- Message becomes visible again if not deleted in time

**Use Case**
- Ensuring safe message processing

**Example**
- Image processing takes 2 minutes → visibility timeout set to 3 minutes

---

## 7. Redrive Policy (Retry Pattern)

**Description**
- Defines how many times a message can be retried
- Works in conjunction with a Dead-Letter Queue

**Use Case**
- Controlled retry and failure handling

**Example**
- Retry message 3 times before moving it to DLQ

---

## 8. Message Deduplication (FIFO Only)

**Description**
- Prevents duplicate messages within a 5-minute window
- Uses a deduplication ID or content-based deduplication

**Use Case**
- Exactly-once message delivery

**Example**
- Same order ID sent twice is processed only once

---

## 9. Long Polling

**Description**
- Consumers wait for messages instead of frequent polling
- Reduces empty responses and cost
- Configurable up to 20 seconds

**Use Case**
- Cost-efficient and scalable message consumption

**Example**
- Worker waits up to 20 seconds for messages to arrive

---

## 10. Fan-Out Pattern (SNS + SQS)

**Description**
- SNS topic publishes messages to multiple SQS queues
- Each queue has independent consumers

**Use Case**
- Decoupling multiple downstream services

**Example**
- Order placed → billing, inventory, and email services process it independently

---

## Summary

| Feature / Pattern | Purpose |
|------------------|--------|
| Standard Queue | High throughput, unordered processing |
| FIFO Queue | Ordered, exactly-once processing |
| Dead-Letter Queue | Capture failed messages |
| Delay Queue | Deferred message delivery |
| Temporary Queue | Short-lived workloads |
| Visibility Timeout | Prevent concurrent processing |
| Long Polling | Reduce cost and empty polls |
| SNS Fan-Out | Broadcast messages to multiple consumers |

---

## References
- AWS Documentation: Amazon Simple Queue Service (SQS)
