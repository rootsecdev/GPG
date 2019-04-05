# GPG
Guide and scripts on GPG.

- Simple Method to generating an encryption key
```
gpg --gen-key
```
- Generate Encryption key with full encryption options. Useful for generating ECC keys for encryption

```
gpg --expert --full-gen-key
```
## Exporting and Importing Keys
- Exporting your public key for sharing. In the example below I am specifying my key by email and writing out to the file name Public.asc.
```
gpg --export -a "example@domain.com" > Public.asc
```
- Export your private key. Caution: It's important to backup your private key to a safe place. Secure with a 14 character or more password.
```
gpg --export-secret-key -a "example@domain.com" > private.asc
```
- Importing a public key. Please note this process is the same for importing a private key in your posession.
```
gpg --import Public.asc
```
## Revoking a keypair
- Revoking a keypair is used to distribute a revocation key to those by email or keyserver. It lets people know that your public key has been revoked. 
It's important to generate a revocation key immediately after key creation in case you ever misplace or lose your encryption key.
```
gpg --gen-revoke example@domain.com
```
## Signing Files, Messages, and other people's keys
- Signing is a method used to your sender that your file or message has not been altered during transit. It simply verifies
authenticity. Everyone should get in a habit of signing and verifying messages and files. 

- This command signs a file with a detached signature that can later be used for verification by the recipient. 
This option is the most useful for simply ensuring the integrity (but not privacy) of a file.
```
gpg --detach-sign -o sig.gpg testfile.txt
```
- Verify that a file has been signed with a good signature
```
gpg --verify sig.gpg testfile.txt
```
- Clearsign messages by wrapping an ASCII armored signature into a message. 
```
gpg --clearsign -o output.txt testfile.txt
```
- Verifying output file with ASCII armored signature
```
gpg --verify output.txt
```

## How to list and delete public and private keys

- How to list all your keys
```
gpg -list-keys
```

- How to list all your private keys
```
gpg --list-secret-keys
```

- How to delete a public key
```
gpg --delete-key "example@example.com"
```

- How to delete a secret key (private key)
```
gpg --delete-secret-key "example@example.com"
```

## working with GPG encryption (Putting it all together)
- Encrypt, sign and ACII Armor file. I find this useful when you are encrypting a message consisting of pure text to the receiver of the message. 
```
gpg --encrypt --sign --armor -r person@email.com name_of_file
```
- To encrypt to multiple receivers. 
```
gpg --encrypt --sign --armor -r person@email.com -r person2@email.com name_of_file
```
- Encrypt files without ASCII Armoring. This is useful when sending docs like PDF's, excel spreadsheets...etc..
```
gpg --encrypt --sign -r person@email.com name_of_file
```
- It is also possible to encrypt without a public key using symmetric encryption. The command below will encrypt a file with a password only. 
```
gpg --output doc.gpg --symmetric doc
```
## Decrypting Documents
- This command will decrypt a document and specify the output. Useful if you want to rename the output of the file. 
```
gpg --output doc --decrypt doc.gpg
```
## Symmetric Encryption secure password tutorial
- In linux a good method to generate secure passwords is to use a program called pwgen. Below is the syntax to use to create 20 character passwords that are secure with special characters. 
```
pwgen -y -s 20
```
- Here is a sample output of the above command:
```
(bionic)rootsecdev@localhost:~/Downloads$ pwgen -y -s 20
;`V'Ewrf+wC?E$*;@0H8 QgMH@0Kf),E&'A&pvpL~ Nzt?NQBXQ;r*4J1]d~-4
#\'0$H{!`&[8a$s9qNXn qX>5D#~9wVp;Pxb,!|[W sjDYqc4p2.={_]`~"sct
=qTR}xlwh`ANL`C#-6<T 4;)K1T+rpiCvbvMF?kY4 pwq:6=a`Ag^oars]`v/4
U|\!V/:w+$|eOPeH("L0 n~A."Fcg=-jfHT1>w^<Q #d0|oZhOC~\]Dhd-g:m>
x)aZ7N{d>V"Q7VYj%[Fb bLBrwi8anqGIcMPOz}6z qsN@_ajMq8)?[%Tl'HSe
[hmi7PZ"ehqP1qXJ?iIA 0}kAKoR7ne0ud'Q~Da&c k{AV0$;P,(b98;/$?u|H
^AWY/mZ7,BwA4.{r:_c} j1/T!?haP?wCP/6sW.e6 iROzbjvC\W195OBGo/2p
|cJBv:C(hS)n#3#K*]G} hEe1XM6cBF/iyO_:vYC8 }q<5i5@yL%[f`R'<\Jc/
Wsf9^CQAw6jVe]\$#DnC U*?VEhlhGD."5-1r-iB/ b6g[b2d6PrcgiHt(@n*9
\7t,TiY,-4nm/RCM<{-l 8&iz&kC_.5%@&[18G>^p YY'etD`BC'(\pT}>11pJ
FTSv;<7?!QDJUH'|m<7{ @4g]"j})]4nEOk#f.KC@ /aJkuL4tE`{(8Jd`Lohc
K3{?m:^"x4~kEgKd!SAO +Z!Z4Ppob[4@inFd.4Cv Qzx\-ub<A}|>[nLvu%>8
0/O?YwZ[+4t9NGf2WBcc FP;2!'jjOepHdSBI%]C/ P3D.QTm&+^XeKBRiI\Az
nZNAFknz8[w\,&<P65/0 w_j+\$5qPoFcmRlOW(%K E8KFT"]Y>dz%,Z5|62e|
k}UbPXPU,VG3zU)B-3l$ 2Sqk"FHBY(Z;<8gZl){b KCk}29yXBLn[kW?7OqhH
F36^|nrCz5me*o-kN3J5 ;l!|@||J1]6s8y&\<Snw Z[4/L&V}5|&pGpz`w?jC
tXjqSG5:OfB(?m,_w77u p()!i},NcWP4s+33N@c] TN|:AFGHHu2h:jH_qL`d
6-)i|G$oS<)&?fguwNg` x-7QEd<-'l$x*+}_f\E_ ">yyQToG)\L8ahIJ#Rw!
Y}Or:;(fFx>RBt,4{.6_ 3#Zmsuv"x&m+}Mmb\>M. FT|qr*Yf[cUmXj2~&W|X
uws\'+8^%W%&F:1[4"'U oO|BTr]_f~S?I}.7AaM/ _$$W.?LKsOJ{k'uIs2-/
(bionic)rootsecdev@localhost:~/Downloads$ 
```
