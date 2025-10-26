# @elizaos/plugin-pyth-data

## `GET_LATEST_PRICE_UPDATES`

### 1 - "can you give me the BTC price rn"

#### Input
```json
actions: [
  "GET_LATEST_PRICE_UPDATES"
]
thought: User wants the current BTC price. I'll acknowledge and fetch the latest BTC price from Pyth Network.
```
#### Output
```json
{
  "result": "Executing action: GET_LATEST_PRICE_UPDATES",
  "status": "executing",
  "thought": "User wants the current BTC price. I'll acknowledge and fetch the latest BTC price from Pyth Network."
}
```

## `GET_LATEST_PUBLISHER_CAPS`

### 1 - "List all publisher caps"

#### Input
```json
actions: [
  "GET_LATEST_PUBLISHER_CAPS"
]
thought: Confirm request and fetch latest publisher caps from Pyth Network to return the full list; ask if they want any filter if necessary.
```
#### Output
```json
{
  "result": "Action GET_LATEST_PUBLISHER_CAPS completed",
  "status": "completed",
  "thought": "Confirm request and fetch latest publisher caps from Pyth Network to return the full list; ask if they want any filter if necessary."
}
```

## `GET_PRICE_FEEDS`

### 1 - "Show me available forex feeds"

#### Input
```json
actions: [
  "GET_PRICE_FEEDS"
]
thought: Confirm intent and fetch available forex feeds from Pyth; ask whether user wants majors, full list (CSV/JSON), or live snapshot/stream.
```
#### Output
```json
{
  "result": "Action GET_PRICE_FEEDS completed",
  "status": "completed",
  "thought": "Confirm intent and fetch available forex feeds from Pyth; ask whether user wants majors, full list (CSV/JSON), or live snapshot/stream."
}
```

## `GET_PRICE_UPDATES_STREAM`

### 1 - "get the sol/usd price variation every 5s"

#### Input
```json
actions: [
  "GET_PRICE_UPDATES_STREAM"
]
thought: Start a real-time SOL/USD price stream at 5s intervals, compute variation per interval. Ask user whether they want percent or absolute change and how long to run the stream before starting the stream call.
```

#### Output
```json
{
  "result": "Executing action: GET_PRICE_UPDATES_STREAM",
	"status": "executing",
	"thought": "Start a real-time SOL/USD price stream at 5s intervals, compute variation per interval. Ask user whether they want percent or absolute change and how long to run the stream before starting the stream call."
}
```