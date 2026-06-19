# 🎉 Event RSVP – AWS Full-Stack Tutorial

A simple AWS-powered app that lists events, shows details & stats, and accepts RSVPs.  

---

## 🧱 Architecture Overview

**Frontend → API Gateway → Lambda → MySQL + DynamoDB → S3 + CloudFront**

---

## 📁 Project Structure

```
.
├── index.html           # Main UI
├── style.css            # Styling
├── app.js               # Entry script (loads events)
├── events.js            # Event logic + modal + RSVP
├── utils.js             # API helpers & formatters
├── index.js             # Lambda backend handler
├── database-notes.txt   # SQL Commands
├── package.json
├── package-lock.json
└── .gitignore
```

---

## 🚀 Guide

### Backend (Lambda)

Set these **environment variables** in your Lambda configuration. Feel free to customize:

| Variable | Example | Description |
|-----------|----------|-------------|
| REGION | ap-south-1 | AWS region |
| DB_HOST | event-rsvp-db.xxxxxx.ap-south-1.rds.amazonaws.com | MySQL host |
| DB_USER | admin | MySQL user |
| DB_PASS | ******** | MySQL password |
| DB_NAME | eventsdb | MySQL database |

---

### API Summary

| Method | Path | Purpose |
|---------|------|----------|
| GET | `/events` | Fetch all events |
| GET | `/event/{event_id}` | Fetch single event |
| GET | `/stats/{event_id}` | Get RSVP counts |
| GET | `/attendees/{event_id}` | Get attendee list |
| POST | `/rsvp` | Submit RSVP |

Make sure **CORS** is set up properly.

---

### Hosting (S3 + CloudFront)

1. Upload all frontend files (`index.html`, `.css`, `.js`) to your S3 bucket.  
2. Create a **CloudFront distribution** pointing to that bucket.  
3. Set **Default Root Object** to `index.html`.

---

## 🔁 Making Frontend Changes

When you update your HTML, CSS, or JS and upload to S3, CloudFront might still serve old cached files.

## CloudFront Invalidation (Console)

1. Go to **CloudFront → your distribution → Invalidations → Create invalidation**  
2. Enter:
   ```
   /*
   ```
   This clears the entire cache.
3. Wait for the status to show **Completed**.  
4. Go back to your site and **hard refresh**:  
   - **Windows:** `Ctrl + F5`  
   - **Mac:** `Cmd + Shift + R`  
   - *(then refresh ✨)*

---
