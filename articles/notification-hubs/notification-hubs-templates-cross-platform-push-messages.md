---
title: aaaTemplates
description: "W tym temacie wyjaśniono szablonów usługi Azure notification hubs."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Szablony
## <a name="overview"></a>Omówienie
Szablony Włącz klienta aplikacji toospecify hello formacie hello powiadomienia musi tooreceive. Za pomocą szablonów, aplikacji może realizować kilka różnych korzyści, w tym następujące hello:

* Niezależne od platformy wewnętrznej bazie danych
* Spersonalizowanych powiadomień
* Niezależność od wersji klienta
* Łatwe lokalizacji

Ta sekcja zawiera dwa szczegółowe przykłady sposobu toouse szablony toosend niezależny od platformy powiadomienia przeznaczonych dla wszystkich urządzeń na platformach i toopersonalize emisji urządzenia tooeach powiadomień.

## <a name="using-templates-cross-platform"></a>Za pomocą szablonów i platform
powiadomienia wypychane toosend standardowy sposób Hello jest toosend do każdego powiadomienia, który jest wysyłany, toobe określonych ładunku tooplatform usługi powiadomień (WNS, APNS). Na przykład toosend alertu tooAPNS ładunek hello jest obiekt Json hello następującej postaci:

    {"aps": {"alert" : "Hello!" }}

toosend podobny komunikat powiadomienia wyskakującego w aplikacji Sklepu Windows hello ładunek XML wygląda następująco:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

Podobne ładunki można tworzyć dla usługi MPNS (Windows Phone) i usługi GCM platform (Android).

To wymaganie wymusza hello aplikacji zaplecza tooproduce różnych ładunków dla każdej platformy i efektywnie sprawia, że zaplecza hello odpowiedzialny za część warstwy prezentacji hello aplikacji hello. Niektóre problemy obejmują lokalizacja i układy graficznego (szczególnie w przypadku aplikacji ze Sklepu Windows obejmujących powiadomień dla różnych typów Kafelki).

Witaj usługi Notification Hubs szablonu funkcja umożliwia aplikacji toocreate specjalne rejestracje klienta, nazywane rejestracji szablonu, które obejmują dodatkowo toohello zestawu tagów, szablon. funkcji szablonu usługi Notification Hubs Hello umożliwia urządzenia klienckie aplikacji tooassociate z szablonami czy korzystasz z urządzenia (preferowane) lub rejestracji. Podana hello poprzedzających przykłady ładunku, hello tylko informacje niezależne od platformy jest hello rzeczywiste komunikat alertu (Witaj!). Szablon jest zestaw instrukcji dla hello Centrum powiadomień w sposób tooformat niezależne od platformy wiadomość hello rejestrację, aplikacja określonego klienta. W hello poprzedzających przykład, komunikat niezależny platformy hello jest jednej właściwości: **wiadomość = Hello!**.

Witaj, na poniższej ilustracji przedstawiono hello powyżej proces:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

Szablon Hello rejestracji aplikacji klienta z systemem iOS hello jest następujący:

    {"aps": {"alert": "$(message)"}}

odpowiedni szablon powitania klienta w Sklepie Windows Hello jest:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Należy zauważyć, że rzeczywista wiadomość hello zastępuje hello wyrażenia $(komunikat). To wyrażenie powoduje, że hello Centrum powiadomień przy każdym wysyła toothis wiadomości w określonej rejestracji, toobuild komunikat, który wykonuje go i przełączników w wartości typowych hello.

Podczas pracy z modelem instalacji klucz "Szablony" instalacji hello przechowuje JSON wielu szablonów. Podczas pracy z modelem rejestracji powitania klienta aplikacji można utworzyć wiele rejestracji w kolejności toouse wielu szablonów; na przykład szablon komunikaty alertów i szablon do aktualizacji kafelka. Aplikacje klienckie można również mieszać rejestracje natywnego (rejestracje z szablonu) i rejestracji szablonu.

Witaj Centrum powiadomień wysyła jedno powiadomienie dla każdego szablonu bez uwzględniania czy należą toohello tej samej aplikacji klienta. To zachowanie może być używane tootranslate niezależne od platformy powiadomień na więcej powiadomienia. Na przykład Witaj tej samej toohello komunikat niezależny platformy Centrum powiadomień można bezproblemowo przekształcana alert wyskakujące i aktualizacji kafelka, bez konieczności toobe zaplecza hello świadomy naruszenia. Należy pamiętać, że niektóre platformy (na przykład iOS) może Zwiń wiele toohello powiadomienia o tym samym urządzeniu, jeśli są one wysyłane w krótkim czasie.

## <a name="using-templates-for-personalization"></a>Za pomocą szablonów na potrzeby personalizacji
Inną zaletą toousing szablonów jest hello toouse możliwości usługi Notification Hubs tooperform na rejestracji personalizacji powiadomień. Rozważmy na przykład aplikację pogodzie, która wyświetla kafelka z pogodą hello z określonej lokalizacji. Użytkownik może wybrać między stopni c lub f i prognozy pojedyncze lub pięć dni. Za pomocą szablonów, każdej instalacji aplikacji klienta można zarejestrować formatu hello wymagane (1-dniowego Celsjusz, 1-dniowego f, 5 dni c, 5 dni Stopnie Fahrenheita), i mieć hello Wyślij pojedynczy komunikat, który zawiera wszystkie informacje hello wymagane toofill tych wewnętrznej bazy danych Szablony (na przykład pięciodniowego prognozy z stopni c i f).

Szablon Hello hello jeden dzień prognozy z c temperatury jest następująca:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

toohello wysłano wiadomość Hello Centrum powiadomień zawiera wszystkie hello następujące właściwości:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Za pomocą tego wzorca, hello wewnętrznej bazy danych tylko wysyła pojedynczą wiadomość bez opcji personalizacji określonych toostore dla użytkowników aplikacji hello. Witaj, na poniższej ilustracji przedstawiono w tym scenariuszu:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Jak szablony tooregister
tooregister z szablonów przy użyciu modelu instalacji hello (preferowane) lub hello modelu rejestracji, zobacz [zarządzania rejestracji](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Język wyrażeń
Szablony są ograniczone tooXML lub formatowania dokumentu JSON. Ponadto tylko można umieścić wyrażenia w szczególności miejscach; na przykład atrybutów węzła lub wartości XML ciągu wartości właściwości dla formatu JSON.

Witaj poniższej tabeli przedstawiono dozwolone w szablonach języka hello:

| wyrażenie | Opis |
| --- | --- |
| $(prop) |Właściwości zdarzenia tooan odwołania o hello podanej nazwie. Nazwy właściwości nie jest rozróżniana. Tego wyrażenia rozpoznaje do wartości tekstowej właściwości hello lub pusty ciąg, jeśli nie ma właściwości hello. |
| $(prop, n) |Jak powyżej, ale hello tekst jest jawnie przycinana n znaków, na przykład $(tytuł, 20) klipy zawartość hello hello tytuł właściwości na 20 znaków. |
| . (prop, n) |Jako powyżej, ale hello tekstu z wielokropkiem jest sufiksem, jak ma zostać przycięta. Całkowity rozmiar hello Hello przycinana ciągu i sufiks hello nie przekracza n znaków. . (tytuł, 20) z właściwości wejściowej "Jest wiersz tytułu hello" skutkuje **jest tytuł hello...** |
| %(Prop) |Podobne too$(name), chyba że te dane wyjściowe hello jest kodowany w formacie identyfikatora URI. |
| #(prop) |Używane w szablonach JSON (na przykład dla systemów iOS i Android szablonów).<br><br>Ta funkcja działa dokładnie hello takie same jak $(prop) wcześniej określony, z wyjątkiem przypadków, gdy używane w szablonach JSON (na przykład szablony Apple). W tym przypadku, jeśli ta funkcja nie jest ujęta w "{","}" (na przykład "myJsonProperty": "#(nazwa)"), a jego wartość numer tooa w formacie Javascript, na przykład regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, a następnie hello dane wyjściowe JSON jest liczbą.<br><br>Na przykład "badge:"#(nazwa)"staje się"badge": 40 (a nie"40"). |
| "tekst" lub "text" |Literału. Literały zawiera dowolny tekst ujęty w pojedynczym lub podwójnym cudzysłowie. |
| Wyr1 + Wyr2 |operator łączenia Hello Sprzęganie dwóch wyrażeń w jednym ciągu. |

Witaj wyrażenia może być dowolny z hello poprzedzających formularzy.

Używając łączenia hello całego wyrażenia musi być ujęty w {}. Na przykład {$(prop) + "-" + $(prop2)}. |

Na przykład hello następujący element nie jest prawidłowy szablon XML:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Jak wyjaśniono łączenia, używając wyrażenia musi być ujęte w nawiasach klamrowych. Na przykład:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

