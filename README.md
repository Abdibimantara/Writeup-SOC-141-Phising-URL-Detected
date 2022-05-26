# Writeup SOC-141 Phising-URL-Detected
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
After knowing the destination address of the tool, we can easily carry out the threat hunting process. Threat hunting process can be started by entering the Log Management menu.

![image](https://user-images.githubusercontent.com/43168046/170480302-3f932251-5184-44e1-9207-2440e1f5b6b8.png)

When we searched by destination address to be accessed, namely 91.189.114.88, we found 2 attempts. where experiments 1 and 2 are loaded on the same source ip. here is the raw log that we managed to get.

![image](https://user-images.githubusercontent.com/43168046/170480947-5e312eff-7d66-47f7-a6cb-937a9a07f83e.png)

![image](https://user-images.githubusercontent.com/43168046/170480972-c62824e0-d885-4909-9f8a-a401344d05de.png)

## The third stage
Based on the information obtained in the log management menu, only ip 172.16.17.49 indicated accessing ip 91.189.114.8. the next step is we have to make sure whether the url is really indicated as phishing and dangerous?.

![image](https://user-images.githubusercontent.com/43168046/170488174-51c93301-5f7b-414e-b681-3ff3b665d14f.png)

### Analysis with Virus Totals
Virus total is a third party tool that is very useful to help investigate whether a file or url link is dangerous.

![image](https://user-images.githubusercontent.com/43168046/170488400-19864e3a-3a2a-432b-b228-653b07abfb85.png)

through virus totals, we can find out that the link is included in phishing. it is supported by bit defender, G-data and Fortinet.

### Analysis with Url Scan
URL scan is a third party tool made by Securitytails. this tool helps us to check whether the url we enter is included in the malicious category or not.

![image](https://user-images.githubusercontent.com/43168046/170490092-b1283553-36fe-47d8-b25e-89f8b4c75efa.png)

![image](https://user-images.githubusercontent.com/43168046/170490167-17950392-cddd-45aa-9a67-bb8d734f594b.png)

![image](https://user-images.githubusercontent.com/43168046/170490408-f32f83d6-10fd-4364-9b34-16d089a509a5.png)

### Analysis with AnyRUN
We try to run the url link in real time. We are using the help of any RUN.
![image](https://user-images.githubusercontent.com/43168046/170491656-c72d6e60-8d7e-4e7d-8881-b60e0dd79592.png)
![image](https://user-images.githubusercontent.com/43168046/170492167-ef421230-9c37-4994-999f-c5bdd3f12bf8.png)
![image](https://user-images.githubusercontent.com/43168046/170492276-afff5ff2-9a9c-477f-b096-0f04e0599e4c.png)

### Analysis with Triage
To ensure analysis, we also apply an online sandbox, namely triage. we tried to use windows x64 and use the firefox user agent to match the results to the alerts generated.

![image](https://user-images.githubusercontent.com/43168046/170492931-0727c459-115c-4b07-972b-95565386d9b5.png)

![image](https://user-images.githubusercontent.com/43168046/170493167-f6245b9f-45c2-4491-841e-5770a3e61039.png)

### Analysis with Hyrbid Analysis
Don't forget, we use sandbox Hybrid Analysis

![image](https://user-images.githubusercontent.com/43168046/170493546-6636f04c-6c67-4d84-b275-a90056b56968.png)
![image](https://user-images.githubusercontent.com/43168046/170493619-8be9d608-eaa0-4988-b54c-3fb8a37e8d3b.png)
![image](https://user-images.githubusercontent.com/43168046/170493696-29e5a128-84d9-4036-be90-ccdc72c271c2.png)

## Answer : The URL is Malicious (Phising)

## The Third Stage
The third step, return to the "Log Management" menu. To check if there are other users trying to access the ip. In addition, we are required to re-collect more detailed information.

![image](https://user-images.githubusercontent.com/43168046/170494331-3052484f-1934-4f24-a5b0-719496e4c247.png)

![image](https://user-images.githubusercontent.com/43168046/170480947-5e312eff-7d66-47f7-a6cb-937a9a07f83e.png)

- When was it accessed ? Mar, 22, 2021, 09:23 PM
- What is the source address ? 172.16.17.4991
- What is the destination address ? 91.189.114.8
- Which users tried to access ? Emily Comp (Ellie)
- What is User Agent ? Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36
- Is the request blocked ? No

## Answer : Accessed

## The Fourth Stage
Because there are users indicated to access the phishing url. we are required to do reuqest containtment

![image](https://user-images.githubusercontent.com/43168046/170502139-9d5e5a5c-4537-4bd9-b2e7-7fc5a11f33b3.png)

![image](https://user-images.githubusercontent.com/43168046/170502157-f1dc0ac8-c676-481f-b262-a53fb205d54a.png)

## The Fourth Stage
After the event analysis has been successfully carried out and the results are obtained. So the event will be closed by the SOC Team by providing a description of the results of the analysis and small notes.

![image](https://user-images.githubusercontent.com/43168046/170502589-e6f2ef90-706a-4f8f-85a4-11b7596ac5f2.png)
![image](https://user-images.githubusercontent.com/43168046/170502991-82cf9a24-941f-4f59-b3b1-7443d20a5fc6.png)
![image](https://user-images.githubusercontent.com/43168046/170503215-02a71664-c868-4c56-bc91-8258f31f7c14.png)





