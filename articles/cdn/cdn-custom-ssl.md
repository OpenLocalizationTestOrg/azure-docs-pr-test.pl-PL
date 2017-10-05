---
title: "Włącz protokół HTTPS na domenę niestandardową Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć protokół HTTPS na punkt końcowy usługi Azure CDN z domeny niestandardowej."
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
ms.openlocfilehash: b334ba6bbec1d0a7e23a514174bffae01c7fff05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-https-on-an-azure-cdn-custom-domain"></a>Włącz protokół HTTPS na domenę niestandardową Azure CDN

[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Obsługa protokołu HTTPS dla domen niestandardowych usługi Azure CDN umożliwia dostarczanie bezpieczne zawartości za pośrednictwem protokołu SSL w celu zwiększenia bezpieczeństwa danych podczas przesyłania przy użyciu nazwy domeny. Przepływ pracy end-to-end, aby włączyć protokół HTTPS dla domeny niestandardowej jest uproszczone, za pomocą jednego kliknięcia aktywacji, pełnego zarządzania certyfikatami i wszystkie bez dodatkowych kosztów.

Bardzo ważne dla zapewnienia prywatności i integralności danych z wszystkich aplikacji sieci web poufnych danych przesyłanych jest. Użycie protokołu HTTPS gwarantuje, że poufne dane są szyfrowane, gdy są wysyłane przez internet. Zapewnia zaufania, uwierzytelniania i chroni przed atakami aplikacji sieci web. Obecnie usługa Azure CDN obsługuje HTTPS na punktu końcowego usługi CDN. Na przykład w przypadku utworzenia punktu końcowego usługi CDN z usługi Azure CDN (np. https://contoso.azureedge.net), protokołu HTTPS jest włączona domyślnie. Teraz z domeny niestandardowej HTTPS, można włączyć bezpieczne dostarczanie dla domeny niestandardowej (np. https://www.contoso.com) oraz. 

Niektóre z kluczowych atrybutów funkcja HTTPS są:

- Bez dodatkowych kosztów: Brak nie koszty nabycia certyfikatu lub odnowienie i bez dodatkowych kosztów dla ruchu HTTPS. Po prostu płacisz za GB wyjście z sieci CDN.

- Włączanie prostego: jeden inicjowania obsługi kliknij przycisk jest dostępny z [portalu Azure](https://portal.azure.com). Aby włączyć tę funkcję, można użyć interfejsu API REST lub innych narzędzi dla deweloperów.

- Zakończenie zarządzania certyfikatami: wszystkie certyfikatów nabywania i zarządzania jest już obsługiwane. Certyfikaty są automatycznie udostępniane i odnowione przed jego wygaśnięciem. Usuwa to całkowicie ryzyka przerw w wyniku certyfikat wygasa.

>[!NOTE] 
>Przed włączeniem obsługi protokołu HTTPS, musi mieć już określone [domenę niestandardową Azure CDN](./cdn-map-content-to-custom-domain.md).

## <a name="step-1-enabling-the-feature"></a>Krok 1: Włączenie funkcji 

1. W [portalu Azure](https://portal.azure.com), przejdź do profilu sieci CDN w warstwie standardowa lub premium Verizon.

2. Na liście punktów końcowych kliknij punkt końcowy zawierający domenę niestandardową.

3. Kliknij przycisk domeny niestandardowej, dla którego chcesz włączyć protokół HTTPS.

    ![Blok końcowy](./media/cdn-custom-ssl/cdn-custom-domain.png)

4. Kliknij przycisk **na** Aby włączyć protokół HTTPS i zapisać zmiany.

    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/cdn-enable-custom-ssl.png)


## <a name="step-2-domain-validation"></a>Krok 2: Weryfikacja domeny

>[!IMPORTANT] 
>Należy ukończyć weryfikacji domeny na domenę niestandardową HTTPS będzie aktywny. Masz 6 dni roboczych, aby zatwierdzić domeny. Żądanie zostanie anulowane z zatwierdzaniem nie w ciągu 6 dni roboczych.  

Po włączeniu HTTPS na domenę niestandardową, naszych HTTPS dostawcę certyfikatów firmy DigiCert sprawdzi poprawność prawo własności do domeny, kontaktując się z rejestratorem domeny, na podstawie informacji rejestratorem WHOIS, za pośrednictwem poczty e-mail (domyślnie) lub telefonu. DigiCert również będzie wysyłać wiadomości e-mail weryfikacji do poniżej adresów. Jeśli prywatne informacje rejestratorem WHOIS, upewnij się, że możesz zatwierdzić bezpośrednio z jednego z tych adresów.

>Administrator @ administratora < name.com Twoja domena > @< name.com your domeny >  
>webmaster @< name.com your domeny >  
>hostmaster @< name.com your domeny >  
>Postmaster @< name.com your domeny >


Po odebraniu wiadomości e-mail, dostępne są dwie opcje weryfikacji:

1. Możesz zatwierdzać wszystkie przyszłe zamówień za pomocą tego samego konta dla tej samej domeny katalogu głównego, np. consoto.com. Jest to zalecane podejście, jeśli zamierzasz dodać dodatkowe domeny niestandardowe w przyszłości dla tej samej domeny głównej.
 
2. Możesz po prostu zatwierdzić nazwę określonego hosta używaną w tym żądaniu. Dodatkowe zatwierdzenie będzie wymagane dla kolejnych żądań.

    Przykład poczty e-mail:
    
    ![Niestandardowe okno protokołu HTTPS](./media/cdn-custom-ssl/domain-validation-email-example.png)

Po zatwierdzeniu żądania DigiCert doda niestandardową nazwę domeny certyfikat SAN. Certyfikat będzie ważny przez jeden rok i będą automatycznie odnawiane przed wygasła.

## <a name="step-3-wait-for-the-propagation-then-start-using-your-feature"></a>Krok 3: Poczekaj, aż propagacji, a następnie rozpocząć korzystanie z funkcji

Po zweryfikowaniu jest nazwą domeny upłynąć do 6-8 godzin dla domeny niestandardowej funkcji HTTPS jest aktywne. Po zakończeniu procesu stan "HTTPS niestandardowych" w portalu Azure będzie ustawiony na "Enabled". Protokół HTTPS z domeny niestandardowej jest teraz gotowy do użycia.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

1. *Kto jest dostawcę certyfikatów i jakiego typu używanego certyfikatu?*

    Używamy nazwy alternatywnej podmiotu (SAN) certyfikatu dostarczonego przez DigiCert. Certyfikat SAN można zabezpieczyć wiele nazw FQDN z jednym certyfikatem.

2. *Można użyć dedykowanego certyfikatu?*
    
    Aktualnie nie ale nie znajduje się na plan.

3. *Co zrobić, jeśli I nie otrzymywać wiadomości e-mail weryfikacji domeny firmy DigiCert?*

    Skontaktuj się z firmy Microsoft, jeśli użytkownik nie otrzyma wiadomość e-mail w ciągu 24 godzin.

4. *Używa mniej bezpieczna niż certyfikat dedykowanych certyfikat SAN?*
    
    Certyfikat SAN wykonuje szyfrowanie i zabezpieczenia standardach jako dedykowane certyfikatu. Wszystkie wystawiane certyfikaty SSL są za pomocą algorytmu SHA-256 rozszerzonego serwera zabezpieczeń.

5. *Można używać protokołu HTTPS domeny niestandardowej z usługą Azure CDN from Akamai?*

    Obecnie ta funkcja jest dostępna tylko z usługą Azure CDN from Verizon. Pracujemy nad Obsługa tej funkcji w programie Azure CDN from Akamai w najbliższych miesiącach.


## <a name="next-steps"></a>Następne kroki

- Dowiedz się, jak skonfigurować [niestandardową domenę na punkt końcowy usługi Azure CDN](./cdn-map-content-to-custom-domain.md)


