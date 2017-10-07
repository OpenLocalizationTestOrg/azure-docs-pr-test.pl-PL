---
title: aaaAdd tooAzure domeny niestandardowej AD | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak tooadd domeny niestandardowej w usłudze Azure Active Directory."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Szybki Start: Dodawanie tooAzure nazwy domeny niestandardowej usługi Active Directory

Każdy katalog usługi Azure AD jest dostarczany z początkową nazwę domeny w postaci hello *domainname*. onmicrosoft.com. hello początkowej nazwy domeny nie można zmienić ani usunąć, ale można dodać użytkownika domeny firmowej nazwa tooAzure AD również. Na przykład firma ma prawdopodobnie innych firm toodo nazw domeny i użytkowników, którzy Zaloguj się przy użyciu nazwy domeny firmowej. Dodawanie domeny niestandardowej nazwy tooAzure AD umożliwia nazwy użytkowników tooassign w katalogu hello, które są znane tooyour użytkowników, takich jak "alice@contoso.com." zamiast "Alicja @*<domain name>*. onmicrosoft.com". Witaj proces jest prosty:

1. Dodaj katalog tooyour nazwy domeny niestandardowej hello
2. Dodaj wpis DNS dla nazwy domeny hello u rejestratora nazw domen hello
3. Sprawdź hello niestandardowej nazwy domeny w usłudze Azure AD

## <a name="add-your-custom-domain"></a>Dodaj domenę niestandardową
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na powitania ***nazwa katalogu*** bloku, wybierz opcję **nazwy domen**.
4. Na powitania  ***nazwa katalogu* -nazwy domen** bloku, wybierz hello **Dodaj** polecenia.
   
   ![Polecenie Dodaj hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Na powitania **nazwy domeny** bloku, w polu hello, takie jak "contoso.com", należy wprowadzić nazwę hello domenę niestandardową, a następnie wybierz **Dodawanie domeny**. Należy się tooinclude hello .com, .net lub inne rozszerzenie najwyższego poziomu.
6. Na powitania ***nazwy domeny*** bloku (z niestandardowej nazwy domeny w tytule hello), Pobierz hello wpis DNS informacji toouse tooverify będącej własnością Twojej organizacji hello niestandardowej nazwy domeny.
   
   ![Pobierz informacje wpisu DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Jeśli planujesz toofederate lokalnego serwera z systemem Windows usługi Active Directory z usługą Azure AD, a następnie należy tooselect hello **zaplanować tę domenę na potrzeby logowania jednokrotnego tooconfigure z mojej lokalnej usługi Active Directory** pola wyboru po uruchomieniu narzędzia do hello Azure AD Connect toosynchronize katalogów. Należy również tooregister hello tej samej nazwy domeny, wybierz dla operacji federowania z katalogu lokalnego w hello **domenowych Azure AD** kroku w Kreatorze hello. Widać, jakie tego kroku w Kreatorze hello wygląda jak [w tych instrukcjach](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Jeśli nie masz hello Azure AD Connect narzędzia, możesz [go pobrać tutaj](http://go.microsoft.com/fwlink/?LinkId=615771).

Teraz, dodaniu nazwy domeny hello Azure AD należy sprawdzić, czy organizacja jest właścicielem nazwy domeny hello. Aby usługi Azure AD mogła przeprowadzić tę weryfikację, należy dodać wpis DNS w pliku strefy DNS hello hello nazwy domeny. To zadanie jest wykonywane na powitania witryny sieci Web dla rejestratora nazw domen dla nazwy domeny hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Dodaj wpis DNS hello na powitania rejestratora nazw domen dla domeny hello
Witaj następny krok toouse nazwy domeny niestandardowej z usługą Azure AD jest pliku strefy DNS hello tooupdate hello domeny. Usługi Azure AD można następnie sprawdź, czy organizacja jest właścicielem hello niestandardowej nazwy domeny.

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
4. Na powitania ***nazwy domeny*** bloku (to znaczy hello bloku, który otwiera mającą nazwę nowej domeny w tytule hello), wybierz **Sprawdź** toocomplete hello weryfikacji.

> [!TIP]
> Suma too900 niestandardowych nazw domen, ale może zawierać tylko jeden [Ustaw jako hello podstawowej nazwy domeny dla katalogu usługi Azure AD](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) używany domyślnie podczas tworzenia nowych kont.

Teraz można tworzyć konta użytkowników w chmurze lub aktualizacji poprzednio zsynchronizowanych lokalnych informacji o koncie użytkownika, przy użyciu niestandardowej nazwy domeny. Można również zmodyfikować uprzednio synchronizowane konta użytkownika domeny sufiks informacji przy użyciu [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) lub hello [interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli nie można zweryfikować niestandardowej nazwy domeny, spróbuj hello następujące kroki rozwiązywania problemów:

1. **Zaczekaj godzinę**. Rekordy DNS należy toopropagate przed usługi Azure AD można sprawdzić hello domeny. Propagacja może zająć godzinę lub dłużej.
2. **Upewnij się, hello wprowadzono rekordu DNS i czy jest poprawna**. Wykonaj ten krok w witrynie sieci Web hello hello rejestratora nazw domen dla domeny hello. Usługi Azure AD nie można zweryfikować nazwy domeny hello, jeśli hello wpis DNS nie jest obecne w hello pliku strefy DNS, lub jeśli nie jest identyczna z wpisu DNS hello tej usługi Azure AD dostarczył. Jeśli nie masz dostępu tooupdate rekordów DNS domeny hello u rejestratora nazw domen hello, udostępniać wpis DNS hello hello osobie lub zespołowi w organizacji, którzy mają odpowiedni dostęp i poproś wpis DNS hello tooadd.
3. **Usuwanie nazwy domeny hello z innego katalogu w usłudze Azure AD**. Nazwę domeny można weryfikować tylko w jednym katalogu. Jeśli nazwa domeny została zweryfikowana wcześniej w innym katalogu, musi zostać usunięta, zanim będzie ją można zweryfikować w nowym katalogu. odczytać toolearn o nazwach domen, usuwanie [Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Dodawanie niestandardowych nazw domen
Jeśli Twoja organizacja korzysta z więcej niż jedną nazwę domeny niestandardowe, takie jak "contoso.com" "czy" contosobank.com ", możesz dodać zapasowej too900 więcej powtarzając kroki hello w tym artykule dla każdego.

### <a name="learn-more"></a>Dowiedz się więcej
[Poglądowe omówienie niestandardowych nazw domen w usłudze Azure AD](active-directory-add-domain-concepts.md)

[Zarządzanie niestandardowymi nazwami domen](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Następne kroki
W tym szybkiego startu, kiedy znasz już jak tooadd tooAzure domeny niestandardowej AD. 

Możesz użyć powitania po tooadd łącze nowej domeny niestandardowej w usłudze Azure AD z hello portalu Azure.

> [!div class="nextstepaction"]
> [Dodaj domenę niestandardową](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 