## Solve certificate issue such as:


##### sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path

I was getting below error and fixed it by installing the certificate:


```
[ERROR] Non-resolvable import POM: Could not transfer artifact org.alfresco:alfresco-platform-distribution:pom:5.2.4 from/to alfresco-private (https://artifacts.alfresco.com/nexus/content/groups/private/): sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target @ line 168, column 16 -> [Help 2]
```


Java program written by Andreas Sterbenz, and posted on a blog in Oct, 2006:
https://blogs.oracle.com/gc/entry/unable_to_find_valid_certification


#### Follow the steps given below:

- Clone the project and navigate to source directory

- Compile InstallCert.java class

```java
javac InstallCert.java
```

- Run the InstallCert java code:

```java
java InstallCert artifacts.alfresco.com:443

```

- You would get following output: 


```java
- When asked "Enter certificate to add to trusted keystore or 'q' to quit: [1]" on command prompt, press 1 or just press enter

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Loading KeyStore C:\Program Files\Java\jdk1.8.0_211\jre\lib\security\cacerts...
Opening connection to artifacts.alfresco.com:443...
Starting SSL handshake...

No errors, certificate is already trusted

Server sent 3 certificate(s):

 1 Subject CN=*.alfresco.com, O=Alfresco Software Ltd., L=Maidenhead, C=GB
   Issuer  CN=DigiCert SHA2 High Assurance Server CA, OU=www.digicert.com, O=DigiCert Inc, C=US
   sha1    45 ba d9 c5 ab a4 47 15 86 54 40 75 86 75 f5 50 22 65 fe d0 
   md5     3c b6 4d aa cb 9c 91 40 a6 cd 81 37 31 d0 05 92 

 2 Subject CN=*.alfresco.com, O=Alfresco Software Ltd., L=Maidenhead, C=GB
   Issuer  CN=DigiCert SHA2 High Assurance Server CA, OU=www.digicert.com, O=DigiCert Inc, C=US
   sha1    45 ba d9 c5 ab a4 47 15 86 54 40 75 86 75 f5 50 22 65 fe d0 
   md5     3c b6 4d aa cb 9c 91 40 a6 cd 81 37 31 d0 05 92 

 3 Subject CN=DigiCert SHA2 High Assurance Server CA, OU=www.digicert.com, O=DigiCert Inc, C=US
   Issuer  CN=DigiCert High Assurance EV Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US
   sha1    a0 31 c4 67 82 e6 e6 c6 62 c2 c8 7c 76 da 9a a6 2c ca bd 8e 
   md5     aa ee 5c f8 b0 d8 59 6d 2e 0c be 67 42 1c f7 db 

Enter certificate to add to trusted keystore or 'q' to quit: [1]


[
[
  Version: V3
  Subject: CN=*.alfresco.com, O=Alfresco Software Ltd., L=Maidenhead, C=GB
  Signature Algorithm: SHA256withRSA, OID = 1.2.840.113549.1.1.11

  Key:  Sun RSA public key, 4096 bits
  modulus: 787948961842385986612811387400787768661733576390349128668324128156507677598700480733234740334472887358099641362625283202609569788279319491153825738000769149235115951123538387845511537598203296085927267328964408628183255712448147620282978929326904437253278405834746130308750179366339591563737693202305201733317851798179943391004722951919889342515261757298864998745120724512463855423348845733838878545511311998135283086478131750737209901039481549221363467960257657588582709449589026527710302554029328429271500725552544526528260169782056935781553756119400936781888508758907047356340364260623149584571912155621492380709361676154810103772631524321221303769582702810622655640249226882994526832346119491535102294907390496391101003671672285446735757855965578517937746115847758639433602242437071407141864616330744391720437958480843919154090650466402330532874054846867699726021743397866019584578398332070817692712819463148350763042601602128416390251175054859057371404377075327858082180055879836982039482044412138423902462880716643536806366606613723876317477784622655740269026286777364219490353151338206737025916940144183178942001724014614608825651923435852733440753282642074741802461853907856973563915144641401753435948942880042094394846388141
  public exponent: 65537
  Validity: [From: Thu Sep 13 20:00:00 EDT 2018,
               To: Fri Sep 18 08:00:00 EDT 2020]
  Issuer: CN=DigiCert SHA2 High Assurance Server CA, OU=www.digicert.com, O=DigiCert Inc, C=US
  SerialNumber: [    040b1cf3 cc0d6629 4fff2fb8 5e951bd6]

Certificate Extensions: 10
[1]: ObjectId: 1.3.6.1.4.1.11129.2.4.2 Criticality=false
Extension unknown: DER encoded OCTET string =
0000: 04 82 01 6D 04 82 01 69   01 67 00 76 00 A4 B9 09  ...m...i.g.v....
0010: 90 B4 18 58 14 87 BB 13   A2 CC 67 70 0A 3C 35 98  ...X......gp.<5.
0020: 04 F9 1B DF B8 E3 77 CD   0E C8 0D DC 10 00 00 01  ......w.........
0030: 65 D8 A0 11 3A 00 00 04   03 00 47 30 45 02 20 71  e...:.....G0E. q
0040: 35 78 BE D9 91 F0 C7 BC   A4 F6 81 3E D7 7F E4 B5  5x.........>....
0050: 12 74 67 7B 8A BE 74 B0   B2 08 E7 11 F3 6C D0 02  .tg...t......l..
0060: 21 00 F8 87 9D 65 E7 67   9C 9A F1 A9 A7 DF C7 ED  !....e.g........
0070: 5B D6 C2 BF 65 33 88 44   D3 F7 8A 89 5D 62 51 1C  [...e3.D....]bQ.
0080: 3C 70 00 76 00 87 75 BF   E7 59 7C F8 8C 43 99 5F  <p.v..u..Y...C._
0090: BD F3 6E FF 56 8D 47 56   36 FF 4A B5 60 C1 B4 EA  ..n.V.GV6.J.`...
00A0: FF 5E A0 83 0F 00 00 01   65 D8 A0 11 79 00 00 04  .^......e...y...
00B0: 03 00 47 30 45 02 21 00   C1 3E 21 15 8C 4A 6C 2E  ..G0E.!..>!..Jl.
00C0: 0C 21 41 1A A6 7C 3F A5   1C 06 7E 80 24 20 60 AF  .!A...?.....$ `.
00D0: C6 7D BE DD 50 22 F4 F7   02 20 7D 92 66 E2 5A 4B  ....P"... ..f.ZK
00E0: A3 41 E2 9E 5B 8F 2E 4B   87 34 ED D5 00 B0 C2 8A  .A..[..K.4......
00F0: CF 1D 3C 9C 52 F1 CB 14   35 70 00 75 00 BB D9 DF  ..<.R...5p.u....
0100: BC 1F 8A 71 B5 93 94 23   97 AA 92 7B 47 38 57 95  ...q...#....G8W.
0110: 0A AB 52 E8 1A 90 96 64   36 8E 1E D1 85 00 00 01  ..R....d6.......
0120: 65 D8 A0 10 B4 00 00 04   03 00 46 30 44 02 20 5D  e.........F0D. ]
0130: 14 45 A1 28 1C 88 47 DF   41 9A C0 B0 95 24 52 7A  .E.(..G.A....$Rz
0140: 9B 2C AF 69 57 D6 ED 2F   29 D2 3E 04 FD 64 D0 02  .,.iW../).>..d..
0150: 20 77 DC 8C D7 95 7D 8A   35 CD 2A BC CF F8 1C 4C   w......5.*....L
0160: 5C 11 0F 57 75 EA 2D C9   DC CC 08 1E B4 08 EF 57  \..Wu.-........W
0170: 72                                                 r


[2]: ObjectId: 1.3.6.1.5.5.7.1.1 Criticality=false
AuthorityInfoAccess [
  [
   accessMethod: ocsp
   accessLocation: URIName: http://ocsp.digicert.com
, 
   accessMethod: caIssuers
   accessLocation: URIName: http://cacerts.digicert.com/DigiCertSHA2HighAssuranceServerCA.crt
]
]

[3]: ObjectId: 2.5.29.35 Criticality=false
AuthorityKeyIdentifier [
KeyIdentifier [
0000: 51 68 FF 90 AF 02 07 75   3C CC D9 65 64 62 A2 12  Qh.....u<..edb..
0010: B8 59 72 3B                                        .Yr;
]
]

[4]: ObjectId: 2.5.29.19 Criticality=true
BasicConstraints:[
  CA:false
  PathLen: undefined
]

[5]: ObjectId: 2.5.29.31 Criticality=false
CRLDistributionPoints [
  [DistributionPoint:
     [URIName: http://crl3.digicert.com/sha2-ha-server-g6.crl]
, DistributionPoint:
     [URIName: http://crl4.digicert.com/sha2-ha-server-g6.crl]
]]

[6]: ObjectId: 2.5.29.32 Criticality=false
CertificatePolicies [
  [CertificatePolicyId: [2.16.840.1.114412.1.1]
[PolicyQualifierInfo: [
  qualifierID: 1.3.6.1.5.5.7.2.1
  qualifier: 0000: 16 1C 68 74 74 70 73 3A   2F 2F 77 77 77 2E 64 69  ..https://www.di
0010: 67 69 63 65 72 74 2E 63   6F 6D 2F 43 50 53        gicert.com/CPS

]]  ]
  [CertificatePolicyId: [2.23.140.1.2.2]
[]  ]
]

[7]: ObjectId: 2.5.29.37 Criticality=false
ExtendedKeyUsages [
  serverAuth
  clientAuth
]

[8]: ObjectId: 2.5.29.15 Criticality=true
KeyUsage [
  DigitalSignature
  Key_Encipherment
]

[9]: ObjectId: 2.5.29.17 Criticality=false
SubjectAlternativeName [
  DNSName: *.alfresco.com
  DNSName: alfresco.com
]

[10]: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: BB E0 77 89 79 BF DE 41   F6 B5 61 0F 0F DE DE FB  ..w.y..A..a.....
0010: 1B A8 03 44                                        ...D
]
]

]
  Algorithm: [SHA256withRSA]
  Signature:
0000: 6E 5F 56 13 54 12 0D 3F   E7 20 3E 5A 74 5F 35 BC  n_V.T..?. >Zt_5.
0010: B4 18 54 93 6C 55 1A B4   20 A0 B6 F3 4A 62 0E 6C  ..T.lU.. ...Jb.l
0020: D7 75 D4 A5 82 EE 9F AB   48 0D 57 F1 8B 33 B5 3B  .u......H.W..3.;
0030: FC 72 8B E4 92 45 05 C8   17 31 4C BF E2 4B 5E 72  .r...E...1L..K^r
0040: 15 D1 B0 18 EE 00 81 96   70 BB 09 32 13 6C 02 0B  ........p..2.l..
0050: C6 31 FC 4D 98 AA FF 31   AE E2 A0 DF DB B5 A1 40  .1.M...1.......@
0060: F7 42 26 70 09 7B 65 CB   1C C9 CC EB 9E A8 B0 2B  .B&p..e........+
0070: 77 7E 53 06 68 18 6E C0   FB 06 3A F3 AC 7D 19 5D  w.S.h.n...:....]
0080: 4D B4 C5 4E 3C 0F 7C 61   C5 0A 55 2E 08 1D 4F 7B  M..N<..a..U...O.
0090: 2A 54 A0 3F B2 3A 69 B1   20 62 BE 48 62 31 F0 71  *T.?.:i. b.Hb1.q
00A0: 0E A3 47 7F 4A F0 4F 40   B3 92 4A 5F 30 8D 0E 46  ..G.J.O@..J_0..F
00B0: D9 C9 62 85 11 FE AC 96   B8 5D 72 B9 86 BF 17 E2  ..b......]r.....
00C0: 27 91 91 92 0F 04 62 AE   0F 9C A3 A6 C0 2E 4E 37  '.....b.......N7
00D0: E4 BF D9 94 71 AA 6B 37   0C E2 3D 73 F1 D3 97 47  ....q.k7..=s...G
00E0: D6 4F 58 1E 30 B0 55 AA   27 48 4B 3D 20 BB B0 35  .OX.0.U.'HK= ..5
00F0: 77 B4 F5 5F DF D0 9C 18   B4 9C D0 32 98 1F 45 C5  w.._.......2..E.

]

Added certificate to keystore 'jssecacerts' using alias 'artifacts.alfresco.com-1'

```

- Open command promot and type 'keytool' to open java keytool and run following command:

```java
keytool -exportcert -alias artifacts.alfresco.com-1 -keystore jssecacerts -storepass changeit -file artifacts.alfresco.com.cer

```

- You will get following output:

```java
Certificate stored in file <artifacts.alfresco.com.cer>
```

- Open command promot and type 'keytool' to open java keytool again and run following command:

```java
keytool -importcert -alias artifacts.alfresco.com -keystore "C:\Program Files\Java\jdk1.8.0_211\jre\lib\security\cacerts" -storepass changeit -file artifacts.alfresco.com.cer
```

- You will get following output:

```java
Owner: CN=*.alfresco.com, O=Alfresco Software Ltd., L=Maidenhead, C=GB
Issuer: CN=DigiCert SHA2 High Assurance Server CA, OU=www.digicert.com, O=DigiCert Inc, C=US
Serial number: 40b1cf3cc0d66294fff2fb85e951bd6
Valid from: Thu Sep 13 20:00:00 EDT 2018 until: Fri Sep 18 08:00:00 EDT 2020
Certificate fingerprints:
         SHA1: 45:BA:D9:C5:AB:A4:47:15:86:54:40:75:86:75:F5:50:22:65:FE:D0
         SHA256: F9:0A:34:EC:AD:C8:DE:25:78:A6:1A:F8:AB:20:0B:5B:DF:BB:1C:58:C7:41:61:08:77:D3:FD:AA:EA:E3:4D:F4
Signature algorithm name: SHA256withRSA
Subject Public Key Algorithm: 4096-bit RSA key
Version: 3

Extensions:

#1: ObjectId: 1.3.6.1.4.1.11129.2.4.2 Criticality=false
0000: 04 82 01 69 01 67 00 76   00 A4 B9 09 90 B4 18 58  ...i.g.v.......X
0010: 14 87 BB 13 A2 CC 67 70   0A 3C 35 98 04 F9 1B DF  ......gp.<5.....
0020: B8 E3 77 CD 0E C8 0D DC   10 00 00 01 65 D8 A0 11  ..w.........e...
0030: 3A 00 00 04 03 00 47 30   45 02 20 71 35 78 BE D9  :.....G0E. q5x..
0040: 91 F0 C7 BC A4 F6 81 3E   D7 7F E4 B5 12 74 67 7B  .......>.....tg.
0050: 8A BE 74 B0 B2 08 E7 11   F3 6C D0 02 21 00 F8 87  ..t......l..!...
0060: 9D 65 E7 67 9C 9A F1 A9   A7 DF C7 ED 5B D6 C2 BF  .e.g........[...
0070: 65 33 88 44 D3 F7 8A 89   5D 62 51 1C 3C 70 00 76  e3.D....]bQ.<p.v
0080: 00 87 75 BF E7 59 7C F8   8C 43 99 5F BD F3 6E FF  ..u..Y...C._..n.
0090: 56 8D 47 56 36 FF 4A B5   60 C1 B4 EA FF 5E A0 83  V.GV6.J.`....^..
00A0: 0F 00 00 01 65 D8 A0 11   79 00 00 04 03 00 47 30  ....e...y.....G0
00B0: 45 02 21 00 C1 3E 21 15   8C 4A 6C 2E 0C 21 41 1A  E.!..>!..Jl..!A.
00C0: A6 7C 3F A5 1C 06 7E 80   24 20 60 AF C6 7D BE DD  ..?.....$ `.....
00D0: 50 22 F4 F7 02 20 7D 92   66 E2 5A 4B A3 41 E2 9E  P"... ..f.ZK.A..
00E0: 5B 8F 2E 4B 87 34 ED D5   00 B0 C2 8A CF 1D 3C 9C  [..K.4........<.
00F0: 52 F1 CB 14 35 70 00 75   00 BB D9 DF BC 1F 8A 71  R...5p.u.......q
0100: B5 93 94 23 97 AA 92 7B   47 38 57 95 0A AB 52 E8  ...#....G8W...R.
0110: 1A 90 96 64 36 8E 1E D1   85 00 00 01 65 D8 A0 10  ...d6.......e...
0120: B4 00 00 04 03 00 46 30   44 02 20 5D 14 45 A1 28  ......F0D. ].E.(
0130: 1C 88 47 DF 41 9A C0 B0   95 24 52 7A 9B 2C AF 69  ..G.A....$Rz.,.i
0140: 57 D6 ED 2F 29 D2 3E 04   FD 64 D0 02 20 77 DC 8C  W../).>..d.. w..
0150: D7 95 7D 8A 35 CD 2A BC   CF F8 1C 4C 5C 11 0F 57  ....5.*....L\..W
0160: 75 EA 2D C9 DC CC 08 1E   B4 08 EF 57 72           u.-........Wr


#2: ObjectId: 1.3.6.1.5.5.7.1.1 Criticality=false
AuthorityInfoAccess [
  [
   accessMethod: ocsp
   accessLocation: URIName: http://ocsp.digicert.com
,
   accessMethod: caIssuers
   accessLocation: URIName: http://cacerts.digicert.com/DigiCertSHA2HighAssuranceServerCA.crt
]
]

#3: ObjectId: 2.5.29.35 Criticality=false
AuthorityKeyIdentifier [
KeyIdentifier [
0000: 51 68 FF 90 AF 02 07 75   3C CC D9 65 64 62 A2 12  Qh.....u<..edb..
0010: B8 59 72 3B                                        .Yr;
]
]

#4: ObjectId: 2.5.29.19 Criticality=true
BasicConstraints:[
  CA:false
  PathLen: undefined
]

#5: ObjectId: 2.5.29.31 Criticality=false
CRLDistributionPoints [
  [DistributionPoint:
     [URIName: http://crl3.digicert.com/sha2-ha-server-g6.crl]
, DistributionPoint:
     [URIName: http://crl4.digicert.com/sha2-ha-server-g6.crl]
]]

#6: ObjectId: 2.5.29.32 Criticality=false
CertificatePolicies [
  [CertificatePolicyId: [2.16.840.1.114412.1.1]
[PolicyQualifierInfo: [
  qualifierID: 1.3.6.1.5.5.7.2.1
  qualifier: 0000: 16 1C 68 74 74 70 73 3A   2F 2F 77 77 77 2E 64 69  ..https://www.di
0010: 67 69 63 65 72 74 2E 63   6F 6D 2F 43 50 53        gicert.com/CPS

]]  ]
  [CertificatePolicyId: [2.23.140.1.2.2]
[]  ]
]

#7: ObjectId: 2.5.29.37 Criticality=false
ExtendedKeyUsages [
  serverAuth
  clientAuth
]

#8: ObjectId: 2.5.29.15 Criticality=true
KeyUsage [
  DigitalSignature
  Key_Encipherment
]

#9: ObjectId: 2.5.29.17 Criticality=false
SubjectAlternativeName [
  DNSName: *.alfresco.com
  DNSName: alfresco.com
]

#10: ObjectId: 2.5.29.14 Criticality=false
SubjectKeyIdentifier [
KeyIdentifier [
0000: BB E0 77 89 79 BF DE 41   F6 B5 61 0F 0F DE DE FB  ..w.y..A..a.....
0010: 1B A8 03 44                                        ...D
]
]

Trust this certificate? [no]:
```

- Type 'yes' to install the certificate:

```
yes

Certificate was added to keystore
```
