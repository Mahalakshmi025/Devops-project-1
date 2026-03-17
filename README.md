# Devops-project-1
I download the log fie using

        curl -O https://gist.githubusercontent.com/kamranahmedse/e66c3b9ea89a1a030d3b739eeeef22d0/raw/77fb3ac837a73c4f0206e78a236d885590b7ae35/nginx-access.log
 
 To check the file, I use

         ls  

 To see the total lines, I use

          wc -l nginx-access.log

 Top 5 IP addresses with the most requests, I use

          awk '{print $1}' nginx-access.log |  sort | uniq -c | sort -nr | head -5

                   OR

          grep -o '^[0-9.]*' nginx-access.log | sort | uniq -c | sort -nr | head -5


 Output will be

   1087 178.128.94.113

   1087 142.93.136.176

   1087 138.68.248.85

   1086 159.89.185.30
   
    277 86.134.118.70


 To see top 5 most requested paths, I use

        awk '{print $7}' nginx-access.log | sort | uniq -c | sort -nr | head -5
              
                  OR

        grep -o '"GET [^ ]*' nginx-access.log | sed 's/"GET //' | sort | uniq -c | sort -nr | head -5


 Output will be

   4560 /v1-health
    270 /
    232 /v1-me
    127 /v1-list-workspaces
     75 /v1-list-timezone-teams

 To see Top 5 response codes , I use

 awk '{if($9 ~ /^[0-9]+$/) print $9}' nginx-access.log | sort | uniq -c | sort -nr | head -5

 grep -o '" [0-9][0-9][0-9] ' nginx-access.log | sed 's/ //g' | sort | uniq -c | sort -nr | head -5


 Output will be
   5740 200
    937 404
    621 304
    192 400
     30 166

 
 To see Top 5 user agents, I use

  awk -F\" '{print $6}' nginx-access.log | sort | uniq -c | sort -nr | head -5

  grep -o '"Mozilla[^"]*"' nginx-access.log | sed 's/"//g' | sort | uniq -c | sort -nr | head -5


  output will be 

   4347 DigitalOcean Uptime Probe 0.22.0 (https://digitalocean.com)
    513 Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
    332 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
    294 Custom-AsyncHttpClient
    282 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

 





