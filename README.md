# JDDJ_Reverse
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
Now you can easily convert the 'm.b' to actual function string, alternatively, you can step in to the function m.b 
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
