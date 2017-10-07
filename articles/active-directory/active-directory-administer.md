---
title: "toouse aaaHow Przegląd katalogu dzierżawy usługi Azure Active Direcory | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, co to jest dzierżawa usługi Azure AD i w jaki sposób toomanage Azure przy użyciu usługi Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Zarządzanie swoim katalogiem usługi Azure AD

## <a name="what-is-an-azure-ad-tenant"></a>Co to jest dzierżawa usługi Azure AD?
W usłudze Azure Active Directory (Azure AD) dzierżawa to dedykowane wystąpienie katalogu usługi Azure AD, które otrzymuje organizacja po zarejestrowaniu w usłudze firmy Microsoft w chmurze, takiej jak Azure lub Office 365. Każdy katalog usługi Azure AD jest odrębny i oddzielony od innych katalogów usługi Azure AD. Podobnie jak budynek biurowy jest tooonly określonych zabezpieczonym zasobem organizacji, katalog usługi Azure AD został również toobe zaprojektowany jako zabezpieczony zasób do użytku tylko Twojej organizacji. Hello architektury usługi Azure AD izoluje informacje danymi i tożsamością klienta, dzięki czemu użytkownicy i Administratorzy jednego katalogu usługi Azure AD nie przypadkowego lub umyślnego dostęp do danych w innym katalogu.

![Zarządzanie usługą Azure Active Directory](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Jak mogę uzyskać katalog usługi Azure AD?
Usługa Azure AD zapewnia hello core katalogami i tożsamościami, możliwości zarządzania bazuje większość usług w chmurze firmy Microsoft, w tym:

* Azure
* Usługa Microsoft Office 365
* Usługa Microsoft Dynamics CRM Online
* Microsoft Intune

Katalog usługi Azure AD uzyskujesz, gdy tworzysz konto w ramach dowolnej z tych usług w chmurze firmy Microsoft. W razie potrzeby możesz utworzyć dodatkowe katalogi. Na przykład możesz zachować pierwszy katalog jako katalog produkcyjny i utworzyć kolejny na potrzeby testowania lub wdrażania przejściowego.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Przy użyciu katalogu usługi Azure AD hello dostarczanego z nową subskrypcją platformy Azure

Zaleca się, że używasz konta administratora hello używanego dla pierwszej usługi po utworzeniu konta dla innych usług firmy Microsoft. Hello informacje podane w hello po raz pierwszy tworzenia konta usługi firmy Microsoft jest używane toocreate nowej usługi Azure AD wystąpienie katalogu dla organizacji. Jeśli używasz, że katalog tooauthenticate prób zalogowania przy subskrybowaniu tooother usług firmy Microsoft, mogą używać hello istniejących kont użytkowników, zasady, ustawienia lub Integracja katalogu lokalnego skonfigurowanych w katalogu domyślnym.

Na przykład, jeśli logujesz się na subskrypcję Microsoft Intune i następnie dalsze synchronizacji lokalnej usługi Active Directory z katalogiem Azure AD, można założyć dla innej usługi firmy Microsoft, takich jak Office 365 i łatwo osiągnąć hello tym samym katalogu korzyści integracji wyposażonych w usłudze Microsoft Intune.

Aby uzyskać więcej informacji na temat integracji Twojego lokalnego katalogu z usługą Azure AD, zobacz [Directory integration with Azure AD Connect](active-directory-aadconnect.md) (Integracja katalogu z usługą Azure AD Connect).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Kojarzenie istniejącego katalogu usługi Azure AD z nową subskrypcją platformy Azure
Możesz skojarzyć nową subskrypcję platformy Azure z hello tym samym katalogu, który uwierzytelnia logowanie dla istniejącej subskrypcji usługi Office 365 lub Microsoft Intune. Aby uzyskać więcej informacji dotyczących tego scenariusza, zobacz [przeniesienia własności tooanother konta subskrypcji platformy Azure](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Tworzenie katalogu usługi Azure AD przez utworzenie konta w usłudze w chmurze firmy Microsoft jako organizacja
Jeśli nie masz jeszcze tooa subskrypcji usługi w chmurze firmy Microsoft, można użyć jednego hello kontynuacji toosign łącza. Rejestracja w pierwszej usłudze spowoduje automatyczne utworzenie katalogu usługi Azure AD.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Jak toochange hello domyślnym katalogiem dla subskrypcji

1. Zaloguj się toohello [Centrum konta platformy Azure](https://account.windowsazure.com/Home/Index) z konta, które hello administratora konta posiadania subskrypcji tootransfer hello w subskrypcji.
2. Upewnij się, tym hello użytkownika, który ma się, że właściciel subskrypcji hello toobe znajduje się w katalogu hello docelowe.
3. Kliknij pozycję **Przenieś subskrypcję**.
4. Określ adresata hello. Adresat Hello automatycznie otrzymuje wiadomość e-mail z łączem akceptacji.
5. Hello odbiorca kliknie hello link i jest zgodna z instrukcji hello, łącznie z wprowadzania ich informacje dotyczące płatności. Podczas odbiorcy hello zakończy się powodzeniem, jest przenoszona hello subskrypcji. 
6. Witaj hello subskrypcji zostanie zmieniony katalog domyślny katalog toohello hello użytkownika jest w przypadku przeniesienia własności subskrypcji hello zakończy się pomyślnie.

### <a name="manage-hello-default-directory-in-azure"></a>Zarządzanie hello domyślny katalog na platformie Azure
Kiedy rejestrujesz się na platformie Azure, domyślny katalog usługi Azure AD jest kojarzony z Twoją subskrypcją. Korzystanie z usługi Azure AD nie wiąże się z żadnymi kosztami, a Twoje katalogi są bezpłatnym zasobem. Istnieją płatne usługi Azure AD, które są licencjonowane osobno i udostępniają dodatkowe funkcje, takie jak oznaczanie marką firmy podczas logowania i samoobsługowe resetowanie hasła. Można również utworzyć domenę niestandardową przy użyciu własnej nazwy DNS, zamiast domyślnej hello *. onmicrosoft.com domeny.

## <a name="how-can-i-manage-directory-data"></a>Jak mogę zarządzać danymi w katalogu?
tooadminister jeden lub więcej Microsoft subskrypcje usług w chmurze, można użyć hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com), hello portal konta Microsoft Intune lub hello [Centrum administracyjne usługi Office 365](https://portal.office.com/) toomanage Twojego dane katalogu organizacji. Można również użyć [poleceń cmdlet programu PowerShell usługi Azure Active Directory](https://docs.microsoft.com/powershell/azure/active-directory) toohelp zarządzanie danymi przechowywanymi w usłudze Azure AD.

Przy użyciu dowolnego z tych portali (lub poleceń cmdlet) możesz:

* Tworzyć konta użytkowników oraz grup i zarządzać nimi
* Zarządzanie powiązanymi usługami w chmurze dla subskrypcji Twojej organizacji
* Konfigurowanie lokalnej integracji z usługami tożsamości i uwierzytelniania usługi Azure AD

Centrum administracyjne usługi Azure AD Hello, Centrum administracyjne usługi Office 365, portal konta Microsoft Intune i hello poleceń cmdlet usługi Azure AD odczytują i zapisują tooa pojedynczego, współużytkowanego wystąpienia usługi Azure AD, który jest skojarzony z katalogu organizacji. Każde z tych narzędzi działa jako interfejs frontonu, który ściąga lub zmienia dane katalogu.

Po wprowadzeniu zmian danych w organizacji przy użyciu dowolnego z portali hello lub poleceń cmdlet, użytkownik jest zalogowany kontekście hello jednego z tych usług, zmiany hello są także wyświetlane w hello innych się, że portali hello następnym logowaniu. Tych danych jest współużytkowana przez toowhich usługi w chmurze firmy Microsoft hello, subskrybowanych.

Na przykład jeśli używasz tooblock Centrum administracyjne usługi Office 365 hello użytkownikowi logowanie, które bloki akcji hello użytkownikowi logowanie tooany toowhich inne usługi organizacji obecnie subskrybuje. Jeśli wyświetlanie hello tego samego konta użytkownika w portalu konta Microsoft Intune hello umożliwia wyświetlenie tego użytkownika hello jest zablokowany.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Jak mogę dodać wiele katalogów i zarządzać nimi?
Możesz [Dodaj katalog usługi Azure AD w portalu Azure hello](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Podanie informacji hello i wybierz **Utwórz**.

Możesz zarządzać każdym katalogiem jako w pełni niezależnym zasobem: każdy katalog jest równorzędny, obsługuje wszystkie funkcje i jest logicznie niezależny od innych katalogów zarządzanych przez Ciebie. Między katalogami nie ma relacji nadrzędny-podrzędny. Ta niezależność między katalogami obejmuje niezależność zasobów, niezależność administracyjną i niezależność synchronizacji.

* **Niezależność zasobów**. Jeśli utworzysz lub usuniesz zasób w jednym katalogu, go nie ma wpływu na żaden zasób w innym katalogu, z wyjątkiem częściowe hello użytkowników zewnętrznych. Jeśli używasz niestandardowej domeny „contoso.com” w jednym katalogu, nie można jej użyć w żadnym innym katalogu.
* **Niezależność administracyjna**.  Jeśli użytkownik, który nie jest administratorem katalogu „Contoso”, utworzy katalog testowy „Test”, wtedy:
  
  * Administratorzy katalogu "Contoso" Hello ma nie bezpośrednich uprawnień administracyjnych toodirectory "Test", chyba że administrator "Test" jawnie nada im odpowiednie uprawnienia. Administratorzy "Contoso" mogą kontrolować dostęp toodirectory "Test" z kontroli konta użytkownika hello utworzony "Test".
    
  * Jeśli można przypisać lub Usuń rolę administratora dla użytkownika w jednym katalogu, zmiana hello nie ma wpływu na żadną rolę administracyjną, którą użytkownik może mieć w innym katalogu.
* **Niezależność synchronizacji**. Można skonfigurować każdego Azure AD niezależnie dzierżawy tooget synchronizowania danych z narzędzie synchronizacji katalogu pojedynczego wystąpienia hello Azure AD Connect.

W przeciwieństwie do innych zasobów platformy Azure, Twoje katalogi nie są zasobami podrzędnymi subskrypcji platformy Azure. Więc jeśli możesz anulować lub pozwolić tooexpire Twojej subskrypcji platformy Azure, nadal dostęp dane katalogu przy użyciu programu PowerShell usługi Azure AD, hello interfejsu API Graph platformy Azure lub inne interfejsy na przykład Centrum administracyjnego usługi Office 365 hello. Można również skojarzyć inną subskrypcję z katalogiem hello.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Jak toodelete tooprepare katalog usługi Azure AD
Administrator globalny może usunąć katalog usługi Azure AD z portalu hello. Po usunięciu katalogu, wszystkie zasoby, które znajdują się w katalogu hello również zostaną usunięte. Upewnij się, że użytkownik nie należy hello katalogu przed jego usunięciem.

> [!NOTE]
> Jeśli hello użytkownik jest zalogowany za pomocą konta służbowego, użytkownik hello musi nie być próbujesz toodelete katalogu macierzystego. Na przykład, jeśli hello użytkownik jest zalogowany jako joe@contoso.onmicrosoft.com, ten użytkownik nie może usunąć katalogu hello, którego domyślna domena to contoso.onmicrosoft.com.

Usługa Azure AD wymaga, że określone warunki są niespełnienia toodelete katalogu. Pozwala to ograniczyć ryzyko negatywnego usunięcie katalogu ma wpływ na użytkowników lub aplikacji, takich jak możliwość hello toosign użytkowników w tooOffice 365 lub dostęp do zasobów na platformie Azure. Na przykład, jeśli katalogu dla subskrypcji zostanie przypadkowo usunięty, następnie użytkownicy nie mogą uzyskiwać dostęp do hello zasobów Azure dla tej subskrypcji.

zaznaczono Hello następujące warunki:

* Witaj tylko użytkownik w katalogu hello powinien być hello administrator globalny, który jest katalogiem hello toodelete. Inni użytkownicy muszą zostać usunięte przed usunięciem katalogu hello. Jeśli użytkownicy są synchronizowani z lokalnej, a następnie synchronizacji musi być wyłączona i hello użytkownicy muszą zostać usunięte w hello katalogiem w chmurze przy użyciu hello portalu Azure lub poleceń cmdlet programu Azure PowerShell. Nie jest wymaganie toodelete grup ani kontaktów, takich jak kontakty dodane za pomocą Centrum administracyjnego usługi Office 365 hello.
* Brak nie może być aplikacji w katalogu hello. Wszystkie aplikacje muszą zostać usunięte przed usunięciem katalogu hello.
* Nie dostawców uwierzytelniania wieloskładnikowego można toohello połączonego katalogu.
* Nie mogą istnieć żadnych subskrypcji dla dowolnej usługi Online firmy Microsoft, takich jak Microsoft Azure, Office 365 lub Azure AD Premium skojarzoną z katalogiem hello. Na przykład jeśli domyślny katalog został utworzony na platformie Azure, nie możesz usunąć tego katalogu, jeśli subskrypcja platformy Azure wciąż korzysta z niego na potrzeby uwierzytelniania. Nie można także usunąć katalogu, jeśli inny użytkownik skojarzył z nim subskrypcję. 


## <a name="next-steps"></a>Następne kroki
* [Forum usługi Azure AD](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Forum usługi Azure Multi-Factor Authentication](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Pytania w witrynie Stack Overflow dotyczące platformy Azure](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Przypisywanie ról administratorów w usłudze Azure AD](active-directory-assign-admin-roles.md)
