---
title: "Rozwiązywanie problemów z punktami końcowymi usługi Azure CDN zwracanie stanu 404 | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f59fbd18413fb44026d8c92b7f6940ed2f8a00a8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404
Ten artykuł ułatwia rozwiązywanie problemów z [punktów końcowych usługi CDN](cdn-create-new-endpoint.md) zwraca błędy 404.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ekspertów platformy Azure na [MSDN Azure i fora przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź do [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz polecenie **Get Support**.

## <a name="symptom"></a>Objaw
Po utworzeniu profilu CDN i punktu końcowego, ale wygląda zawartości są dostępne w sieci CDN.  Użytkownicy, którzy próba uzyskania dostępu do zawartości za pośrednictwem adresu CDN odbierają kodów stanu HTTP 404. 

## <a name="cause"></a>Przyczyna
Istnieje kilka możliwych przyczyn, w tym:

* Do pochodzenia pliku nie jest widoczny do sieci CDN
* Punkt końcowy jest nieprawidłowa, powodując CDN do wyszukiwania w niewłaściwym miejscu
* Host odrzuca nagłówek hosta z sieci CDN
* Punkt końcowy nie było Czas propagacji w całej sieci CDN

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów
> [!IMPORTANT]
> Po utworzeniu punktu końcowego usługi CDN, nie natychmiast będzie dostępny do użycia, ponieważ czas rejestracji propagację za pośrednictwem sieci CDN.  W przypadku profili usługi <b>Azure CDN from Akamai</b> propagacja zwykle trwa do minuty.  W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.  Wykonaj kroki w tym dokumencie i nadal otrzymujesz odpowiedzi 404, warto rozważyć oczekiwanie na kilka godzin, aby sprawdzić ponownie przed otwarciem biletu pomocy technicznej.
> 
> 

### <a name="check-the-origin-file"></a>Sprawdzanie pliku pierwotnego
Po pierwsze, weryfikacji się, że plik chcemy pamięci podręcznej jest dostępny na naszych pochodzenia i jest dostępny publicznie.  Jest najszybszym sposobem, w tym celu otwórz w przeglądarce w sesji Incognito lub w trybie prywatnym, a następnie przejdź bezpośrednio do pliku.  Po prostu wpisz lub wklej adres URL w polu adres i zobacz, jeśli wynikiem który plik oczekiwane.  W tym przykładzie użyjemy przy użyciu pliku mam na koncie magazynu Azure, dostępny pod `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Jak widać, przekazuje pomyślnie testu.

![Powodzenie!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Jest najszybszym i Najprostszym sposobem Sprawdź, czy plik jest dostępny publicznie, niektóre konfiguracje sieci w organizacji można zapewnić wrażenie, że ten plik jest publicznie dostępna, jeśli jest on w rzeczywistości widoczne tylko dla użytkowników sieci (nawet jeśli jest obsługiwany na platformie Azure).  Jeśli masz zewnętrznej przeglądarki, z którego można przetestować, takich jak urządzenia przenośnego, które nie jest podłączony do sieci danej organizacji lub maszynę wirtualną na platformie Azure, która będzie najlepsza.
> 
> 

### <a name="check-the-origin-settings"></a>Sprawdź ustawienia źródła
Teraz, kiedy możemy zostały zweryfikowane się, że plik jest dostępny publicznie w Internecie, weryfikacji naszych ustawienia źródła.  W [Azure Portal](https://portal.azure.com), przejdź do profilu sieci CDN i kliknij punkt końcowy jest rozwiązywanie problemów.  W wynikowym **punktu końcowego** bloku, kliknij przycisk źródła.  

![Blok końcowy z pochodzenia wyróżnione](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

**Pochodzenia** zostanie wyświetlony blok. 

![Początek bloku](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Typ źródła i nazwy hosta
Sprawdź **typ źródła** są prawidłowe, a następnie sprawdź **nazwę hosta źródła**.  W naszym przykładzie `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, nazwy hosta część adresu URL jest `cdndocdemo.blob.core.windows.net`.  Jak widać na zrzucie ekranu, jest poprawny.  Dla usługi Azure Storage, aplikacji sieci Web i usługi w chmurze źródeł **nazwę hosta źródła** pole jest listy rozwijanej, aby firma Microsoft nie musisz martwić się o poprawnie sprawdzania pisowni.  Jednak jeśli używasz źródła niestandardowego, jest *absolutnie krytyczne* Twojego nazwa hosta jest poprawna!

#### <a name="http-and-https-ports"></a>Porty HTTP i HTTPS
Jeszcze inną czynność do sprawdzenia, w tym miejscu jest Twoje **HTTP** i **porty HTTPS**.  W większości przypadków 80 i 443 są poprawne, a użytkownik będzie nie wymagają żadnych zmian.  Jednak jeśli serwer pochodzenia nasłuchuje na innym porcie, który należy być reprezentowane w tym miejscu.  Jeśli nie masz pewności, po prostu Spójrz na adres URL dla pliku źródła.  Specyfikacje protokołów HTTP i HTTPS, określ porty 80 i 443 jako ustawienia domyślne. W moich URL `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, port nie jest określony, przyjmowana jest wartość domyślna 443 i ustawienia są poprawne.  

Jednak powiedzieć adres URL dla pliku źródła, które wcześniej przetestowane jest `http://www.contoso.com:8080/file.txt`.  Uwaga `:8080` końcem segmentu nazwy hosta.  Które informuje przeglądarkę, aby używał portu `8080` do łączenia się z serwerem sieci web w `www.contoso.com`, więc musisz wprowadzić 8080 w **HTTP port** pola.  Należy pamiętać, że te ustawienia portów wpływ tylko na jakie port punktu końcowego używany do pobierania informacji ze źródła.

> [!NOTE]
> Punkty końcowe usługi **Azure CDN from Akamai** nie zezwalają na pełny zakres portów TCP dla źródeł.  Lista niedozwolonych portów źródłowych znajduje się w artykule [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Azure CDN from Akamai — dozwolone porty źródłowe).  
> 
> 

### <a name="check-the-endpoint-settings"></a>Sprawdź ustawienia punktu końcowego
Ponownie **punktu końcowego** bloku, kliknij przycisk **Konfiguruj** przycisku.

![Blok końcowy z podświetlony przycisk Konfiguruj](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Punkt końcowy **Konfiguruj** zostanie wyświetlony blok.

![Skonfiguruj bloku](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protokoły
Aby uzyskać **protokołów**, sprawdź, czy wybrano protokół używany przez klientów.  Ten sam protokół używany przez klienta będzie używane do dostępu pochodzenia, dlatego ważne jest, aby mieć porty źródła poprawnie skonfigurowane w poprzedniej sekcji.  Punkt końcowy nasłuchuje tylko na domyślne portach HTTP i HTTPS (80 i 443), niezależnie od portów pochodzenia.

Teraz wróć do naszych hipotetyczny przykład `http://www.contoso.com:8080/file.txt`.  Jako zapamiętania, Contoso określonego `8080` jako ich HTTP portu, ale również Załóżmy podał `44300` jako ich portu HTTPS.  Jeśli one utworzone punktu końcowego o nazwie `contoso`, będzie ich hosta punktu końcowego CDN `contoso.azureedge.net`.  Żądanie `http://contoso.azureedge.net/file.txt` jest żądanie HTTP, więc punktu końcowego użyje HTTP na porcie 8080, aby pobrać go ze źródła.  Bezpieczne żądania za pośrednictwem protokołu HTTPS, `https://contoso.azureedge.net/file.txt`, spowodowałoby punktu końcowego do używania protokołu HTTPS na porcie 44300 podczas pobrać plików ze źródła.

#### <a name="origin-host-header"></a>Nagłówek hosta źródła
**Nagłówka hosta źródła** jest wartość nagłówka hosta wysyłana do źródła z każdym żądaniem.  W większości przypadków ta powinna być taka sama jak **nazwę hosta źródła** możemy zweryfikować wcześniej.  Nieprawidłowa wartość w tym polu zwykle nie będzie powodować stany 404, ale może powodować innych stanów 4xx, w zależności od początkowego oczekuje.

#### <a name="origin-path"></a>Ścieżka do źródła
Ponadto możemy zweryfikować naszych **ścieżki źródła**.  Domyślnie to pole jest puste.  W tym polu należy używać tylko, jeśli chcesz zawęzić zakres hostowanej pochodzenia zasobów, które chcesz udostępnić w sieci CDN.  

Na przykład w Mój punkt końcowy miała wszystkich zasobów na moim koncie magazynu mają być dostępne, więc po lewej I **ścieżki źródła** puste.  Oznacza to, że żądanie `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` wyniki w połączeniu z mojego punktu końcowego `cdndocdemo.core.windows.net` który żąda `/publicblob/lorem.txt`.  Podobnie, żądanie `https://cdndocdemo.azureedge.net/donotcache/status.png` wynikiem żądania punktu końcowego `/donotcache/status.png` ze źródła.

Ale co zrobić, jeśli nie ma być użyty w sieci CDN dla każdej ścieżki na Moje źródła?  Powiedz I miał być użyty tylko do udostępnienia `publicblob` ścieżki.  Jeśli wprowadzić */publicblob* w mojej **ścieżki źródła** pola, który spowoduje, że punkt końcowy wstawić */publicblob* przed każde żądanie do źródła.  Oznacza to, że żądanie `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` teraz potrwa faktycznie żądania część adresu URL, `/publicblob/lorem.txt`i Dołącz `/publicblob` na początku. Powoduje to żądanie `/publicblob/publicblob/lorem.txt` ze źródła.  W przypadku tej ścieżki nie jest rozpoznawane jako rzeczywisty plik, punkt początkowy zwraca stanu 404.  Faktycznie będzie poprawny adres URL do pobrania lorem.txt w tym przykładzie `https://cdndocdemo.azureedge.net/lorem.txt`.  Należy pamiętać, że firma Microsoft nie zawierają */publicblob* ścieżki gwarancja, ponieważ żądanie część adresu URL jest `/lorem.txt` i dodaje punkt końcowy `/publicblob`, co `/publicblob/lorem.txt` żądanie przesyłane do źródła.

