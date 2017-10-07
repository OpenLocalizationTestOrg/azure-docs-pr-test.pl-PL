---
title: "aaaAdd nazwa domeny niestandardowej tooAzure usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooadd firmy nazw domen usługi Active Directory tooAzure i jak tooverify hello nazwy domeny."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Dodaj tooAzure nazwy domeny niestandardowej usługi Active Directory
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-domains-add-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-add-domain.md)
> 
> 

Masz co najmniej jedną nazwę domeny Twoja organizacja korzysta z toodo biznesowych, czy użytkownicy logują się tooyour sieci firmowej przy użyciu nazwy domeny firmowej. Teraz, gdy używasz usługi Azure Active Directory (Azure AD), można dodać użytkownika domeny firmowej nazwa tooAzure AD również. Dzięki temu można nazwy użytkowników tooassign w katalogu hello, które są znane tooyour użytkowników, takich jak "alice@contoso.com." Witaj proces jest prosty:

1. Dodaj katalog tooyour nazwy domeny niestandardowej hello
2. Dodaj wpis DNS dla nazwy domeny hello u rejestratora nazw domen hello
3. Sprawdź hello niestandardowej nazwy domeny w usłudze Azure AD

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać tooadd nazwę domeny firmowej w Centrum administracyjnym hello Azure AD, zobacz temat [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-domains-add-azure-portal.md).

Jeśli planujesz tooconfigure Twojego toobe nazwy domeny niestandardowej używane z usługi Active Directory Federation Services (AD FS) lub innej usługi tokenu zabezpieczającego (STS) w sieci firmowej, postępuj zgodnie z instrukcjami hello [Dodaj i skonfiguruj domeny Federacja z usługą Azure Active Directory](active-directory-add-domain-federated.md). Jest to przydatne, jeśli planujesz toosynchronize użytkowników z sieci firmowej katalogu tooAzure AD, a [synchronizacji skrótów haseł](active-directory-aadconnectsync-implement-password-synchronization.md) nie spełnia wymagań.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Dodaj katalog tooyour nazwy domeny niestandardowej
1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu konta użytkownika, który jest administratorem globalnym katalogu usługi Azure AD.
2. W **usługi Active Directory**, otwórz katalog i wybierz hello **domen** kartę.
3. Na pasku poleceń hello, wybierz **Dodaj**. Wprowadź nazwę hello domenę niestandardową, takie jak "contoso.com". Upewnij się, tooinclude hello .com, .net lub inne rozszerzenie najwyższego poziomu i hello wyboru dla "Logowanie jednokrotne" wyczyszczone (federacyjnych).
4. Wybierz pozycję **Dodaj**.
5. Na powitania drugiej stronie kreatora Dodawanie domeny hello Pobierz hello wpisu DNS, które będą używane przez usługi Azure AD tooverify będącej własnością Twojej organizacji hello niestandardowej nazwy domeny.

Teraz, dodaniu nazwy domeny hello Azure AD należy sprawdzić, czy organizacja jest właścicielem nazwy domeny hello. Aby usługi Azure AD mogła przeprowadzić tę weryfikację, należy dodać wpis DNS w pliku strefy DNS hello hello nazwy domeny. To zadanie jest wykonywane na powitania witryny sieci Web dla rejestratora nazw domen dla nazwy domeny hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Dodaj wpis DNS hello na powitania rejestratora nazw domen dla domeny hello
Witaj następny krok toouse nazwy domeny niestandardowej z usługą Azure AD jest pliku strefy DNS hello tooupdate hello domeny. Dzięki temu tooverify usługi Azure AD, czy organizacja jest właścicielem hello niestandardowej nazwy domeny.

1. Zaloguj się toohello rejestratora nazw domen dla domeny hello. Jeśli nie masz dostępu tooupdate hello wpisu DNS, poproś o hello osobę lub zespół posiadający ten dostęp toocomplete krok 2 i toolet, które znasz po jego ukończeniu.
2. Pliku strefy DNS hello aktualizacji dla domeny hello przez dodanie wpisu DNS hello tooyou są dostarczane przez usługę Azure AD. Ten wpis DNS umożliwia usłudze Azure AD tooverify prawa własności hello domeny. Witaj wpis DNS nie zmienia żadnych zachowań, takich jak routing poczty lub hosting sieci web.

Aby uzyskać pomoc dotyczącą tego dodanie wpisu DNS hello, przeczytaj [instrukcje dotyczące dodawania wpisu DNS u popularnych rejestratorów DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Sprawdź nazwę domeny hello z usługą Azure AD
Po dodaniu wpisu DNS hello jest gotowy tooverify nazwy domeny hello z usługą Azure AD.

Jeśli nadal masz hello **Dodaj domenę** po otwarciu kreatora wybierz opcję **Sprawdź** na trzeciej stronie kreatora hello hello. Po wybraniu **Sprawdź**, usługi Azure AD będzie szukać hello wpis DNS w hello pliku strefy DNS dla domeny hello. Usługi Azure AD można zweryfikować nazwy domeny hello tylko wtedy, gdy zostaną rozpropagowane hello rekordów DNS. Propagacja często zajmuje tylko kilka sekund, ale czasami może potrwać godzinę lub dłużej. Jeśli weryfikacja nie zadziała powitania po raz pierwszy, spróbuj ponownie później.

Jeśli hello **Dodaj domenę** kreatora nie jest jeszcze otwarty, można zweryfikować domeny hello w hello [klasycznego portalu Azure](https://manage.windowsazure.com/):

1. Zaloguj się przy użyciu konta użytkownika będącego administratorem globalnym katalogu usługi Azure AD.
2. Otwórz z katalogu i zaznacz hello **domen** kartę.
3. Nazwa domeny wybierz hello mają tooverify, a następnie wybierz **Sprawdź** na powitania paska poleceń.
4. Wybierz **Sprawdź** hello okna dialogowego pole toocomplete hello weryfikacji.

Teraz możesz [przypisać nazwy użytkowników, które zawierają niestandardową nazwę domeny](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj następujących hello. Zaczniemy hello najczęstszych i pracy w dół toohello najrzadziej występujących.

1. **Zaczekaj godzinę**. Rekordy DNS należy toopropagate przed usługi Azure AD można sprawdzić hello domeny. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, hello wprowadzono rekordu DNS i czy jest poprawna**. Wykonaj ten krok w witrynie sieci Web hello hello rejestratora nazw domen dla domeny hello. Usługi Azure AD nie można zweryfikować nazwy domeny hello, jeśli hello wpis DNS nie jest obecne w hello pliku strefy DNS, lub jeśli nie jest identyczna z wpisu DNS hello tej usługi Azure AD dostarczył. Jeśli nie masz dostępu tooupdate rekordów DNS domeny hello u rejestratora nazw domen hello, udostępniać wpis DNS hello hello osobie lub zespołowi w organizacji, którzy mają odpowiedni dostęp i poproś wpis DNS hello tooadd.
3. **Usuwanie nazwy domeny hello z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. odczytać toolearn o nazwach domen, usuwanie [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli organizacja używa wielu niestandardowych nazw domen, takich jak "contoso.com" "czy" contosobank.com ", można je sumują tooa maksymalnie 900 nazw domen. Użyj hello same kroki opisane w tym artykule tooadd każdego nazwa domeny.

## <a name="next-steps"></a>Następne kroki
* [Przypisywanie nazw użytkowników, które zawierają niestandardową nazwę domeny](active-directory-add-domain-add-users.md)
* [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md)
* [Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD](active-directory-add-domain-concepts.md)
* [Wyświetlanie znakowania firmowego podczas logowania użytkowników](active-directory-add-company-branding.md)
* [Użyj nazwy domeny toomanage programu PowerShell w usłudze Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

