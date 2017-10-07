---
title: "zasoby aaaPre obciążenia dla punktu końcowego usługi Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak obciążenia toopre buforowanej zawartości dla punktu końcowego usługi Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Wstępne ładowanie zasobów w punkcie końcowym usługi Azure CDN
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Domyślnie zasoby najpierw są buforowane, ponieważ są one wymagane. Oznacza to, że hello pierwsze żądanie z każdego regionu może trwać dłużej, ponieważ serwery krawędzi hello nie będą mieć hello zawartość w pamięci podręcznej i będzie konieczne serwera pochodzenia toohello tooforward hello żądania. Wstępnego ładowania zawartości pozwala uniknąć ten pierwszy opóźnienia trafień.

Ponadto tooproviding lepsze środowisko klienta wstępne ładowanie pamięci podręcznej zasobów pomaga również zmniejszyć ruch sieciowy na powitania serwera źródłowego.

> [!NOTE]
> Wstępne ładowanie zasobów jest przydatne w przypadku dużych zdarzenia lub zawartości, która staje się jednocześnie dostępne tooa dużą liczbę użytkowników, takich jak nowe wydanie filmu lub aktualizacji oprogramowania.
> 
> 

W tym samouczku przedstawiono wstępnego ładowania zawartości w pamięci podręcznej na wszystkich węzłach krawędzi Azure CDN.

## <a name="walkthrough"></a>Przewodnik
1. W hello [Azure Portal](https://portal.azure.com), Przeglądaj profil CDN toohello zawierający punkt końcowy hello mają toopre obciążenia.  zostanie otwarty blok profilu Hello.
2. Kliknij punkt końcowy hello hello na liście.  zostanie otwarty blok końcowy Hello.
3. W bloku punktu końcowego CDN hello przycisk hello obciążenia.
   
    ![Blok punktu końcowego CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    zostanie otwarty blok obciążenia Hello.
   
    ![Blok obciążenia CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Wprowadź pełną ścieżkę hello każdego trwałego mają tooload (np. `/pictures/kitten.png`) w hello **ścieżki** pola tekstowego.
   
   > [!TIP]
   > Więcej **ścieżki** pola tekstowe pojawią się po wprowadzeniu tooallow tekst toobuild lista wiele zasobów.  Zasoby można usunąć z listy hello, klikając przycisk wielokropka (...) hello.
   > 
   > Ścieżki musi być względnym adresem URL, która pasuje do następujących hello [wyrażenia regularnego](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Załadować ścieżki pojedynczy plik `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Załaduj pojedynczy plik z ciągu zapytania`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Każdego zasobu musi mieć własny ścieżkę.  Nie ma żadnych funkcji symboli wieloznacznych dla wstępnego ładowania zasobów.
   > 
   > 
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Kliknij przycisk hello **obciążenia** przycisku.
   
    ![Przycisk obciążenia](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Istnieje ograniczenie 10 obciążenia żądań na minutę na profilu CDN. 50 ścieżek są dozwolone na żądanie. Każda ścieżka ma limit długość ścieżki 1024 znaków.
> 
> 

## <a name="see-also"></a>Zobacz też
* [Przeczyszczanie punktu końcowego usługi Azure CDN](cdn-purge-endpoint.md)
* [Azure dokumentacji interfejsu API REST usługi CDN - przeczyścić lub wstępnie załadować punktu końcowego](https://msdn.microsoft.com/library/mt634451.aspx)

