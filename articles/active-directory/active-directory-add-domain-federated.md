---
title: "aaaAdd Twojego niestandardową nazwę domeny i konfigurowanie federacyjnego logowania tooAzure usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooadd firmy nazw domen tooset usługi Active Directory tooAzure się federacyjnego logowania między usługą Azure Active Directory i rozwiązania do federacyjnego lokalnej"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Dodaj użytkownika tooAzure nazwy domeny niestandardowej usługi Active Directory
Możesz skonfigurować niestandardową nazwę domeny, taką jak „contoso.com”, aby użytkownicy w contoso.com mogli mieć środowisko federacyjnego logowania jednokrotnego z sieci firmowej. Jeśli masz już Active Directory Federation Services (AD FS) lub serwer federacyjny innej działający w sieci firmowej, można skonfigurować usługi Azure AD toouse niestandardową nazwę domeny przy użyciu narzędzia Azure AD Connect hello. Można także użyć usługi Azure AD Connect środowiska toodeploy nowych usług AD FS i skonfigurować który dla federacyjnych pojedynczego logowania jednokrotnego tooAzure AD.

Jeśli nie masz i nie planujesz toodeploy usług AD FS lub inny serwer federacyjny, wykonaj te instrukcje: [tooAzure nazwy domeny niestandardowej usługi Active Directory dodać](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Dodaj katalog tooyour nazwy domeny niestandardowej
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu konta użytkownika, który jest administratorem globalnym katalogu usługi Azure AD.
2. W **usługi Active Directory**, otwórz katalog i wybierz hello **domen** kartę.
3. Na pasku poleceń hello, wybierz **Dodaj**, a następnie wprowadź nazwę hello domeny niestandardowe, takie jak "contoso.com". Należy się tooinclude hello .com, .net lub inne rozszerzenie najwyższego poziomu.
4. Wybierz hello **zaplanować tę domenę na potrzeby logowania jednokrotnego tooconfigure z mojej lokalnej usługi Active Directory** wyboru.
5. Wybierz pozycję **Dodaj**.

Uruchom wpis DNS hello tooget hello Azure AD Connect narzędzia tej usługi Azure AD będą używać tooverify hello domeny. Zobaczysz wpis DNS hello w hello **domenowych Azure AD** kroku w Kreatorze hello. Widać, jakie tego kroku w Kreatorze hello wygląda jak [w tych instrukcjach](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Jeśli nie masz hello Azure AD Connect narzędzia, możesz [go pobrać tutaj](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Dodaj wpis DNS hello na powitania rejestratora nazw domen dla domeny hello
Witaj następny krok toouse nazwy domeny niestandardowej z usługą Azure AD jest pliku strefy DNS hello tooupdate hello domeny. Dzięki temu tooverify usługi Azure AD, czy organizacja jest właścicielem hello niestandardowej nazwy domeny.

1. Zaloguj się toohello witryny sieci Web dla rejestratora nazw domen dla nazwy domeny. Jeśli nie masz dostępu toodo to, poproś o hello osobie lub zespołowi w organizacji, którzy mają ten krok toocomplete dostępu 2 i toolet, które znasz po jego ukończeniu.
2. Pliku strefy DNS hello aktualizacji dla domeny hello przez dodanie wpisu DNS hello tooyou są dostarczane przez usługę Azure AD. Ten wpis DNS umożliwia usłudze Azure AD tooverify prawa własności hello domeny. Witaj wpis DNS nie zmienia żadnych zachowań, takich jak routing poczty lub hosting sieci web.

Aby uzyskać pomoc dotyczącą tego kroku, przeczytaj [Instrukcje dotyczące dodawania wpisu DNS u popularnych rejestratorów DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Sprawdź nazwę domeny hello z usługą Azure AD
Po dodaniu wpisu DNS hello jest gotowy tooverify nazwy domeny hello z usługą Azure AD.

tooverify hello domeny, wybierz opcję **dalej** na powitania **domenowych Azure AD** kroku kreatora Połącz hello Azure AD. Usługi Azure AD będzie szukać hello wpis DNS w hello pliku strefy DNS dla domeny hello. Usługi Azure AD tylko Sprawdź nazwę domeny powitania po zostaną rozpropagowane hello rekordów DNS. Propagacja często zajmuje tylko kilka sekund, ale czasami może potrwać godzinę lub dłużej. Jeśli weryfikacja nie zadziała powitania po raz pierwszy, spróbuj ponownie później.

Następnie należy kontynuować hello pozostałe kroki w Kreatorze Azure AD Connect hello. Spowoduje to synchronizację użytkowników z programu Windows Server AD tooAzure AD. Zsynchronizowanych użytkowników w domenie hello, skonfigurowanego w Federacji, będzie możliwe tooget federacyjnego logowania jednokrotnego doświadczenia z sieci firmowej tooAzure AD.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj następujących hello. Zaczniemy hello najczęstszych i pracy w dół toohello najrzadziej występujących.

1. **Zaczekaj godzinę**. Rekordy DNS należy toopropagate przed usługi Azure AD można sprawdzić hello domeny. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, hello wprowadzono rekordu DNS i czy jest poprawna**. Wykonaj ten krok w witrynie sieci Web hello hello rejestratora nazw domen dla domeny hello. Usługi Azure AD nie można zweryfikować nazwy domeny hello, jeśli hello wpis DNS nie jest obecne w hello pliku strefy DNS, lub jeśli nie jest identyczna z wpisu DNS hello tej usługi Azure AD dostarczył. Jeśli nie masz dostępu tooupdate rekordów DNS domeny hello u rejestratora nazw domen hello, udostępniać wpis DNS hello hello osobie lub zespołowi w organizacji, którzy mają odpowiedni dostęp i poproś wpis DNS hello tooadd.
3. **Usuwanie nazwy domeny hello z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. odczytać toolearn o nazwach domen, usuwanie [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli organizacja używa wielu niestandardowych nazw domen, takich jak "contoso.com" "czy" contosobank.com ", można je sumują tooa maksymalnie 900 nazw domen. Użyj hello same kroki opisane w tym artykule tooadd każdego nazwa domeny.

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md)
* [Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD](active-directory-add-domain-concepts.md)
* [Wyświetlanie znakowania firmowego podczas logowania użytkowników](active-directory-add-company-branding.md)
* [Użyj nazwy domeny toomanage programu PowerShell w usłudze Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

