# ActivityWatch API Notes

## 1. ActivityWatch Local API

Base URL:

http://localhost:5600

ActivityWatch provides a local REST API that can be accessed from a browser, curl, Postman, or Python requests.

---

## 2. List All Buckets

API:

GET http://localhost:5600/api/0/buckets

Purpose:

Returns all ActivityWatch buckets available on the local system.

Buckets identified during testing:

- aw-watcher-window_RAVI
- aw-watcher-afk_RAVI

---

## 3. Window Watcher

Bucket:

aw-watcher-window_RAVI

API:

GET http://localhost:5600/api/0/buckets/aw-watcher-window_RAVI/events

Purpose:

Returns application and window activity events.

Sample event:

{
    "id": 21,
    "timestamp": "2026-10-08T09:42:14.690000+00:00",
    "duration": 1.043,
    "data": {
        "app": "chrome.exe",
        "title": "localhost:5600/api/0/buckets/ - Google Chrome"
    }
}

### Window Event Schema

- id: Unique event identifier
- timestamp: Event start time
- duration: Duration of the event in seconds
- data.app: Application name
- data.title: Window or browser title

---

## 4. AFK Watcher

Bucket:

aw-watcher-afk_RAVI

API:

GET http://localhost:5600/api/0/buckets/aw-watcher-afk_RAVI/events

Purpose:

Tracks whether the computer is active or idle.

Possible status values observed:

- not-afk
- afk

Example:

{
    "id": 33,
    "timestamp": "2026-10-08T09:44:09.995000+00:00",
    "duration": 862.319,
    "data": {
        "status": "afk"
    }
}

The AFK bucket will later be used to exclude idle periods from developer focus calculations.

---

## 5. Query Events by Time Range

ActivityWatch supports querying events for a selected time range.

Example:

GET http://localhost:5600/api/0/buckets/aw-watcher-window_RAVI/events?start=2026-10-08T09:00:00+00:00&end=2026-10-08T10:00:00+00:00

Purpose:

Returns window-watcher events between the specified start and end times.

The same approach can be used with the AFK bucket.

---

## 6. Useful API Endpoints

### List buckets

GET /api/0/buckets

### Get window events

GET /api/0/buckets/aw-watcher-window_RAVI/events

### Get AFK events

GET /api/0/buckets/aw-watcher-afk_RAVI/events

### Get events for a time range

GET /api/0/buckets/aw-watcher-window_RAVI/events?start=<START_TIME>&end=<END_TIME>

---

## 7. Day 11 Findings

ActivityWatch was successfully accessed through its local REST API.

The following buckets were identified:

1. aw-watcher-window_RAVI
2. aw-watcher-afk_RAVI

Window events provide application, window title, timestamp, and duration information.

AFK events provide the user's active or idle status.

The collected information will be used in Day 12 to calculate developer focus time while excluding idle periods.