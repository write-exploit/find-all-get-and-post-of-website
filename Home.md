```
import requests
from bs4 import BeautifulSoup
#bu kod bWAPP icin hazırlanmıştır
linkler = []
kendine_dene = []
def istek(link):
    a = requests.get(link).content
    global çıktı
    çıktı = BeautifulSoup(a,'html.parser').find_all('a')
    for i in çıktı:
        if str(i["href"]).startswith("https") or str(i["href"]).startswith("http"):
            linkler.append(i["href"]) #linkde bir sıkıntı yoksa ekliyoruz
        else:      
            if i["href"] == "#":
                pass #burada pass ettik ama bunun linki listeye kayıt oluyor sadece href bolümündeki # değeri eklenmiyor
            else:   
                if not str(i["href"]).startswith("/"): #link https yada http ile başlamıyorsa link'i başa koyuyoruz ve / koyup ardından linkin son kısmını yazıyoruz
                    kendine_dene.append(i["href"])
                    #linkler.append(link+'/'+i["href"]) #yaparsak user_new.php gibi degerler http://192.168.1.39/bWAPP/login.php/user_new.php olur ve anlamsız bir linke dönüşür  
                    #bu değerlerin elle denenmesi lazım
                else:
                    linkler.append(link+i["href"]) #link https yada http ile başlamıyorsa verilen link + linkin son kısmı'nı ekliyoruz
                    
istek("http://192.168.1.39/bWAPP/login.php") #burayı bWAPP'in içindeki linkide yazabiliriz yazdıgım otomatik kütüphanesindeki yuathay ile
for q in range(len(linkler)):
    try:
        istek(linkler[q])
    except:
        pass

print(linkler)
print("\n"*3)
print("diğer uzantılar :\n")
print(kendine_dene)
```
