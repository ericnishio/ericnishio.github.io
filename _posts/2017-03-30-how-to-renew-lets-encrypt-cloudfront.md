---
layout: post
title: How to Renew a Let's Encrypt SSL Certificate on AWS CloudFront
permalink: /blog/renew-lets-encrypt-ssl-certificate-aws-cloudfront/
---

1. Install *certbot* on your Mac by running `brew install certbot`.
2. Begin the certificate renewal process:

```
sudo certbot certonly --manual
```

3. When asked, enter your domain names (e.g. `example.com www.example.com`).
4. Create the verification text files based on the URLs and contents given on the screen, and upload them to S3.
5. Go to Amazon Certificate Manager (https://console.aws.amazon.com/acm/home?region=us-east-1#/).
6. Click **Import a certificate**.
7. View the new certificate data you created earlier:

```
sudo cat /etc/letsencrypt/live/example.com/cert.pem # Certificate body
sudo cat /etc/letsencrypt/live/example.com/privkey.pem # Certificate private key
sudo cat /etc/letsencrypt/live/example.com/fullchain.pem # Certificate chain
```

8. Copy and paste the data into the form and hit **Review and import**.
9. Go to CloudFront (https://console.aws.amazon.com/cloudfront/home?region=us-east-1).
10. Select your Web distribution, and click **Edit**.
11. Under **Custom SSL Certificate**, select the new certificate.
12. Deploy the changes by hitting **Yes, Edit**.
