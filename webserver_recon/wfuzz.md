wfuzz -c -w /usr/share/seclists/Discovery/Web-Content/api/objects.txt -d "token=838e8d8e8ehd8d8u7y6t5r43e2wd1&source=FUZZ" -H "User-Agent: Mozilla/5.1" https://example.com/dirapp/api_data.php
