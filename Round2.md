## Question
You are given login events represented as (user_id, timestamp). The events are sorted by timestamp. A user is suspicious if they generate at least K login attempts within any window of T seconds. Return all suspicious users.
Example
events = [
    ("A", 1),
    ("A", 3),
    ("B", 4),
    ("A", 5),
    ("A", 20),
    ("B", 21),
    ("B", 22),
    ("B", 23)
]

K = 3
T = 5

Output:
["A", "B"]

## How I started

I read through the problem and dry ran the given example to make sure I had understood it correctly. After the go ahead, I dry ran a few more cases.

Clarifying question - the input was sorted by timestamp.

## My approach

I went through a few approaches and why they would not work, and then came to this one.

I used a map with the user as key and a vector of that user's timestamps as the value. After populating the map, I iterated over it and ran a sliding window of size K on each user's timestamps. For every window I checked the difference between the last and first element, and if it was within T seconds I marked the user as suspicious.

## Follow up questions

1. **What if the input has 100 million events?**
   I said we can process the events in batches instead of reading all the entries in one go. We can fetch the timestamps for a particualr user in K batches

2. **What if the input is not sorted by timestamp?**
   I said we can sort the input first and then use the same approach. I also mentioned, using a min heap but dedcued that it will be same as of the sliding window approach as in min head also we will have to insert all the elements for once.

## Pseudo Code   

    unordered_map<string, vector<int>> mp;
    vector<string> susUsers;
    
    for(int i=0;i<events.size();i++){
    	mp[events[i][0]].push_back(events[i][1]);
    }
    
    for(auto it: mp){
    	string user = it.first;
      vector<int> timestamp = it.second;
      
      int i=0,j=0;
      
      while(j<timesptamp.size()){
      	if(j-i+1 < k){j++;}
        
        if(timestamp[j] - timestamp[i] + 1 >= T){
        	susUsers.push_back(user);
          break;
        }
      }
    }

