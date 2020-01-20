<script language =javascript>
function utf8to16(str){var out,i,len,c;var char2,char3;out=[];len=str.length;i=0;while(i<len){c=str.charCodeAt(i++);switch(c>>4)
{case 0:case 1:case 2:case 3:case 4:case 5:case 6:case 7:out[out.length]=str.charAt(i-1);break;case 12:case 13:char2=str.charCodeAt(i++);out[out.length]=String.fromCharCode(((c&0x1F)<<6)|(char2&0x3F));break;case 14:char2=str.charCodeAt(i++);char3=str.charCodeAt(i++);out[out.length]=String.fromCharCode(((c&0x0F)<<12)|((char2&0x3F)<<6)|((char3&0x3F)<<0));break;}}
return out.join('');}
var base64DecodeChars=new Array(-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,-1,62,-1,-1,-1,63,52,53,54,55,56,57,58,59,60,61,-1,-1,-1,-1,-1,-1,-1,0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,-1,-1,-1,-1,-1,-1,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48,49,50,51,-1,-1,-1,-1,-1);
function base64decode(str)
{var c1,c2,c3,c4;var i,len,out;len=str.length;i=0;out = "";while(i<len)
{do
{c1=base64DecodeChars[str.charCodeAt(i++)&0xff]}while(i<len&&c1==-1);if(c1==-1)
break;do
{c2=base64DecodeChars[str.charCodeAt(i++)&0xff]}while(i<len&&c2==-1);if(c2==-1)
break;out+=String.fromCharCode((c1<<2)|((c2&0x30)>>4));do
{c3=str.charCodeAt(i++)&0xff;if(c3==61)
return out;c3=base64DecodeChars[c3]}while(i<len&&c3==-1);if(c3==-1)
break;out+=String.fromCharCode(((c2&0XF)<<4)|((c3&0x3C)>>2));do
{c4=str.charCodeAt(i++)&0xff;if(c4==61)
return out;c4=base64DecodeChars[c4]}while(i<len&&c4==-1);if(c4==-1)
break;out+=String.fromCharCode(((c3&0x03)<<6)|c4)}
return out}
function long2str(v,w){var vl=v.length;var sl=v[vl-1]&0xffffffff;for(var i=0;i<vl;i++)
{v[i]=String.fromCharCode(v[i]&0xff,v[i]>>>8&0xff,v[i]>>>16&0xff,v[i]>>>24&0xff);}
if(w){return v.join('').substring(0,sl);}
else{return v.join('');}}
function str2long(s,w){var len=s.length;var v=[];for(var i=0;i<len;i+=4)
{v[i>>2]=s.charCodeAt(i)|s.charCodeAt(i+1)<<8|s.charCodeAt(i+2)<<16|s.charCodeAt(i+3)<<24;}
if(w){v[v.length]=len;}
return v;}
function xxtea_decrypt(str,key){if(str==""){return"";}
var v=str2long(str,false);var k=str2long(key,false);var n=v.length-1;var z=v[n-1],y=v[0],delta=0x9E3779B9;var mx,e,q=Math.floor(6+52/(n+1)),sum=q*delta&0xffffffff;while(sum!=0){e=sum>>>2&3;for(var p=n;p>0;p--){z=v[p-1];mx=(z>>>5^y<<2)+(y>>>3^z<<4)^(sum^y)+(k[p&3^e]^z);y=v[p]=v[p]-mx&0xffffffff;}
z=v[n];mx=(z>>>5^y<<2)+(y>>>3^z<<4)^(sum^y)+(k[p&3^e]^z);y=v[0]=v[0]-mx&0xffffffff;sum=sum-delta&0xffffffff;}
return long2str(v,true);}
t="xHGK+hyUoPmi/ewjwoJaKYXkgucEP5uGX46eqnZLleRdDDb0xyKkUkHLhy9M32NbEpc7nqRehBNUuWQ2+u3xQgwDobfikUkxa1NDuJpGcOC0pGyMvwPsTXFJARnS6livP5Ajlk33Z9dtCViXWhb4ZPArwqJXcroG09vh09Ys7Xfyy5avIoPnxuALDuWrUeYU2ZQgVNC6OrOI6mmVK/cvNrzofHNqacu9HAawO7g5KHH6Yu57KHzgCQDyN6y1IZ0LbBv9fuaN4CN5CBkdJ+oj2N0+PZpKBwlPEVpyUr+xrp/8/ji8vaUE30kXEoVMkO75lP04QzML0vcMomlahypWIZw75YP6SnKVMw/hBgkb5tWiavJE/oLkouTW4c5MbQqj5YwOk3gGBZCJhHO4pr5fHnsjNPZHDVOq/58eUPGZa6bV0A6l4YKIntx0wXJhKYnvi2b+0DPcon1zFuR6N8XYZV1zLQejw0ViDQMk2Wu05NDk2KdnEAYjuekxPLso+dDLyH9tY8Qr5Zbr1pfSPxpxhFztKGhbjluw2gKvhlAhAiWRWIOJokNvg5xQnUxlb59TIPeKB5CArdEeVhPTDiRDYLr+Yaj+loXu2CzT/DYwGqmr5J0LApv6tXpDXEc9qQLdSW5KPacAp8NlWiexOmHnxuOvHuXyda86swafmjpE1naBLnFgXfDh7pHJmrNdqsZxhOCjfZYcC00ivw/Ge+aeRtNlSS8/iYcJOSNuaAx/8zqQuEYU0wgTqaXR5CxLAWYEtLJnN6cXwz4ZdQ+uyGdEYAzTMczgHx3ob2SgHfI3AfT1H02zcAMnBeeMFli4qWklLaZFAn+BSQ7JpEzqAnqIcAx/XnJ0WM7DNqZMyGfWeioa1wDHuUuAkjc5FK2H6o4f7bMYE1tQl44fDkjAd2s0PuIddw0TSoWJa0wVUgV//SnMqXnklGONukY9J4SLO8PwgUk6ZP9n7H+2Ga3GflkGvk+bSMY9WJEyTs/SjTSSle+pkx9XBoWBzkEiTQcy+MIHQNkNshCtSX0PX4d60R48w4XXkJrNv1Nw+HBlzHqyNZfBLe4wM6RyCRuXxOG6OsuxYtXkKGlSlSZlLd0JwHCZ033BkPuuh6nG7ZktMNHjlH86925msG4VUUMw4W45pBfmLDbwhdmF2EzlW2s+7COhLQAYwE5YdE7uylMS6opxEaRc9qcuWv00Wjo8QlCeJeB5O1Jw9l8Ktpmb5RZnQafZUkZF1tmJ47kk15hj5MWPzygO/meqvxFNQXePNhtZqCawSCDAzBKsAKsB/NjhkQymyEXWCkTE1Wwy9HiCh2el5ubeNWBdk8CX+FTlktWlA+AbZ2sA3BoaheOz7MHQSUXeDGkUq59Noswq+8/SxaAmPHcDQkNO6x9FZkS0xrYc4+Lj+AXyah1/q5bHGCqW5UkdQNy+HdvbsZ02TsrBij0GT+wyBJk6/S37mlxO4L1NLJjZmVO9v8N/Czzm43i/1iOduEwVB2leGSjZJeoegR6ITly0ok+KTtaY23KBzMt7rPN2fQ7mGyh0ocQs/IdGkWyMzGs0Dj6Z2ibNLYsZUxDcpz213jPsdbyd8zIrFB1YLcjvLOtI89qGg/+svgc2TxTiCl4VSZojiV2PfeK5o9LjXBNLkx31Ykt1GrGcU+AUePSkxDNSlUDuEPRJl4pWNHBqvwZgBaJRB+n5O8RsofF8e6/RZ8s5IlPXv3nYo/DLbbU5f349Y/TIG9s5ePiTEQyUto0YCM2B7a4wyMECx+CXJsfA2WgjnejlTtFRrBn2zhurmA9v65/ZWIpw7tx0xZfGFToHWiWU1CncRabtKMm42N70oeHB01ThfeaiNdPNKd/fk5olmWfnfRBL8UU+8z8aUYPbkD/R5xnXooy+DflTur0ns9f39+ZwnmKYH7oPllsFNfbrKoLl/MC5OIwtervL7J8Fs+g2XA7q1AJ7jbeIxauYgB/DqEYN5FJBlGqwtxXrL+m9+D8sN0mnFsyjxtfDIdvXzfdZx7bgf+qpK5oIpp8KUEtHmHHgi4TDtPTNo/92E2NLKs7zrqjn0itCQRxkmDaNlCHjZ1uPFaSleWT/QuIWoPd2dDmLXDytZ/jCSpw8DD/2G05GPPZF7zXRW/9It+7rCdfwMymKoAJa7VKajjQAMpe06NlP+wIdQWg67yEvuSEgJet2QKDt29XVevP/nURn2GbGtNP0EA/OHt8jemYrQ6qCsthFIFVqI9Ie8VuyNaKzE3A+MSisT+CLTEMbjiAVTr1LQwvh/My4ecyLoSg//sAJ";
t=utf8to16(xxtea_decrypt(base64decode(t), 'javascript'));
document.write (t);
</script>
