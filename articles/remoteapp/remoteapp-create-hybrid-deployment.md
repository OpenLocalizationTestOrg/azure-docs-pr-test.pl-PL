---
title: "toocreate aaaHow kolekcji hybrydowej usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate wdrażania RemoteApp, która łączy tooyour sieci wewnętrznej."
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
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Jak toocreate kolekcji hybrydowej usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Istnieją dwa rodzaje kolekcji usługi Azure RemoteApp:

* Chmury: znajduje się całkowicie w systemie Azure. Można wybrać toosave wszystkich danych w chmurze hello (tak kolekcji tylko w chmurze) lub tooconnect tooa Twojego kolekcji sieci Wirtualnej i zapisywania danych istnieje.   
* Hybrydowe: zawiera sieć wirtualną dla dostępu lokalnego - wymaga hello korzystanie z usługi Azure AD i środowisku lokalnej usługi Active Directory.

Nie wiadomo, która jest potrzebna? Zapoznaj się z [jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp](remoteapp-collections.md).

Ten samouczek przeprowadzi Cię przez proces tworzenia kolekcji hybrydowej hello. Obejmuje 8 kroków:

1. Zdecyduj, co [obrazu](remoteapp-imageoptions.md) toouse kolekcji. Możesz utworzyć niestandardowy obraz lub użyć jednego z obrazów Microsoft hello uwzględnionych w subskrypcji.
2. Konfigurowanie sieci wirtualnej. Zapoznaj się z hello [planowania sieci Wirtualnej](remoteapp-planvnet.md) i [sizing](remoteapp-vnetsizing.md) informacji.
3. Utwórz kolekcję.
4. Dołącz do domeny lokalnej tooyour kolekcji.
5. Dodaj kolekcję tooyour obrazu szablonu.
6. Konfigurowanie synchronizacji katalogów. Usługa Azure RemoteApp wymaga integracji z usługą Azure Active Directory przez albo 1) Konfigurowanie synchronizacji Azure Active Directory z hello opcję synchronizacji haseł lub 2) Konfigurowanie synchronizacji Azure Active Directory bez hello opcję synchronizacji haseł, ale przy użyciu domeny, która jest tooAD federacyjnych FS. Zapoznaj się z hello [informacje o konfiguracji dla usługi Active Directory z usługą RemoteApp](remoteapp-ad.md).
7. Publikowanie aplikacji usługi RemoteApp.
8. Konfigurowanie dostępu użytkowników.

**Przed rozpoczęciem**

Potrzebne są następujące hello toodo przed utworzeniem hello kolekcji:

* [Zarejestruj się](https://azure.microsoft.com/services/remoteapp/) usługi Azure RemoteApp.
* Utwórz konto użytkownika w usłudze Active Directory toouse jako hello konta usługi Azure RemoteApp. Ogranicz uprawnienia hello dla tego konta, tak aby tylko można przyłączyć maszyny toohello domeny.
* Zbieranie informacji o sieci lokalnej: adres IP informacje i szczegóły urządzenia sieci VPN.
* Zainstaluj hello [programu Azure PowerShell](/powershell/azure/overview) modułu.
* Zbierz informacje o hello użytkowników, którzy mają dostęp toogrant do. Będzie konieczne hello główna nazwa użytkownika usługi Azure Active Directory (na przykład name@contoso.com) dla każdego użytkownika. Upewnij się, że hello nazwy UPN odpowiadają informacjom między usługą Azure AD i usługi Active Directory.
* Wybierz obraz szablonu. Obraz szablonu usługi Azure RemoteApp zawiera hello aplikacje i programy, które mają toopublish dla użytkowników. Zobacz [opcje obrazu usługi Azure RemoteApp](remoteapp-imageoptions.md) Aby uzyskać więcej informacji.
* Chcesz obrazu usługi Office 365 ProPlus hello toouse? Zapoznaj się z informacji o [tutaj](remoteapp-officesubscription.md).
* [Skonfiguruj usługę Active Directory dla usługi RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Krok 1: Konfigurowanie sieci wirtualnej
Można wdrażać kolekcję hybrydową, który korzysta z istniejącej sieci wirtualnej platformy Azure, lub można utworzyć nowej sieci wirtualnej. Sieć wirtualna umożliwia Twojej użytkownikom dostęp do danych w sieci lokalnej za pośrednictwem usługi RemoteApp zasobów zdalnych. Przy użyciu sieci wirtualnej platformy Azure udostępnia tooother dostępu bezpośredniego sieci z kolekcji usług platformy Azure i maszyny wirtualne wdrażane toothat sieci wirtualnej.

Upewnij się, że przegląd hello [planowania sieci Wirtualnej](remoteapp-planvnet.md) i [rozmiaru sieci Wirtualnej](remoteapp-vnetsizing.md) informacji przed utworzeniem sieci wirtualnej.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Utwórz sieć Wirtualną platformy Azure i przyłączyć go tooyour wdrażanie usługi Active Directory
Rozpocznij od utworzenia [sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Ta próba polega na powitania **sieci** kartę w hello portalu Azure. Należy tooconnect toohello Twojej sieci wirtualnej wdrożenia usługi Active Directory, które jest tooyour zsynchronizowanej dzierżawy usługi Azure Active Directory.

Zobacz [Utwórz sieć wirtualną przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) Aby uzyskać więcej informacji.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Upewnij się, że sieci wirtualnej jest gotowy do usługi Azure RemoteApp
Przed utworzeniem kolekcji upewnijmy się, że sieci wirtualne jest gotowe. Można to sprawdzić, wykonując następujące hello:

1. Utwórz maszynę wirtualną platformy Azure wewnątrz hello podsieci sieci wirtualnej hello utworzonego dla programów RemoteApp.
2. Użyć maszyny wirtualnej toohello tooconnect pulpitu zdalnego. (Kliknij **połączyć**.)
3. Przyłączenie jej toohello tego samego wdrożenia usługi Active Directory mają toouse usługi RemoteApp.

Czy to pomoże? Sieć wirtualna i podsieć są gotowe do usługi Azure RemoteApp!

Więcej informacji na temat tworzenia maszyn wirtualnych platformy Azure i łączenie toothem przy użyciu pulpitu zdalnego można znaleźć [tutaj](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Krok 2: Tworzenie kolekcji usługi Azure RemoteApp
1. W hello [portalu Azure](http://manage.windowsazure.com), przejdź do pozycji toohello strony usługi Azure RemoteApp.
2. Kliknij przycisk **nowy > Utwórz z sieci Wirtualnej**.
3. Wprowadź nazwę kolekcji.
4. Wybierz plan hello, które mają toouse — standard lub podstawowa.
5. Wybierz sieci wirtualnej hello rozwijanej listy, a następnie podsieć.
6. Wybierz toojoin on tooyour domeny.
7. Kliknij przycisk **kolekcji RemoteApp Utwórz**.

Po utworzeniu kolekcji usługi Azure RemoteApp, kliknij dwukrotnie nazwę hello hello kolekcji. Które powoduje wyświetlenie hello **Szybki Start** strony — jest to, gdzie skonfigurowaniu hello kolekcji.

Czy coś wystąpić? Zapoznaj się z hello [kolekcji hybrydowej informacje dotyczące rozwiązywania problemów](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Krok 3: Link domeny lokalnej toohello kolekcji
1. Na powitania **Szybki Start** kliknij przycisk **Przyłącz do domeny lokalnej**.
2. Dodaj hello Azure RemoteApp domena konta usługi tooyour lokalnej usługi Active Directory. Należy hello nazwy domeny, jednostki organizacyjnej, nazwa użytkownika konta usługi i hasło.
   
    Jest to hello informacje zbierane, jeśli zostały wykonane kroki hello [skonfiguruj usługę Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Krok 4: Link tooan usługi Azure RemoteApp obrazu
Obraz szablonu usługi Azure RemoteApp zawiera programy hello mają tooshare z użytkownikami. Możesz utworzyć nową [obrazu szablonu](remoteapp-imageoptions.md) lub łącze tooan istniejącego obrazu (jedna już zaimportowane lub przekazać tooAzure RemoteApp). Możesz również połączyć tooone hello Azure RemoteApp [obrazy szablonów](remoteapp-images.md) zawierających usługi Office 365 lub programy pakietu Office 2013 (dla wersji próbnej).

Jeśli przesyłasz nowy obraz powitania należy tooenter hello nazwę i wybierz lokalizację hello hello obrazu. Na następnej stronie powitania hello kreatora możesz zapoznać się z zestawem poleceń cmdlet programu PowerShell - kopiowania i uruchamiania tych poleceń cmdlet z podwyższonym poziomem uprawnień programu Windows PowerShell monitu tooupload hello określonego obrazu.

Łącze tooan istniejącego obrazu szablonu, po prostu Określ nazwę obrazu hello, lokalizacji i skojarzone subskrypcji platformy Azure.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Krok 5: Konfigurowanie synchronizacji katalogów w usłudze Active Directory
Usługa Azure RemoteApp wymaga integracji z usługą Azure Active Directory przez albo 1) Konfigurowanie synchronizacji Azure Active Directory z hello opcję synchronizacji haseł lub 2) Konfigurowanie synchronizacji Azure Active Directory bez hello opcję synchronizacji haseł, ale przy użyciu domeny, która jest tooAD federacyjnych FS.

Zapoznaj się z [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) — ten artykuł ułatwia konfigurowanie integracji katalogu w kroku 4.

Zobacz [plan synchronizacji katalogów](http://msdn.microsoft.com//library/azure/hh967642.aspx) dotyczących planowania informacji i szczegółowy opis kroków.

## <a name="step-6-publish-apps"></a>Krok 6: Publikowanie aplikacji
Aplikacja Azure RemoteApp jest aplikacji hello lub program, aby zapewnić użytkownikom tooyour. Znajduje się on w obrazu szablonu hello, który został przekazany do kolekcji hello. Gdy użytkownik uzyskuje dostęp do aplikacji, prawdopodobnie toorun w środowisku lokalnym, ale rzeczywiście jest uruchomiona na platformie Azure.

Aby użytkownicy mają dostęp do aplikacji, musisz toopublish ich — umożliwia to aplikacji hello dostępu użytkowników za pośrednictwem powitania klienta pulpitu zdalnego.

Możesz opublikować wielu kolekcji tooyour aplikacji. Ze strony publikowania hello, kliknij przycisk **publikowania** tooadd aplikacji. Możesz opublikować z hello **Start** menu obrazu szablonu hello lub określ ścieżkę hello na powitania obrazu szablonu dla aplikacji hello. Jeśli wybierzesz tooadd z hello **Start** menu, wybierz hello program tooadd. Jeśli wybierzesz tooprovide hello ścieżki toohello aplikacji, podaj nazwę dla aplikacji hello i toowhere ścieżka hello, jest zainstalowana na powitania obrazu szablonu.

## <a name="step-7-configure-user-access"></a>Krok 7: Konfigurowanie dostępu użytkowników
Po utworzeniu kolekcji, trzeba tooadd hello użytkownicy będą mogli toouse toobe zasobów zdalnych. Użytkownicy Hello tooexist tooneed dostępu w dzierżawie usługi Active Directory hello skojarzone z subskrypcją hello, musisz podać używane toocreate tę kolekcję usługi Azure RemoteApp.

1. Ze strony Szybki Start powitania kliknij **Konfigurowanie dostępu użytkowników**.
2. Wprowadź konto służbowe hello (z usługi Active Directory) lub konta Microsoft interesujące toogrant dostępu.
   
   **Uwagi:**
   
   Upewnij się, że używasz hello  *user@domain.com*  format.
   
   Jeśli używasz usługi Office 365 ProPlus w kolekcji, należy użyć hello tożsamości usługi Active Directory dla użytkowników. Dzięki temu można sprawdzić poprawności licencji.
3. Po zweryfikowaniu użytkowników hello kliknij **zapisać**.

## <a name="next-steps"></a>Następne kroki
To wszystko — pomyślnie utworzyć i wdrożyć kolekcji hybrydowej usługi Azure RemoteApp. Witaj następnym krokiem jest toohave użytkowników, Pobierz i zainstaluj powitania klienta pulpitu zdalnego. Adres URL hello powitania klienta można znaleźć na stronie Szybki Start usługi Azure RemoteApp hello. Następnie mają użytkownicy logują się na powitania klienta i uzyskiwać dostęp do aplikacji hello, która została opublikowana.

### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że w toorating dodanie ten artykuł i dodać komentarze poniżej, możesz wprowadzić samym artykule toohello zmiany? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij przycisk **Edytuj w serwisie GitHub** zmiany toomake - te modyfikacje zostaną toous do przeglądu, a następnie, zatwierdzeniu na nich, zostanie wyświetlone Twoje zmiany i udoskonalenia tutaj.

