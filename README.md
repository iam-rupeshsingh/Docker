PROJECT: Host a Downloaded Website Using Docker (Apache)


Perfect 👍
Here is a CLEAN, END-TO-END MINI PROJECT exactly as you asked — simple, short, no confusion.

I’ll assume:
	•	You are using Amazon EC2
	•	OS = Ubuntu
	•	Website = any free static template (from a template site)

⸻

🔹 PROJECT: Host a Downloaded Website Using Docker (Apache)

⸻

STEP 1️⃣ Download website (on your laptop or EC2)

Download any static website ZIP
(example: free HTML template)

You will get:

website.zip

Upload this ZIP to your EC2 or download directly on EC2.

⸻

STEP 2️⃣ Create project directory on EC2

mkdir docker-website
cd docker-website

Put website.zip inside this folder.

⸻

STEP 3️⃣ Unzip the website

unzip website.zip

Usually it creates something like:

website-template/
 ├── index.html
 ├── css/
 ├── js/
 └── images/


⸻

STEP 4️⃣ Go INSIDE the website folder (VERY IMPORTANT)

cd website-template

👉 index.html must be here, not inside another folder.

⸻

STEP 5️⃣ Create tar.gz (this is what Docker likes)

tar -czvf website.tar.gz *

What this means (SHORT):
	•	c → create
	•	z → gzip compress
	•	v → show files
	•	f → file name

Result:

website.tar.gz


⸻

STEP 6️⃣ Move tar file to project root

mv website.tar.gz ..
cd ..

Now structure:

docker-website/
 ├── website.tar.gz


⸻

STEP 7️⃣ Create Dockerfile

nano Dockerfile

✅ CLEAN Dockerfile (Apache)

FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y apache2

WORKDIR /var/www/html

ADD website.tar.gz /var/www/html

EXPOSE 80

CMD ["apache2ctl", "-D", "FOREGROUND"]


⸻

STEP 8️⃣ What each IMPORTANT thing means (VERY SHORT)

Thing	Meaning
FROM ubuntu	Base OS
apache2	Web server
/var/www/html	Apache website folder
ADD	Copy + auto-extract tar.gz
EXPOSE 80	Website port
-D FOREGROUND	Keep container running


⸻

STEP 9️⃣ Build Docker image

docker build -t my-website .


⸻

STEP 🔟 Run container

docker run -d -p 80:80 my-website

Meaning:
	•	Host port 80
	•	Container port 80

⸻

STEP 1️⃣1️⃣ Open Security Group (EC2)

Allow:
	•	HTTP
	•	Port 80
	•	0.0.0.0/0

⸻

STEP 1️⃣2️⃣ Access website 🌍

Open browser:

http://<EC2-PUBLIC-IP>

🎉 WEBSITE HOSTED SUCCESSFULLY

⸻

🔹 VERY IMPORTANT RULES (REMEMBER)
	1.	index.html must be at root
	2.	Apache serves /var/www/html
	3.	tar.gz is created after cleaning folder
	4.	ADD auto-extracts tar
	5.	FOREGROUND keeps container alive

⸻

🔹 ONE-LINE SUMMARY 🧠

Download → unzip → go inside → tar.gz → Dockerfile → build → run → browser

⸻

If you want next:
	•	Same project using Nginx
	•	Add volume for logs
	•	Convert this into interview explanation
	•	Push image to Docker Hub

Just tell me 👍
