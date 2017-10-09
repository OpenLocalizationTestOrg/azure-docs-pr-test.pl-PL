---
title: "aaaCustom domen w serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Zarządzanie domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD, dlatego tego adresu URL hello aplikacji hello jest hello sama niezależnie od tego, gdzie użytkownicy do niego dostęp."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Praca z domenami niestandardowymi w serwera Proxy aplikacji usługi Azure AD

Podczas publikowania aplikacji za pośrednictwem serwera Proxy usługi Azure Active Directory aplikacji tworzenia zewnętrznego adresu URL dla Twojego toowhen toogo użytkowników, które działają w zdalnie. Ten adres URL pobiera hello domyślnej domeny *yourtenant.msappproxy.net*. Na przykład opublikowaniu aplikacji o nazwie kosztów dzierżawy jest o nazwie Contoso, a następnie hello zewnętrzny adres URL będzie https://expenses-contoso.msappproxy.net. Jeśli chcesz toouse z własnej nazwy domeny, skonfiguruj niestandardową domenę na potrzeby aplikacji. 

Zaleca się skonfigurowanie domeny niestandardowej dla aplikacji, jeśli to możliwe. Oto niektóre z zalet hello domen niestandardowych:

- Użytkowników można uzyskać toohello aplikacji hello sam adres URL, czy działają wewnątrz lub na zewnątrz sieci.
- Jeśli wszystkie aplikacje mają hello tych samych adresów URL wewnętrznych i zewnętrznych, linki w jednej aplikacji, które wskazują tooanother nadal toowork nawet spoza sieci firmowej hello. 
- Kontrolowanie znakowanie i tworzyć adresy URL hello ma. 


## <a name="configure-a-custom-domain"></a>Skonfigurować własną domenę niestandardową

### <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować domenę niestandardową, upewnij się, że jest możesz hello wymogów przygotowany: 
- A [tooAzure usługi Active Directory dodać zweryfikowanej domeny](active-directory-domains-add-azure-portal.md).
- Niestandardowe certyfikat dla domeny hello w formie hello pliku PFX. 
- Aplikację lokalną [opublikowana przy użyciu serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Skonfiguruj domenę niestandardową

Jeśli te wymagania trzy gotowy, wykonaj te kroki tooset się domeny niestandardowej:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Przejdź za**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** i wybierz polecenie aplikacji hello ma toomanage.
3. Wybierz **serwera Proxy aplikacji**. 
4. W polu zewnętrznego adresu URL hello Użyj tooselect listy rozwijanej hello domeny niestandardowej. Jeśli nie widzisz domeny na liście hello, następnie go nie zostało zweryfikowane jeszcze. 
5. Wybierz **Zapisz**
5. Witaj **certyfikatu** staje się aktywny pola, które zostało wyłączone. Zaznaczenie tego pola. 

   ![Kliknij przycisk tooupload certyfikatu](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Jeśli już przekazany certyfikat dla tej domeny, pole certyfikatu hello Wyświetla informacje o certyfikacie hello. 

6. Przekaż certyfikat PFX hello i podaj hasło hello hello certyfikatu. 
7. Wybierz **zapisać** toosave zmiany. 
8. Dodaj [rekord DNS](../dns/dns-operations-recordsets-portal.md) czy przekierowuje hello nowego adresu URL toohello msappproxy.net domeny zewnętrznej. 

>[!TIP] 
>Wystarczy tylko jeden certyfikat tooupload na domenę niestandardową. Po przekazaniu certyfikatu można hello domeny niestandardowej podczas publikowania nowej aplikacji i nie ma dodatkowych konfiguracji toodo z wyjątkiem rekordu DNS hello. 

## <a name="manage-certificates"></a>Zarządzanie certyfikatami

### <a name="certificate-format"></a>Format certyfikatu
Nie podlega ograniczeniom na powitania certyfikat podpisu metody. Obsługiwane są wszystkie kryptografii krzywej eliptycznej (ECC), alternatywnej nazwy podmiotu (SAN) i inne popularne typy certyfikatów. 

Można użyć certyfikatu symboli wieloznacznych, jak długo symbolu wieloznacznego hello odpowiada hello żądanego zewnętrznego adresu URL. 

Można używać certyfikatów z podpisem własnym, jak również. Jeśli używasz urzędu certyfikacji prywatnej hello punktu dystrybucji list CRL (punkt dystrybucji punktu odwołania certyfikatu) dla certyfikatu hello powinny być publiczne.

### <a name="changing-hello-domain"></a>Zmiana domeny hello
Wszystkie zweryfikowanych domen są wyświetlane na liście rozwijanej zewnętrznego adresu URL hello aplikacji. toochange hello domeny, tylko aktualizacji aplikacji hello do pola. Jeśli hello domeny, nie jest na liście hello [Dodaj go jako zweryfikowanej domeny](active-directory-domains-add-azure-portal.md). W przypadku wybrania domeny, która nie ma jeszcze certyfikatu skojarzonego wykonaj kroki 5-7 tooadd hello certyfikatu. Następnie upewnij się, że aktualizacja hello tooredirect rekordów DNS z hello nowego zewnętrznego adresu URL. 

### <a name="certificate-management"></a>Zarządzanie certyfikatami
Możesz użyć hello, które same certyfikatu dla wielu zastosowań, chyba że aplikacji hello udostępnianie hoście zewnętrznym. 

Zostanie wyświetlone ostrzeżenie po wygaśnięciu certyfikatu informujący tooupload innego certyfikatu za pośrednictwem portalu hello. Jeśli hello certyfikat został odwołany, użytkownicy mogą pojawić ostrzeżenie o zabezpieczeniach podczas uzyskiwania dostępu do aplikacji hello. Nie możemy wykonać sprawdzanie odwołań certyfikatów.  tooupdate hello certyfikat dla danej aplikacji, przejdź toohello aplikacji i wykonaj kroki 5-7 do konfigurowania domeny niestandardowe na tooupload opublikowanych aplikacji nowego certyfikatu. W przypadku hello stary certyfikat nie jest używany przez inne aplikacje, zostaną usunięte automatycznie. 

Obecnie wszystkie zarządzania certyfikatami jest stronach poszczególnych aplikacji warto toomanage certyfikaty w kontekście hello hello odpowiednie aplikacje. 

## <a name="next-steps"></a>Następne kroki
* [Włącz rejestrację jednokrotną](active-directory-application-proxy-sso-using-kcd.md) tooyour opublikowane aplikacje przy użyciu uwierzytelniania usługi Azure AD.
* [Włącz dostęp warunkowy](active-directory-application-proxy-conditional-access.md) tooyour opublikowane aplikacje.
* [Dodaj użytkownika domeny niestandardowej nazwy tooAzure AD](active-directory-domains-add-azure-portal.md)


