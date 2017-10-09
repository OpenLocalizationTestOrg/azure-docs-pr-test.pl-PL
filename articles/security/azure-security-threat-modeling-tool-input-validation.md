---
title: "aaaInput weryfikacji - narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Ramka zabezpieczeń: Sprawdzanie poprawności danych wejściowych | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Aplikacja sieci Web** | <ul><li>[Wyłącz XSLT skryptów dla wszystkich przekształceń przy użyciu arkuszy stylów niezaufanych](#disable-xslt)</li><li>[Upewnij się, że każdej strony, która może zawierać zawartość sterowane użytkownika zdecyduje się poza automatyczne wykrywanie MIME](#out-sniffing)</li><li>[Ograniczenia funkcjonalności lub wyłączyć rozpoznawanie jednostek XML](#xml-resolution)</li><li>[Aplikacje przy użyciu pliku http.sys przeprowadzenia weryfikacji zapewniania kanoniczności adresu URL](#app-verification)</li><li>[Upewnij się, że odpowiednie formanty są stosowane podczas akceptowania plików od użytkowników](#controls-users)</li><li>[Upewnij się, że bezpieczny parametry są używane w aplikacji sieci Web dla dostępu do danych](#typesafe)</li><li>[Użyj modelu oddzielne powiązanie klasy lub filtr powiązania wymieniono tooprevent MVC masowej przypisania luki w zabezpieczeniach](#binding-mvc)</li><li>[Kodowanie toorendering uprzedniego wyjścia niezaufanych sieci web](#rendering)</li><li>[Sprawdzania poprawności danych wejściowych i filtrowanie na typ ciągu wszystkie właściwości modelu](#typemodel)</li><li>[Ich oczyszczania powinny być stosowane na pola formularza, które akceptują znaków, np., Edytor tekstu sformatowanego](#richtext)</li><li>[Nie należy przypisywać toosinks elementy modelu DOM, które nie mają wbudowane kodowania](#inbuilt-encode)</li><li>[Sprawdź poprawność wszystkich przekierowania aplikacji hello zostały zamknięte lub wykonywane w sposób bezpieczny](#redirect-safe)</li><li>[Implementowanie sprawdzania poprawności danych wejściowych na wszystkie parametry typu ciąg zaakceptowane przez metody kontrolera](#string-method)</li><li>[Ustawić limitu górnego limitu czasu dla wyrażenia regularnego przetwarzania DoS tooprevent powodu toobad wyrażeń regularnych](#dos-expression)</li><li>[Należy unikać używania Html.Raw w widokami Razor](#html-razor)</li></ul> | 
| **Baza danych** | <ul><li>[Nie używaj zapytań dynamicznych procedury składowane](#stored-proc)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Upewnij się, że weryfikacja modelu jest wykonywana na metody interfejsu API sieci Web](#validation-api)</li><li>[Implementowanie sprawdzania poprawności danych wejściowych na wszystkie parametry typu ciąg zaakceptowane przez metody interfejsu API sieci Web](#string-api)</li><li>[Upewnij się, czy bezpieczny parametry są używane w interfejsie API sieci Web dla dostępu do danych](#typesafe-api)</li></ul> | 
| **Dokumentów w usłudze Azure DB** | <ul><li>[Użyj sparametryzowanego zapytania SQL usługi documentdb](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Sprawdzanie poprawności danych wejściowych WCF przez powiązanie ze schematem](#schema-binding)</li><li>[Sprawdzanie poprawności wejściowy WCF za pomocą parametru inspektorzy](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Wyłącz XSLT skryptów dla wszystkich przekształceń przy użyciu arkuszy stylów niezaufanych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zabezpieczenia XSLT](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [właściwości XsltSettings.EnableScript](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Kroki** | Obsługuje XSLT skryptów wewnątrz arkusze stylów przy użyciu hello `<msxml:script>` elementu. Dzięki temu używany podczas przekształcania XSLT toobe funkcji niestandardowych. Witaj skrypt jest wykonywany w kontekście hello hello procesu wykonywania hello transformacji. Skrypt XSLT musi zostać wyłączona w przypadku wykonywania tooprevent niezaufanych środowiska kodzie niezaufanym. *Jeśli przy użyciu platformy .NET:* XSLT skryptów jest domyślnie wyłączona; jednak pamiętaj, że go nie została jawnie włączona przy użyciu hello `XsltSettings.EnableScript` właściwości.|

### <a name="example"></a>Przykład 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Przykład
Jeśli używasz przy użyciu programu MSXML 6.0 XSLT skryptów jest domyślnie wyłączona; należy jednak upewnić się, czy go nie została jawnie włączona przy użyciu właściwości obiektu XML DOM hello AllowXsltScript. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Przykład
Jeśli używasz MSXML 5 lub poniżej, skryptów XSLT jest domyślnie włączona, więc użytkownik musi jawnie należy ją wyłączyć. Ustaw hello XML DOM obiektu właściwości AllowXsltScript toofalse. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>Upewnij się, że każdej strony, która może zawierać zawartość sterowane użytkownika zdecyduje się poza automatyczne wykrywanie MIME

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Programu IE 8 V części zabezpieczeń - kompleksową ochronę](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **Kroki** | <p>Dla każdej strony zawierających zawartość sterowane użytkownika, należy użyć hello nagłówka HTTP `X-Content-Type-Options:nosniff`. toocomply z tym wymaganiem, możesz albo zestaw hello wymaganego nagłówka przez strony dla tych stron, które mogą zawierać zawartość kontroli użytkownika, lub możesz ustawić globalnie do wszystkich stron w aplikacji hello.</p><p>Każdy typ pliku dostarczonych przez serwer sieci web ma skojarzoną [typ MIME](http://en.wikipedia.org/wiki/Mime_type) (skrót *typu zawartości*), który opisuje rodzaj hello hello zawartości (czyli obraz, tekst, aplikacji, itp.)</p><p>Nagłówek X-Content-typu-Options Hello jest nagłówka HTTP, która umożliwia deweloperom stosowanie toospecify, że jego zawartość nie powinny być ten sposób MIME. Ten nagłówek jest zaprojektowana toomitigate wykrywanie MIME ataków. Dodano obsługę dla tego nagłówka w programie Internet Explorer 8 (programu IE 8)</p><p>Tylko użytkownicy programu Internet Explorer 8 (programu IE 8) będą korzystać z X-Content-typu-Options. Poprzednie wersje programu Internet Explorer aktualnie nie przestrzega nagłówek X-Content-typu-Options powitania</p><p>Program Internet Explorer 8 (lub nowszy) są hello tylko główne przeglądarki funkcji Wypisz tooimplement wykrywanie MIME. Jeśli inne główne przeglądarki (Firefox, Safari, Chrome) zaimplementować podobne funkcje, to zalecenie będzie składni tooinclude zaktualizowane dla tych przeglądarek, jak również</p>|

### <a name="example"></a>Przykład
tooenable hello wymaganego nagłówka globalnie do wszystkich stron w aplikacji hello, możesz wybrać jedną z następujących hello: 

* Dodaj nagłówek hello w pliku web.config hello, jeśli aplikacja hello jest obsługiwana przez Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Dodaj nagłówek hello za pośrednictwem hello globalnego aplikacji\_powstaniem zdarzenia BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Implementowanie niestandardowego modułu HTTP 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Można włączyć wymaganego nagłówka hello tylko dla określonych stron, dodając tooindividual odpowiedzi: 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Ograniczenia funkcjonalności lub wyłączyć rozpoznawanie jednostek XML

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Rozszerzenia jednostki XML](http://capec.mitre.org/data/definitions/197.html), [ataki odmowy usługi XML i zabezpieczenia](http://msdn.microsoft.com/magazine/ee335713.aspx), [Omówienie zabezpieczeń MSXML](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [najlepsze rozwiązania dotyczące zabezpieczania kodu MSXML](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [referencyjne protokołu NSXMLParserDelegate](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [rozpoznawania odwołań zewnętrznych](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Kroki**| <p>Chociaż nie jest powszechnie używane, jest funkcją XML, który umożliwia tooexpand analizatora składni XML hello jednostek makro z wartości zdefiniowanych w obrębie samego dokumentu hello lub ze źródeł zewnętrznych. Na przykład dokument hello zdefiniować jednostki "NazwaFirmy" o wartości hello "Microsoft", tak, aby zawsze hello tekst "&companyname;" pojawia się w dokumencie hello, automatycznie zostaje zastąpiony tekst hello firmy Microsoft. Lub dokument hello zdefiniować jednostki "MSFTStock", który odwołuje się do zewnętrznych sieci web usługi toofetch hello bieżącej wartości zasobu firmy Microsoft.</p><p>Następnie w dowolnym momencie "&MSFTStock;" pojawia się w dokumencie hello, automatycznie zostaje zastąpiony bieżącego giełdowy hello. Jednak ta funkcja może być użyte toocreate odmowa warunki usługi (DoS). Osoba atakująca można zagnieżdżać wiele jednostek toocreate wykładniczej rozszerzenia bomba XML, który wykorzystuje wszystkie dostępnej pamięci w systemie hello. </p><p>Alternatywnie on można tworzyć odwołania zewnętrznego, który strumieni wstecz nieskończoną ilość danych lub która po prostu zawiesza się hello wątku. W związku z tym wszystkie zespoły należy wyłączyć wewnętrznych lub zewnętrznych rozpoznawania jednostki XML, jeśli ich stosowania nie używać jej lub ręcznie ograniczyć hello ilość pamięci i czasu, który aplikacji hello może używać do rozpoznawania jednostek, jeśli jest to bezwzględnie konieczne. Jeśli jednostka rozpoznawania nie jest wymagane przez aplikację, należy go wyłączyć. </p>|

### <a name="example"></a>Przykład
Dla kodu platformy .NET Framework można użyć hello następujących metod:

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Należy pamiętać, że wartość domyślna hello `ProhibitDtd` w `XmlReaderSettings` ma wartość true, ale w `XmlTextReader` ma wartość false. Jeśli używasz XmlReaderSettings tootrue ProhibitDtd dla elementu tooset nie ma potrzeby jawnie, ale jest zalecane dla bezpieczeństwa sake wykonanie. Należy również zauważyć, że domyślnie klasy XmlDocument hello zezwala na rozpoznawanie jednostek. 

### <a name="example"></a>Przykład
rozpoznawanie jednostek toodisable XmlDocuments, użyj hello `XmlDocument.Load(XmlReader)` przeciążenia hello Load — metoda i ustaw odpowiednie właściwości hello hello XmlReader argument toodisable rozdzielczość zgodnie z opisami w hello następującego kodu: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Przykład
Jeśli wyłączenie rozpoznawania jednostki nie jest możliwe w dla aplikacji, należy ustawić hello XmlReaderSettings.MaxCharactersFromEntities tooa rozsądne wartości właściwości zgodnie z potrzebami tooyour aplikacji. Ograniczy hello skutków potencjalnych ataków DoS wykładniczej rozszerzenia. Witaj następującego kodu zawiera przykład tej metody: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Przykład
Jeśli potrzebna tooresolve wbudowanego jednostek, ale nie ma potrzeby tooresolve podmioty zewnętrzne, należy ustawić hello XmlReaderSettings.XmlResolver właściwości toonull. Na przykład: 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Należy zauważyć, że w MSXML6, ProhibitDtd dla elementu jest tootrue (wyłączenie przetwarzanie elementu DTD) domyślnie. Kod, OS x firmy Apple dla systemu iOS, istnieją dwie analizatorów składni XML można użyć: NSXMLParser i libXML2. 

## <a id="app-verification"></a>Aplikacje przy użyciu pliku http.sys przeprowadzenia weryfikacji zapewniania kanoniczności adresu URL

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Dowolnej aplikacji, która korzysta z pliku http.sys należy przestrzegać następujących wytycznych:</p><ul><li>Ogranicz toono długość adresu URL hello więcej niż 16 384 znaków (ASCII lub Unicode). Jest to hello bezwzględną maksymalna długość adresu URL na podstawie ustawienia usług Internet Information Services (IIS) 6 domyślne hello. Witryn sieci Web należy dążyć do krótszego niż to, jeśli to możliwe</li><li>Używać hello standardowe .NET Framework we/wy pliku klas (na przykład FileStream), jak te skorzystają z hello zasady zapewniania kanoniczności w hello .NET FX</li><li>Jawne tworzenie listy dozwolonych, znane nazw plików</li><li>Jawnie Odrzuć znane typy plików, nie będzie obsługiwać odrzuca UrlScan: exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm [l], stm, drukarki, ini, pol, pliki dat</li><li>CATCH hello następujące wyjątki:<ul><li>System.ArgumentException (dla nazwy urządzenia)</li><li>System.NotSupportedException (dla strumieni danych)</li><li>System.IO.FileNotFoundException (dla nieprawidłowy zmienionym nazwy plików)</li><li>System.IO.DirectoryNotFoundException (dla nieprawidłowy katalogi zmienionym)</li></ul></li><li>*Nie* wyróżnienia pliku tooWin32 interfejsów API we/wy. Na nieprawidłowy adres URL bezpiecznie zwróci błąd 400 toohello użytkownika i hello rzeczywistych błąd logowania.</li></ul>|

## <a id="controls-users"></a>Upewnij się, że odpowiednie formanty są stosowane podczas akceptowania plików od użytkowników

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Nieograniczonych przekazywania pliku](https://www.owasp.org/index.php/Unrestricted_File_Upload), [tabeli podpisu pliku](http://www.garykessler.net/library/file_sigs.html) |
| **Kroki** | <p>Przekazano pliki reprezentują tooapplications znaczące zagrożenie.</p><p>pierwszym etapem wiele ataków w Hello jest tooget ataku niektórych toobe systemu toohello kodu. Następnie atak powitania musi wykonać kod hello tooget sposób toofind. Przy użyciu przekazywania pliku pomaga atakująca hello osiągnąć hello pierwszym krokiem. Hello skutków przekazywania pliku nieograniczony może różnić się w tym przejęcia całego systemu, system plików przeciążone lub bazy danych, przekazywanie systemami ataków tooback i proste atak skutkujący zmianą zawartości.</p><p>To zależy jakie aplikacji hello nie hello przekazać pliku, a szczególnie, gdzie są przechowywane. Brak sprawdzania poprawności po stronie serwera przekazywania plików. Następujące opcje zabezpieczeń powinny być implementowane przekazywanie plików funkcji:</p><ul><li>Sprawdź rozszerzenia plików (powinna być akceptowana prawidłowy zbiór dozwolonego typu plików)</li><li>Maksymalny limit rozmiaru</li><li>Plik nie powinien być przekazanym toowebroot; Lokalizacja Hello powinna być katalogu na dysku niesystemowym</li><li>Konwencja nazewnictwa, należy wykonać, tak, aby hello przekazana nazwa pliku ma niektórych losowości, tak jak tooprevent spowoduje zastąpienie pliku</li><li>Pliki powinny zostać przeskanowane pod kątem oprogramowania antywirusowego przed zapisaniem toohello dysku</li><li>Upewnij się, sprawdzania poprawności dla złośliwego znaków hello nazwę pliku i wszystkie inne metadane (np. ścieżka pliku)</li><li>Podpis format pliku powinna być sprawdzana, tooprevent użytkownika z przekazywania masqueraded pliku (np. przekazywanie pliku exe, zmieniając rozszerzenie tootxt)</li></ul>| 

### <a name="example"></a>Przykład
Hello ostatniego punktu dotyczące sprawdzania poprawności podpisu format pliku można znaleźć klasy toohello poniżej, aby uzyskać szczegółowe informacje: 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>Upewnij się, że bezpieczny parametry są używane w aplikacji sieci Web dla dostępu do danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Jeśli używasz hello kolekcji parametrów, SQL traktuje hello w danych wejściowych jest jako wartość literału, a nie jako kod wykonywalny. Witaj kolekcji parametrów można ograniczenia typu i długości tooenforce używane w danych wejściowych. Wartości spoza zakresu hello wyzwolenia Wystąpił wyjątek. Jeśli nie są używane parametry SQL bezpieczny, osoby atakujące może być możliwe tooexecute iniekcji atakom, które są osadzone w danych wejściowych hello niefiltrowane.</p><p>Parametry typu bezpieczne podczas konstruowania SQL zapytań tooavoid możliwe ataki które mogą wystąpić przy użyciu niefiltrowane danych wejściowych. Umożliwia bezpieczne parametry typu z procedur składowanych i dynamicznych instrukcji SQL. Parametry są traktowane jako wartości literałów przez hello bazę danych, a nie kodu wykonywalnego. Parametry są również sprawdzane pod kątem typu i długości.</p>|

### <a name="example"></a>Przykład 
Witaj poniższy kod przedstawia sposób toouse bezpieczne parametry typu z hello SqlParameterCollection podczas wywoływania procedury składowanej. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
W hello poprzedzających przykładowego kodu hello wartość wejściowa nie może być dłuższa niż 11 znaków. Jeśli dane hello niezgodny typ toohello lub długość zdefiniowaną przez parametr hello, hello klasy SqlParameter zgłasza wyjątek. 

## <a id="binding-mvc"></a>Użyj modelu oddzielne powiązanie klasy lub filtr powiązania wymieniono tooprevent MVC masowej przypisania luki w zabezpieczeniach

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Atrybuty metadanych](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [publiczny klucz zabezpieczeń luki w zabezpieczeniach i środki zaradcze](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [tooMass kompletny przewodnik po przydziału na platformie ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [wprowadzenie EF przy użyciu MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Kroki** | <ul><li>**Gdy powinna wyglądać dla zbyt księgowej luk w zabezpieczeniach? -** Zbyt księgowej luk w zabezpieczeniach, może wystąpić miejsce wiązania klasy modeli z danych wprowadzonych przez użytkownika. Struktury, takich jak MVC może reprezentować danych użytkownika w niestandardowej klasy .NET, w tym zwykły stare obiekty CLR (POCOs). MVC automatycznie wypełni te klasy modelu danych z żądaniem hello, zapewniając wygodny reprezentacja zajmujących się dane wejściowe użytkownika. Te klasy zawierają właściwości, które nie powinny być ustawiane przez użytkownika hello, aplikacji hello mogą być narażone ataków tooover publikowanie, umożliwiających kontrolki użytkownika danych, które nigdy nie aplikacji hello przeznaczone. Podobnie jak wiązania modelu MVC, technologii dostępu do bazy danych, takich jak mapowań obiektu/relacyjnych jak Entity Framework często również obsługiwać przy użyciu POCO obiektów toorepresent bazy danych. Te klasy modelu danych Podaj hello funkcję w dotyczących danych z bazy danych, tak jak w przypadku MVC przy danych wejściowych użytkownika. Ponieważ baza danych zarówno MVC i hello obsługuje podobnych modeli, jak w przypadku obiektów POCO wydaje się hello łatwe tooreuse sam klasy zarówno w celach. To kończy się niepowodzeniem rozwiązaniem, rozdzielenie toopreserve problemy, a jest jednego obszaru wspólnego, gdzie niezamierzone właściwości są widoczne powiązanie toomodel, umożliwiające publikowanie uwierzytelniając ataków.</li><li>**Dlaczego nie należy używać zajęć niefiltrowane bazy danych modelu jako parametry toomy MVC akcje? -** Wiązania modelu MVC ponieważ powiąże niczego w tej klasie. Nawet jeśli dane wyświetlane w widoku, złośliwy użytkownik może wysyłać żądań HTTP przy użyciu tych danych uwzględnione powitalne i MVC zostanie gladly powiązać ponieważ akcję tym, że baza danych klasy hello kształt danych powinien akceptować dla danych wejściowych użytkownika.</li><li>**Dlaczego należy interesujących kształtu hello używane do wiązania modelu? -** Wiązania modelu przy użyciu platformy ASP.NET MVC przy użyciu modeli nadmiernych przedstawia ataków tooover publikowanie aplikacji. Publikowanie uwierzytelniając można włączyć danych aplikacji toochange osoby atakujące poza jakiego developer hello przeznaczone, takie jak zastępowanie hello cen dla elementu lub hello uprawnień zabezpieczeń dla konta. Aplikacje powinny używać określonych akcji wiązanie modeli (lub listy filtrów określoną właściwość dozwolone) tooprovide jawne kontraktu dla jakie niezaufanych tooallow wejściowych za pośrednictwem wiązania modelu.</li><li>**Występują modeli oddzielne powiązania właśnie duplikowania kod? -** Nie jest to kwestia separacji. Ponowne użycie bazy danych modeli w metod akcji, są opinie żadnych właściwość (lub podrzędnego), w tej klasy można ustawić przez użytkownika hello w żądaniu HTTP. Jeśli nie chcesz MVC toodo, potrzebujesz listę filtrów lub tooshow kształtu osobnej klasy MVC, jakie dane mogą pochodzić z danych wejściowych zamiast tego użytkownika.</li><li>**Jeśli modele oddzielne powiązania dla danych wejściowych użytkownika, należy tooduplicate wszystkie moje atrybuty adnotacji danych? -** Niekoniecznie. Można użyć MetadataTypeAttribute na powitania metadanych bazy danych modelu klasy toolink toohello na klasy wiązania modelu. Po prostu pamiętać, że hello typu odwołuje się hello MetadataTypeAttribute musi być podzbiorem hello odwołanie do typu (może mieć mniej właściwości, ale nie więcej).</li><li>**Przenoszenie danych i z powrotem między modelami wejściowych użytkownika i modele bazy danych jest niewygodny. Wystarczy skopiować na wszystkie właściwości, za pomocą odbicia? -** Tak. Witaj tylko właściwości, które są wyświetlane w modelach powiązanie hello są hello widocznych zostały uznane toobe bezpiecznych danych wejściowych użytkownika. To nie ma powodu zabezpieczeń, co uniemożliwia ich przy użyciu odbicia toocopy przez wszystkie właściwości, które istnieją wspólne między te dwa modele.</li><li>**Jak [Bind (Wyklucz = "â €¦")]. Czy za pomocą którego zamiast modeli oddzielne powiązania? -** Tej metody nie jest zalecane. Przy użyciu [Bind (Wyklucz = "â €¦")] oznacza, że wszystkie nowe właściwości powiązania domyślnie. Po dodaniu nowej właściwości rzeczy tookeep tooremember dodatkowego kroku jest bezpieczne, a nie o hello projektu można domyślnie zabezpieczone. W zależności od dewelopera hello ryzykowne jest sprawdzanie tej listy za każdym razem, gdy właściwość została dodana.</li><li>**Jest [Bind (Dołącz = "â €¦")] przydatne w przypadku operacji edycji? -** Nie. [Powiązanie (Dołącz = "â €¦")] nadaje się tylko do operacji INSERT stylu (Dodawanie nowych danych). Dla operacji aktualizacji stylu (zmiana istniejących danych) Użyj innego podejścia, takie jak mających oddzielne powiązania modele lub przekazywanie jawną listę dozwolonych właściwości tooUpdateModel lub TryUpdateModel. Dodawanie [Bind (Dołącz = "â €¦")] atrybutu na operację edycji oznacza, że MVC zostanie utworzenie wystąpienia obiektu ustawione jako tylko hello na liście właściwości, pozostawiając pozostałe wartości domyślne. W przypadku danych hello jest trwały, całkowicie zastąpi hello istniejącej jednostki, resetowanie wartości hello tootheir właściwości pominięte wartości domyślne. Na przykład, jeśli został pominięty IsAdmin [Bind (Dołącz = "â €¦")] atrybutu na operację edycji, każdy użytkownik, którego nazwa została edytować za pomocą tej akcji będą tooIsAdmin resetowania = false (każdy użytkownik edytowanych spowoduje utratę stan administratora). Jeśli chcesz tooprevent aktualizacji właściwości toocertain, użyj jednej z hello inne podejścia powyżej. Należy pamiętać, że niektóre wersje narzędzi MVC wygenerowane klasy kontrolera z [Bind (Dołącz = "â €¦")] edytowanie akcji i oznacza, że usunięcie właściwości z tej listy będą zapobiegać atakom uwierzytelniając publikowanie. Jednak zgodnie z powyższym opisem tego podejścia nie działać zgodnie z oczekiwaniami i zamiast tego zostaną zresetowane wszystkie dane w hello pominięcia właściwości tootheir domyślne wartości.</li><li>**Dla operacji Create, czy istnieją wszystkie ostrzeżenia przy użyciu [Bind (Dołącz = "â €¦")] zamiast modeli oddzielne powiązania? -** Tak. Takie podejście najpierw nie działa w przypadku scenariuszy edycji konieczności utrzymania dwa podejścia oddzielne łagodzenia wszystkie luki w zabezpieczeniach publikowanie nadmierne. Modele powiązanie drugiej, oddzielnej wymuszania separacji między kształtu hello używany dla kształtu danych wejściowych i hello użytkownika używane do trwałości, coś [Bind (Dołącz = "â €¦")] nie działa. Trzecie, należy pamiętać, że [Bind (Dołącz = "â €¦")] może obsługiwać tylko właściwości najwyższego poziomu; Nie można zezwolić tylko części właściwości podrzędnych (na przykład "Details.Name") w atrybucie hello. Na koniec i prawdopodobnie przede wszystkim za pomocą [powiązania (Dołącz = "â €¦")] dodaje dodatkowy krok, który należy pamiętać, każda klasa hello czasu jest używany do wiązania modelu. Jeśli nowej metody akcji wiąże toohello klasy danych bezpośrednio i zapomni tooinclude [powiązania (Dołącz = "â €¦")] atrybutu, może być narażony tekst hello ataków tooover publikowanie [powiązania (Dołącz = "â €¦")] podejście jest domyślnie nieco mniej bezpieczne. Jeśli używasz [Bind (Dołącz = "â €¦")], zajmie się zawsze tooremember toospecify go za każdym razem, gdy klas danych są wyświetlane jako parametry metody akcji.</li><li>**Dla operacji Create, co o wprowadzenie hello [Bind (Dołącz = "â €¦")] atrybutu w samej klasy modelu hello? Nie takie podejście uniknąć hello potrzeby tooremember odkładanie hello atrybutu w każdej metody akcji? -** Ta metoda działa w niektórych przypadkach. Przy użyciu [powiązać (Dołącz = "â €¦")] na typ modelu hello sam (a nie na parametry akcji za pomocą tej klasy), należy unikać hello potrzeby tooremember tooinclude hello [powiązania (Dołącz = "â €¦")] atrybutu w każdej metody akcji. Przy użyciu atrybutu hello bezpośrednio w klasie hello skutecznie tworzy oddzielne powierzchni tej klasy w celach powiązania modelu. Jednak takie podejście umożliwia tylko na jeden kształt powiązanie modelu na model klasy. Jeśli jedna metoda akcji musi wiązania modelu tooallow pola (na przykład tylko administrator akcję, która aktualizuje role użytkowników), a inne akcje muszą wiązania modelu tooprevent tego pola, ta metoda nie będzie działać. Każda klasa może mieć tylko jeden kształt powiązanie modelu; Jeżeli różne akcje muszą kształtów powiązania innego modelu, muszą toorepresent je rozdzielić kształtów za pomocą klasy powiązanie albo oddzielnym modelu lub różnych [powiązania (Dołącz = "â €¦")] atrybuty hello metody akcji.</li><li>**Co to są wiązanie modeli? Czy na pewno one hello odpowiednikiem modeli widok? -** Są dwa pojęcia pokrewne. termin Hello klasy modelu tooa używany w akcja odwołuje się powiązanie modelu jest lista parametrów (kształtu hello przekazywane z metody akcji toohello powiązanie modelu MVC). model widoku termin Hello odwołuje się tooa klasy modelu przekazywane z widoku tooa metody akcji. Przy użyciu modelu specyficzne dla widoku jest typowym podejściem przekazywania danych z widoku tooa metody akcji. Często ten kształt jest również odpowiedniego do wiązania modelu i model widoku termin hello mogą być używane toorefer hello samego modelu używane w obu miejscach. toobe dokładne, ta procedura wspomniana specjalnie wiązanie modeli koncentrujących się na kształt hello przekazany toohello akcji, która jest, co jest ważne dla celów masowej przypisania.</li></ul>| 

## <a id="rendering"></a>Kodowanie toorendering uprzedniego wyjścia niezaufanych sieci web

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC6 MVC5, formularzy sieci Web |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Jak tooprevent Cross-site skryptów w programie ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [skryptów krzyżowych](http://cwe.mitre.org/data/definitions/79.html), [arkusza Cheat zapobiegania XSS (skryptów krzyżowych)](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Kroki** | Skryptów między witrynami (zwykle skrót XSS) jest celem ataków usług online lub dowolnej aplikacji/składnik, który zużywa dane wejściowe z hello sieci web. Luki w zabezpieczeniach XSS może umożliwić atakującemu skryptu tooexecute komputera innego użytkownika przy użyciu aplikacji sieci web narażone. Złośliwych skryptów można toosteal używanych plików cookie i inaczej manipulowanie ofiara komputera przy użyciu języka JavaScript. Walidacja danych wejściowych użytkownika, zapewnienie, że jest poprawnie sformułowany i kodowanie, zanim zostanie wyświetlony na stronie sieci web nie będzie mógł XSS. Sprawdzania poprawności danych wejściowych i wyjściowych kodowanie może odbywać się przy użyciu biblioteki ochrony sieci Web. Dla kodu zarządzanego (C\#, VB.net, itp.), użyj jednej lub więcej odpowiednich metod kodowania z hello Biblioteka ochrony sieci Web (Anti-XSS), w zależności od kontekstu hello, gdy dane wejściowe użytkownika hello pobiera dyskowe wyświetlane:| 

### <a name="example"></a>Przykład

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Sprawdzania poprawności danych wejściowych i filtrowanie na typ ciągu wszystkie właściwości modelu

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Dodawanie walidacji](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [sprawdzanie poprawności modelu danych w aplikacji MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [wytyczne dla aplikacji ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Kroki** | <p>Wszystkie parametry wejściowe hello musi zostać zweryfikowany, zanim zostaną użyte w tooensure aplikacji hello czy aplikacji hello jest chronione przed danych wprowadzonych przez złośliwego użytkownika. Sprawdź poprawność wartości wejściowe hello za pomocą wyrażeń regularnych operacji sprawdzania poprawności po stronie serwera ze strategią sprawdzania poprawności listy dozwolonych adresów IP. Unsanitized danych wprowadzonych przez użytkownika / parametry przekazywane do metody toohello może spowodować kodu iniekcji luk w zabezpieczeniach.</p><p>Punkty wejścia można także dla aplikacji sieci web, pól formularza, QueryStrings plików cookie, nagłówków HTTP i parametry usługi sieci web.</p><p>Witaj następujące testy sprawdzania poprawności danych wejściowych należy wykonać podczas wiązania modelu:</p><ul><li>właściwości modelu Hello powinny być adnotowany przy adnotacji wyrażenia regularnego, Zaakceptuj dozwolonych znaków, a maksymalna dopuszczalna długość</li><li>metody kontrolera Hello należy wykonać ModelState ważności</li></ul>|

## <a id="richtext"></a>Ich oczyszczania powinny być stosowane na pola formularza, które akceptują znaków, np., Edytor tekstu sformatowanego

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Kodowanie niebezpiecznych danych wejściowych](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [moduł czyszczący HTML](https://github.com/mganss/HtmlSanitizer) |
| **Kroki** | <p>Znajdź wszystkie tagi znaczników statycznych, które mają toouse. Popularną praktyką jest toorestrict formatowania toosafe HTML elementów, takich jak `<b>` (pogrubienie) i `<i>` (kursywą).</p><p>Przed zapisaniem danych hello, kodowanie HTML go. To sprawia, że wszystkie złośliwy skrypt bezpieczne powodując toobe obsługiwane jako tekst, a nie jako kod wykonywalny.</p><ol><li>Wyłącz sprawdzanie poprawności, dodając hello hello parametr ValidateRequest żądania programu ASP.NET = "false" atrybutu toohello @ Page — dyrektywa</li><li>Kodowanie hello ciąg na wejściu metodą HtmlEncode hello</li><li>Używanie StringBuilder i wywołanie hello kodowanie na powitania HTML elementy, które mają toopermit usunąć jego Zamień tooselectively — metoda</li></ol><p>Hello odwołuje się do strony w hello wyłącza sprawdzanie poprawności żądań ASP.NET przez ustawienie `ValidateRequest="false"`. Go koduje HTML hello argument wejściowy i umożliwia selektywne hello `<b>` i `<i>` Alternatywnie można również użyć biblioteki .NET dla ich oczyszczania HTML.</p><p>HtmlSanitizer to biblioteka .NET do czyszczenia fragmentów kodu HTML i dokumentów z konstrukcji, które mogą prowadzić tooXSS ataków. Używa AngleSharp tooparse, manipulowanie nimi oraz renderowania kodu HTML i CSS. HtmlSanitizer można zainstalować jako pakietu NuGet, a dane wejściowe użytkownika hello mogą zostać przekazane za pomocą odpowiednich HTML i CSS ich oczyszczania metod, zgodnie z wymaganiami na powitania po stronie serwera. Należy pamiętać, że ich oczyszczania jako kontrolę zabezpieczeń należy traktować wyłącznie jako ostatnia opcja.</p><p>Sprawdzania poprawności danych wejściowych i wyjściowych kodowanie są traktowane jako lepszą kontrolę zabezpieczeń.</p> |

## <a id="inbuilt-encode"></a>Nie należy przypisywać toosinks elementy modelu DOM, które nie mają wbudowane kodowania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wiele funkcji javascript nie wykonuj kodowaniu. Podczas przypisywania niezaufanych tooDOM wprowadzania elementów za pomocą takich funkcji, może spowodować między wykonaniami skryptu (XSS) w lokacji.| 

### <a name="example"></a>Przykład
Poniżej przedstawiono przykłady niezabezpieczone: 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
Nie używaj `innerHtml`; zamiast tego użyć `innerText`. Podobnie, a nie z `$("#elm").html()`, użyj`$("#elm").text()` 

## <a id="redirect-safe"></a>Sprawdź poprawność wszystkich przekierowania aplikacji hello zostały zamknięte lub wykonywane w sposób bezpieczny

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Witaj OAuth 2.0 autoryzacji Framework - readresatory otwarte](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Kroki** | <p>Projekt aplikacji wymagających lokalizacji dostarczone przez użytkownika tooa przekierowania należy ograniczyć hello przekierowania możliwe cele tooa wstępnie zdefiniowanych "bezpiecznej" Lista Lokacje lub domeny. Wszystkie przekierowania w aplikacji hello musi być zamknięty bezpieczne.</p><p>toodo to:</p><ul><li>Zidentyfikuj wszystkie przekierowania</li><li>Implementuje odpowiednie środki zaradcze dla każdego przekierowania. Odpowiednie środki zaradcze zawierają potwierdzenie przekierowania listy dozwolonych lub użytkownika. Jeśli do witryny sieci web lub usługi z usterki Otwórz przekierowania używa dostawcy tożsamości usługi Facebook/OAuth/OpenID, osoba atakująca może wykradać tokenu logowania użytkownika i personifikacji tego użytkownika. Jest to ryzykiem w przypadku w trybie OAuth, które opisano w dokumencie RFC 6749 "hello Framework autoryzacji OAuth 2.0", podobnie sekcji 10.15 "otworzyć przekierowuje", poświadczeń użytkowników mogą zostać złamane przez ukierunkowanego wyłudzania przy użyciu przekierowania Otwórz</li></ul>|

## <a id="string-method"></a>Implementowanie sprawdzania poprawności danych wejściowych na wszystkie parametry typu ciąg zaakceptowane przez metody kontrolera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Sprawdzanie poprawności modelu danych w aplikacji MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [wytyczne dla aplikacji ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Kroki** | Dla metod, które wystarczy zaakceptować jako argument typu danych pierwotnych, a nie modeli można wykonać sprawdzania poprawności danych wejściowych przy użyciu wyrażenia regularnego. W tym miejscu Regex.IsMatch powinien być używany z wzorcem prawidłowe wyrażenie regularne. Hello danych wejściowych nie odpowiada hello określonego wyrażenia regularnego, formantu nie powinien kontynuować i powinna być wyświetlana odpowiedniego ostrzeżenia dotyczące niepowodzenia weryfikacji.| 

## <a id="dos-expression"></a>Ustawić limitu górnego limitu czasu dla wyrażenia regularnego przetwarzania DoS tooprevent powodu toobad wyrażeń regularnych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC6 MVC5, formularzy sieci Web  |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Właściwość DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Kroki** | tooensure "odmowa usługi" przeciwko nieprawidłowo tworzone wyrażenia regularne, powodujących dużo śledzenie wsteczne ustawić hello globalne domyślny limit czasu operacji. Jeśli czas przetwarzania hello trwa dłużej, niż górny limit zdefiniowany hello, go spowoduje zgłoszenie wyjątku limitu czasu. Jeśli niczego nie skonfigurowano hello limitu czasu może być nieskończona.| 

### <a name="example"></a>Przykład
Na przykład hello następującej konfiguracji zgłosi RegexMatchTimeoutException, jeśli przetwarzanie hello ma więcej niż 5 sekund: 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Należy unikać używania Html.Raw w widokami Razor

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| Krok | Stron sieci Web ASP.Net (Razor) wykonaj automatyczne kodowania HTML. Wszystkie ciągi drukowanymi przez nuggets osadzonego kodu (@ bloki) są automatycznie kodowany w formacie HTML. Jednakże, gdy `HtmlHelper.Raw` wywołania metody, zwraca kod znaczników, który nie ma kodowania HTML. Jeśli `Html.Raw()` używana jest metoda pomocnika, pomijany hello automatyczne kodowania ochrony, która zapewnia Razor.|

### <a name="example"></a>Przykład
Poniżej przedstawiono przykładowy niezabezpieczonych: 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
Nie używaj `Html.Raw()` chyba, że należy toodisplay znaczników. Ta metoda nie przeprowadza kodowania niejawnie danych wyjściowych. Użyj innych pomocników platformy ASP.NET, np.`@Html.DisplayFor()` 

## <a id="stored-proc"></a>Nie używaj zapytań dynamicznych procedury składowane

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Ataku polegającego na iniekcji SQL wykorzystuje luki w zabezpieczeniach w sprawdzania poprawności danych wejściowych polecenia dowolnego toorun hello bazy danych. Go może wystąpić, gdy aplikacja używa wejściowych tooconstruct dynamiczne się, że tooaccess instrukcji SQL hello bazy danych. Może również wystąpić, jeśli procedury składowane przekazywane ciągi zawierające dane wejściowe użytkownika raw używa Twój kod. Przy użyciu hello ataku polegającego na iniekcji SQL, osoba atakująca hello polecenia można wykonywać dowolne hello bazy danych. Wszystkie instrukcje SQL (w tym instrukcje SQL hello w procedur składowanych) musi sparametryzowana. Sparametryzowanych instrukcji SQL akceptuje znaków, które mają specjalne znaczenie tooSQL (na przykład pojedynczy cudzysłów) bez problemów, ponieważ są one silnie typizowane. |

### <a name="example"></a>Przykład
Poniżej przedstawiono przykład niezabezpieczonych dynamiczne procedury składowanej: 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Przykład
Tej samej procedury składowanej zaimplementowana bezpiecznie hello jest następujący: 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>Upewnij się, że weryfikacja modelu jest wykonywana na metody interfejsu API sieci Web

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Weryfikacja modelu w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Kroki** | Gdy klient wysyła dane interfejsu API sieci web tooa, jest obowiązkowy toovalidate hello danych przed wykonaniem jakiegokolwiek przetwarzania. Dla interfejsów API sieci Web ASP.NET, która akceptuje modeli jako dane wejściowe, użyj adnotacji danych na reguł sprawdzania poprawności tooset modeli na powitania właściwości hello modelu.|

### <a name="example"></a>Przykład
Witaj następującego kodu pokazano hello na tym samym: 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Przykład
W metodzie akcji hello hello kontrolerów interfejsu API ważność hello modelu ma toobe jawnie zaznaczone, jak pokazano poniżej: 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Implementowanie sprawdzania poprawności danych wejściowych na wszystkie parametry typu ciąg zaakceptowane przez metody interfejsu API sieci Web

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, MVC 5, 6 MVC |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Sprawdzanie poprawności modelu danych w aplikacji MVC](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [wytyczne dla aplikacji ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Kroki** | Dla metod, które wystarczy zaakceptować jako argument typu danych pierwotnych, a nie modeli można wykonać sprawdzania poprawności danych wejściowych przy użyciu wyrażenia regularnego. W tym miejscu Regex.IsMatch powinien być używany z wzorcem prawidłowe wyrażenie regularne. Hello danych wejściowych nie odpowiada hello określonego wyrażenia regularnego, formantu nie powinien kontynuować i powinna być wyświetlana odpowiedniego ostrzeżenia dotyczące niepowodzenia weryfikacji.|

## <a id="typesafe-api"></a>Upewnij się, czy bezpieczny parametry są używane w interfejsie API sieci Web dla dostępu do danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Jeśli używasz hello kolekcji parametrów, SQL traktuje hello w danych wejściowych jest jako wartość literału, a nie jako kod wykonywalny. Witaj kolekcji parametrów można ograniczenia typu i długości tooenforce używane w danych wejściowych. Wartości spoza zakresu hello wyzwolenia Wystąpił wyjątek. Jeśli nie są używane parametry SQL bezpieczny, osoby atakujące może być możliwe tooexecute iniekcji atakom, które są osadzone w danych wejściowych hello niefiltrowane.</p><p>Parametry typu bezpieczne podczas konstruowania SQL zapytań tooavoid możliwe ataki które mogą wystąpić przy użyciu niefiltrowane danych wejściowych. Umożliwia bezpieczne parametry typu z procedur składowanych i dynamicznych instrukcji SQL. Parametry są traktowane jako wartości literałów przez hello bazę danych, a nie kodu wykonywalnego. Parametry są również sprawdzane pod kątem typu i długości.</p>|

### <a name="example"></a>Przykład
Witaj poniższy kod przedstawia sposób toouse bezpieczne parametry typu z hello SqlParameterCollection podczas wywoływania procedury składowanej. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
W hello poprzedzających przykładowego kodu hello wartość wejściowa nie może być dłuższa niż 11 znaków. Jeśli dane hello niezgodny typ toohello lub długość zdefiniowaną przez parametr hello, hello klasy SqlParameter zgłasza wyjątek. 

## <a id="sql-docdb"></a>Użyj sparametryzowanego zapytania SQL dla bazy danych rozwiązania Cosmos

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dokumentów w usłudze Azure DB | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Anonsowanie parametryzacja SQL w usłudze DocumentDB](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **Kroki** | Chociaż usługa DocumentDB obsługuje tylko zapytania tylko do odczytu, iniekcja kodu SQL jest nadal możliwe, jeśli zapytania zostały utworzone przez łączenie z danych wejściowych użytkownika. Może się zdarzyć toodata dostępu toogain użytkownika nie należy korzystać w ramach hello tej samej kolekcji przez obsługuje tworzenie złośliwego zapytania SQL. Użyj sparametryzowane zapytania SQL Jeśli zbudowanych zapytania oparte na danych wejściowych użytkownika. |

## <a id="schema-binding"></a>Sprawdzanie poprawności danych wejściowych WCF przez powiązanie ze schematem

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Kroki** | <p>Brak weryfikacji prowadzi toodifferent iniekcji ataków.</p><p>Sprawdzanie poprawności komunikatu reprezentuje jedną linię obrony w przypadku ochrony hello aplikacji WCF. Z tej metody Sprawdź poprawność wiadomości przy użyciu operacji usługi WCF tooprotect schematy przed atakami złośliwego klienta. Sprawdź poprawność wszystkich komunikatów odebranych przez powitania klienta tooprotect powitania klienta przed atakiem przez złośliwe usługi. Sprawdzanie poprawności komunikatu ułatwia wiadomości możliwych toovalidate podczas operacji korzystać kontraktów komunikatu lub kontraktów danych, których nie można wykonać przy użyciu sprawdzanie poprawności parametru. Sprawdzanie poprawności komunikatu umożliwia logikę weryfikacji toocreate wewnątrz schematów, a tym samym zapewniając większą elastyczność i zmniejsza czas programowania. Schematy mogą być ponownie używane w różnych aplikacjach wewnątrz organizacji hello, standardów dotyczących reprezentację danych. Ponadto sprawdzanie poprawności komunikatu pozwala operacji tooprotect jeśli używają oni bardziej złożone typy danych obejmujących reprezentującej logiki biznesowej.</p><p>Sprawdzanie poprawności komunikatu tooperform, najpierw utworzyć schemat, który reprezentuje hello operacji usługi i hello typów danych używanych przez te operacje. Następnie można utworzyć klasy .NET, która implementuje inspektora komunikat niestandardowego klienta i wiadomości powitania od niestandardowych dyspozytora komunikatów Inspektor toovalidate wysłać/odebrać z hello usługi. Następnie implementuje weryfikacji wiadomości tooenable zachowania punktu końcowego niestandardowe na powitania klienta i hello usługi. Na koniec wdrożenia elementu konfiguracji niestandardowej klasy hello, które umożliwia tooexpose hello rozszerzony zachowania niestandardowe punktu końcowego w pliku konfiguracyjnym hello hello usługi lub klienta hello"</p>|

## <a id="parameters"></a>Sprawdzanie poprawności wejściowy WCF za pomocą parametru inspektorzy

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny, NET Framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Kroki** | <p>Sprawdzanie poprawności danych wejściowych i danych reprezentuje jeden ważne linię obrony w przypadku ochrony hello aplikacji WCF. Należy sprawdzić, czy wszystkie parametry ujawnione podczas obsługi operacji usługi WCF hello tooprotect przed atakiem przez złośliwego klienta. Z drugiej strony należy także sprawdzić, czy wszystkie wartości zwracanych odebranych przez powitania klienta tooprotect powitania klienta przed atakiem przez złośliwe usługi</p><p>Usługi WCF udostępniają punkty rozszerzeń różnych, umożliwiających zachowanie środowiska uruchomieniowego WCF hello toocustomize tworząc niestandardowe rozszerzenia. Wiadomości są dwa mechanizmy rozszerzania inspektorzy i inspektorzy parametr używany toogain większą kontrolę nad danymi hello przekazywanie między klientem a usługą. Należy użyć parametru inspektorzy do sprawdzania poprawności danych wejściowych i użyć inspektorzy komunikatów tylko wtedy, gdy potrzebujesz wiadomości powitania tooinspect całego przepływu i usługi.</p><p>Sprawdzanie poprawności danych wejściowych tooperform, zostanie Tworzenie klasy .NET i zaimplementować inspektora parametru niestandardowego w kolejności toovalidate parametrów operacji w usłudze. Następnie zostaną zaimplementowane weryfikacji tooenable zachowania punktu końcowego niestandardowe na powitania klienta i hello usługi. Na koniec zostaną zaimplementowane element konfiguracji niestandardowej klasy hello, które umożliwia tooexpose hello rozszerzony zachowanie punktu końcowego niestandardowych w pliku konfiguracyjnym hello usługi hello lub powitania klienta</p>|
