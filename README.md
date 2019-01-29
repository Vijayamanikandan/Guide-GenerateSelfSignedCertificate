1.Generate an RSA private key:
>C:\Openssl\bin\openssl.exe genrsa -out <Key Filename> <Key Size>
Where:
<Key Filename> is the desired filename for the private key file
<Key Size> is the desired key length of either 1024, 2048, or 4096
For example, type:
>C:\Openssl\bin\openssl.exe genrsa -out my_key.key 2048.
2. Generate a Certificate Signing Request:
In version 0.9.8h and later:
>C:\Openssl\bin\openssl.exe req -new -key <Key Filename> -out <Request Filename> -config C:\Openssl\bin\openssl.cfg
Where:
<Key Filename> is the input filename of the previously generated private key
<Request Filename> is the output filename of the certificate signing request
For example, type:
>C:\Openssl\bin\openssl.exe req -new -key my_key.key -out my_request.csr -config C:\Openssl\bin\openssl.cnf
3. Follow the on-screen prompts for the required certificate request information.
4. Generate a self-signed public certificate based on the request:
>C:\Openssl\bin\openssl.exe x509 -req -days 3650 -in <Request Filename> -signkey <Key Filename> -out <Certificate Filename>
Where:
<Request Filename> is the input filename of the certificate signing request
<Key Filename> is the input filename of the previously generated private key
<Certificate Filename> is the output filename of the public certificate
For example, type:
>C:\Openssl\bin\openssl.exe x509 -req -days 3650 -in my_request.csr -signkey my_key.key -out my_cert.crt
5. Generate a PKCS#12 file:
>C:\Openssl\bin\openssl.exe pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in <Public Certificate Filename> -inkey <Private Key Filename> -out <PKCS#12 Filename> -name "<Display Name>"
Where:
<Public Certificate Filename> is the input filename of the public certificate, in PEM format
<Private Key Filename> is the input filename of the private key
<PKCS#12 Filename> is the output filename of the pkcs#12 format file
<Display Name> is the desired name that will sometimes be displayed in user interfaces.
For example, type:
>C:\Openssl\bin\openssl.exe pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in my_cert.crt -inkey my_key.key -out my_pkcs12.pfx -name "my-name"
6. (Optional) Delete unneeded files.
At this point, you only need the PKCS#12 format file, so you can delete the certificate signing request (.csr) file, the private key (.key) file, and the public certificate (.crt) file.
The resulting PKCS#12 format file may now be used within Secure FTP Server - FIPS.
The resulting PKCS#12 format (.pfx) file may now be used with the Firefox browser ver 34.0.5.
