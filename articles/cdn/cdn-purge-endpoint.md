---
title: "punkt końcowy usługi Azure CDN aaaPurge | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toopurge wszystkie buforowane zawartości z punktu końcowego usługi Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Przeczyszczanie punktu końcowego usługi Azure CDN
## <a name="overview"></a>Omówienie
Azure CDN krawędzi węzły będą buforowane zasoby, do momentu wygaśnięcia hello zasobu czas wygaśnięcia (TTL).  Po wygaśnięciu TTL hello zasobów, gdy klient żąda zawartości hello z węzłem krawędzi hello, węzłem krawędzi hello pobiera zaktualizowane nową kopię żądania hello zasobów tooserve powitania klienta i przechowywać odświeżania hello w pamięci podręcznej.

Witaj najlepsze praktyki toomake się, że użytkownicy zawsze uzyskać najnowszą kopię zasobów hello jest tooversion zasobów dla każdej aktualizacji i opublikujesz je jako nowego adresu URL.  CDN natychmiast pobierze hello nowych zasobów hello dalej żądań klientów.  Czasami warto zapoznać się z toopurge buforowanej zawartości z dowolnych węzłów edge i wymusić wszystkie tooretrieve nowe zasoby zaktualizowane.  Może to być aplikacji sieci web tooyour tooupdates lub tooquickly aktualizacji zasobów, które zawierają nieprawidłowe informacje.

> [!TIP]
> Należy pamiętać, że tylko przeczyszczanie czyści hello w pamięci podręcznej zawartości na serwerach krawędzi CDN hello.  Wszystkie podrzędne pamięci podręcznych, takich jak serwery proxy i pamięci podręcznej przeglądarki lokalnego, może nadal posiadają pamięci podręcznej kopię pliku hello.  Jest ważne tooremember to podczas ustawiania pliku time-to-live.  Możesz wymusić podrzędne klienta toorequest hello najnowszej wersji pliku przez nadanie mu unikatową nazwę za każdym razem, należy zaktualizować lub korzystając z [buforowanie ciągu zapytania](cdn-query-string.md).  
> 
> 

W tym samouczku przedstawiono przeczyszczanie zasoby ze wszystkich węzłów krawędzi punktu końcowego.

## <a name="walkthrough"></a>Przewodnik
1. W hello [Azure Portal](https://portal.azure.com), Przeglądaj profil CDN toohello zawierający punkt końcowy hello mają toopurge.
2. Z blok profilu CDN hello kliknij przycisk Wyczyść hello.
   
    ![Blok profilu CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    zostanie otwarty blok przeczyszczania Hello.
   
    ![Blok przeczyszczania CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Na powitania przeczyścić bloku, zaznacz adres usługi hello mają toopurge z hello adres URL z listy rozwijanej.
   
    ![Przeczyść formularza](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > Toohello przeczyszczania bloku można także uzyskać, klikając hello **przeczyścić** przycisk na blok punktu końcowego CDN hello.  W takim przypadku hello **adres URL** pole będzie wstępnie wypełniane adres usługi hello tego określonego punktu końcowego.
   > 
   > 
4. Wybierz, jakie zasoby mają toopurge z hello węzłów krawędzi.  Tooclear wszystkie zasoby, kliknij przycisk hello **Przeczyść wszystko** wyboru.  W przeciwnym razie wpisz ścieżkę hello każdego trwałego mają toopurge w hello **ścieżki** pola tekstowego. Poniżej formaty są obsługiwane w ścieżce hello.
    1. **Pojedynczy adres URL przeczyszczania**: czyszczenie poszczególnych zasobów, określając hello pełny adres URL, z lub bez hello rozszerzenie, np.`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Symbol wieloznaczny przeczyszczania**: gwiazdki (\*) może być używany jako symbol wieloznaczny. Wyczyść wszystkie foldery, podfoldery i pliki w obszarze punkt końcowy z `/*` w hello ścieżki lub przeczyścić wszystkie podfoldery i pliki w określonym folderze, określając folder hello następuje `/*`, np.`/pictures/*`.  Należy pamiętać, czyszczenie tego symbolu wieloznacznego nie jest obsługiwany przez usługi Azure CDN from Akamai obecnie. 
    3. **Przeczyszczanie domeny katalogu głównego**: główny hello przeczyszczenia punktu końcowego Witaj, "/" w ścieżce hello.
   
   > [!TIP]
   > Ścieżki musi być określona dla przeczyszczania i musi być względnym adresem URL, który mieści się następujące hello [wyrażenie regularne](https://msdn.microsoft.com/library/az24scfc.aspx). **Przeczyść wszystko** i **przeczyszczania symbolu wieloznacznego** nie są obsługiwane przez **Azure CDN from Akamai** obecnie.
   > > Pojedynczy adres URL przeczyszczenia`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Ciąg zapytania`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Symbol wieloznaczny przeczyszczania `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Więcej **ścieżki** pola tekstowe pojawią się po wprowadzeniu tooallow tekst toobuild lista wiele zasobów.  Zasoby można usunąć z listy hello, klikając przycisk wielokropka (...) hello.
   > 
5. Kliknij przycisk hello **przeczyścić** przycisku.
   
    ![Przeczyść przycisku](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Przeczyść żądań zająć około 2 – 3 minuty tooprocess z **Azure CDN from Verizon** (Standard i Premium), a około 7 minut z **Azure CDN from Akamai**.  Usługi Azure CDN ma limit współbieżnych 50 przeczyścić żądań w danym momencie. 
> 
> 

## <a name="see-also"></a>Zobacz też
* [Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN](cdn-preload-endpoint.md)
* [Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego](https://msdn.microsoft.com/library/mt634451.aspx)

