# JDDJ_Reverse

## Background
京东到家API很容易通过Fiddler或其它类似流量代理程序抓到，

## Tools
京东到家web版signKeyV1逆向分析
分析工具： Chrome, <a href="https://chrome.google.com/webstore/detail/resource-override/pkoacgokdfckfpndoffpifphamojphii">Resource override extension</href>

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
Now you can easily convert the 'm.b' to actual function codes, alternatively, you can step in to the function m.b 
<img src="2.1.png" />
<img src="2.2.png" />

```
function c(e) {
    var t = "object" == typeof e ? e : JSON.parse(e),
        o = {};
    Object.keys(t).sort().forEach(function(e) {
        "functionId" != e && (o[e] = t[e])
    });
    var a = Object.values(o).filter(function(e) {
            if ("" != e) return e
        }),
        i = n(931),
        c = i.HmacSHA256(a.join("&"), r.e);
    return i.enc.Hex.stringify(c)
}
```
What the code lines will do is:

1) Sorting the each of parameters by parementer name (alphabetic)
2) Populates an array of those parameter values.
3) Getting a string by concatenating all parameter values in the array with '&' separator.
4) Generating a hash value to the string by <a href="https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.hmacsha256?view=net-5.0">HmacSHA256</a> ，
*note: when generating the hash value, it will use a fixed salt value - 923047ae3f8d11d8b19aeb9f3d1bc200 
<img src="2.3.png" />

So you won't need to step into the actual codes how to generate the hash value, 
instead, you can develop yourself function using any programming language to simulate what this javascript function does.

## A function written in C# to generate signKeyV1


