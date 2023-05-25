

## Attack: 
## Refs
https://arstechnica.com/information-technology/2023/05/critics-say-googles-new-zip-and-mov-domains-will-be-a-boon-to-scammers/

## Blue
use the following regex pattern to detect malicious domains
```
(?:[a-z0-9](?:[a-z0-9-]{0,61}[a-z0-9])?\.)+[a-z0-9][a-z0-9-]{0,61}[a-z0-9]⁄[a-zA-Z0-9_-]*@((?:[a-z0-9](?:[a-z0-9-]{0,61}[a-z0-9])?\.)+(?:zip))
```

Test with: 
```
http://thisdoesntexist.exampke⁄whatever@test.zip --> fraction slash
http://thisdoesntexist.exampke∕whatever@test.zip --> division slash
http://thisdoesntexist.exampke∕whatever@test.mov --> division slash with .mov
```

## Red
Characters: 
* Solidus (/): The UTF-8 representation for the solidus is simply the ASCII value for the forward slash character, which is 0x2F.
* Fraction Slash (⁄): The UTF-8 representation for the fraction slash is 0xE2 0x81 0x84. This symbol is encoded using multiple bytes in UTF-8.
* Division Slash (∕): corresponds to the division slash symbol. Represented by U+2215  or in 0xE2 0x88 0x95