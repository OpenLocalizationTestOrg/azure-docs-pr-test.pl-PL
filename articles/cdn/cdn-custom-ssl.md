---
title: "AAA \"Włącz protokół HTTPS na domenę niestandardową Azure CDN | Dokumentacja firmy Microsoft\""
description: "Dowiedz się, jak tooenable HTTPS na punkt końcowy usługi Azure CDN z domeny niestandardowej."
services: cdn
documentationcenter: 
author: camsoper
manager: erikre
editor: 
ms.assetid: 10337468-7015-4598-9586-0b66591d939b
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: casoper
ms.openlocfilehash: 93746222616c9ed7977ec3b22c38ac1d43b118f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Włącz protokół HTTPS na domenę niestandardową Azure CDN

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Obsługa protokołu HTTPS dla domen niestandardowych usługi Azure CDN umożliwia bezpieczne zawartości za pośrednictwem protokołu SSL przy użyciu własnego domeny nazwa tooimprove hello bezpieczeństwa danych przesyłanych za toodeliver. Hello przepływu pracy na trasie tooenable HTTPS dla domeny niestandardowej jest uproszczone, za pomocą pełnego zarządzania certyfikatami, na jednym kliknięciem włączenie i wszystkie bez dodatkowych kosztów.

Jest krytyczne tooensure hello prywatność i integralność danych ze wszystkich aplikacji sieci web poufne dane przesyłane. Przy użyciu protokołu HTTPS gwarantuje, że poufne dane są szyfrowane, gdy są przesyłane przez hello hello internet. Zapewnia zaufania, uwierzytelniania i chroni przed atakami aplikacji sieci web. Obecnie usługa Azure CDN obsługuje HTTPS na punktu końcowego usługi CDN. Na przykład w przypadku utworzenia punktu końcowego usługi CDN z usługi Azure CDN (np. https://contoso.azureedge.net), protokołu HTTPS jest włączona domyślnie. Teraz z domeny niestandardowej HTTPS, można włączyć bezpieczne dostarczanie dla domeny niestandardowej (np. https://www.contoso.com) oraz. 

Atrybuty klucza hello funkcji HTTPS, należą:

- Bez dodatkowych kosztów: Brak nie koszty nabycia certyfikatu lub odnowienie i bez dodatkowych kosztów dla ruchu HTTPS. Płacisz tylko za wyjście GB z hello CDN.

- Włączanie prostego: jeden inicjowania obsługi kliknij jest dostępna z hello [portalu Azure](https://portal.azure.com). Można również użyć interfejsu API REST lub innych funkcji hello tooenable narzędzia developer.

- Zakończenie zarządzania certyfikatami: wszystkie certyfikatów nabywania i zarządzania jest już obsługiwane. Certyfikaty są automatycznie konfigurowani i odnowione przed tooexpiration. Usuwa to całkowicie hello ryzyko przerw w wyniku certyfikat wygasa.

>[!NOTE] 
>Obsługa protokołu HTTPS wcześniejsze tooenabling, musi mieć już określone [domenę niestandardową Azure CDN](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-hello-feature"></a>Krok 1: Włączenie funkcji hello 

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj tooyour Verizon standard lub premium profilu CDN.

2. Kliknij punkt końcowy hello zawierający domenę niestandardową na liście hello punktów końcowych.

3. Kliknij domenę niestandardową hello, dla której ma zostać tooenable HTTPS.

    ![Blok końcowy](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Kliknij przycisk **na** tooenable HTTPS i Zapisz zmiany hello.

    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Krok 2: Weryfikacja domeny

>[!IMPORTANT] 
>Należy ukończyć weryfikacji domeny na domenę niestandardową HTTPS będzie aktywny. Masz 6 firm dni tooapprove hello domeny. Żądanie zostanie anulowane z zatwierdzaniem nie w ciągu 6 dni roboczych.  

Po włączeniu HTTPS na domenę niestandardową, naszych HTTPS dostawcę certyfikatów firmy DigiCert sprawdzi poprawność prawo własności do domeny, kontaktując się z rejestratorem hello domeny, na podstawie informacji rejestratorem WHOIS, za pośrednictwem poczty e-mail (domyślnie) lub telefonu. DigiCert również będzie wysyłać hello weryfikacji e-mail toohello poniżej adresów. Jeśli prywatne informacje rejestratorem WHOIS, upewnij się, że możesz zatwierdzić bezpośrednio z jednego z tych adresów.

>Administrator @ administratora < name.com Twoja domena > @< name.com your domeny >  
>webmaster @< name.com your domeny >  
>hostmaster @< name.com your domeny >  
>Postmaster @< name.com your domeny >


Po odebraniu wiadomości e-mail hello, dostępne są dwie opcje weryfikacji:

1. Możesz zatwierdzać wszystkie przyszłe zamówień za pośrednictwem hello tego samego konta dla hello tej samej domeny katalogu głównego, np. consoto.com. Jest to zalecane podejście, jeśli planujesz tooadd dodatkowe domeny niestandardowe w przyszłości dla hello hello tej samej domeny katalogu głównego.
 
2. Możesz po prostu zatwierdzić hello określoną nazwę hosta używane w tym żądaniu. Dodatkowe zatwierdzenie będzie wymagane dla kolejnych żądań.

    Przykład poczty e-mail:
    
    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Po zatwierdzeniu żądania DigiCert doda certyfikat SAN toohello nazwy domeny niestandardowej. certyfikat Hello będzie ważny przez jeden rok i będą automatycznie odnawiane przed wygasła.

## <a name="step-3-wait-for-hello-propagation-then-start-using-your-feature"></a>Krok 3: Hello propagacji poczekać i rozpocząć korzystanie z funkcji

Po zweryfikowaniu jest nazwa domeny hello zajmuje too6 8 godzin dla active toobe funkcji HTTPS domeny niestandardowej hello. Po ukończeniu procesu hello stan "HTTPS niestandardowego" hello w portalu Azure hello zostanie ustawiona zbyt "Enabled". Protokół HTTPS z domeny niestandardowej jest teraz gotowy do użycia.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

1. *Kto jest hello dostawcę certyfikatów i jakiego typu używanego certyfikatu?*

    Używamy nazwy alternatywnej podmiotu (SAN) certyfikatu dostarczonego przez DigiCert. Certyfikat SAN można zabezpieczyć wiele nazw FQDN z jednym certyfikatem.

2. *Można użyć dedykowanego certyfikatu?*
    
    Aktualnie nie, ale jego na powitania plan.

3. *Co zrobić, jeśli nie pojawia się hello domeny weryfikacji w wiadomości e-mail od firmy DigiCert?*

    Skontaktuj się z firmy Microsoft, jeśli użytkownik nie otrzyma wiadomość e-mail w ciągu 24 godzin.

4. *Używa mniej bezpieczna niż certyfikat dedykowanych certyfikat SAN?*
    
    Certyfikat SAN się, że następujące hello standardach szyfrowania i zabezpieczeń jako dedykowane certyfikatu. Wszystkie wystawiane certyfikaty SSL są za pomocą algorytmu SHA-256 rozszerzonego serwera zabezpieczeń.

5. *Można używać protokołu HTTPS domeny niestandardowej z usługą Azure CDN from Akamai?*

    Obecnie ta funkcja jest dostępna tylko z usługą Azure CDN from Verizon. Pracujemy nad Obsługa tej funkcji w programie Azure CDN from Akamai w najbliższych miesiącach hello.


## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak tooset się [niestandardową domenę na punkt końcowy usługi Azure CDN](./cdn-map-content-to-custom-domain.md)


