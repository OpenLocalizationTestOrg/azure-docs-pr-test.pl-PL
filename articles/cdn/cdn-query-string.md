---
title: "zachowanie buforowania Azure CDN z ciągami zapytań aaaControl | Dokumentacja firmy Microsoft"
description: "Ciąg zapytania Azure CDN buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Formant Azure CDN buforowanie z ciągami zapytań
> [!div class="op_single_selector"]
> * [Standardowa](cdn-query-string.md)
> * [Azure CDN Premium from Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Omówienie
Buforowanie kontroli, jak pliki są toobe, które zawierają ciągi zapytań w pamięci podręcznej ciągów zapytań.

> [!IMPORTANT]
> Witaj Standard i Premium CDN produkty zawierają hello zapytania takie same parametry funkcji buforowania, ale hello interfejs użytkownika różni się.  W tym dokumencie opisano interfejs hello **Azure CDN Standard from Akamai** i **Azure CDN Standard from Verizon**.  Dla zapytania z buforowania ciągu **Azure CDN Premium from Verizon**, zobacz [kontrolowanie zachowania buforowania CDN żądań z ciągami zapytań - Premium](cdn-query-string-premium.md).
> 
> 

Dostępne są trzy tryby:

* **Ignorować ciągi kwerendy**: jest to tryb domyślny hello.  węzeł brzegowy CDN Hello przechodzą ciągu zapytania hello pochodzenia toohello obiektu żądającego hello na pierwsze Żądanie hello i zasobów hello pamięci podręcznej.  Wszystkie kolejne żądania dla tego zasobu, które są obsługiwane z węzłem krawędzi hello zignoruje hello ciąg zapytania do momentu wygaśnięcia hello zasobów pamięci podręcznej.
* **Pomiń buforowanie adresu URL z ciągami zapytań**: W tym trybie żądań z ciągami zapytań nie są buforowane na węzeł brzegowy hello CDN.  węzeł brzegowy Hello pobiera hello zasobów bezpośrednio ze źródła hello i przekazuje ją obiektu żądającego toohello z każdym żądaniem.
* **Buforuj każdy unikatowy adres URL**: w tym trybie traktuje każde żądanie zawierające ciąg zapytania jako unikatowy zasób ze swojej własnej pamięci podręcznej.  Na przykład Witaj odpowiedzi pochodzenia hello na żądanie dla *foo.ashx?q=bar* będą buforowane na węzeł brzegowy hello i zwrócony dla kolejnych pamięci podręcznych z tym samym ciągu zapytania.  Żądanie *foo.ashx?q=somethingelse* będzie buforowana jako zasób oddzielne ze swoim toolive czasie.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Zmiana ustawienia profilów sieci CDN w warstwie standardowa buforowanie ciągów zapytań
1. Blok profilu CDN hello kliknij punkt końcowy CDN hello mają toomanage.
   
    ![Punkty końcowe blok profilu CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    zostanie otwarty blok punktu końcowego CDN Hello.
2. Kliknij przycisk hello **Konfiguruj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    zostanie otwarty blok konfiguracji CDN Hello.
3. Wybierz ustawienie z hello **zachowanie buforowania ciągu kwerendy** listy rozwijanej.
   
    ![Opcje buforowania ciągu kwerendy CDN](./media/cdn-query-string/cdn-query-string.png)
4. Po dokonaniu wyboru kliknij przycisk hello **zapisać** przycisku.

> [!IMPORTANT]
> zmiany ustawień Hello mogą nie być od razu widoczne, zajmuje trochę czasu hello toopropagate rejestracji za pomocą hello CDN.  W przypadku profilów usługi <b>Azure CDN from Akamai</b> propagacja zwykle zostanie ukończona w ciągu minuty.  W przypadku profilów usługi <b>Azure CDN from Verizon</b> propagacja zwykle zostanie ukończona w ciągu 90 minut, ale niekiedy może to zająć więcej czasu.
> 
> 

