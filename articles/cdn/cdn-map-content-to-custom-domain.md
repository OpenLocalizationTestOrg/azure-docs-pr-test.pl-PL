---
title: "domeny niestandardowej zawartości tooa Azure CDN aaaMap | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomap Azure CDN zawartości tooa domeny niestandardowej."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Domena niestandardowa tooa zawartości mapy usługi Azure CDN
Możesz mapować punktu końcowego usługi CDN tooa domeny niestandardowej w kolejności toouse z własnej nazwy domeny w zawartości zamiast używania poddomeny azureedge.net toocached adresów URL.

Istnieją dwa sposoby toomap punktu końcowego CDN tooa domeny niestandardowej:

1. [Utwórz rekord CNAME u rejestratora domen i Mapowanie niestandardowych domen i poddomen toohello punktu końcowego CDN](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Rekord CNAME jest funkcją DNS, która mapuje domeny źródłowej, jak `www.contosocdn.com` lub `cdn.contoso.com`, tooa domeny docelowej. W takim przypadku domeny źródłowej hello jest Twoje niestandardowe domen i poddomen (poddomeny, takiej jak **www** lub **cdn** jest zawsze wymagane). Domena docelowego Hello jest punktu końcowego CDN.  
   
    proces Hello mapowanie punktu końcowego CDN tooyour domeny niestandardowej mogą jednak spowoduje przez krótki czas przestoju dla domeny hello podczas rejestrowania domeny hello w hello portalu Azure.
2. [Dodaj etap pośredni rejestracji z **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Jeśli domeny niestandardowej aktualnie obsługiwanych aplikacji przy użyciu umowy poziomu usług (SLA), który wymaga istnienia bez przestojów, a następnie użyć hello Azure **cdnverify** tooprovide poddomeny pośredniego rejestracji krok, dzięki czemu użytkownicy będą mogli tooaccess domeny podczas hello DNS mapowanie ma miejsce.  

Po zarejestrowaniu domeny niestandardowej przy użyciu jednej z hello powyżej procedury, można za[Sprawdź tego poddomeny niestandardowych hello odwołuje się do punktu końcowego CDN](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Należy utworzyć rekord CNAME z Twojej domeny Rejestrator toomap punktu końcowego CDN toohello domeny. Rekordy CNAME mapy określonych poddomen, takich jak `www.contoso.com` lub `cdn.contoso.com`. Nie jest możliwe toomap domena główna tooa rekordów CNAME, takich jak `contoso.com`.
> 
> Poddomeny może być skojarzony tylko z jednym punktem końcowym CDN. Witaj rekord CNAME, który utworzono będzie przekierowywać wszystkie ruchu kierowanego toohello poddomeny toohello określony punkt końcowy.  Na przykład, jeśli użytkownik jest kojarzony `www.contoso.com` z punktu końcowego CDN, możesz nie można powiązać go z innymi punkty końcowe systemu Azure, takich jak punkt końcowy konta magazynu lub punkt końcowy usługi w chmurze. Jednak można użyć różnych poddomen z hello tej samej domeny dla punktów końcowych innej usługi. Można również mapować toohello różnych domen podrzędnych tego samego punktu końcowego CDN.
> 
> Dla **Azure CDN from Verizon** punktów końcowych (Standard i Premium), należy pamiętać, że zajmuje on zbyt**90 minut** dla domeny niestandardowej zmieni toopropagate tooCDN krawędzi węzłów.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Zarejestruj domeny niestandardowej dla punktu końcowego usługi Azure CDN
1. Zaloguj się do hello [Azure Portal](https://portal.azure.com/).
2. Kliknij przycisk **Przeglądaj**, następnie **profilów usługi CDN**, następnie hello profilu CDN z punktem końcowym hello ma niestandardową domenę tooa toomap.  
3. W hello **profilu CDN** bloku, kliknij punkt końcowy CDN hello z którym ma zostać tooassociate hello poddomeny.
4. U góry bloku końcowego hello hello, kliknij przycisk hello **Dodawanie domeny niestandardowe** przycisku.  W hello **dodać niestandardową domenę** bloku, wyświetlana nazwa hosta punktu końcowego hello pochodzące z punktu końcowego CDN, toouse podczas tworzenia nowego rekordu CNAME. format Hello adres przypisany nazwie hosta hello będą wyświetlane jako  **&lt;EndpointName >. azureedge.net**.  Tworzenie rekordu CNAME hello można skopiować tego toouse nazwy hosta.  
5. Przejdź do witryny sieci web rejestratora domen tooyour, a następnie zlokalizuj hello sekcji do tworzenia rekordów DNS. Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).
6. Znajdź sekcję hello zarządzania CNAME. Może mieć toogo tooan Zaawansowane ustawienia strony i poszukaj słowa hello CNAME, aliasu lub poddomeny.
7. Utwórz nowy rekord CNAME mapujący z wybranym poddomeny (na przykład **www** lub **cdn**) toohello nazwy hosta dostarczone w hello **dodać niestandardową domenę** bloku. 
8. Zwraca toohello **dodać niestandardową domenę** bloku, a następnie wprowadź domenę niestandardową, w tym poddomeny hello, w oknie dialogowym hello. Na przykład wpisz nazwę domeny hello w formacie hello `www.contoso.com` lub `cdn.contoso.com`.   
   
   Azure sprawdzi, czy istnieje rekord CNAME powitania dla hello nazwy domeny, który został wprowadzony. Jeśli hello CNAME jest poprawny, domeny niestandardowej jest weryfikowana.  Aby uzyskać **Azure CDN from Verizon** punktów końcowych (Standard i Premium), może potrwać too90 minut dla domen niestandardowych ustawień toopropagate tooall CDN krawędzi węzłów, jednak.  
   
   Należy pamiętać, że w niektórych przypadkach go może trwać hello CNAME rekordów toopropagate tooname serwerów na powitania Internet. Jeśli domena nie została zweryfikowana natychmiast i uważasz, że hello rekord CNAME jest poprawna, zaczekaj kilka minut i spróbuj ponownie.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Zarejestruj domeny niestandardowej dla punktu końcowego usługi Azure CDN przy użyciu hello cdnverify pośredniczące poddomeny
1. Zaloguj się do hello [Azure Portal](https://portal.azure.com/).
2. Kliknij przycisk **Przeglądaj**, następnie **profilów usługi CDN**, następnie hello profilu CDN z punktem końcowym hello ma niestandardową domenę tooa toomap.  
3. W hello **profilu CDN** bloku, kliknij punkt końcowy CDN hello z którym ma zostać tooassociate hello poddomeny.
4. U góry bloku końcowego hello hello, kliknij przycisk hello **Dodawanie domeny niestandardowe** przycisku.  W hello **dodać niestandardową domenę** bloku, wyświetlana nazwa hosta punktu końcowego hello pochodzące z punktu końcowego CDN, toouse podczas tworzenia nowego rekordu CNAME. format Hello adres przypisany nazwie hosta hello będą wyświetlane jako  **&lt;EndpointName >. azureedge.net**.  Tworzenie rekordu CNAME hello można skopiować tego toouse nazwy hosta.
5. Przejdź do witryny sieci web rejestratora domen tooyour, a następnie zlokalizuj hello sekcji do tworzenia rekordów DNS. Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).
6. Znajdź sekcję hello zarządzania CNAME. Może mieć toogo tooan Zaawansowane ustawienia strony i wyszukaj słowa hello **CNAME**, **Alias**, lub **poddomen**.
7. Utwórz nowy rekord CNAME i podaj alias poddomeny, która obejmuje hello **cdnverify** poddomeny. Na przykład będzie poddomeny hello, którą można określić w formacie hello **cdnverify.www** lub **cdnverify.cdn**. Następnie podaj nazwę hosta hello, czyli punktu końcowego CDN, w formacie hello **cdnverify.&lt; EndpointName >. azureedge.net**. Mapowanie DNS powinien wyglądać podobnie jak:`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Zwraca toohello **dodać niestandardową domenę** bloku, a następnie wprowadź domenę niestandardową, w tym poddomeny hello, w oknie dialogowym hello. Na przykład wpisz nazwę domeny hello w formacie hello `www.contoso.com` lub `cdn.contoso.com`. Należy pamiętać, że w tym kroku, nie trzeba poddomeny hello toopreface z **cdnverify**.  
   
    Azure Sprawdź, czy istnieje rekord CNAME powitania dla nazwy domeny cdnverify hello, który został wprowadzony.
9. W tym momencie domeny niestandardowej została zweryfikowana przez platformę Azure, ale ruch tooyour domeny nie jest jeszcze routingiem tooyour punktu końcowego CDN. Po upływie toopropagate ustawienia wystarczająco długie tooallow hello domeny niestandardowej toohello CDN krawędzi węzłów (90 minut **Azure CDN from Verizon**, 1 – 2 minuty dla **Azure CDN from Akamai**), zwraca tooyour DNS Witryna sieci web rejestratora i utwórz inny rekord CNAME mapujący punktu końcowego CDN tooyour poddomeny. Na przykład określić poddomeny hello jako **www** lub **cdn**, i hello hostname jako  **&lt;EndpointName >. azureedge.net**. W ramach tego kroku rejestracji hello domeny niestandardowej jest ukończona.
10. Na koniec możesz usunąć rekord CNAME hello zostały utworzone za pomocą **cdnverify**, ponieważ konieczne było tylko jako etap pośredniczące.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Sprawdź, czy tej poddomeny niestandardowych hello odwołuje się do punktu końcowego CDN
* Po zakończeniu rejestracji hello domeny niestandardowej jest dostępna zawartość jest buforowana na punkt końcowy CDN przy użyciu hello domeny niestandardowej.
  Najpierw upewnij się, że masz zbuforowana w punkcie końcowym hello zawartości publicznej. Na przykład jeśli punkt końcowy CDN jest skojarzony z kontem magazynu, hello CDN buforuje zawartość w kontenerach publicznego obiektu blob. tootest hello domeny niestandardowej, upewnij się, że Twoje kontenera ustawiono tooallow dostępu publicznego i czy zawiera on co najmniej jednego obiektu blob.
* W przeglądarce Przejdź toohello adres obiektu blob hello przy użyciu hello domeny niestandardowej. Na przykład, jeśli domena niestandardowa jest `cdn.contoso.com`, hello adresu URL tooa pamięci podręcznej blob będzie podobne toohello następującego adresu URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Zobacz też
[Jak tooEnable hello sieci dostarczania zawartości (CDN) dla platformy Azure](cdn-create-new-endpoint.md)  

