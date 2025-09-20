- **Time Complexity:** O(1) for both encode and decode methods, on average
- **Space Complexity:** O(N), where N is the number of URLs encoded. We store each URL once.
- **Key Points:**
    - Approach: HashMap with Random and Base62 Encoding
    - Generate random 6 character long unique key using base62 alphanumeric string and put [random key, longUrl] in map
    - Find longUrl by key from map

```java
public class Codec {

    private final String BASE_URL = "http://tinyurl.com/";
    private final HashMap<String, String> map = new HashMap<>();
    private final String characters = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
    private final int KEY_LENGTH = 6;
    private Random rand = new Random();

    // Encodes a URL to a shortened URL.
    public String encode(String longUrl) {
        String key;

        // Generate random 6 character long unique key using base62 alphanumeric string
        do {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < KEY_LENGTH; i++) {
                // pick a char from base62 by random index
                sb.append(characters.charAt(rand.nextInt(characters.length())));
            }

            key = sb.toString();
        } while (map.containsKey(key));

        // Put [random key, longUrl] in map
        map.put(key, longUrl);
        return BASE_URL + key;  
    }

    // Decodes a shortened URL to its original URL.
    public String decode(String shortUrl) {
        // Find longUrl by key from map
        String key = shortUrl.replace(BASE_URL, "");
        return map.get(key);
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(url));
```