# xampp-domain-ssl
Add custom domain to XAMPP projects in Localhost and make those are SSL Certified

<h3>1.	Windows Host Edit</h3>
<p>Backup & add entries to <code>C:\Windows\System32\drivers\etc\hosts</code>
<br><code>127.0.0.1       localhost		#For localhost </code><br><code>
  127.0.0.1       akjpro.in		#For new domain(s)</code>
</p>
<h3>2. 	SSL Certificate creation</h3><p>
  Create folder <code>C:\xampp\apache\cert</code> and Download following files in this folder<br>
  &nbsp;&nbsp;&nbsp;&nbsp;<code> i) https://raw.githubusercontent.com/akjpro/xampp-domain-ssl/main/src/cert.conf</code><a href="https://raw.githubusercontent.com/akjpro/xampp-domain-ssl/main/src/cert.conf">Download</a></br>
&nbsp;&nbsp;&nbsp;&nbsp;<code>ii) https://raw.githubusercontent.com/akjpro/xampp-domain-ssl/main/src/make-cert.bat</code><a href="https://raw.githubusercontent.com/akjpro/xampp-domain-ssl/main/src/make-cert.bat">Download</a><br>
Replace <code>{{YOUR DOMAIN NAME}}</code> with your domain name in <code>cert.conf</code> file (Lines : 25 & 51)<br>
Run <code>make-cert.bat</code> by double clicking on it. And when prompt, enter your domain name.</p>
<h3>3.	SSL Certificate Installation</h3>
<p>Double click on the <code>server.crt</code> to install it on Windows. so Windows can trust it.<br>
In prompt, click <code>Install Certificate</code> -> <code>Local Machine</code> -><code> Next</code> -><code> Place all certificate in the following store </code>
-> <code>Browse</code> -> <code>Trusted Root Certification Authorities</code> -> <code>OK</code> -> <code>Next</code> -> <code>Finish</code></p>
<h3>4.	Adding VirtualHost entries </h3>
<p>Backup & add entries to <code>C:\xampp\apache\conf\extra\httpd-vhosts.conf</code> and replace <code>{{YOUR-PROJECT-DIR}}</code> with your project directory & <code>{{YOUR-DOMAIN-NAME}}</code> with your domain name<pre>
NameVirtualHost *:80
#For localhost
&lt;VirtualHost *:80>
    DocumentRoot "c:/xampp/htdocs"
    ServerName localhost
    &lt;Directory  "c:/xampp/htdocs">;
       Require all granted
    &lt;/Directory>
&lt;/VirtualHost>
#For new domain(s)
&lt;VirtualHost *:80>
    DocumentRoot "c:/xampp/htdocs/{{YOUR-PROJECT-DIR}}"
    ServerName {{YOUR-DOMAIN-NAME}}
    &lt;Directory  "c:/xampp/htdocs/{{YOUR-PROJECT-DIR}}">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    &lt;/Directory>
    SSLEngine on 
    SSLCertificateFile "crt/{{YOUR-DOMAIN-NAME}}/server.crt"
    SSLCertificateKeyFile "crt/{{YOUR-DOMAIN-NAME}}/server.key"
  &lt;/VirtualHost></code></pre></p>
<h3>5.	Restrat Apache in Xampp & Browser</h3>
  <p>Open XAMPP Control Panel and Stop and Start Apache Module.</p>
