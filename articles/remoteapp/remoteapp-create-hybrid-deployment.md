---
title: "Tworzenie kolekcji hybrydowej usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia wdrożenia programów RemoteApp, która nawiązuje połączenie z siecią wewnętrzną."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 346a5fe3e4011985e4247ceef0d5ca858049fd28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-hybrid-collection-for-azure-remoteapp"></a>Tworzenie kolekcji hybrydowej usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Istnieją dwa rodzaje kolekcji usługi Azure RemoteApp:

* Chmury: znajduje się całkowicie w systemie Azure. Można wybrać zapisać wszystkie dane w chmurze (tak kolekcji tylko w chmurze) lub do połączenia z kolekcji sieci Wirtualnej i zapisać dane.   
* Hybrydowe: zawiera sieć wirtualną dla dostępu lokalnego - wymaga użycia usługi Azure AD i środowisku lokalnej usługi Active Directory.

Nie wiadomo, która jest potrzebna? Zapoznaj się z [jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp](remoteapp-collections.md).

Ten samouczek przeprowadzi Cię przez proces tworzenia kolekcji hybrydowej. Obejmuje 8 kroków:

1. Zdecyduj, co [obrazu](remoteapp-imageoptions.md) dla kolekcji. Możesz utworzyć niestandardowy obraz lub użyć jednego z obrazów Microsoft uwzględnionych w subskrypcji.
2. Konfigurowanie sieci wirtualnej. Zapoznaj się z [planowania sieci Wirtualnej](remoteapp-planvnet.md) i [sizing](remoteapp-vnetsizing.md) informacji.
3. Utwórz kolekcję.
4. Dołącz kolekcję do lokalnej domeny.
5. Obraz szablonu należy dodać do kolekcji.
6. Konfigurowanie synchronizacji katalogów. Usługa Azure RemoteApp wymaga integracji z usługą Azure Active Directory albo 1) Konfigurowanie synchronizacji Azure Active Directory z opcją synchronizacji haseł lub 2) Konfigurowanie synchronizacji Azure Active Directory bez opcji synchronizacji haseł, ale przy użyciu domeny, która jest federacyjnego do usług AD FS. Zapoznaj się z [informacje o konfiguracji dla usługi Active Directory z usługą RemoteApp](remoteapp-ad.md).
7. Publikowanie aplikacji usługi RemoteApp.
8. Konfigurowanie dostępu użytkowników.

**Przed rozpoczęciem**

Należy wykonać następujące czynności przed utworzeniem kolekcji:

* [Zarejestruj się](https://azure.microsoft.com/services/remoteapp/) usługi Azure RemoteApp.
* Utwórz konto użytkownika w usłudze Active Directory do użycia jako konto usługi Azure RemoteApp. Ograniczyć uprawnienia dla tego konta, tak aby tylko można przyłączyć maszyny do domeny.
* Zbieranie informacji o sieci lokalnej: adres IP informacje i szczegóły urządzenia sieci VPN.
* Zainstaluj [programu Azure PowerShell](/powershell/azure/overview) modułu.
* Zbierz informacje o użytkownikach, które chcesz udzielić dostępu do. Konieczne będzie główną nazwę użytkownika w usłudze Azure Active Directory (na przykład name@contoso.com) dla każdego użytkownika. Upewnij się, że nazwy UPN odpowiadają informacjom między usługą Azure AD i usługi Active Directory.
* Wybierz obraz szablonu. Obraz szablonu usługi Azure RemoteApp zawiera aplikacje i programy, które chcesz opublikować dla użytkowników. Zobacz [opcje obrazu usługi Azure RemoteApp](remoteapp-imageoptions.md) Aby uzyskać więcej informacji.
* Chcesz użyć obrazu usługi Office 365 ProPlus? Zapoznaj się z informacji o [tutaj](remoteapp-officesubscription.md).
* [Skonfiguruj usługę Active Directory dla usługi RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Krok 1: Konfigurowanie sieci wirtualnej
Można wdrażać kolekcję hybrydową, który korzysta z istniejącej sieci wirtualnej platformy Azure, lub można utworzyć nowej sieci wirtualnej. Sieć wirtualna umożliwia Twojej użytkownikom dostęp do danych w sieci lokalnej za pośrednictwem usługi RemoteApp zasobów zdalnych. Przy użyciu sieci wirtualnej platformy Azure zapewnia dostęp do sieci bezpośrednich kolekcji do innych usług platformy Azure i maszyn wirtualnych wdrożonych na tej sieci wirtualnej.

Upewnij się, że należy przejrzeć [planowania sieci Wirtualnej](remoteapp-planvnet.md) i [rozmiaru sieci Wirtualnej](remoteapp-vnetsizing.md) informacji przed utworzeniem sieci wirtualnej.

### <a name="create-an-azure-vnet-and-join-it-to-your-active-directory-deployment"></a>Utwórz sieć Wirtualną platformy Azure i przyłączyć go do wdrożenia usługi Active Directory
Rozpocznij od utworzenia [sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Ta próba polega na **sieci** kartę w portalu Azure. Należy połączyć sieci wirtualnych do wdrożenia usługi Active Directory, który jest synchronizowany z dzierżawą usługi Azure Active Directory.

Zobacz [utworzyć sieć wirtualną przy użyciu portalu Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) Aby uzyskać więcej informacji.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Upewnij się, że sieci wirtualnej jest gotowy do usługi Azure RemoteApp
Przed utworzeniem kolekcji upewnijmy się, że sieci wirtualne jest gotowe. Można to sprawdzić, wykonując następujące czynności:

1. Utwórz maszynę wirtualną platformy Azure w podsieci sieci wirtualnej utworzone dla programów RemoteApp.
2. Aby nawiązać połączenie z maszyną wirtualną za pomocą pulpitu zdalnego. (Kliknij **połączyć**.)
3. Przyłączenie jej do tego samego wdrożenia usługi Active Directory, który ma być używany dla programów RemoteApp.

Czy to pomoże? Sieć wirtualna i podsieć są gotowe do usługi Azure RemoteApp!

Więcej informacji na temat tworzenia maszyn wirtualnych platformy Azure i połączenia można znaleźć w nich przy użyciu pulpitu zdalnego [tutaj](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Krok 2: Tworzenie kolekcji usługi Azure RemoteApp
1. W [portalu Azure](http://manage.windowsazure.com), przejdź do strony usługi Azure RemoteApp.
2. Kliknij przycisk **nowy > Utwórz z sieci Wirtualnej**.
3. Wprowadź nazwę kolekcji.
4. Wybierz plan chcesz użyć — standard lub podstawowa.
5. Wybierz sieci wirtualnej z listy rozwijanej listy, a następnie podsieć.
6. Wybierz przyłączyć się do domeny.
7. Kliknij przycisk **kolekcji RemoteApp Utwórz**.

Po utworzeniu kolekcji usługi Azure RemoteApp, kliknij dwukrotnie nazwę kolekcji. Które powoduje wyświetlenie **Szybki Start** strony — jest to, gdzie skonfigurowaniu kolekcji.

Czy coś wystąpić? Zapoznaj się z [kolekcji hybrydowej informacje dotyczące rozwiązywania problemów](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-to-the-local-domain"></a>Krok 3: Link kolekcji z domeną lokalną
1. Na **Szybki Start** kliknij przycisk **Przyłącz do domeny lokalnej**.
2. Dodaj konto usługi Azure RemoteApp do lokalnej domeny usługi Active Directory. Należy nazwy domeny, jednostki organizacyjnej, nazwa użytkownika konta usługi i hasło.
   
    Są to informacje zbierane, jeśli zostały wykonane kroki przedstawione w [skonfiguruj usługę Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-to-an-azure-remoteapp-image"></a>Krok 4: Łącze do obrazu usługi Azure RemoteApp
Obraz szablonu usługi Azure RemoteApp zawiera programy, które chcesz udostępnić użytkownikom. Możesz utworzyć nową [obrazu szablonu](remoteapp-imageoptions.md) lub łączenie istniejącego obrazu (po jednym już zaimportowane lub przekazane do usługi Azure RemoteApp). Można także połączyć jednej z usługą Azure RemoteApp [obrazy szablonów](remoteapp-images.md) zawierających usługi Office 365 lub programy pakietu Office 2013 (dla wersji próbnej).

Przekazujesz nowy obraz, należy wprowadzić nazwę i wybierz lokalizację dla obrazu. Na następnej stronie kreatora możesz zapoznać się z zestawem poleceń cmdlet programu PowerShell - kopiowania i Uruchom te polecenia cmdlet z podniesionego wiersza środowiska Windows PowerShell można przekazać określonego obrazu.

Łącze do istniejącego obrazu szablonu, po prostu Określ nazwę obrazu, lokalizacji i skojarzone subskrypcji platformy Azure.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Krok 5: Konfigurowanie synchronizacji katalogów w usłudze Active Directory
Usługa Azure RemoteApp wymaga integracji z usługą Azure Active Directory albo 1) Konfigurowanie synchronizacji Azure Active Directory z opcją synchronizacji haseł lub 2) Konfigurowanie synchronizacji Azure Active Directory bez opcji synchronizacji haseł, ale przy użyciu domeny, która jest federacyjnego do usług AD FS.

Zapoznaj się z [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) — ten artykuł ułatwia konfigurowanie integracji katalogu w kroku 4.

Zobacz [plan synchronizacji katalogów](http://msdn.microsoft.com//library/azure/hh967642.aspx) dotyczących planowania informacji i szczegółowy opis kroków.

## <a name="step-6-publish-apps"></a>Krok 6: Publikowanie aplikacji
Aplikacja Azure RemoteApp jest aplikacji lub programu, które zapewniają użytkownikom. Znajduje się on w obrazu szablonu, który został przekazany do kolekcji. Gdy użytkownik uzyskuje dostęp do aplikacji, wygląda na to, aby uruchomić w środowisku lokalnym, ale rzeczywiście jest uruchomiona na platformie Azure.

Zanim użytkownicy mają dostęp do aplikacji, należy je opublikować — pozwala to użytkownikom uzyskiwania dostępu do aplikacji za pomocą klienta usług pulpitu zdalnego.

Wiele aplikacji można publikować w kolekcji. Na stronie publikowania kliknij **publikowania** można dodać aplikację. Możesz opublikować z **Start** menu obrazu szablonu lub podając ścieżkę w obrazie szablonu dla aplikacji. Jeśli chcesz dodać z **Start** menu, wybierz program do dodania. Jeśli chcesz podać ścieżkę do aplikacji, podaj nazwę aplikacji i ścieżkę do miejsca na obrazie szablonu, w którym jest zainstalowany.

## <a name="step-7-configure-user-access"></a>Krok 7: Konfigurowanie dostępu użytkowników
Teraz, po utworzeniu kolekcji, należy dodać użytkowników, którzy mają mieć możliwość użycia zasobów zdalnych. Użytkownicy, musisz zapewnić dostęp do muszą istnieć w dzierżawie usługi Active Directory skojarzone z subskrypcją używany podczas tworzenia tej kolekcji usługi Azure RemoteApp.

1. Na stronie Szybki Start kliknij **Konfigurowanie dostępu użytkowników**.
2. Wprowadź konto służbowe (z usługi Active Directory) lub konta Microsoft, który chcesz udzielić dostępu.
   
   **Uwagi:**
   
   Upewnij się, że używasz  *user@domain.com*  format.
   
   Jeśli używasz usługi Office 365 ProPlus w kolekcji, należy użyć tożsamości usługi Active Directory dla użytkowników. Dzięki temu można sprawdzić poprawności licencji.
3. Gdy użytkownicy są weryfikowane, kliknij przycisk **zapisać**.

## <a name="next-steps"></a>Następne kroki
To wszystko — pomyślnie utworzyć i wdrożyć kolekcji hybrydowej usługi Azure RemoteApp. Następnym krokiem jest Poproś użytkowników, Pobierz i zainstaluj klienta pulpitu zdalnego. Dla klienta na stronie Szybki Start usługi Azure RemoteApp można znaleźć adres URL. Następnie przygotuj dziennik użytkowników do klienta i uzyskiwania dostępu do aplikacji, która została opublikowana.

### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że możesz nie tylko ocenić ten artykuł i dodać komentarze poniżej, ale także wprowadzać zmiany w samym artykule? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij pozycję **Edit on GitHub** (Edytuj w serwisie GitHub) w celu wprowadzenia zmian. Te modyfikacje zostaną przez nas sprawdzone, a po zatwierdzeniu Twoje zmiany i poprawki będą widoczne w tym miejscu.

