---
title: "zachowanie buforowania Azure CDN z ciągami zapytań - Premium aaaControl | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania Azure CDN buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Formant Azure CDN buforowanie z ciągami zapytań - Premium
> [!div class="op_single_selector"]
> * [Standardowa](cdn-query-string.md)
> * [Azure CDN Premium from Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Omówienie
Buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej ciągów zapytań.

> [!IMPORTANT]
> Witaj Standard i Premium CDN produkty zawierają hello zapytania takie same parametry funkcji buforowania, ale hello interfejs użytkownika różni się.  W tym dokumencie opisano interfejs hello **Azure CDN Premium from Verizon**.  Dla zapytania z buforowania ciągu **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań](cdn-query-string.md).
> 
> 

Dostępne są trzy tryby:

* **pamięć podręczna standard**: jest to tryb domyślny hello.  węzeł brzegowy CDN Hello przechodzą ciągu zapytania hello pochodzenia toohello obiektu żądającego hello na pierwsze Żądanie hello i zasobów hello pamięci podręcznej.  Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi hello zignoruje hello ciąg zapytania do momentu wygaśnięcia hello zasobów pamięci podręcznej.
* **pamięć podręczna nie**: W tym trybie żądań z ciągami zapytań nie są buforowane na węzeł brzegowy hello CDN.  węzeł brzegowy Hello pobiera hello zasobów bezpośrednio ze źródła hello i przekazuje ją obiektu żądającego toohello z każdym żądaniem.
* **Unikatowy pamięci podręcznej**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.  Na przykład Witaj odpowiedzi pochodzenia hello na żądanie dla *foo.ashx?q=bar* będą buforowane na węzeł brzegowy hello i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.  Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako zasób oddzielne ze swoim toolive czasie.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Zmiana ustawienia profilów sieci CDN w warstwie premium buforowanie ciągów zapytań
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.  Polecenie **buforowania ciągu kwerendy**.
   
    Opcje buforowania ciągu kwerendy są wyświetlane.
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. Po dokonaniu wyboru kliknij przycisk hello **aktualizacji** przycisku.

> [!IMPORTANT]
> zmiany ustawień Hello mogą nie być od razu widoczne, zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.  W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.
> 
> 

