---
title: "Dodawanie niestandardowej nazwy domeny do usługi Azure Active Directory | Microsoft Docs"
description: "Jak dodać nazwy domeny firmy do usługi Azure Active Directory oraz jak zweryfikować nazwę domeny."
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
ms.openlocfilehash: 0228bf7ce261cfccdec9431d3c9fb67f461eefbd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-custom-domain-name-to-azure-active-directory"></a>Dodawanie niestandardowej nazwy domeny do usługi Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-domains-add-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-add-domain.md)
> 
> 

Masz co najmniej jedną nazwę domeny, której organizacja używa do prowadzenia działalności, a użytkownicy logują się do sieci firmowej przy użyciu nazwy domeny firmowej. Teraz, gdy używasz usługi Azure Active Directory (Azure AD), możesz dodać nazwę domeny firmowej również do usługi Azure AD. Dzięki temu w katalogu można przypisać nazwy użytkowników znane użytkownikom, takie jak „alice@contoso.com”. Proces jest prosty:

1. Dodawanie niestandardowej nazwy domeny do katalogu
2. Dodawanie wpisu DNS dla nazwy domeny w rejestratorze nazw domen
3. Weryfikowanie niestandardowej nazwy domeny w usłudze Azure AD

> [!IMPORTANT]
> Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule. Jak dodać nazwę domeny firmowej w Centrum administracyjnym usługi Azure AD, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-domains-add-azure-portal.md).

Jeśli zamierzasz skonfigurować niestandardową nazwę domeny do użycia w sieci firmowej z usługami federacyjnymi Active Directory (AD FS) lub inną usługą tokenu zabezpieczającego (STS), wykonaj instrukcje podane w artykule dotyczącym [dodawania i konfigurowania domeny na potrzeby federacji w usłudze Azure Active Directory](active-directory-add-domain-federated.md). Jest to przydatne, jeśli planujesz zsynchronizować użytkowników z katalogu firmy z usługą Azure AD, a [synchronizacja skrótów haseł](active-directory-aadconnectsync-implement-password-synchronization.md) nie spełnia wymagań.

## <a name="add-a-custom-domain-name-to-your-directory"></a>Dodawanie niestandardowej nazwy domeny do katalogu
1. Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu konta użytkownika będącego administratorem globalnym katalogu usługi Azure AD.
2. W usłudze **Active Directory** otwórz katalog i wybierz kartę **Domeny**.
3. Na pasku poleceń wybierz pozycję **Dodaj**. Wprowadź nazwę domeny niestandardowej, na przykład „contoso.com”. Należy uwzględnić rozszerzenie .com, .net lub inne rozszerzenie najwyższego poziomu i pozostawić pole wyboru dla opcji „logowanie jednokrotne” (federacja) niezaznaczone.
4. Wybierz pozycję **Dodaj**.
5. Na drugiej stronie kreatora dodawania domeny uzyskaj wpis DNS, który będzie używany przez usługę Azure AD do weryfikowania, czy organizacja jest właścicielem niestandardowej nazwy domeny.

Teraz, po dodaniu nazwy domeny, usługa Azure AD musi sprawdzić, czy organizacja jest właścicielem nazwy domeny. Aby usługa Azure AD mogła przeprowadzić tę weryfikację, należy dodać wpis DNS w pliku strefy DNS dla nazwy domeny. To zadanie jest wykonywane w witrynie sieci Web u rejestratora nazw domen dla nazwy domeny.

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a>Dodawanie wpisu DNS w rejestratorze nazw domen dla domeny
Następnym krokiem do korzystania z niestandardowej nazwy domeny w usłudze Azure AD jest zaktualizowanie pliku strefy DNS dla domeny. Umożliwi to usłudze Azure AD sprawdzenie, czy organizacja jest właścicielem niestandardowej nazwy domeny.

1. Zaloguj się do rejestratora nazw domen dla domeny. Jeśli nie masz dostępu potrzebnego do zaktualizowania wpisu DNS, poproś osobę lub zespół, którzy mają odpowiedni dostęp, o wykonanie kroku 2 i powiadomienie Cię o jego zakończeniu.
2. Zaktualizuj plik strefy DNS dla domeny, dodając wpis DNS udostępniony przez usługę Azure AD. Ten wpis DNS umożliwia usłudze Azure AD zweryfikowanie prawa własności do domeny. Ten wpis DNS nie zmienia żadnych zachowań, takich jak routing poczty lub hosting sieci Web.

Aby uzyskać pomoc dotyczącą dodawania wpisu DNS, przeczytaj [Instrukcje dotyczące dodawania wpisu DNS u popularnych rejestratorów DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-the-domain-name-with-azure-ad"></a>Weryfikowanie nazwy domeny w usłudze Azure AD
Po dodaniu wpisu DNS można przystąpić do weryfikowania nazwy domeny w usłudze Azure AD.

Jeśli nadal masz otwarty kreator **Dodaj domenę**, wybierz opcję **Weryfikuj** na trzeciej stronie kreatora. Po wybraniu opcji **Weryfikuj** usługa Azure AD poszuka wpisu DNS w pliku strefy DNS dla domeny. Usługa Azure AD może zweryfikować nazwę domeny dopiero po wykonaniu propagacji rekordów DNS. Propagacja często zajmuje tylko kilka sekund, ale czasami może potrwać godzinę lub dłużej. Jeśli weryfikacja nie zadziała za pierwszym razem, spróbuj ponownie później.

Jeśli kreator **Dodaj domenę** nie jest nadal otwarty, można zweryfikować domenę w [klasycznym portalu Azure](https://manage.windowsazure.com/):

1. Zaloguj się przy użyciu konta użytkownika będącego administratorem globalnym katalogu usługi Azure AD.
2. Otwórz katalog i wybierz kartę **Domeny**.
3. Wybierz nazwę domeny, którą chcesz zweryfikować, a następnie na pasku poleceń wybierz pozycję **Weryfikuj**.
4. Wybierz pozycję **Weryfikuj** w oknie dialogowym, aby zakończyć weryfikację.

Teraz możesz [przypisać nazwy użytkowników, które zawierają niestandardową nazwę domeny](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj następujących rozwiązań. Zaczniemy od najczęstszych i skończymy na najrzadziej występujących.

1. **Zaczekaj godzinę**. Rekordy DNS muszą zostać poddane propagacji, aby usługa Azure AD mogła zweryfikować domenę. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, że wprowadzono rekord DNS i że jest on poprawny**. Ten krok należy wykonać w witrynie sieci Web u rejestratora nazw domen dla domeny. Usługa Azure AD nie może zweryfikować nazwy domeny, jeśli wpis DNS nie jest obecny w pliku strefy DNS lub jeśli nie jest identyczny z wpisem DNS udostępnionym użytkownikowi przez usługę Azure AD. Jeśli nie masz dostępu do aktualizowania rekordów DNS domeny w rejestrze nazw domen, udostępnij wpis DNS osobie lub zespołowi w organizacji, którzy mają taki dostęp, i poproś o dodanie wpisu DNS.
3. **Usuń nazwę domeny z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. Aby dowiedzieć się więcej na temat usuwania nazw domen, przeczytaj artykuł [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli Twoja organizacja używa wielu niestandardowych nazw domen, takich jak „contoso.com” czy „contosobank.com”, możesz je dodać (maksymalnie 900 nazw domen). Dla każdej dodawanej nazwy domeny wykonaj kroki opisane w tym artykule.

## <a name="next-steps"></a>Następne kroki
* [Przypisywanie nazw użytkowników, które zawierają niestandardową nazwę domeny](active-directory-add-domain-add-users.md)
* [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md)
* [Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD](active-directory-add-domain-concepts.md)
* [Wyświetlanie znakowania firmowego podczas logowania użytkowników](active-directory-add-company-branding.md)
* [Zarządzanie nazwami domen w usłudze Azure AD przy użyciu programu PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

