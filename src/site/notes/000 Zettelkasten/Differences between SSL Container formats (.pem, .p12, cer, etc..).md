---
{"dg-publish":true,"permalink":"/000-zettelkasten/differences-between-ssl-container-formats-pem-p12-cer-etc/","tags":["type/note, topic/information-security,"],"noteIcon":""}
---


# Differences Between SSL Container Formats (.pem, .p12, Cer, etc..)

SSL has been around for a long time and there are a few different standards and container formats to encode [[X.509\|X.509]] Certs.  
But in essence these container formats are only different in terms of how much data is packed inside and how the data is encoded. Data is either encoded in BASE64 ASCII or Binary. 

## Requesting a Certificate

## .csr

- The Certificate Signing Request is the file that gets generated when you want to request a [[X.509\|X.509]] certificate. The file gets sent to a Certificate Authority. Below you can find some information that is 
- contents of the file ([[000 Zettelkasten/Krypto ist verwirrend, aber glücklicherweise hat es jemand durchnummiert - Eine PKCS Übersicht\|PKCS]] in ASN.1 format) includes information like 

- like CNAME, is in the file that is sent to an certificate authority. The actual format is PKCS10. The CSR contains the data for the requested certificate  
 like subject name, state and so on. Also the the public key of the certificate to be signed. The CA then returns the public certificate with the public key but not the private key

| DN[1]  | Information          | Description                                                                                                  | Sample                     |
|--------|----------------------|--------------------------------------------------------------------------------------------------------------|----------------------------|
| CN     | Common Name          | This is fully qualified domain name that you wish to secure                                                  | \*.wikipedia.org           |
| O      | Organization Name    | Usually the legal name of a company or entity and should include any suffixes such as Ltd., Inc., or Corp.   | Wikimedia Foundation, Inc. |
| OU     | Organizational Unit  | Internal organization department/division name                                                               | IT                         |
| L      | Locality             | Town, city, village, etc. name                                                                               | San Francisco              |
| ST     | State                | Province, region, county or state. This should not be abbreviated (e.g. West Sussex, Normandy, New Jersey).  | California                 |
| C      | Country              | The two-letter ISO code for the country where your organization is located                                   | US                         |
| EMAIL  | Email Address        | The organization contact, usually of the certificate administrator or IT department                          |

# Pem

- Name: Privacy Enhanced Email
- File extension: .pem
- .pem is a BASE64 ASCII Encoded Text file 
	- Includes plain text file headers 
		- `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`
- Unencrypted container format that can include
	- Private keys
	- Public key 
	- Complete certificate chain 
	- even CSR could be included

## Example

```ad-example
title: The SSL/TLS certificate for www.ssl.com is shown below in PEM format
collapse: closed
```-----BEGIN CERTIFICATE-----
MIIH/TCCBeWgAwIBAgIQaBYE3/M08XHYCnNVmcFBcjANBgkqhkiG9w0BAQsFADBy
MQswCQYDVQQGEwJVUzEOMAwGA1UECAwFVGV4YXMxEDAOBgNVBAcMB0hvdXN0b24x
ETAPBgNVBAoMCFNTTCBDb3JwMS4wLAYDVQQDDCVTU0wuY29tIEVWIFNTTCBJbnRl
cm1lZGlhdGUgQ0EgUlNBIFIzMB4XDTIwMDQwMTAwNTgzM1oXDTIxMDcxNjAwNTgz
M1owgb0xCzAJBgNVBAYTAlVTMQ4wDAYDVQQIDAVUZXhhczEQMA4GA1UEBwwHSG91
c3RvbjERMA8GA1UECgwIU1NMIENvcnAxFjAUBgNVBAUTDU5WMjAwODE2MTQyNDMx
FDASBgNVBAMMC3d3dy5zc2wuY29tMR0wGwYDVQQPDBRQcml2YXRlIE9yZ2FuaXph
dGlvbjEXMBUGCysGAQQBgjc8AgECDAZOZXZhZGExEzARBgsrBgEEAYI3PAIBAxMC
VVMwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDHheRkbb1FCc7xRKst
wK0JIGaKY8t7JbS2bQ2b6YIJDgnHuIYHqBrCUV79oelikkokRkFvcvpaKinFHDQH
UpWEI6RUERYmSCg3O8Wi42uOcV2B5ZabmXCkwdxY5Ecl51BbM8UnGdoAGbdNmiRm
SmTjcs+lhMxg4fFY6lBpiEVFiGUjGRR+61R67Lz6U4KJeLNcCm07QwFYKBmpi08g
dygSvRdUw55Jopredj+VGtjUkB4hFT4GQX/ght69Rlqz/+8u0dEQkhuUuucrqalm
SGy43HRwBfDKFwYeWM7CPMd5e/dO+t08t8PbjzVTTv5hQDCsEYIV2T7AFI9ScNxM
kh7/AgMBAAGjggNBMIIDPTAfBgNVHSMEGDAWgBS/wVqH/yj6QT39t0/kHa+gYVgp
vTB/BggrBgEFBQcBAQRzMHEwTQYIKwYBBQUHMAKGQWh0dHA6Ly93d3cuc3NsLmNv
bS9yZXBvc2l0b3J5L1NTTGNvbS1TdWJDQS1FVi1TU0wtUlNBLTQwOTYtUjMuY3J0
MCAGCCsGAQUFBzABhhRodHRwOi8vb2NzcHMuc3NsLmNvbTAfBgNVHREEGDAWggt3
d3cuc3NsLmNvbYIHc3NsLmNvbTBfBgNVHSAEWDBWMAcGBWeBDAEBMA0GCyqEaAGG
9ncCBQEBMDwGDCsGAQQBgqkwAQMBBDAsMCoGCCsGAQUFBwIBFh5odHRwczovL3d3
dy5zc2wuY29tL3JlcG9zaXRvcnkwHQYDVR0lBBYwFAYIKwYBBQUHAwIGCCsGAQUF
BwMBMEgGA1UdHwRBMD8wPaA7oDmGN2h0dHA6Ly9jcmxzLnNzbC5jb20vU1NMY29t
LVN1YkNBLUVWLVNTTC1SU0EtNDA5Ni1SMy5jcmwwHQYDVR0OBBYEFADAFUIazw5r
ZIHapnRxIUnpw+GLMA4GA1UdDwEB/wQEAwIFoDCCAX0GCisGAQQB1nkCBAIEggFt
BIIBaQFnAHcA9lyUL9F3MCIUVBgIMJRWjuNNExkzv98MLyALzE7xZOMAAAFxM0ho
bwAABAMASDBGAiEA6xeliNR8Gk/63pYdnS/vOx/CjptEMEv89WWh1/urWIECIQDy
BreHU25DzwukQaRQjwW655ZLkqCnxbxQWRiOemj9JAB1AJQgvB6O1Y1siHMfgosi
LA3R2k1ebE+UPWHbTi9YTaLCAAABcTNIaNwAAAQDAEYwRAIgGRE4wzabNRdD8kq/
vFP3tQe2hm0x5nXulowh4Ibw3lkCIFYb/3lSDplS7AcR4r+XpWtEKSTFWJmNCRbc
XJur2RGBAHUA7sCV7o1yZA+S48O5G8cSo2lqCXtLahoUOOZHssvtxfkAAAFxM0ho
8wAABAMARjBEAiB6IvboWss3R4ItVwjebl7D3yoFaX0NDh2dWhhgwCxrHwIgCfq7
ocMC5t+1ji5M5xaLmPC4I+WX3I/ARkWSyiO7IQcwDQYJKoZIhvcNAQELBQADggIB
ACeuur4QnujqmguSrHU3mhf+cJodzTQNqo4tde+PD1/eFdYAELu8xF+0At7xJiPY
i5RKwilyP56v+3iY2T9lw7S8TJ041VLhaIKp14MzSUzRyeoOAsJ7QADMClHKUDlH
UU2pNuo88Y6igovT3bsnwJNiEQNqymSSYhktw0taduoqjqXn06gsVioWTVDXysd5
qEx4t6sIgIcMm26YH1vJpCQEhKpc2y07gRkklBZRtMjThv4cXyyMX7uTcdT7AJBP
ueifCoV25JxXuo8d5139gwP1BAe7IBVPx2u7KN/UyOXdZmwMf/TmFGwDdCfsyHf/
ZsB2wLHozTYoAVmQ9FoU1JLgcVivqJ+vNlBhHXhlxMdN0j80R9Nz6EIglQjeK3O8
I/cFGm/B8+42hOlCId9ZdtndJcRJVji0wD0qwevCafA9jJlHv/jsE+I9Uz6cpCyh
sw+lrFdxUgqU58axqeK89FR+No4q0IIO+Ji1rJKr9nkSB0BqXozVnE1YB/KLvdIs
uYZJuqb2pKku+zzT6gUwHUTZvBiNOtXL4Nxwc/KT7WzOSd2wP10QI8DKg4vfiNDs
HWmB1c4Kji6gOgA5uSUzaGmq/v4VncK5Ur+n9LbfnfLc28J5ft/GotinMyDk3iar
F10YlqcOmeX1uFmKbdi/XorGlkCoMF3TDx8rmp9DBiB/
-----END CERTIFICATE-----```
```

# .PKCS12

- Name: Public-Key Cryptography Standards
- File extension: `.p12`, `.PKCS12` or `.pfx`
- Binary Format for storing certificate chain and private key in a encrypted single file
- Apart from the encryption very similar to .pem 

# .key

  - Kein offizielles Format nur Community Standards, um Keys abzuspeichern

# .der

- DER (Distinguished Encoding Rules) is way to encode ASN.1 syntax in binary
- Unlike .pem comes without a plaintext header 
- .der and .pem are basically the same just different encodings 
	- .der (binary)
	- .pem (BASE64 ASCII)
- Commonly found in java applications 

## Example

```ad-example
title: The SSL/TLS certificate for www.ssl.com is shown below in DER format
collapse: closed
```-----BEGIN CERTIFICATE-----
3082 07fd 3082 05e5 a003 0201 0202 1068
1604 dff3 34f1 71d8 0a73 5599 c141 7230
0d06 092a 8648 86f7 0d01 010b 0500 3072
310b 3009 0603 5504 0613 0255 5331 0e30
0c06 0355 0408 0c05 5465 7861 7331 1030
0e06 0355 0407 0c07 486f 7573 746f 6e31
1130 0f06 0355 040a 0c08 5353 4c20 436f
7270 312e 302c 0603 5504 030c 2553 534c
2e63 6f6d 2045 5620 5353 4c20 496e 7465
726d 6564 6961 7465 2043 4120 5253 4120
5233 301e 170d 3230 3034 3031 3030 3538
3333 5a17 0d32 3130 3731 3630 3035 3833
335a 3081 bd31 0b30 0906 0355 0406 1302
5553 310e 300c 0603 5504 080c 0554 6578
6173 3110 300e 0603 5504 070c 0748 6f75
7374 6f6e 3111 300f 0603 5504 0a0c 0853
534c 2043 6f72 7031 1630 1406 0355 0405
130d 4e56 3230 3038 3136 3134 3234 3331
1430 1206 0355 0403 0c0b 7777 772e 7373
6c2e 636f 6d31 1d30 1b06 0355 040f 0c14
5072 6976 6174 6520 4f72 6761 6e69 7a61
7469 6f6e 3117 3015 060b 2b06 0104 0182
373c 0201 020c 064e 6576 6164 6131 1330
1106 0b2b 0601 0401 8237 3c02 0103 1302
5553 3082 0122 300d 0609 2a86 4886 f70d
0101 0105 0003 8201 0f00 3082 010a 0282
0101 00c7 85e4 646d bd45 09ce f144 ab2d
c0ad 0920 668a 63cb 7b25 b4b6 6d0d 9be9
8209 0e09 c7b8 8607 a81a c251 5efd a1e9
6292 4a24 4641 6f72 fa5a 2a29 c51c 3407
5295 8423 a454 1116 2648 2837 3bc5 a2e3
6b8e 715d 81e5 969b 9970 a4c1 dc58 e447
25e7 505b 33c5 2719 da00 19b7 4d9a 2466
4a64 e372 cfa5 84cc 60e1 f158 ea50 6988
4545 8865 2319 147e eb54 7aec bcfa 5382
8978 b35c 0a6d 3b43 0158 2819 a98b 4f20
7728 12bd 1754 c39e 49a2 9ade 763f 951a
d8d4 901e 2115 3e06 417f e086 debd 465a
b3ff ef2e d1d1 1092 1b94 bae7 2ba9 a966
486c b8dc 7470 05f0 ca17 061e 58ce c23c
c779 7bf7 4efa dd3c b7c3 db8f 3553 4efe
6140 30ac 1182 15d9 3ec0 148f 5270 dc4c
921e ff02 0301 0001 a382 0341 3082 033d
301f 0603 551d 2304 1830 1680 14bf c15a
87ff 28fa 413d fdb7 4fe4 1daf a061 5829
bd30 7f06 082b 0601 0505 0701 0104 7330
7130 4d06 082b 0601 0505 0730 0286 4168
7474 703a 2f2f 7777 772e 7373 6c2e 636f
6d2f 7265 706f 7369 746f 7279 2f53 534c
636f 6d2d 5375 6243 412d 4556 2d53 534c
2d52 5341 2d34 3039 362d 5233 2e63 7274
3020 0608 2b06 0105 0507 3001 8614 6874
7470 3a2f 2f6f 6373 7073 2e73 736c 2e63
6f6d 301f 0603 551d 1104 1830 1682 0b77
7777 2e73 736c 2e63 6f6d 8207 7373 6c2e
636f 6d30 5f06 0355 1d20 0458 3056 3007
0605 6781 0c01 0130 0d06 0b2a 8468 0186
f677 0205 0101 303c 060c 2b06 0104 0182
a930 0103 0104 302c 302a 0608 2b06 0105
0507 0201 161e 6874 7470 733a 2f2f 7777
772e 7373 6c2e 636f 6d2f 7265 706f 7369
746f 7279 301d 0603 551d 2504 1630 1406
082b 0601 0505 0703 0206 082b 0601 0505
0703 0130 4806 0355 1d1f 0441 303f 303d
a03b a039 8637 6874 7470 3a2f 2f63 726c
732e 7373 6c2e 636f 6d2f 5353 4c63 6f6d
2d53 7562 4341 2d45 562d 5353 4c2d 5253
412d 3430 3936 2d52 332e 6372 6c30 1d06
0355 1d0e 0416 0414 00c0 1542 1acf 0e6b
6481 daa6 7471 2149 e9c3 e18b 300e 0603
551d 0f01 01ff 0404 0302 05a0 3082 017d
060a 2b06 0104 01d6 7902 0402 0482 016d
0482 0169 0167 0077 00f6 5c94 2fd1 7730
2214 5418 0830 9456 8ee3 4d13 1933 bfdf
0c2f 200b cc4e f164 e300 0001 7133 4868
6f00 0004 0300 4830 4602 2100 eb17 a588
d47c 1a4f fade 961d 9d2f ef3b 1fc2 8e9b
4430 4bfc f565 a1d7 fbab 5881 0221 00f2
06b7 8753 6e43 cf0b a441 a450 8f05 bae7
964b 92a0 a7c5 bc50 5918 8e7a 68fd 2400
7500 9420 bc1e 8ed5 8d6c 8873 1f82 8b22
2c0d d1da 4d5e 6c4f 943d 61db 4e2f 584d
a2c2 0000 0171 3348 68dc 0000 0403 0046
3044 0220 1911 38c3 369b 3517 43f2 4abf
bc53 f7b5 07b6 866d 31e6 75ee 968c 21e0
86f0 de59 0220 561b ff79 520e 9952 ec07
11e2 bf97 a56b 4429 24c5 5899 8d09 16dc
5c9b abd9 1181 0075 00ee c095 ee8d 7264
0f92 e3c3 b91b c712 a369 6a09 7b4b 6a1a
1438 e647 b2cb edc5 f900 0001 7133 4868
f300 0004 0300 4630 4402 207a 22f6 e85a
cb37 4782 2d57 08de 6e5e c3df 2a05 697d
0d0e 1d9d 5a18 60c0 2c6b 1f02 2009 fabb
a1c3 02e6 dfb5 8e2e 4ce7 168b 98f0 b823
e597 dc8f c046 4592 ca23 bb21 0730 0d06
092a 8648 86f7 0d01 010b 0500 0382 0201
0027 aeba be10 9ee8 ea9a 0b92 ac75 379a
17fe 709a 1dcd 340d aa8e 2d75 ef8f 0f5f
de15 d600 10bb bcc4 5fb4 02de f126 23d8
8b94 4ac2 2972 3f9e affb 7898 d93f 65c3
b4bc 4c9d 38d5 52e1 6882 a9d7 8333 494c
d1c9 ea0e 02c2 7b40 00cc 0a51 ca50 3947
514d a936 ea3c f18e a282 8bd3 ddbb 27c0
9362 1103 6aca 6492 6219 2dc3 4b5a 76ea
2a8e a5e7 d3a8 2c56 2a16 4d50 d7ca c779
a84c 78b7 ab08 8087 0c9b 6e98 1f5b c9a4
2404 84aa 5cdb 2d3b 8119 2494 1651 b4c8
d386 fe1c 5f2c 8c5f bb93 71d4 fb00 904f
b9e8 9f0a 8576 e49c 57ba 8f1d e75d fd83
03f5 0407 bb20 154f c76b bb28 dfd4 c8e5
dd66 6c0c 7ff4 e614 6c03 7427 ecc8 77ff
66c0 76c0 b1e8 cd36 2801 5990 f45a 14d4
92e0 7158 afa8 9faf 3650 611d 7865 c4c7
4dd2 3f34 47d3 73e8 4220 9508 de2b 73bc
23f7 051a 6fc1 f3ee 3684 e942 21df 5976
d9dd 25c4 4956 38b4 c03d 2ac1 ebc2 69f0
3d8c 9947 bff8 ec13 e23d 533e 9ca4 2ca1
b30f a5ac 5771 520a 94e7 c6b1 a9e2 bcf4
547e 368e 2ad0 820e f898 b5ac 92ab f679
1207 406a 5e8c d59c 4d58 07f2 8bbd d22c
b986 49ba a6f6 a4a9 2efb 3cd3 ea05 301d
44d9 bc18 8d3a d5cb e0dc 7073 f293 ed6c
ce49 ddb0 3f5d 1023 c0ca 838b df88 d0ec
1d69 81d5 ce0a 8e2e a03a 0039 b925 3368
69aa fefe 159d c2b9 52bf a7f4 b6df 9df2
dcdb c279 7edf c6a2 d8a7 3320 e4de 26ab
175d 1896 a70e 99e5 f5b8 598a 6dd8 bf5e
8ac6 9640 a830 5dd3 0f1f 2b9a 9f43 0620
7f
-----END CERTIFICATE-----``` 
```

# Common Conversion Commands

## View Contents of DER-encoded Certificate File

openssl x509 -inform der -in CERTIFICATE.der -text -noout

Convert .der file to .pem 

```shell
openssl x509 -inform der -in to-convert.der -out converted.pem
```

# .cert, .cer And .crt

- .crt files are normally formated like .pem files 
	- rarley like .der (binary) files
- Windows Explorer recognizes this file extension unlike .pem. 

- **.p7b .keystore** - Defined in [RFC 2315](https://www.rfc-editor.org/rfc/rfc2315) as PKCS number 7, this is a format used by Windows for certificate interchange. Java understands these natively, and often uses `.keystore` as an extension instead. Unlike .pem style certificates, this format has a _defined_ way to include certification-path certificates.

- **.crl** - A certificate revocation list. Certificate Authorities produce these as a way to de-authorize certificates before expiration. You can sometimes download them from CA websites.