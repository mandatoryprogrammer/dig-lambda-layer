# Lambda `dig` Layer

Adds support for the awesome DNS tool `dig` to your Lambda function.

Install it by going to your AWS console, navigation to `Lambda`, followed by `Layers`, `Create layer`, upload this zip and use the ARN in your Lambda function.

```
START RequestId: b7abb31c-10a2-11e9-859c-b9daa8e62050 Version: $LATEST

; <<>> DiG 9.8.2rc1-RedHat-9.8.2-0.68.rc1.58.amzn1 <<>> NS com. @a.gtld-servers.net.
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39470
;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 12
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;com.				IN	NS

;; ANSWER SECTION:
com.			172800	IN	NS	l.gtld-servers.net.
com.			172800	IN	NS	d.gtld-servers.net.
com.			172800	IN	NS	h.gtld-servers.net.
com.			172800	IN	NS	m.gtld-servers.net.
com.			172800	IN	NS	i.gtld-servers.net.
com.			172800	IN	NS	b.gtld-servers.net.
com.			172800	IN	NS	e.gtld-servers.net.
com.			172800	IN	NS	f.gtld-servers.net.
com.			172800	IN	NS	g.gtld-servers.net.
com.			172800	IN	NS	a.gtld-servers.net.
com.			172800	IN	NS	j.gtld-servers.net.
com.			172800	IN	NS	k.gtld-servers.net.
com.			172800	IN	NS	c.gtld-servers.net.

;; ADDITIONAL SECTION:
l.gtld-servers.net.	172800	IN	A	192.41.162.30
l.gtld-servers.net.	172800	IN	AAAA	2001:500:d937::30
d.gtld-servers.net.	172800	IN	A	192.31.80.30
d.gtld-servers.net.	172800	IN	AAAA	2001:500:856e::30
h.gtld-servers.net.	172800	IN	A	192.54.112.30
h.gtld-servers.net.	172800	IN	AAAA	2001:502:8cc::30
m.gtld-servers.net.	172800	IN	A	192.55.83.30
m.gtld-servers.net.	172800	IN	AAAA	2001:501:b1f9::30
i.gtld-servers.net.	172800	IN	A	192.43.172.30
i.gtld-servers.net.	172800	IN	AAAA	2001:503:39c1::30
b.gtld-servers.net.	172800	IN	A	192.33.14.30
b.gtld-servers.net.	172800	IN	AAAA	2001:503:231d::2:30

;; Query time: 10 msec
;; SERVER: 192.5.6.30#53(192.5.6.30)
;; WHEN: Sat Jan  5 04:31:06 2019
;; MSG SIZE  rcvd: 509



END RequestId: b7abb31c-10a2-11e9-859c-b9daa8e62050
REPORT RequestId: b7abb31c-10a2-11e9-859c-b9daa8e62050	Duration: 1206.05 ms	Billed Duration: 1300 ms 	Memory Size: 128 MB	Max Memory Used: 35 MB	
```

---

## Building a new version

Please see the (AWS guide to create a deployment package](https://aws.amazon.com/premiumsupport/knowledge-center/lambda-linux-binary-package/). The following steps are tailored to `dig`.

1. Launch an Amazon EC2 instance from the Amazon Linux AMI
1. Connect to the instance, and then install tools to extract the packages:
    - `sudo yum install -y yum-utils rpmdevtools`
1. Download and extract the libraries and the dependencies:
    - `cd /tmp`
    - `yumdownloader bind-utils.x86_64`
    - `rpmdev-extract *rpm`
1. Copy the libraries into a directory for the Lambda deployment package:
    - `sudo mkdir -p /var/task`
    - `sudo chown ec2-user:ec2-user /var/task`
    - `cd /var/task`
    - `/bin/cp /tmp/bind-utils-9.8.2-0.68.rc1.59.amzn1.x86_64/usr/* /var/task -R` _(note: replace `bind-utils-9.8.2-0.68.rc1.59.amzn1.x86_64` with the respective directory name)_
1. Copy all dependencies into the Lambda deployment package:
    - `mkdir /var/task/lib`
    - Get a list of all dependencies - `ldd /usr/bin/dig`
    - Copy each of the listed dependencies into your deployment package lib folder: eg. `sudo /bin/cp /usr/lib64/liblwres.so.80 /var/task/lib/liblwres.so.80`
1. Create a deployment package ZIP:
    - `cd /var/task`
    - `zip -r9 /tmp/dig-layer.zip *`
1. Download a copy of `dig-layer.zip` (eg. via SFTP) and upload as a new layer in your Lambda console
