---
title: "Obsługa udostępniania (CORS) zasobu pochodzenia aaaCross | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable Obsługa mechanizmu CORS hello usług magazynu Microsoft Azure."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Obsługa udostępniania zasobów między źródłami (CORS) hello usług magazynu Azure
Począwszy od wersji 2013-08-15, hello usług Azure storage obsługuje udostępniania zasobów między źródłami (CORS) hello usług obiektów Blob, tabeli, kolejki i plików. CORS jest funkcja HTTP, która umożliwia aplikacja sieci web w jednej domenie tooaccess zasobów w innej domenie. Przeglądarki sieci Web zaimplementować ograniczenia zabezpieczeń znany jako [zasad samego pochodzenia](http://www.w3.org/Security/wiki/Same_Origin_Policy) uniemożliwiający strony sieci web na podstawie wywoływania interfejsów API w innej domenie; Mechanizm CORS zapewnia bezpieczny sposób tooallow jednej domeny (domena pochodzenia hello) toocall interfejsów API w innej domenie. Zobacz hello [specyfikacji CORS](http://www.w3.org/TR/cors/) szczegółowe informacje dotyczące mechanizmu CORS.

Można ustawić zasady CORS osobno dla każdego hello usługi magazynu, wywołując [ustawić właściwości usługi Blob](https://msdn.microsoft.com/library/hh452235.aspx), [ustawić właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452232.aspx), i [ustawić właściwości usługi tabeli](https://msdn.microsoft.com/library/hh452240.aspx). Po ustawieniu hello zasady CORS usługi hello prawidłowo uwierzytelnione żądania dotyczącego usługi hello z innej domeny zostaną ocenione toodetermine czy jest dozwolone, zgodnie z toohello reguł, które określono.

> [!NOTE]
> Należy pamiętać, że CORS nie jest mechanizmem uwierzytelniania. Wszystkie żądania dla zasobu magazynu po włączeniu CORS muszą mieć podpisu właściwe uwierzytelnienie lub musi być dokonana przed publicznego zasobów.
> 
> 

## <a name="understanding-cors-requests"></a>Opis żądań CORPS
Żądanie CORS z domeny pochodzenia może składać się z dwóch oddzielnych żądania:

* Żądania wstępnego, który sprawdza hello CORS ograniczenia narzucone przez usługę hello. żądania wstępnego Hello jest wymagany, chyba że jest metoda żądania hello [prosta metoda](http://www.w3.org/TR/cors/), co oznacza, GET, HEAD lub POST.
* Hello rzeczywistego żądania, przed hello żądanego zasobu.

### <a name="preflight-request"></a>Żądania wstępnego
zapytania żądania wstępnego Hello hello ograniczenia CORS, które zostały utworzone przez właściciela konta hello hello usługi magazynu. przeglądarki sieci web Hello (lub agenta użytkownika) wysyła żądanie opcji, która zawiera nagłówki żądań hello, metody i pochodzenia domeny. Usługa Magazyn Hello ocenia operacji hello przeznaczone na podstawie zestawu wstępnie skonfigurowanych reguł CORS, które określić, które domeny pochodzenia, żądań metody, a następnie nagłówki żądania można określić rzeczywistego żądania względem zasobów magazynu.

Jeśli istnieje reguła CORS odpowiadający hello żądania wstępnego CORS jest włączone dla usługi hello, usługa hello odpowiedzi z kodem stanu 200 (OK) i obejmuje hello wymagane nagłówki kontroli dostępu w odpowiedzi hello.

Jeśli nie zasady CORS odpowiada hello żądania wstępnego CORS nie jest włączone dla usługi hello, usługa hello będzie odpowiadać z kodem stanu 403 (Dostęp zabroniony).

Jeśli opcje żądania nie zawiera hello hello wymagane nagłówki CORS (hello pochodzenia i nagłówki Access-Control-Request-Method), usługa hello będzie odpowiadać z kodem stanu 400 (nieprawidłowe żądanie).

Należy pamiętać, że żądania wstępnego zostaną ocenione względem usługi hello (obiektów Blob, kolejki i tabeli), a nie względem hello żądanego zasobu. Właściciel konta Hello najpierw włączyć CORS jako część właściwości usługi konta hello aby hello toosucceed żądania.

### <a name="actual-request"></a>Rzeczywistego żądania
Po zaakceptowaniu żądania wstępnego hello i hello odpowiedzi jest zwracany, przeglądarki hello wyśle hello rzeczywistego żądania względem hello zasobów magazynu. Przeglądarka Hello odmówi hello rzeczywistego żądania natychmiast Jeśli hello wstępnej żądanie zostanie odrzucone.

rzeczywistego żądania Hello jest traktowana jako normalne żądania dotyczącego hello usługi magazynu. obecność Hello hello źródła nagłówka wskazuje, że hello żądanie jest żądaniem CORS i usługa hello sprawdzi hello dopasowywania zasady CORS. W przypadku odnalezienia pasującego hello kontroli dostępu nagłówki są dodane toohello odpowiedzi i wysyłane wstecz toohello klienta. Jeśli nie, nie są zwracane hello nagłówki CORS Access-Control.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Włączanie mechanizmu CORS dla usługi Azure Storage hello
Zasady CORS są ustawione na poziomie usługi hello, dlatego należy tooenable lub wyłączenia CORS dla każdej usługi (obiektów Blob, kolejki i tabeli) oddzielnie. Domyślnie CORS jest wyłączone dla każdej usługi. tooenable CORS należy tooset hello odpowiednią usługę właściwości, za pomocą wersji 2013-08-15 lub nowszym i Dodaj właściwości usługi toohello zasady CORS. Aby uzyskać szczegółowe informacje o tym, jak tooenable lub wyłączenia CORS dla usługi oraz sposób tooset CORS zasady, należy odwoływać się za[ustawić właściwości usługi Blob](https://msdn.microsoft.com/library/hh452235.aspx), [ustawić właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452232.aspx), i [Tabela zestaw Właściwości usługi](https://msdn.microsoft.com/library/hh452240.aspx).

Poniżej przedstawiono przykładowe jednej zasady CORS określona za pomocą operacji ustawić właściwości usługi:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Poniżej opisano każdy element uwzględnione w regule CORS hello:

* **AllowedOrigins**: hello domeny pochodzenia, które są dozwolone toomake Żądanie hello magazynu usługi za pomocą mechanizmu CORS. domeny pochodzenia Hello jest hello domeny, z których hello pochodzi żądanie. Należy pamiętać, że hello źródła musi być identyczna z uwzględnieniem wielkości liter z pochodzenia hello hello wiek użytkownika i wysyła toohello usługi. Można również użyć znaku wieloznacznego hello ' *' tooallow wszystkie żądania toomake domeny pochodzenia za pomocą mechanizmu CORS. W powyższym przykładzie hello, hello domen [http://www.contoso.com](http://www.contoso.com) i [http://www.fabrikam.com](http://www.fabrikam.com) mogą wysyłać żądania usługi hello przy użyciu mechanizmu CORS.
* **AllowedMethods**: hello metody (zlecenia HTTP żądania) tej domeny pochodzenia hello mogą używać żądania CORS. W powyższym przykładzie hello dozwolone są tylko żądania PUT i GET.
* **AllowedHeaders**: hello nagłówki żądania może określać tej domeny pochodzenia hello na powitania CORS żądania. W powyższym przykładzie hello wszystkie nagłówki metadanych, począwszy od x-ms metadane x-ms-meta docelowego, a x-ms-meta-abc są dozwolone. Należy pamiętać, że wieloznacznego hello "*" wskazuje, że wszystkie nagłówka, począwszy od hello określić prefiks jest dozwolone.
* **ExposedHeaders**: hello nagłówki odpowiedzi, które mogą być wysyłane żądania CORS toohello odpowiedzi hello i udostępniane przez hello przeglądarki toohello żądania wystawcy. Przykład Witaj powyżej przeglądarki hello jest instrukcją tooexpose żadnych począwszy nagłówka x-ms-meta.
* **MaxAgeInSeconds**: hello maksymalną ilość czasu przeglądarki powinien buforowania przez żądania wstępnego opcje hello.

Witaj usług Azure storage obsługuje określanie prefiksem nagłówków dla obu hello **AllowedHeaders** i **ExposedHeaders** elementów. tooallow kategorii nagłówków, można określić typowe kategorii toothat prefiks. Na przykład określenie *x-ms-meta** jako nagłówek prefiksem Określa regułę, która będzie odpowiadała wszystkie nagłówki, które zaczynają się od x-ms-meta.

następujące ograniczenia Hello Zastosuj reguły tooCORS:

* Możesz określić się toofive zasad CORS dla usługi magazynowania (obiektu Blob, tabel i kolejek).
* Witaj maksymalny rozmiar wszystkich ustawień specyfikacji CORS reguł na żądanie hello, z wyłączeniem tagi XML nie może przekraczać 2 KB.
* Długość Hello nagłówku dozwolonych, narażonych nagłówka lub dozwolone pochodzenie nie może przekraczać 256 znaków.
* Dozwolone nagłówki i nagłówki narażonych mogą być:
  * Nagłówki literału, gdzie nazwa nagłówka dokładne hello podano, takich jak **x-ms-meta przetwarzane**. Można określić maksymalnie 64 literału nagłówki na powitania żądania.
  * Prefiks nagłówków, gdy prefiks nagłówka hello jest dostępne, takich jak **x-ms-meta-data***. Określenie prefiksu w ten sposób pozwala lub ujawnia żadnych nagłówek, który rozpoczyna się od hello podany prefiks. Można określić maksymalnie dwa nagłówki prefiksem na powitania żądania.
* Witaj metod (lub zlecenia HTTP) określona w hello **AllowedMethods** elementu musi być zgodna toohello metod obsługiwanych przez usługi Azure storage interfejsów API. Obsługiwane metody to DELETE, GET, HEAD, scalania, POST, opcje i PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Opis logiki oceny reguły CORS
Gdy usługa Magazyn odbiera żądanie dotyczące stanu wstępnego lub rzeczywistego, ocenia tego żądania na podstawie hello CORS reguł, które zostało ustanowione dla usługi hello za pośrednictwem hello odpowiednich operacji ustawić właściwości usługi. Zasady CORS są oceniane w kolejności hello, w którym zostały ustawione w treści żądania hello hello operacji ustawić właściwości usługi.

Zasady CORS są oceniane następująco:

1. Najpierw hello domeny pochodzenia żądania hello jest porównywany domen hello wymienionych dla hello **AllowedOrigins** elementu. Domeny pochodzenia hello znajduje się na liście hello, czy wszystkie domeny są dozwolone hello symbol wieloznaczny "*", następnie zasady oceny będzie kontynuowane. Jeśli nie dołączono hello domeny pochodzenia, hello żądanie kończy się niepowodzeniem.
2. Następnie metoda hello (lub zlecenie HTTP) żądania hello zostaje sprawdzony pod kątem metod hello wymienionych hello **AllowedMethods** elementu. Jeśli metoda hello jest uwzględniona w liście hello, będzie kontynuowana oceny zasad; Jeśli nie, Żądanie hello nie powiedzie się.
3. Jeśli Żądanie hello zgodny z regułą w jego domenie pochodzenia i jej metodę, tej reguły jest wybrany tooprocess hello żądania i nie dodatkowe reguły są sprawdzane. Przed żądania hello mogła zakończyć się pomyślnie, jednak wszelkie nagłówki określony w żądaniu hello są porównywane z nagłówków hello na liście hello **AllowedHeaders** elementu. Nagłówki hello wysyłane są niezgodne hello dozwolone nagłówki, hello żądanie kończy się niepowodzeniem.

Ponieważ hello reguły są przetwarzane w kolejności hello są obecne w treści żądania hello, najlepszym rozwiązaniem jest określenie się, że hello najbardziej restrykcyjne zasady z przestrzegania tooorigins najpierw na liście hello, dzięki czemu są one oceniane najpierw. Określ reguły, które są mniej restrykcyjnych — na przykład reguła tooallow wszystkie pochodzenia — w końcu hello hello listy.

### <a name="example--cors-rules-evaluation"></a>Przykład — CORS reguł oceny
Witaj poniższy przykład przedstawia treści żądania częściowe zasady CORS tooset operacji hello usług magazynu. Zobacz [ustawić właściwości usługi Blob](https://msdn.microsoft.com/library/hh452235.aspx), [ustawić właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452232.aspx), i [ustawić właściwości usługi tabeli](https://msdn.microsoft.com/library/hh452240.aspx) szczegółowe informacje dotyczące konstruowania żądania hello.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Następnie należy wziąć pod uwagę następujące żądań CORPS hello:

| Żądanie |  |  | Odpowiedź |  |
| --- | --- | --- | --- | --- |
| **— Metoda** |**Punkt początkowy** |**Nagłówki żądania** |**Reguła dopasowania** |**Wynik** |
| **UMIEŚĆ** |http://www.contoso.com |x-ms-blob-content-type |Pierwsza reguła |Powodzenie |
| **POBIERZ** |http://www.contoso.com |x-ms-blob-content-type |Drugą regułę |Powodzenie |
| **POBIERZ** |http://www.contoso.com |x-ms-client żądania id |Drugą regułę |Niepowodzenie |

pierwsze żądanie Hello zgodny z regułą pierwszy hello — domeny pochodzenia hello odpowiada hello dozwolone źródła, hello — metoda dopasowuje hello dozwolone metody i nagłówek hello odpowiada hello dozwolone nagłówki — i tak zakończy się pomyślnie.

Hello drugie żądanie nie pasuje hello pierwszej reguły, ponieważ metoda hello jest niezgodna z hello dozwolone metody. Jednak odpowiadać hello drugą regułę, dlatego próba powiedzie się.

Hello trzeci żądanie jest zgodne hello drugą regułę w jego domenie pochodzenia i metody, więc nie dodatkowe reguły są sprawdzane. Jednak hello *nagłówka x-ms-client żądania id* nie jest dozwolona przez hello drugą regułę, więc hello żądanie kończy się niepowodzeniem, pomimo faktu hello semantyki hello hello trzeci reguły będzie mieć możliwość go toosucceed.

> [!NOTE]
> Chociaż ten przykład przedstawia mniej restrykcyjnych reguł przed bardziej restrykcyjne jeden, ogólnie hello najlepszym rozwiązaniem jest najbardziej restrykcyjne zasady hello toolist najpierw.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Opis konfiguracji nagłówka Vary hello
Witaj *Vary* nagłówek jest standardowy nagłówek HTTP/1.1 zawierający zestaw pól nagłówka żądania, które zalecamy hello agenta przeglądarki lub użytkowników o kryteriach hello, które zostały wybrane na powitania serwera tooprocess hello żądanie. Witaj *Vary* nagłówka jest głównie używane do buforowania przez serwery proxy, przeglądarki i CDN, które używają jej toodetermine jak mają być buforowane odpowiedzi hello. Aby uzyskać więcej informacji, zobacz specyfikację hello na powitania [nagłówka Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Gdy hello przeglądarki lub innego agenta użytkownika buforuje hello odpowiedzi z żądania CORS, hello domeny pochodzenia są buforowane jako hello dozwolone pochodzenie. Gdy drugi problemów z domeną hello tego samego żądania dostarczenia zasobu magazynu, gdy hello pamięci podręcznej jest aktywny, agent użytkownika hello pobiera hello domeny pochodzenia pamięci podręcznej. Hello drugiej domeny nie pasuje hello domeny pamięci podręcznej, więc Żądanie hello nie powiedzie się, gdy go w przeciwnym razie powiedzie się. W niektórych przypadkach usługi Azure Storage ustawia Nagłówek Vary hello zbyt**pochodzenia** tooinstruct hello użytkownika toosend hello kolejnych CORS żądania toohello Usługa agenta kiedy hello żąda domeny różni się od hello buforowane pochodzenia.

Magazyn Azure ustawia hello *Vary* nagłówka zbyt**pochodzenia** do rzeczywistego żądania GET/HEAD w hello w następujących przypadkach:

* W przypadku żądania hello pochodzenia dokładnie odpowiada hello dozwolone pochodzenie zdefiniowana przez regułę CORS. toobe dokładnego dopasowania hello CORS reguły nie może zawierać symbol wieloznaczny "*" znaków.
* Nie istnieje żadne reguły dopasowywania hello żądanie danych pierwotnych, ale CORS jest włączone dla usługi magazynowania hello.

W przypadku hello gdzie żądania GET/HEAD zgodny z regułą CORS, który zezwala na wszystkie pochodzenia hello odpowiedź wskazuje, że wszystkie źródła są dozwolone i pamięci podręcznej agenta użytkownika hello umożliwi kolejnych żądań wysyłanych z dowolnej domeny pochodzenia, gdy hello pamięci podręcznej jest aktywny.

Należy zauważyć, że dla żądania za pomocą metod innych niż GET/HEAD, usług magazynu hello zostanie nie nagłówka Vary hello, ponieważ metody toothese odpowiedzi nie są obsługiwane przez agentów użytkownika.

Witaj poniższej tabeli przedstawiono sposób usługa Azure storage będzie odpowiadać na żądania tooGET/HEAD oparte na powitania wcześniej wspomniano przypadkach:

| Żądanie | Ustawienia konta i wyniki oceny reguły |  |  | Odpowiedź |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Nagłówek Origin na żądanie** |**Zasady CORS określony dla tej usługi** |**Istnieje reguła dopasowywania, która zezwala na wszystkie pochodzenia (*)** |**Istnieje reguła dopasowywania pochodzenia dokładnego dopasowania** |**Odpowiedź zawiera tooOrigin zestaw nagłówka Vary** |**Odpowiedź zawiera Access-Control-dozwolone-Origin: "*"** |**Odpowiedź zawiera Access-Control-widoczne-Headers** |
| Nie |Nie |Nie |Nie |Nie |Nie |Nie |
| Nie |Tak |Nie |Nie |Tak |Nie |Nie |
| Nie |Tak |Tak |Nie |Nie |Tak |Tak |
| Tak |Nie |Nie |Nie |Nie |Nie |Nie |
| Tak |Tak |Nie |Tak |Tak |Nie |Tak |
| Tak |Tak |Nie |Nie |Tak |Nie |Nie |
| Tak |Tak |Tak |Nie |Nie |Tak |Tak |

## <a name="billing-for-cors-requests"></a>Rozliczeń dla żądań CORS
Inspekcja pomyślnych żądań są rozliczane włączenie mechanizmu CORS dla usług magazynu hello konta (wywołując [ustawić właściwości usługi Blob](https://msdn.microsoft.com/library/hh452235.aspx), [ustawić właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452232.aspx), lub [ Ustaw właściwości usługi tabeli](https://msdn.microsoft.com/library/hh452240.aspx)). toominimize opłat, rozważ ustawienie hello **MaxAgeInSeconds** element z CORS zasady tooa duża wartość tak, aby hello agenta użytkownika buforuje żądania hello.

Niepomyślnych żądań wstępnych nie będą naliczane.

## <a name="next-steps"></a>Następne kroki
[Ustaw właściwości usługi Blob](https://msdn.microsoft.com/library/hh452235.aspx)

[Ustaw właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452232.aspx)

[Ustaw właściwości usługi tabel](https://msdn.microsoft.com/library/hh452240.aspx)

[W3C Cross-Origin Resource Sharing specyfikacji](http://www.w3.org/TR/cors/)

