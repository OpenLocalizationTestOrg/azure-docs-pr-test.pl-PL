---
title: "punkty końcowe usługi Azure CDN aaaTroubleshooting zwracanie stanu 404 | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z 404 kody odpowiedzi z punktów końcowych usługi Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404
Ten artykuł ułatwia rozwiązywanie problemów z [punktów końcowych usługi CDN](cdn-create-new-endpoint.md) zwraca błędy 404.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.

## <a name="symptom"></a>Objaw
Po utworzeniu profilu CDN i punktu końcowego, ale zawartość wygląda toobe dostępne na powitania CDN.  Użytkownicy, którzy podejmować tooaccess zawartości za pośrednictwem hello adresu CDN odbierania kodów stanu HTTP 404. 

## <a name="cause"></a>Przyczyna
Istnieje kilka możliwych przyczyn, w tym:

* pochodzenie pliku Hello nie jest widoczne toohello CDN
* Hello punktu końcowego jest nieprawidłowo skonfigurowana, co powoduje hello CDN toolook w niewłaściwym miejscu hello
* Hello host odrzuca hello nagłówek hosta z hello CDN
* punkt końcowy Hello nie było toopropagate czasu w całym hello CDN

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów
> [!IMPORTANT]
> Po utworzeniu punktu końcowego usługi CDN, nie natychmiast będzie dostępny do użycia, jak czas na powitania toopropagate rejestracji za pomocą hello CDN.  Aby uzyskać <b>Azure CDN from Akamai</b> profile, propagacji zazwyczaj kończy w ciągu jednej minuty.  W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.  Po ukończeniu czynności hello w tym dokumencie i nadal przygotowujemy odpowiedzi 404, należy wziąć pod uwagę oczekiwania kilka godzin toocheck ponownie przed otwarciem biletu pomocy technicznej.
> 
> 

### <a name="check-hello-origin-file"></a>Sprawdź hello pliku pierwotnego
Najpierw należy sprawdzić hello tego pliku hello chcemy pamięci podręcznej jest dostępne w naszym pochodzenia i jest dostępny publicznie.  Witaj najszybszy sposób toodo, który jest tooopen przeglądarce w sesji w trybie prywatnym lub Incognito, a następnie przejdź bezpośrednio toohello pliku.  Po prostu wpisz lub wklej adres URL hello hello pola adresu w i zobacz, jeśli wynikiem który plik hello, oczekiwane.  W tym przykładzie użyjemy toouse mam na koncie magazynu Azure, dostępny w pliku `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Jak widać, pomyślnie przekazuje hello testu.

![Powodzenie!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Gdy to hello najszybszym i Najprostszym sposobem tooverify Twojego pliku jest publicznie dostępna, niektóre konfiguracje sieci w organizacji można nadać hello wrażenie ten plik jest publicznie dostępna, gdy jest w rzeczywistości z Twojej sieci (tylko widoczne toousers nawet jeśli jest obsługiwany na platformie Azure).  Jeśli masz zewnętrznej przeglądarki, z którego można przetestować, takie jak urządzenia przenośnego, które nie jest połączone siecią organizacji tooyour lub maszynę wirtualną na platformie Azure, która będzie najlepsza.
> 
> 

### <a name="check-hello-origin-settings"></a>Sprawdź ustawienia źródła hello
Teraz, gdy mamy już zweryfikowana plik hello jest ogólnie dostępna w hello internet, weryfikacji naszych ustawienia źródła.  W hello [Azure Portal](https://portal.azure.com), przeglądanie profilu CDN tooyour i kliknij punkt końcowy hello jest rozwiązywanie problemów.  W co hello **punktu końcowego** bloku, kliknij hello pochodzenia.  

![Blok końcowy z pochodzenia wyróżnione](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Witaj **pochodzenia** zostanie wyświetlony blok. 

![Początek bloku](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Typ źródła i nazwy hosta
Sprawdź hello **typ źródła** są prawidłowe, a następnie sprawdź hello **nazwę hosta źródła**.  W naszym przykładzie `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, hello hostname część hello adres URL jest `cdndocdemo.blob.core.windows.net`.  Jak widać na zrzucie ekranu pokazano hello jest poprawny.  Dla usługi Azure Storage, aplikacji sieci Web i usługi w chmurze źródeł hello **nazwę hosta źródła** pole jest listy rozwijanej, więc nie potrzebujemy tooworry temat niepoprawnie sprawdzania pisowni.  Jednak jeśli używasz źródła niestandardowego, jest *absolutnie krytyczne* Twojego nazwa hosta jest poprawna!

#### <a name="http-and-https-ports"></a>Porty HTTP i HTTPS
Witaj innych toocheck co w tym miejscu jest Twoje **HTTP** i **porty HTTPS**.  W większości przypadków 80 i 443 są poprawne, a użytkownik będzie nie wymagają żadnych zmian.  Jednak jeśli serwer pochodzenia hello nasłuchuje na innym porcie, który należy toobe reprezentowana w tym miejscu.  Jeśli nie masz pewności, po prostu przyjrzyj hello adres URL pliku źródła.  Hello HTTP i HTTPS specyfikacje jako domyślne hello należy określić porty 80 i 443. W moich URL `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, port nie jest określony, dzięki czemu zakłada, że domyślna hello 443 i ustawienia są poprawne.  

Jednak powiedzieć hello adres URL dla pliku źródła, które wcześniej przetestowane jest `http://www.contoso.com:8080/file.txt`.  Uwaga hello `:8080` na końcu hello hello hostname segmentu.  Witaj przeglądarki toouse portu, który zawiadamia `8080` serwera sieci web toohello tooconnect w `www.contoso.com`, dlatego potrzebujesz tooenter 8080 w hello **HTTP port** pola.  Jest ważne toonote, że te ustawienia portów dotyczą tylko punktu końcowego jakie portu hello używa informacji tooretrieve z hello źródła.

> [!NOTE]
> **Azure CDN from Akamai** punktów końcowych nie zezwalaj na powitania pełny zakres portów TCP dla źródeł.  Lista niedozwolonych portów źródłowych znajduje się w artykule [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Azure CDN from Akamai — dozwolone porty źródłowe).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Sprawdź ustawienia punktu końcowego hello
Wstecz na powitania **punktu końcowego** bloku, kliknij przycisk hello **Konfiguruj** przycisku.

![Blok końcowy z podświetlony przycisk Konfiguruj](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Witaj punktu końcowego **Konfiguruj** zostanie wyświetlony blok.

![Skonfiguruj bloku](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protokoły
Aby uzyskać **protokołów**, sprawdź, czy protokół hello jest używany przez klientów hello jest zaznaczone.  Witaj tego samego protokołu używany przez klienta na powitania będzie co najmniej jedna używana początek hello tooaccess, dlatego jest ważne toohave hello niedozwolonych portów prawidłowo skonfigurowane w poprzedniej sekcji hello hello.  punkt końcowy Hello nasłuchuje tylko na hello domyślne portach HTTP i HTTPS (80 i 443), niezależnie od hello pochodzenia portów.

Możemy zwrócić hipotetyczny przykład tooour z `http://www.contoso.com:8080/file.txt`.  Jako zapamiętania, Contoso określonego `8080` jako ich HTTP portu, ale również Załóżmy podał `44300` jako ich portu HTTPS.  Jeśli one utworzone punktu końcowego o nazwie `contoso`, będzie ich hosta punktu końcowego CDN `contoso.azureedge.net`.  Żądanie `http://contoso.azureedge.net/file.txt` jest żądanie HTTP, więc punktu końcowego hello użyje HTTP na porcie 8080 tooretrieve z hello pochodzenia.  Bezpieczne żądania za pośrednictwem protokołu HTTPS, `https://contoso.azureedge.net/file.txt`, spowodowałoby hello toouse punkt końcowy HTTPS na porcie 44300 podczas pobrać hello pliku z hello źródła.

#### <a name="origin-host-header"></a>Nagłówek hosta źródła
Witaj **nagłówka hosta źródła** wartość nagłówka hosta hello wysłaniu toohello źródła z każdym żądaniem.  W większości przypadków, to powinno być hello takie same jako hello **nazwę hosta źródła** możemy zweryfikować wcześniej.  Nieprawidłowa wartość w tym polu zwykle nie będzie powodować stany 404, ale jest prawdopodobnie toocause innych stanów 4xx, w zależności od tego, jakie źródła hello oczekuje.

#### <a name="origin-path"></a>Ścieżka do źródła
Ponadto możemy zweryfikować naszych **ścieżki źródła**.  Domyślnie to pole jest puste.  To pole należy używać tylko, jeśli chcesz, aby zakres hello toonarrow hello hostowanej pochodzenia zasobów ma toomake dostępne na powitania CDN.  

Na przykład w Mój punkt końcowy miała wszystkie zasoby na Moje konto magazynu toobe dostępna, więc po lewej I **ścieżki źródła** puste.  Oznacza to, że żądanie zbyt`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` wynikiem połączenia z mojej punktu końcowego za`cdndocdemo.core.windows.net` który żąda `/publicblob/lorem.txt`.  Podobnie, żądanie `https://cdndocdemo.azureedge.net/donotcache/status.png` wynikiem żądania punktu końcowego hello `/donotcache/status.png` z hello źródła.

Ale co zrobić, jeśli nie chcę toouse hello CDN dla każdej ścieżki na Moje źródła?  Powiedz I miał być użyty tylko tooexpose hello `publicblob` ścieżki.  Jeśli wprowadzić */publicblob* w mojej **ścieżka do źródła** pola, które spowodują tooinsert punktu końcowego hello */publicblob* przed każdym żądaniem wykonywane toohello pochodzenia.  Oznacza to, że tego żądania hello `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` teraz potrwa faktycznie hello żądania część adresu URL hello, `/publicblob/lorem.txt`i Dołącz `/publicblob` toohello początku. Powoduje to żądanie `/publicblob/publicblob/lorem.txt` z hello źródła.  Jeśli ta ścieżka nie jest rozpoznawane tooan rzeczywisty plik, pochodzenia hello zwróci stanu 404.  faktycznie byłoby Hello poprawny adres URL tooretrieve lorem.txt w tym przykładzie `https://cdndocdemo.azureedge.net/lorem.txt`.  Należy pamiętać, że firma Microsoft nie zawierają hello */publicblob* ścieżki, ponieważ hello żądania część hello adres URL jest `/lorem.txt` i dodaje punkt końcowy hello `/publicblob`, co `/publicblob/lorem.txt` żądania hello przekazywany toohello źródła .

