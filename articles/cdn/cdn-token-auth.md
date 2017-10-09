---
title: "zasoby usługi Azure CDN aaaSecuring token uwierzytelniania | Dokumentacja firmy Microsoft"
description: "Korzystanie z uwierzytelniania tokenu toosecure dostępu tooyour Azure CDN zasobów."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Zabezpieczanie zasobów Azure CDN z tokenu uwierzytelniania

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Omówienie

Token uwierzytelniania jest mechanizm umożliwiający tooprevent Azure CDN z obsługiwać zasoby toounauthorized klientów.  Jest to zazwyczaj wykonywane tooprevent "hotlinking" zawartości, w których różne witryny sieci Web, często tablica wiadomości, używa zasobów bez uprawnienia.  Może to mieć wpływ na koszty dostarczania zawartości. Przez włączenie tej funkcji w sieci CDN w warstwie, żądania są uwierzytelniane przez krawędź CDN POP przed dostarczeniem zawartości hello. 

## <a name="how-it-works"></a>Jak to działa

Token uwierzytelniania sprawdza, czy żądania są generowane przez zaufanych witryn, gdyż toocontain żądania tokenu wartość zawierającą zakodowanego informacji na temat żądający hello. Zawartość będzie tylko udostępniania toorequester zakodowana hello informacji hello spełnianie wymagań, w przeciwnym razie żądania zostaną odrzucone. Można skonfigurować przy użyciu poniższych parametrów jednego lub wielu wymaganie hello.

- Kraju: akceptować lub odrzucać żądania, które pochodzą z określonego krajów.  [Lista poprawnych kodów kraju.](https://msdn.microsoft.com/library/mt761717.aspx) 
- Adres URL: Zezwalaj tylko na określony toorequest zasobów lub ścieżki.  
- Host: akceptować lub odrzucać żądania w nagłówku żądania hello przy użyciu określonych hostów.
- Odwołania: akceptować lub odrzucać toorequest określonego odwołania.
- Adres IP: Zezwalaj tylko na żądania, które pochodzą z określonego adresu IP lub podsieci IP.
- Zezwalaj na protokół: lub blokowanie żądań na podstawie protokołu hello używane toorequest hello zawartości.
- Czas wygaśnięcia: Przypisz datę i godzinę okresu tooensure, czy łącze tylko pozostaje ważny przez pewien czas.

Zobacz przykład szczegółowej konfiguracji poszczególnych parametrów.

## <a name="reference-architecture"></a>Architektura odwołań

Wymienione poniżej architektura referencyjna, konfigurowania token uwierzytelniania w sieci CDN toowork z aplikacji sieci Web.

![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Logikę weryfikacji tokenu na punkt końcowy CDN
    
Ten wykres opisano, jak Azure CDN weryfikuje żądanie klienta, gdy token uwierzytelniania jest skonfigurowane na punkt końcowy CDN.

![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Konfigurowanie uwierzytelniania tokenu

1. Z hello [portalu Azure](https://portal.azure.com), Przeglądaj profilu CDN tooyour, a następnie kliknij przycisk hello **Zarządzaj** przycisk toolaunch hello uzupełniające portalu.

    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Umieść kursor nad **HTTP dużych**, a następnie kliknij przycisk **Token uwierzytelniania** w wysuwane hello. Zostanie skonfigurowany klucz szyfrowania i szyfrowania parametrów na tej karcie.

    1. Wprowadź unikatowy klucz szyfrowania dla **klucz podstawowy**.  Wprowadź inny dla **kopii zapasowej klucza**

        ![Klucz tokenu uwierzytelniania CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Ustawianie parametrów szyfrowania za pomocą narzędzia szyfrowania (akceptować lub odrzucać żądania oparte na czas wygaśnięcia, kraj, odwołania, protokołu, adresu IP klienta. Można użyć dowolnej kombinacji.)

        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - WE-wygaśnie: przypisuje czas wygaśnięcia tokenu po upływie określonego czasu. Żądań przesłanych po czas wygaśnięcia hello będą odrzucane. Sygnatura czasowa Unix używa tego parametru (oparte na sekund od standardowego epoka 1/1/1970 GMT 00:00:00. Można użyć narzędzia online tooprovide konwersji między czasem Unix a (czas standardowy).)  Na przykład, jeżeli chcesz tooset zapasowe wygasł hello token toobe na 12/31 grudnia 2016 r. 12:00:00 GMT, użyj czasu Unix hello: 1483185600 zgodnie z poniższymi instrukcjami:
    
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - Zezwalaj adresu url WE: pozwala tootailor tokenów tooa konkretnego trwałego lub ścieżki. Ogranicza ona zakres toorequests dostępu, którego adres URL rozpoczynać się od określonej ścieżki względnej. Można wprowadzić wiele ścieżek, oddzielając każda ścieżka przecinkami. Adresy URL jest rozróżniana wielkość liter. W zależności od wymagań hello można skonfigurować różne wartości tooprovide różne poziomy dostępu. Poniżej przedstawiono kilka scenariuszy:
        
            Jeśli adres URL: http://www.mydomain.com/pictures/city/strasbourg.png. Zobacz wartości wejściowej "" i jego dostęp na poziomie odpowiednio

            1. Wartość wejściowa "/": wszystkie żądania będą dozwolone
            2. Wartość wejściowa "/ obrazy": umożliwi hello wszystkie następujące żądania
            
                - http://www.myDomain.com/Pictures.PNG
                - http://www.myDomain.com/Pictures/City/Strasbourg.PNG
                - http://www.myDomain.com/picturesnew/City/strasbourgh.PNG
            3. Wprowadź wartość "/ obrazy /": tylko żądania dla /pictures/ będą dozwolone
            4. Wartość wejściowa "/ pictures/city/strasbourg.png": tylko zezwala na żądania dla tego zasobu
    
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - Zezwalaj kraju WE: zezwala tylko na żądania, które pochodzą z co najmniej jeden określony krajów. Żądania, które pochodzą z innych krajów zostaną odrzucone. Użyj tooset kod kraju hello parametrów i oddzielając każdy kod kraju przecinkami. Na przykład jeśli chcesz tooallow dostępu w Stanach Zjednoczonych i Francja wejściowe nam FR w kolumnie hello jako poniżej.  
        
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - Odmów kraju WE: odrzucanie żądań pochodzących z jednego lub więcej określonych krajów. Może być żądań pochodzących z innych krajów. Użyj tooset kod kraju hello parametrów i oddzielając każdy kod kraju przecinkami. Na przykład jeśli chcesz toodeny dostępu w Stanach Zjednoczonych i Francja wejściowe nam FR w kolumnie hello.
    
        - Zezwalaj ref WE: tylko zezwala na żądania pochodzące z określonej odwołania. Odwołania identyfikuje hello adres URL strony sieci web hello połączonego zasobu toohello żądanej. wartość parametru odwołania Hello nie powinny zawierać hello protokołu. Można wprowadzić nazwę hosta i/lub określonej ścieżki na tej nazwy hosta. Można również dodać wiele odwołań w jeden parametr, oddzielając każdy z nich przecinkami. Jeśli podano wartość odwołania, ale hello odwołania informacje nie są wysyłane w żądaniu hello ukończenia konfiguracji przeglądarki toosome, te żądania zostaną odrzucone domyślnie. Można przypisać "Brak" lub wartość pusta w tooallow parametru hello te żądania z brakującymi informacji odwołania. Można również użyć "*. consoto.com" tooallow wszystkich poddomen consoto.com.  Na przykład jeśli chcesz tooallow dostępu dla żądań z www.consoto.com, wszystkimi domenami podrzędnymi w consoto2.com i erquests z pustą lub brak reffers wartość wejściowa jest poniżej:
        
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - Odmów ref WE: odrzucanie żądań z określonego odwołania. Znajdują się toodetails i przykład w parametrze "WE ref — Zezwalaj".
         
        - Zezwalaj proto WE: zezwala tylko na żądania od wybranego protokołu. Na przykład http lub https.
        
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - Odmów proto WE: odrzucanie żądań z wybranego protokołu. Na przykład http lub https.
    
        - we clientip: ogranicza dostęp toospecified żądającego adresu IP. Obsługiwane są protokoły IPV4 i IPV6. Można określić pojedyncze żądanie adresu IP lub podsieci IP.
            
        ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Można przetestować token hello wywieranych przez narzędzie.

    4. Można również dostosować hello typu odpowiedzi, który zostanie zwrócony toouser gdy żądanie zostanie odrzucone. Domyślnie używamy 403.

3. Teraz kliknij **aparatu reguł** w obszarze **HTTP dużych**. Spowoduje funkcja ta karta toodefine ścieżki tooapply hello, włączyć funkcję uwierzytelniania tokenu hello i włączenie możliwości związane z dodatkowego uwierzytelniania tokenu.

    - Użyj zasobów toodefine kolumny "IF" lub ścieżki, które mają tooapply tokenu uwierzytelniania. 
    - Kliknij przycisk tooadd "Token uwierzytelniania" z hello funkcji listy rozwijanej tooenable tokenu uwierzytelniania.
        
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. W hello **aparatu reguł** jest kilka dodatkowych możliwości, możesz włączyć.
    
    - Token uwierzytelniania odmowa kodu: Określa typ hello odpowiedzi, który zostanie zwrócony toouser po odrzuceniu żądania. Reguł ustawionych w tym miejscu zastępuje ustawienie kodu odmowa hello hello karcie tokenu uwierzytelniania.
    - Ignoruj token uwierzytelniania: Określa, czy token toovalidate adres URL używany będzie uwzględniana wielkość liter.
    - Parametr tokenu uwierzytelniania: Zmień nazwę parametru ciągu przedstawiający w hello żądanego adresu URL zapytania token uwierzytelniania hello. 
        
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Można dostosować z tokenem, który jest aplikacja, która generuje token dla funkcji uwierzytelniania opartego na tokenie. Kod źródłowy jest dostępny w tym miejscu w [GitHub](https://github.com/VerizonDigital/ectoken).
Dostępne języki:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Azure CDN funkcji i cenach dostawcy

Zobacz hello [Omówienie usługi CDN](cdn-overview.md) tematu.
