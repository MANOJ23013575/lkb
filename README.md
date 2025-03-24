# MANOJ
```
Finding the Number of Visible Mountains
```
### program
```
class Solution {
    public int visibleMountains(int[][] peaks) {
        int n = peaks.length;
        int[][] arr = new int[n][2];
        Map<String, Integer> cnt = new HashMap<>();
        for (int i = 0; i < n; ++i) {
            int x = peaks[i][0], y = peaks[i][1];
            arr[i] = new int[] {x - y, x + y};
            cnt.merge((x - y) + "" + (x + y), 1, Integer::sum);
        }
        Arrays.sort(arr, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);
        int ans = 0;
        int cur = Integer.MIN_VALUE;
        for (int[] e : arr) {
            int l = e[0], r = e[1];
            if (r <= cur) {
                continue;
            }
            cur = r;
            if (cnt.get(l + "" + r) == 1) {
                ++ans;
            }
        }
        return ans;
    }
}
```
# RAHUL
```
Number of Excellent Pairs 👍
```
class Solution {
  public long countExcellentPairs(int[] nums, int k) {
    final int MAX_BIT = 30;
    // bits(num1 | num2) + bits(num1 & num2) = bits(num1) + bits(num2)
    long ans = 0;
    long[] count = new long[MAX_BIT];

    for (final int num : Arrays.stream(nums).boxed().collect(Collectors.toSet()))
      ++count[Integer.bitCount(num)];

    for (int i = 0; i < MAX_BIT; ++i)
      for (int j = 0; j < MAX_BIT; ++j)
        if (i + j >= k)
          ans += count[i] * count[j];

    return ans;
  }
}

# JAISRIRAM
```
 Most Popular Video Creator 👎

 class Creator {
  public long popularity; // the popularity sum
  public String videoId;  // the video id that has the maximum view
  public int maxView;     // the maximum view of the creator
  public Creator(long popularity, String videoId, int maxView) {
    this.popularity = popularity;
    this.videoId = videoId;
    this.maxView = maxView;
  }
}

class Solution {
  public List<List<String>> mostPopularCreator(String[] creators, String[] ids, int[] views) {
    List<List<String>> ans = new ArrayList<>();
    Map<String, Creator> nameToCreator = new HashMap<>();
    long maxPopularity = 0;

    for (int i = 0; i < creators.length; ++i) {
      if (!nameToCreator.containsKey(creators[i])) {
        nameToCreator.put(creators[i], new Creator(views[i], ids[i], views[i]));
        maxPopularity = Math.max(maxPopularity, (long) views[i]);
        continue;
      }
      Creator creator = nameToCreator.get(creators[i]);
      creator.popularity += views[i];
      maxPopularity = Math.max(maxPopularity, (long) creator.popularity);
      if (creator.maxView < views[i] ||
          creator.maxView == views[i] && creator.videoId.compareTo(ids[i]) > 0) {
        creator.videoId = ids[i];
        creator.maxView = views[i];
      }
    }

    for (Map.Entry<String, Creator> entry : nameToCreator.entrySet())
      if (entry.getValue().popularity == maxPopularity)
        ans.add(Arrays.asList(entry.getKey(), entry.getValue().videoId));

    return ans;
  }
}


