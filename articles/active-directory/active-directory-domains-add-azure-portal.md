---
title: "aaaAdd nazwa domeny niestandardowej tooAzure usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooadd firmy nazw domen usługi Active Directory tooAzure i jak tooverify hello nazwy domeny."
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
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
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

Za pomocą usługi Azure Active Directory (Azure AD), można dodać użytkownika domeny firmowej nazwa tooAzure AD również. Może być nazwy domeny, możesz organizacji używa toodo biznesowe i użytkowników, którzy Zaloguj się przy użyciu nazwy domeny firmowej. Dodanie tooAzure nazwy domeny hello AD umożliwia nazwy użytkowników tooassign w katalogu hello, które są znane tooyour użytkowników, takich jak "alice@contoso.com." Witaj proces jest prosty:

1. Dodaj katalog tooyour nazwy domeny niestandardowej hello
2. Dodaj wpis DNS dla nazwy domeny hello u rejestratora nazw domen hello
3. Sprawdź hello niestandardowej nazwy domeny w usłudze Azure AD

## <a name="how-do-i-add-a-domain-name"></a>Jak dodać nazwę domeny?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na powitania ***nazwa katalogu*** bloku, wybierz opcję **nazwy domen**.
4. Na powitania  ***nazwa katalogu* -nazwy domen** bloku, wybierz hello **Dodaj** polecenia.
   
   ![Polecenie Dodaj hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Na powitania **nazwy domeny** bloku, w polu hello, takie jak "contoso.com", należy wprowadzić nazwę hello domenę niestandardową, a następnie wybierz **Dodawanie domeny**. Należy się tooinclude hello .com, .net lub inne rozszerzenie najwyższego poziomu.
6. Na powitania ***domainname*** bloku (to znaczy hello bloku, który otwiera mającą nazwę nowej domeny w tytule hello), Pobierz informacje wpis DNS hello że usługi Azure AD będzie używać tooverify będącej własnością Twojej organizacji hello niestandardowej nazwy domeny.
   
   ![Pobierz informacje wpisu DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Teraz, dodaniu nazwy domeny hello Azure AD należy sprawdzić, czy organizacja jest właścicielem nazwy domeny hello. Aby usługi Azure AD mogła przeprowadzić tę weryfikację, należy dodać wpis DNS w pliku strefy DNS hello hello nazwy domeny. To zadanie jest wykonywane na powitania witryny sieci Web dla rejestratora nazw domen dla nazwy domeny hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Dodaj wpis DNS hello na powitania rejestratora nazw domen dla domeny hello
Witaj następny krok toouse nazwy domeny niestandardowej z usługą Azure AD jest pliku strefy DNS hello tooupdate hello domeny. Dzięki temu tooverify usługi Azure AD, czy organizacja jest właścicielem hello niestandardowej nazwy domeny.

1. Zaloguj się toohello rejestratora nazw domen dla domeny hello. Jeśli nie masz dostępu tooupdate hello wpisu DNS, poproś o hello osobę lub zespół posiadający ten dostęp toocomplete krok 2 i toolet, które znasz po jego ukończeniu.
2. Pliku strefy DNS hello aktualizacji dla domeny hello przez dodanie wpisu DNS hello tooyou są dostarczane przez usługę Azure AD. Ten wpis DNS umożliwia usłudze Azure AD tooverify prawa własności hello domeny. Witaj wpis DNS nie zmienia żadnych zachowań, takich jak routing poczty lub hosting sieci web.

Aby uzyskać pomoc dotyczącą tego dodanie wpisu DNS hello, przeczytaj [instrukcje dotyczące dodawania wpisu DNS u popularnych rejestratorów DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Sprawdź nazwę domeny hello z usługą Azure AD
Po dodaniu wpisu DNS hello jest gotowy tooverify nazwy domeny hello z usługą Azure AD.

Nazwa domeny można sprawdzić tylko wtedy, gdy zostaną rozpropagowane hello rekordów DNS. Propagacja często zajmuje tylko kilka sekund, ale czasami może potrwać godzinę lub dłużej. Jeśli weryfikacja nie zadziała powitania po raz pierwszy, spróbuj ponownie później.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **Przeglądaj**, wprowadź w polu tekstowym hello Zarządzanie użytkownikami, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na powitania **Zarządzanie użytkownikami - nazwy domen** bloku, wybierz hello nazwa niezweryfikowanej domeny, które mają tooverify.
4. Na powitania ***domainname*** bloku (to znaczy hello bloku, który otwiera mającą nazwę nowej domeny w tytule hello), wybierz **Sprawdź** toocomplete hello weryfikacji.

Teraz możesz [przypisać nazwy użytkowników, które zawierają niestandardową nazwę domeny](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj następujących hello. Zaczniemy hello najczęstszych i pracy w dół toohello najrzadziej występujących.

1. **Zaczekaj godzinę**. Rekordy DNS należy toopropagate przed usługi Azure AD można sprawdzić hello domeny. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, hello wprowadzono rekordu DNS i czy jest poprawna**. Wykonaj ten krok w witrynie sieci Web hello hello rejestratora nazw domen dla domeny hello. Usługi Azure AD nie można zweryfikować nazwy domeny hello, jeśli hello wpis DNS nie jest obecne w hello pliku strefy DNS, lub jeśli nie jest identyczna z wpisu DNS hello tej usługi Azure AD dostarczył. Jeśli nie masz dostępu tooupdate rekordów DNS domeny hello u rejestratora nazw domen hello, udostępniać wpis DNS hello hello osobie lub zespołowi w organizacji, którzy mają odpowiedni dostęp i poproś wpis DNS hello tooadd.
3. **Usuwanie nazwy domeny hello z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. odczytać toolearn o nazwach domen, usuwanie [Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli organizacja używa wielu niestandardowych nazw domen, takich jak "contoso.com" "czy" contosobank.com ", można je sumują tooa maksymalnie 900 nazw domen. Użyj hello same kroki opisane w tym artykule tooadd każdego nazwa domeny.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md)

