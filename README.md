Copyright 2011 Rodolfo Wilhelmy

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

---

A Google Reader API façade for Adobe Air.
=

Supports:
-  
* Secure authentication (No OAuth yet).  
* Subscriptions management.  
* Tagging items.

TODO
-
1. User interface as a PoC.  
2. Unit testing.  
3. onRequestSuccess/onRequestError should return "result" object with more info.  
4. Find a better way to handle error messages (such as a dictionary).  
5. Handle CAPTCHA requirements.  

References
-
* http://code.google.com/p/pyrfeed/wiki/GoogleReaderAPI  
* http://anirudhs.chaosnet.org/blog/2009.11.04.html  
* http://blog.martindoms.com/2009/08/15/using-the-google-reader-api-part-1/  

---

Usage
-

**Initialize and setup listeners**

	var reader:GoogleReader = new GoogleReader();
	reader.onRequestSuccess = reqSuccess;
	reader.onRequestError = reqError;

**Authentication**

	"OK" = reader.authenticate("koolaid@gmail.com", "ohyeah!", "myAuthCallback");

**Get user's RSS subscriptions**
	
	{
	  "subscriptions":[
	    {
	      "id":"feed/http://rss.cnn.com/rss/cnn_topstories.rss",
	      "title":"CNN.com - Breaking News, ...",
	      "categories":[],
	      "sortid":"FF1EEAB5",
	      "firstitemmsec":"1308122816904"
	    },
	    {
	      "id":"feed/http://feedproxy.google.com/TechCrunch",
	      "title":"TechCrunch",
	      "categories":[
	        {
	          "id":"user/35397781436425093193/label/Tech",
	          "label":"Tech"
	        }
	      ],
	      "sortid":"53F9A2C3",
	      "firstitemmsec":"1308146223866"
	    }
	  ]
	} = reader.getSubscriptions("mySubsCallback");

**User information**

	{
	  "userId":"26397781466425093193",
	  "userName":"KoolAid",
	  "userProfileId":"219036081246954240029",
	  "userEmail":"koolaid@gmail.com",
	  "isBloggerUser":false,
	  "signupTimeSec":0,
	  "isMultiLoginEnabled":false
	} = reader.getUser("myUserCallback");

**Get subscription's items**

	reader.getItemsForFeed("feed/http://feedproxy.google.com/TechCrunch", 10, "myItemsCallback");

