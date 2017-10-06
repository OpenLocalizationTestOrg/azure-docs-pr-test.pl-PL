---
title: "wprowadzenie do usługi Azure CDN aaaGetting | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooenable hello Azure sieci dostarczania zawartości (CDN). Hello samouczek przeprowadza przez tworzenie hello nowy profil CDN i punktu końcowego."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Wprowadzenie do usługi Azure CDN
W tym temacie opisano włączanie usługi Azure CDN z tworzeniem nowego profilu i punktu końcowego usługi CDN.

> [!IMPORTANT]
> Wprowadzenie toohow CDN działa, a także listę funkcji, zobacz hello [Omówienie usługi CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Tworzenie nowego profilu CDN
Profil CDN jest kolekcją punktów końcowych usługi CDN.  Każdy profil zawiera jeden lub więcej punktów końcowych usługi CDN.  Możesz toouse wiele profilów tooorganize punktami końcowymi CDN według domeny internetowej, aplikacji sieci web lub innych kryteriów.

> [!NOTE]
> Domyślnie jedna subskrypcja platformy Azure jest ograniczona tooeight profilów usługi CDN. Każdy profil CDN jest ograniczony tooten punktów końcowych usługi CDN.
> 
> Cennik usługi CDN jest stosowany na poziomie profilu CDN hello. Jeśli chcesz toouse kombinację Azure CDN warstw cenowych, konieczne będzie wiele profilów CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Tworzenie nowego punktu końcowego usługi CDN
**toocreate nowy punkt końcowy CDN**

1. W hello [Azure Portal](https://portal.azure.com), przejdź tooyour profilu CDN.  Użytkownik może został on przypięty toohello pulpitu nawigacyjnego w poprzednim kroku hello.  Jeśli użytkownik nie, możesz go znaleźć, klikając **Przeglądaj**, następnie **profilów usługi CDN**, i klikając profil hello planujesz tooadd punkt końcowy.
   
    zostanie wyświetlony blok profilu CDN Hello.
   
    ![Profil CDN][cdn-profile-settings]
2. Kliknij przycisk hello **Dodawanie punktu końcowego** przycisku.
   
    ![Przycisk dodawania punktu końcowego][cdn-new-endpoint-button]
   
    Witaj **Dodawanie punktu końcowego** zostanie wyświetlony blok.
   
    ![Blok dodawania punktu końcowego][cdn-add-endpoint]
3. Wprowadź **nazwę** dla tego punktu końcowego usługi CDN.  Ta nazwa będzie używana tooaccess buforowanych zasobów w domenie hello `<endpointname>.azureedge.net`.
4. W hello **typ źródła** listy rozwijanej wybierz typ źródła.  Wybierz typ **Storage** dla konta usługi Azure Storage, **Usługa w chmurze** dla usługi Azure Cloud Service, **Web App** dla usługi Azure Web App lub **Źródło niestandardowe** dla każdego innego publicznie dostępnego źródła serwera sieci Web (hostowanego na platformie Azure lub gdziekolwiek indziej).
   
    ![Typ źródła usługi CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. W hello **nazwę hosta źródła** listy rozwijanej wybierz lub wpisz domenę źródła.  Witaj liście rozwijanej będą wyświetlane wszystkie dostępne źródła typu hello określonego w kroku 4.  W przypadku wybrania *Źródło niestandardowe* jako sieci **typ źródła**, zostanie tekst w domenie hello źródła niestandardowego.
6. W hello **ścieżki źródła** tekst Wprowadź hello ścieżki toohello zasoby, które chcesz toocache lub pozostaw puste tooallow w pamięci podręcznej dowolnego zasobu w domenie hello określonego w kroku 5.
7. W hello **nagłówka hosta źródła**, wprowadź nagłówek hosta hello ma hello toosend CDN z każdym żądaniem, lub pozostaw domyślną hello.
   
   > [!WARNING]
   > Niektóre typy źródeł, takich jak usługi Azure Storage i Web Apps, wymagają hello hosta nagłówka toomatch hello domeny pochodzenia hello. Jeśli nie masz źródło, które wymaga nagłówka hosta innego niż jego domena, należy pozostawić hello wartości domyślnej.
   > 
   > 
8. Dla **protokołu** i **port źródła**, określ hello protokoły i porty używane tooaccess zasobów hello pochodzenia.  Należy wybrać co najmniej jeden protokół (HTTP lub HTTPS).
   
   > [!NOTE]
   > Witaj **port źródła** wpływa tylko na jakie punktu końcowego hello portu informacje tooretrieve pochodzenia hello są używane.  Witaj sam punkt końcowy będzie tylko klientów tooend dostępne na powitania domyślne portach HTTP i HTTPS (80 i 443), niezależnie od hello **port źródła**.  
   > 
   > **Azure CDN from Akamai** punktów końcowych nie zezwalaj na powitania pełny zakres portów TCP dla źródeł.  Lista niedozwolonych portów źródłowych znajduje się w artykule [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Azure CDN from Akamai — dozwolone porty źródłowe).  
   > 
   > Uzyskiwanie dostępu do sieci CDN zawartości przy użyciu protokołu HTTPS ma hello następujące ograniczenia:
   > 
   > * Należy użyć hello certyfikatu SSL dostarczonego przez hello CDN. Certyfikaty innych firm nie są obsługiwane.
   > * Należy użyć domeny udostępnionej do sieci CDN hello (`<endpointname>.azureedge.net`) tooaccess zawartości HTTPS. Obsługa protokołu HTTPS nie jest dostępny dla niestandardowych nazw domen (rekordy CNAME), ponieważ w tej chwili hello CDN nie obsługuje niestandardowych certyfikatów.
   > 
   > 
9. Kliknij przycisk hello **Dodaj** toocreate przycisk hello nowy punkt końcowy.
10. Po utworzeniu punktu końcowego hello pojawia się na liście punktów końcowych dla profilu hello. Widok listy Hello pokazuje tooaccess toouse adres URL hello w pamięci podręcznej zawartości, a także domeny źródła hello.
    
    ![Punkt końcowy usługi CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > punkt końcowy Hello nie natychmiast będzie dostępny do użycia, jak zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.  W przypadku profilów usługi <b>Azure CDN from Akamai</b> propagacja zwykle zostanie ukończona w ciągu minuty.  W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.
    > 
    > Użytkownicy, którzy podejmą nazwy domeny usługi CDN hello toouse przed konfiguracji punktu końcowego hello zakończeniem propagacji toohello POP otrzymają kody odpowiedzi HTTP 404.  Jeśli od czasu utworzenia punktu końcowego minęło kilka godzin, a nadal otrzymujesz odpowiedzi 404, zapoznaj się z artykułem [Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Zobacz też
* [Kontrolowanie zachowania buforowania żądań z ciągami zapytań](cdn-query-string.md)
* [Jak tooa CDN zawartości tooMap domeny niestandardowe](cdn-map-content-to-custom-domain.md)
* [Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN](cdn-preload-endpoint.md)
* [Przeczyszczanie punktu końcowego usługi Azure CDN](cdn-purge-endpoint.md)
* [Rozwiązywanie problemów z punktami końcowymi usługi CDN zwracającymi stany 404](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
