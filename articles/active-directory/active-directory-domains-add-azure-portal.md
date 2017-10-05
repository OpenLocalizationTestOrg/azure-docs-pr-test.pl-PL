---
title: "Dodawanie niestandardowej nazwy domeny do usługi Azure Active Directory | Microsoft Docs"
description: "Jak dodać nazwy domeny firmy do usługi Azure Active Directory oraz jak zweryfikować nazwę domeny."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: ad72f768add7edc1d34a85c27dc2aa1b4e4b3a50
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

Za pomocą usługi Azure Active Directory (Azure AD), można dodać nazwę domeny firmowej do również usługi Azure AD. Może mieć nazwy domen, które możesz organizacja używa robić biznesowe i użytkowników, którzy Zaloguj się przy użyciu nazwy domeny firmowej. Dodawanie nazwy domeny do usługi Azure AD umożliwia przypisywanie nazw użytkowników w katalogu, które są znajome dla użytkowników, takich jak "alice@contoso.com." Proces jest prosty:

1. Dodawanie niestandardowej nazwy domeny do katalogu
2. Dodawanie wpisu DNS dla nazwy domeny w rejestratorze nazw domen
3. Weryfikowanie niestandardowej nazwy domeny w usłudze Azure AD

## <a name="how-do-i-add-a-domain-name"></a>Jak dodać nazwę domeny?
1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w polu tekstowym, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na ***nazwa katalogu*** bloku, wybierz opcję **nazwy domen**.
4. Na  ***nazwa katalogu* -nazwy domen** bloku, wybierz opcję **Dodaj** polecenia.
   
   ![Dodaj polecenie](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Na **nazwy domeny** bloku, wprowadź nazwę domeny niestandardowej w polu, takie jak "contoso.com", a następnie wybierz **Dodawanie domeny**. Należy uwzględnić rozszerzenie .com, .net lub inne rozszerzenie najwyższego poziomu.
6. Na ***domainname*** bloku (to znaczy bloku otwartym mającą nazwę nowej domeny w tytule), Pobierz informacje wpis DNS używanego usługi Azure AD można zweryfikować, czy organizacja jest właścicielem nazwy domeny niestandardowej.
   
   ![Pobierz informacje wpisu DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Teraz, po dodaniu nazwy domeny, usługa Azure AD musi sprawdzić, czy organizacja jest właścicielem nazwy domeny. Aby usługa Azure AD mogła przeprowadzić tę weryfikację, należy dodać wpis DNS w pliku strefy DNS dla nazwy domeny. To zadanie jest wykonywane w witrynie sieci Web u rejestratora nazw domen dla nazwy domeny.

## <a name="add-the-dns-entry-at-the-domain-name-registrar-for-the-domain"></a>Dodawanie wpisu DNS w rejestratorze nazw domen dla domeny
Następnym krokiem do korzystania z niestandardowej nazwy domeny w usłudze Azure AD jest zaktualizowanie pliku strefy DNS dla domeny. Umożliwi to usłudze Azure AD sprawdzenie, czy organizacja jest właścicielem niestandardowej nazwy domeny.

1. Zaloguj się do rejestratora nazw domen dla domeny. Jeśli nie masz dostępu potrzebnego do zaktualizowania wpisu DNS, poproś osobę lub zespół, którzy mają odpowiedni dostęp, o wykonanie kroku 2 i powiadomienie Cię o jego zakończeniu.
2. Zaktualizuj plik strefy DNS dla domeny, dodając wpis DNS udostępniony przez usługę Azure AD. Ten wpis DNS umożliwia usłudze Azure AD zweryfikowanie prawa własności do domeny. Ten wpis DNS nie zmienia żadnych zachowań, takich jak routing poczty lub hosting sieci Web.

Aby uzyskać pomoc dotyczącą dodawania wpisu DNS, przeczytaj [Instrukcje dotyczące dodawania wpisu DNS u popularnych rejestratorów DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-the-domain-name-with-azure-ad"></a>Weryfikowanie nazwy domeny w usłudze Azure AD
Po dodaniu wpisu DNS można przystąpić do weryfikowania nazwy domeny w usłudze Azure AD.

Nazwa domeny można sprawdzić tylko wtedy, gdy zostaną rozpropagowane rekordów DNS. Propagacja często zajmuje tylko kilka sekund, ale czasami może potrwać godzinę lub dłużej. Jeśli weryfikacja nie zadziała za pierwszym razem, spróbuj ponownie później.

1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **Przeglądaj**wprowadź Zarządzanie użytkownikami w polu tekstowym, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na **Zarządzanie użytkownikami - nazwy domen** bloku, wybierz nazwę niezweryfikowanej domeny, który chcesz zweryfikować.
4. Na ***domainname*** bloku (to znaczy bloku otwartym mającą nazwę nowej domeny w tytule), wybierz **Sprawdź** do zakończenia weryfikacji.

Teraz możesz [przypisać nazwy użytkowników, które zawierają niestandardową nazwę domeny](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj następujących rozwiązań. Zaczniemy od najczęstszych i skończymy na najrzadziej występujących.

1. **Zaczekaj godzinę**. Rekordy DNS muszą zostać poddane propagacji, aby usługa Azure AD mogła zweryfikować domenę. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, że wprowadzono rekord DNS i że jest on poprawny**. Ten krok należy wykonać w witrynie sieci Web u rejestratora nazw domen dla domeny. Usługa Azure AD nie może zweryfikować nazwy domeny, jeśli wpis DNS nie jest obecny w pliku strefy DNS lub jeśli nie jest identyczny z wpisem DNS udostępnionym użytkownikowi przez usługę Azure AD. Jeśli nie masz dostępu do aktualizowania rekordów DNS domeny w rejestrze nazw domen, udostępnij wpis DNS osobie lub zespołowi w organizacji, którzy mają taki dostęp, i poproś o dodanie wpisu DNS.
3. **Usuń nazwę domeny z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. Aby dowiedzieć się więcej na temat usuwania nazw domen, przeczytaj artykuł [Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli Twoja organizacja używa wielu niestandardowych nazw domen, takich jak „contoso.com” czy „contosobank.com”, możesz je dodać (maksymalnie 900 nazw domen). Dla każdej dodawanej nazwy domeny wykonaj kroki opisane w tym artykule.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md)

