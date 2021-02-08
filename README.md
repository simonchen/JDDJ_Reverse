# JDDJ_Reverse
京东到家web版signKeyV1逆向分析

## Resource override
Searching the keyword 'signKeyV1' , converting the obfuscated js content  by clicking on 'Beautify JS' button
<img src="1.png" />
<img src="1.1.png" />

## Intercepts 'signKeyV1'
Enable the option - "mobile device"(inspector tool > Toggle device toolbar) to access JDDJ home page, then break point at signKeyV1 
<img src="2.png" />
Now, you can convert the 'm.b' to actual function string
<img src="2.1.png" />
