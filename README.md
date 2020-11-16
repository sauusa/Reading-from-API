# Reading-from-API

Reading data from API, making connection to End Point using Python

### API Status Codes:

    200: Everything went okay, and the result has been returned (if any).
    
    301: The server is redirecting you to a different endpoint. 
         This can happen when a company switches domain names, or an endpoint name is changed.
    
    400: The server thinks you made a bad request. This can happen when you don’t send along the right data, 
         among other things.
    
    401: The server thinks you’re not authenticated. Many APIs require login ccredentials, so this happens 
         when you don’t send the right credentials to access an API.
    
    403: The resource you’re trying to access is forbidden: you don’t have the right permissions to see it.
    
    404: The resource you tried to access wasn’t found on the server.
    
    503: The server is not ready to handle the request.

### Connect to API using Get Request:

   import requests

   #Get access key from fixer.io, after subsription and replace it here:

   url = "http://data.fixer.io/api/latest?access_key=?????????????????????"

   response = requests.get(url)

   print(response.status_code)

   response.json()
   
### Read specific data set

   import requests

   url = "http://data.fixer.io/api/latest?access_key=c7ccf53a014674baa6f92a63ee62b6eb&base=EUR&symbols=USD,GBP,CAD,INR"

   response = requests.get(url)

   response.json()

### Perform a function or Store json values in variable

   import json

   data = response.text

   parsed = json.loads(data)

   e_cad = parsed["rates"]["CAD"]
   e_inr = parsed["rates"]["INR"]

   c_base = 1 / e_cad
   c_inr  = c_base * e_inr

   print("1 CAD = {} INR".format(c_inr))
   
### Using pandas

   import pandas as pd
   import json

   df = pd.DataFrame(json.loads(response.text))
   print(df) 
