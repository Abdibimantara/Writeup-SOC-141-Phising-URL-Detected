# Writeup-SOC-141-Phising-URL-Detected
A simple analysis to solve a SOC problem is "URL phishing". The issue raised is SOC141 - Phishing URL Detected

## Source Link 
https://app.letsdefend.io/

## Third Party Tools Analysis 
Virus Totals : https://www.virustotal.com/gui/home/search
Url Scan : https://urlscan.io/
Anyrun : https://app.any.run/
Hybrid Analysis : https://www.hybrid-analysis.com/sample/f64073d48d8906dce854719776066eae65db4600d34cbac34a7bdff50060f060
Triage : https://tria.ge/

## Details Alert
On March 22, 2021, around 9.23 am. The SOC team again found an alert on the monitoring menu. The alert is "SOC141 - Phishing URL Detected". It is known that source host emily comp is trying to access phishing urls. the alert was detected with id 86 and severity level "high".

![image](https://user-images.githubusercontent.com/43168046/170426156-fae32529-ad99-4321-bc2c-feec33bf5fe5.png)

## The First Stage
After knowing the details of the event, we enter into the analysis process. Starting with the stage of gathering detailed information.

![image](https://user-images.githubusercontent.com/43168046/170426400-e796f7d6-df37-4ee1-862d-ad24daa32589.png)

Through detailed information that has been known from the home monitoring menu,
- Source Address : 172.16.17.49 (Emily Comp)
- Destination Address : 91.189.114.48
- User Agent : Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36

## The Second Stage
After knowing the details of the event, we enter into the analysis process. Starting with the stage of gathering detailed information.

![image](https://user-images.githubusercontent.com/43168046/170426400-e796f7d6-df37-4ee1-862d-ad24daa32589.png)

Through detailed information that has been known from the home monitoring menu,
- Source Address : 172.16.17.49 (Emily Comp)
- Destination Address : 91.189.114.48
- User Agent : Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36
