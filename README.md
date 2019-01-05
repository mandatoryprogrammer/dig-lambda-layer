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
