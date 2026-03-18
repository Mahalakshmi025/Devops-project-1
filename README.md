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
          
          awk '{a[i]++} END{(for i in a) {print a[i], i}}' nginx-access.log | sort -nr | head -5

                   OR

          grep -o '^[0-9.]*' nginx-access.log | sort | uniq -c | sort -nr | head -5


 Output will be

   1087 178.128.94.113

   1087 142.93.136.176

   1087 138.68.248.85

   1086 159.89.185.30
   
    277 86.134.118.70


 To see top 5 most requested paths, I use

        awk -F'"' '{print $2}' nginx-access.log | cut -d' ' -f2 | cut -d'?' -f1 | sort | uniq -c | sort -nr | head -5
              
                  OR

        grep -o '"[A-Z]\+ [^ ]*' nginx-access.log | sed 's/"[A-Z]\+ //' | cut -d'?' -f1 | sort | uniq -c | sort -nr | head -5


 Output will be

   4560 /v1-health
    283 /
    232 /v1-me
    127 /v1-list-workspaces
     82 /v1-list-all-tasks/66ffec2665c85844abd1b6a1


 To see Top 5 response codes , I use

        awk -F '"' '{print $3}' nginx-access.log | awk '{if($1 ~ /^[0-9]{3}$/) print $1}' | sort | uniq -c | sort -nr | head -5

                    OR

        grep -o '" [0-9]\{3\} ' nginx-access.log | sed 's/" \([0-9]\{3\}\) /\1/' | sort | uniq -c | sort -nr | head -5


 Output will be
   5740 200
    937 404
    621 304
    260 400
     23 403

 
 To see Top 5 user agents, I use

        awk 'match($0, /"[^"]*"$/) { ua = substr($0, RSTART+1, RLENGTH-2); print ua }' nginx-access.log | sort | uniq -c | sort -nr | head -5

                   OR

         grep -o '"Mozilla[^"]*"' nginx-access.log | sed 's/"//g' | sort | uniq -c | sort -nr | head -5

  output will be 

    4347 DigitalOcean Uptime Probe 0.22.0 (https://digitalocean.com)
    513 Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
    332 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36
    294 Custom-AsyncHttpClient
    282 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36

 





