1. How many TCP ports are open on Granny?
First what we need to do is check with nmap what's running on this server.
We can see only one, 80 HTTP

![obraz](https://github.com/Anogota/Granny/assets/143951834/a3eb36c1-d304-4ab3-8ab5-2b19c979fbe4)

2.What is the name of the nmap script that identifies the allowed HTTP methods on Granny?
From previouse scan we see allowed HTTP methods, this is a http-webdav-scan. I don't know what is this exacly, but this is funfact, this is also switch for nmap.

3.Which DOTNET-based web application framework is running on the target web server?
We can use wapalyzer on webpage to indetifa, what's framwework use webpage, and we can see ASP.NET.
ASP.NET is an open source web framework, created by Microsoft, for building modern web apps and services that run on macOS, Linux, Windows, and Docker

![obraz](https://github.com/Anogota/Granny/assets/143951834/9ad75f84-4346-4021-ba14-d44e12eec262)

4.Which HTTP method can be used to upload files onto Granny?
After some recon, i found something intresting i don't use any tools but i recomend devtest, but i have some expirience and i know we can here use HTTP method PUT

5.What is the 2017 CVE ID for a vulnerability that takes advantage of this IIS version and WebDAV, resulting in remote code execution?
i copy paste this IIS WedDAV and i quick found this exploit, on exploit-db this is exploit:

![obraz](https://github.com/Anogota/Granny/assets/143951834/6c32276f-9233-454b-9574-41f34f8efd1d)

6.Which metasploit reconnaissance module can be used to list possible privilege escalation paths on a compromised system?

And also here is a small a description for this exploit
Description:Buffer overflow in the ScStoragePathFromUrl function in the WebDAV service in Internet Information Services (IIS) 6.0 in Microsoft Windows Server 2003 R2 allows remote attackers to execute arbitrary code via a long header beginning with "If: <http://" in a PROPFIND request, as exploited in the wild in July or August 2016.
We can find this exploit also on metasploit, using this command use: windows/iis/iis_webdav_upload_asp with this exploit from metasploit we can get a meterpter then shell, and there we can execute command to see user.txt, we need to trafic into this directory C:\Documents and Settings\Lakis\Desktop

If we want get a right administrator, we need back into the metasploit, but don't kill ur session, then use post/multi/recon/local_exploit_suggester and there can see 5 exploit, the correct one is windows/local/ms14_058_track_popup_menu with this we can get a right administrator and get a administrator flag.
