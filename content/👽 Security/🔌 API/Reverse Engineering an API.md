Tags: #api #reverse-enginerring
Related to: #hacking 
See also: 
Index: [[🗂️ Index of API Hacking]] 

- If no documentation = I have to build my own
- 2 Methods discussed
	- Using postman to collect requests and build a collection manually - tedious but good to know
	- Automatically do it using mitmproxy2swagger

#### **Building a Collection in Postman**

-  2 ways to make collection in postman
	- construct each request - cumbersome - but u can focus on endpoints you care about
	- Proxy web traffic through postman, capture stream of requests and remove unwanted ones

Refer this - https://university.apisec.ai/products/apisec-certified-expert/categories/2150251353/posts/2157921175

#### **Automatic documentation using mitmweb and mitmproxy2swagger**

- Run mitmweb
- set proxy to proxy port
- on browser go to locahost port 8081
- you can see your requests
- Save them after you have explored the app
- it will be saved as flows file
- `sudo mitmproxy2swagger -i /Downloads/flows -o spec.yml -p [http://crapi.apisec.ai](http://crapi.apisec.ai/) -f flow` - Run this to convert to yml file
- Update the YAML file so that "ignore:" is removed from the endpoints that you want to include. Once you have edited the file it should look something similar to the image below. Note that the "title" has been updated to "crAPI Swagger" and that the endpoints no longer contain "ignore:".
-  Save the updated spec.yml file and run the mitmproxy2swagger again. This time around add the "--examples" flag to enhance your API documentation
- Validate the documentation using https://editor.swagger.io/
- You can import yml file into postman and create a collection