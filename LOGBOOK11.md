## Task 1

As requested we identified all the components, as can be verified in the screenshots below:

The part of the ca.crt file where it says it is a CA's certificate:

[Logbook 11 - Task 1.1](/screenshots/logbook11-task1-1.png)

The part where it indicates it is self-signed (the issuer and subject are the same):

[Logbook 11 - Task 1.2](/screenshots/logbook11-task1-2.png)

The public and private exponents:

[Logbook 11 - Task 1.3 - Exponents](/screenshots/logbook11-task1-3-exponents.png)

The modulus:

[Logbook 11 - Task 1.3 - Modulus](/screenshots/logbook11-task1-3-modulus.png)

The two secret numbers:

[Logbook 11 - Task 1.3 - Primes](/screenshots/logbook11-task1-3-primes.png)

## Task 2

In this task we chose "fsi2022" for our domain name.

A screenshot of the commands we used to generate a certificate request, that include the alternate hostnames we chose:

[Logbook 11 - Task 2](/screenshots/logbook11-task2-1.png)

## Task 3

Screenshots of the commands used to generate the actual certificate:

[Logbook 11 - Task 3.1](/screenshots/logbook11-task3-1.png)

[Logbook 11 - Task 3.1](/screenshots/logbook11-task3-2.png)

## Task 4

To configure our Apache-based HTTPS website we had to use a slightly different approach from the one given to us in the lab's script. 

First we configured the DNS at /etc/hosts, by adding the following line:

```127.0.0.1 	www.fsi2022.com```

Then we created a folder at /var/www/ for our website and placed an arbitrary html file to serve as our index file. (we used the standard index.html used for apache web servers).

After that we created a directory /ssl in /etc/apache2 to store the public and private keys of the webpage. We copied our server keys into that folder.

Instead of creating a separate VirtualHosts file, we appended the configurations of our website to the default-ssl.conf and 000-default.conf, located at the /etc/apache2/sites-available directory.

Finally we restarted the apache server. The following screenshots show what we observed when we accessed our website:

[Logbook 11 - Task 4.1](/screenshots/logbook11-task4-1.png)

[Logbook 11 - Task 4.2](/screenshots/logbook11-task4-2.png)

When we tried to access the website through the www.fsi2022.com link we were successful, but when we added the https:// prefix, the browser warned us that the website wasn't safe. After adding our Certificate Authority to the list of trusted authorities in our browser, this warning disappeared. As can be seen in the screenshot below:

[Logbook 11 - Task 4.3](/screenshots/logbook11-task4-3.png)

## Task 5

As suggested we configured a public website (we chose a bank's website CGD - Caixa Geral de Depósitos). First we configured DNS, by adding the following line to the /etc/hosts file:

```127.0.0.1 	www.cgd.pt```

And then we repeated the process we did earlier by adding configurations to the default-ssl.conf and 000-default.conf, located at the /etc/apache2/sites-available directory, but this time, using the certificates generated for the fsi2022 server.

When we tried to access the bank's website through the www.cgd.pt link we were successful, however, when we added the https:// prefix we got another security warning. This happened because we were using a certificate generated for our previous website.

[Logbook 11 - Task 5.1](/screenshots/logbook11-task5-1.png)

[Logbook 11 - Task 5.2](/screenshots/logbook11-task5-2.png)

## Task 6

In this task we wanted to remove the security warning we mentioned in the previous task. To do this we generated a custom certificate and key for the www.cgd.pt website. After doing this and altering the configurations to reflect this change, we successfully removed the security warning, as can be seen in the following screenshot:

[Logbook 11 - Task 6](/screenshots/logbook11-task6.png)