# Headache Extravaganza (local discord challenge)

## discription :
a misc challenge that have been hosted on our local discord server.<br>
it's a mics of cryptography & OSINT and other stuff in general.<br>
it requires a little of knowledge in some cryptography types and a lot of thinking 
<br>
<br>
the challenge have only one flag but you get it in 3 parts let's see how 
## first part of flag :
let's take a look at the callenge description : 
<br><br>
<img src="images/2023-07-28_08-37.png">
<br>
<br>
here we get who links one named A and the other named B, and after that it says A + B is the key to start the challenge <br>
so that means that the two links are linked to each other to solve the challenge <br>
lets visit the first one and see what we got :
<br>
<br>
<img src="images/2023-07-28_08-54.png">
<br>
<br>
here we can see that we are looking for a password to unlock some link 
<br>
<br>
now lets see the other link :
<br>
<br>
<img src="images/2023-07-28_09-01.png">
<br>
<br>
here we get some place in google maps but if we look closely there is a code on the truck :
<br>
<br>
![2023-07-28_09-02](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/a6624ad4-a729-4f6c-925a-cd9dd232faee)
<br>
<br>
and if put that code in first website it will unlock and pass us to the next website :
<br>
<br>
![2023-07-28_09-10](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/cb9b1c67-a8fe-4f90-8118-ea200da68497)
<br>
<br>
we get a screenshot of a room in our discord server, let's see what's in there :
<br>
<br>
![2023-07-28_09-13](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/a092a325-1ab6-41ff-bb0d-9899e3f289c8)
<br>
<br>
we got so many encrypted stuff, let's go to cyebrchef and start decrypting this. <br>
the first one is the channel name, it's a rot13 encryption, you can learn more about it in [here](https://en.wikipedia.org/wiki/ROT13)
<br>
<br>
![2023-07-28_09-16](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/12d330f4-d7a2-4969-9606-ba65e8a9cfff)
<br>
<br>
it's useless but now let's get into the middle part 
<br>
```
domain.toplvldomain/watch?v=M-R0YhVRYto
Rkrk! myzid g 7kdsdrk uswk roik vyv wk3knmr d5kwow lkuk ov
lvkcck zvc hn k9bk g jk3wk omr sxktow suyex kdrouk,
dkg g7ovod ps odrs -_- g xogs duwv (nrobs dkg hn)!
```
<br>
as we can se we have two parts the first one we have a like link we will se itt late but for now we will decrypt the second part 
<br>
we can do that through bruteforce the rot13 amount 
<br>
<br>

![2023-07-28_09-24](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/90953dad-dd7a-45d8-9a8a-5161544059db)
<br>
<br>
as we can see in here it's a rot13 with 16 amount, obviously we know that because it's the only one readable in there. <br>
you can decrypt on your own and see the full message but it's kinda useless, let's go back and take a look at the url provided.
<br>

```
domain.toplvldomain/watch?v=M-R0YhVRYto
```
wait the end of the link looks like a youtube link but the first referring that we need to guess it so we do and here is the link :
<br>
```
www.youtube.com/watch?v=M-R0YhVRYto
```
<br>
let's visit the link and see what we got :
<br>
<br>

![2023-07-28_09-38](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/b9e5eedd-0cf1-4faf-a8a2-479a2d293b82)
<br>
<br>
we get a youtube video but if we take a look closely at the video discription we will see that there is two encrypted messages, <br>
the first one is a base64 encryption and the other is some hex encryption , <br>vigenere cipher
the second part is a note that says you need to click twice to copy the first part since its too long and you cannot copy it using mouse selection, <br>
and after doing that and using cyberchef for decryption we get a message with another encrypted link , 
<br>
<br>
![2023-07-28_09-45](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/81ce2982-592c-4ca9-8ac4-3f587a501652)
<br>
<br>
it's a rot13 with 19 amount we obviously cracked this through bruteforc using the method above, <br>
and we got this : 
<br>

```
https://youtu.be/BoQHQDKMk9A
```
<br>
as well we see the channel description it have two encrypted messages they are both base64 and rot47. <br>
let's take a look at the first one : <br><br>

![2023-07-28_10-31](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/be43780d-da25-4c20-a865-2538e34b3bd2)
<br>
<br>

```
57 5f 52 50 4a 43 41 03 52 04 02 54 02 6c
```
here we get some hex encrypted text, and it's telling us that it's the first part of the flage plus we will find xor in here, <br>
but first what is xor encryption ? <br>
it's an encryption you can learn more about it in [here](https://en.wikipedia.org/wiki/XOR_cipher) but let's learn more about his tricks :<br>
<br>
decrypted data + key = encrypted data <br>
encrypted data + key = decrypted data <br>
<br>
but the trick in here is : <br>
<br>
decrypted data + encrypted data = key <br>
<br>
so lets take a look at what we know about the flag , it starts with flag{...<br>
so using cyberchef we do this :
<br>
<br>

![2023-07-28_11-04](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/b8f06dae-655d-464f-ab67-f2aef33988b8)
<br>
<br>
so the key is "1337", we decrypt the whole text using this key and we get the first part of the flag :

```
flag{pr4c71c3_
```
<br>
now let's go back to the second message in the youtube video description, after decrypting that message we can see that it tells us to look at the vid name <br>
lets do it :
<br>
<br>

![2023-07-28_09-53](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/cb2621c3-08dd-4691-a59d-a184a47448f5)
<br>
<br>
lets decrypt this message and see what we got :
<br>
<br>

![2023-07-28_09-56](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/b180cc69-1939-4950-99a7-59460f31e48c)
<br>
<br>
we go to the about page of channel to see the email and stuff and see what we get :
<br>
<br>
![2023-07-28_09-58](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/59786c4e-d42c-45ed-b3f3-63c5e99e0c18)
<br>
<br>
yet another two encrypted message , the first one dosen't matter so much but the second one is this :
<br>

```
STs7NzppXl5FSjpENjlFXUhIXkR7eEVkOXN2
```
<br>
it's a base64 with rot47 then rot13 with 10 amount in the end we get this discord server invite link :
<br>
<br>

```
https://discord.gg/cVSd5rNQ
```
<br>
it's a normal looking discord server with nothing unusual but if we look at our discord roles we will see this :
<br>
<br>

![2023-07-28_10-05](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/e3a6290f-cb3e-4a2c-8d87-f1ab215c3736)
<br>
<br>
yet another discord invite link, we join the second server and find that ther is some room with mesages :
<br>
<br>

![2023-07-28_10-07](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/8521de92-08d8-4aed-871c-9a7b6abf7919)
<br>
<br>

let's decrypt this one 
<br>
<br>
![2023-07-28_10-22](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/1520d8f4-b0de-4ea1-ad3c-9ec268dddc55)
<br>
<br>

it's telling us to visit xanax profile and see what we got :
<br>
<br>

![2023-07-28_10-26](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/554370a0-bd4f-4c07-99a5-ac4b44a9946a)
<br>
<br>
as you can see in the about we see some text with a pastebin link, let's see what's in that link  
<br>
![2023-07-28_11-31](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/1f8059c6-ef22-46a0-a8bb-46429fac90e2)


```
5AA=@i^^DDD]F<B?BI2]J<:^DHAJ5nlTc+TbcTc)TbbTbd0
```
we decrypt this with cyberchef it's rot47 and rot13 with amount of 4 and some url decode we get this :
<br>

```
https://www.yourube.com/watch?=M4K35_
```
it's clearly a youtube url but sadly the link doesn't work but why ? <br>
take a look at the last part of  the link, it's the next part of the flag.
so now our flag is :
<br>

```
flag{pr4c71c3_M4K35_
```
now let's get back to the first encrypted long text in xanax profile :
<br>

```
crreu cue5 t hyecx5 nrsp pfpp j3au Xa b qih eaoeq qzosj vvdbt Psyquoe ui yipms uij gfcw :
etgpp://bna.cluguyj.tsq/phbrqx/vdg2oz2pz0B
```
this looks like a vigenere cipher <br>
let's try decrypting this out .
first we try xanax word ( since all the challenge talking about him... ) :
<br>
<br>
![2023-07-28_11-53](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/be116d5e-38a1-4ebb-bc84-c0e3f1ddb682)
<br>
<br>
Mmmm ... <br>
we see the word free ? <br>
how it would be possibly ? <br>
freexanax ? : 
<br>
<br>
![2023-07-28_11-55](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/eb261a16-d2c0-4687-a3b6-f9be1ca9efde)
<br>
<br>
yes it is and we get a youtube link :

```
https://www.youtube.com/shorts/ezc2rz2cz0E
```
so this is  a youtube short link i recommend editing this link to a normal video like this 

```
https://www.youtube.com/watch/ezc2rz2cz0E
```
so it can be easy to manipulate . <br>
first we see the video descryption :
<br>
<br>
![2023-07-28_12-05](https://github.com/hamzarezig/CTFs_writeups/assets/99124488/a488b2f8-b115-4045-b375-2511be0d7f63)
<br>
<br>
we can see there is 5 points, with a base32 text :

```
FB2WGN3LOYQDGMRAPJTCAIJANVVWQZ3FNIQGQ2ZAM53GU4LPEBXWO3TDEBVHO2RAH4UT2PJ6FB3WKN3NPAQGK3ZAGNSWQ3LYEB3HG6BAOBZXS4DFEBRGQIDRMVSGS4BAOFSWI2LQEAQSAZTYMEQG63JAPBZXS53JOAQHA2LQEBUXE2BAOF4GKMZANF4GYYZAKNLU2USYMMQGSIDHNRSXE4TJOAQGK6DMNF3CCLBAMJUCA33FOFUXAIDYMVQSA4DFMFUW4IBTMVYCAZTFMVUWQ3DFEAUT2PJ6FBTWU4LKNVXCA4LUPJYWU2JAOBXCAYTKG5VGSIDSMZSGW3LSNBWSA4LUPJWG2ZRANNXCAYLONFVHIIDEPEQGQ3LTNJSGMIDEMZZGU4JAM5VGQ3JANZZWM33KOIQGI2TLNVVHEIB7H47SYIBVMZ4WU5ZAGNTHG2LOEA3WM33GEBZTO2THEBZWMM3XNJVW2ZRAEEQDOZTPMYQHINLXMYQGO4LNNYQGUNLEEBSHSIDEMYZXE2TREBQWM4LONFTHS3TUOMQHC2TREBQW42LKOQTXQIB7EBZGMZBTMZUW42DNEBVHC3RANZXW4IDOMFTHC3TJNYQGU4JAMFXGS2TUEBXWMYTUPIQGO3LOEBRCAZ3GGNVGSIDOPJ2XC5DGNFXG2IDNPJWSAPZJEE
```
<br>
we decrypt that and we get this :

```
(uc7kv 32 zf ! mkhgej hk gvjqo ognc jwj ?)==>
(we7mx eo 3ehmx vsx psype bh qedip qedip ! fxa om xsywip pip irh qxe3 ixlc SWMRXc i glerrip exliv!, bh oeqip xea peain 3ep feeihle )==>
(gjqjmn qtzqji pn bj7ji rfdkmrhm qtzlmf kn anijt dy hmsjdf dfrjq gjhm nsfojr djkmjr ???, 5fyjw 3fsin 7fof s7jg sf3wjkmf ! 7fof t5wf gqmn j5d dy df3rjq afqnifynts qjq anijt'x ? rfd3finhm jqn non nafqnin jq anijt ofbtz gmn b gf3ji nzuqtfinm mzm ?)!
```
<br>
so these are 3 lines with different encryption <br>
first one is rot13 with 







