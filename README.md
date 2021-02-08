# JDDJ_Reverse
京东到家web版signKeyV1逆向分析

## Resource override
Searching the keyword 'signKeyV1' , converting the obfuscated js content  by clicking on 'Beautify JS' button
<img src="1.png" />
<img src="1.1.png" />

## Intercepts 'signKeyV1'
Enable the option - "mobile device"(inspector tool > Toggle device toolbar) to access JDDJ home page, then break point at signKeyV1 
Where has the main function to generate the sign key:
```
  Object(m.b)(Object.assign(T, {
                        _jdrandom: R
                    }))
```
<img src="2.png" />
Now you can easily convert the 'm.b' to actual function string, of course, step over to the function m.b as follow:
<img src="2.1.png" />
Deeply, you will see the final key function called 'n(931)'
<img src="2.2.png" />
