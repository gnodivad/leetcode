# 0359. Logger Rate Limiter

## Approach 1: HashMap
Use a HashMap to keep the incoming `message` and the `timestamp` when the message is received. Everytime, we just check in HashMap when there are an incoming message. If the message is never see before, then we put the message into HashMap with the timestamp together. Otherwise, we need to confirm that the elapsed time between current message and previous message is more than 10 seconds.

```Java
class Logger {
    private HashMap<String, Integer> map;
    /** Initialize your data structure here. */
    public Logger() {
        map = new HashMap<>();
    }
    
    /** Returns true if the message should be printed in the given timestamp, otherwise returns false.
        If this method returns false, the message will not be printed.
        The timestamp is in seconds granularity. */
    public boolean shouldPrintMessage(int timestamp, String message) {
        if (!map.containsKey(message)) {
            map.put(message, timestamp);
            return true;
        }
        
        int previousTimestamp = map.get(message);
        if (timestamp - previousTimestamp >= 10) {
            map.put(message, timestamp);
            return true;
        }
        
        return false;
    }
}

/**
 * Your Logger object will be instantiated and called as such:
 * Logger obj = new Logger();
 * boolean param_1 = obj.shouldPrintMessage(timestamp,message);
 */
```

### Time and Space Complexity

N = number of unique incoming message
- Time: `O(1)`
- Space: `O(N)`
