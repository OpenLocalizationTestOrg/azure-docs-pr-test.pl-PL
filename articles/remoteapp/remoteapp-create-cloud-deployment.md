---
title: toocreate aaaHow kolekcji w chmurze Azure RemoteApp | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate wdrożenia usługi Azure RemoteApp, która zapisuje dane w hello chmury Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Jak toocreate kolekcji w chmurze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Istnieją dwa rodzaje [kolekcji usługi Azure RemoteApp](remoteapp-collections.md): 

* Chmury: znajduje się całkowicie w systemie Azure. Można wybrać toosave wszystkich danych w chmurze hello (tak kolekcji tylko w chmurze) lub tooconnect tooa Twojego kolekcji sieci Wirtualnej i zapisywania danych istnieje.   
* Hybrydowe: zawiera sieć wirtualną dla dostępu lokalnego - wymaga hello korzystanie z usługi Azure AD i środowisku lokalnej usługi Active Directory.

Ten samouczek przeprowadzi Cię przez proces tworzenia kolekcji w chmurze hello. Istnieją cztery kroki: 

1. Utwórz kolekcję usługi Azure RemoteApp.
2. Opcjonalnie można skonfigurować synchronizację katalogów. Jeśli używasz usługi Azure AD i usługi Active Directory, masz toosynchronize użytkowników, kontaktów i haseł z dzierżawą lokalnej usługi Active Directory tooyour usługi Azure AD.
3. Publikowanie aplikacji.
4. Konfigurowanie dostępu użytkowników.

**Przed rozpoczęciem**

Potrzebne są następujące hello toodo przed utworzeniem hello kolekcji:

* [Zarejestruj się](https://azure.microsoft.com/services/remoteapp/) usługi Azure RemoteApp. 
* Zbierz informacje o hello użytkowników, którzy mają dostęp toogrant do. Może to być informacje o koncie Microsoft lub informacje o koncie pracy usługi Active Directory dla użytkowników.
* W tej procedurze przyjęto założenie, że są albo będzie toouse jedną hello szablonu obrazów w ramach subskrypcji lub ma już przekazać obrazu szablonu hello ma toouse. Jeśli potrzebujesz tooupload obraz inny szablon, możesz to zrobić na stronie obrazy szablonów hello. Po prostu kliknij **przekazania obrazu szablonu** i wykonaj kroki powitania w Kreatorze hello. 
* Chcesz obrazu usługi Office 365 ProPlus hello toouse? Zapoznaj się z informacji o [tutaj](remoteapp-officesubscription.md).
* Chcesz tooprovide niestandardowych aplikacjach albo programów FIRMOWYCH? Utwórz nową [obrazu](remoteapp-imageoptions.md) i używać go w kolekcji w chmurze.
* Ustal, czy jest potrzebny tooa tooconnect sieci Wirtualnej. Jeśli wybierzesz tooa tooconnect sieci Wirtualnej, upewnij się, spełnia hello [zmiany rozmiaru wytyczne](remoteapp-vnetsizing.md) i że [mogą się łączyć tooRemoteApp](remoteapp-vnet.md). Zapoznaj się z hello [artykułu planowania sieci Wirtualnej ](remoteapp-planvnet.md)Aby uzyskać więcej informacji.
* Jeśli używasz sieci Wirtualnej zdecydować, czy toojoin on tooyour lokalnej domeny usługi Active Directory.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Krok 1: Tworzenie kolekcji w chmurze - z lub bez sieci Wirtualnej
Użyj hello następujące kroki zbyt**Utwórz kolekcję tylko w chmurze**:

1. W portalu zarządzania hello Przejdź toohello programów RemoteApp.
2. Kliknij przycisk **nowy > Szybkie tworzenie**.
3. Wprowadź nazwę kolekcji, a następnie wybierz region.
4. Wybierz plan hello, które mają toouse — standard lub podstawowa.
5. Wybierz hello toouse szablonu dla tej kolekcji. 
   
    **Porada:** subskrypcji dla usługi RemoteApp jest dostarczany z [obrazy szablonów](remoteapp-images.md) zawierających usługi Office 365 lub Office 2013 (dla wersji próbnej) programów, niektóre opublikowane (takich jak Word) i inne gotowe toopublish. Można również utworzyć nowy [obrazu](remoteapp-imageoptions.md) i używać go w kolekcji w chmurze.
6. Kliknij przycisk **kolekcji RemoteApp Utwórz**.
   
    **Ważne:** może potrwać tooprovision minut too30 kolekcji.

Po utworzeniu kolekcji usługi Azure RemoteApp, kliknij dwukrotnie nazwę hello hello kolekcji. Które powoduje wyświetlenie hello **Szybki Start** strony — jest to, gdzie skonfigurowaniu hello kolekcji.

Użyj następujących hello kroki toocreate **chmury i sieci Wirtualnej kolekcji**:

1. W portalu zarządzania hello Przejdź toohello usługi Azure RemoteApp.
2. Kliknij przycisk **nowe** > **utworzyć z sieci Wirtualnej**.
3. Wprowadź nazwę kolekcji.
4. Wybierz plan hello, które mają toouse — standard lub podstawowa.
5. Wybierz hello utworzone sieci Wirtualnej. Nie wiadomo, jak toodo który? Na razie hello kroki opisano w hello [hybrydowego](remoteapp-create-hybrid-deployment.md) tematu.
6. Zdecyduj, czy chcesz toojoin domenę tooyour kolekcji. Jeśli tak, konieczne będzie toouse AD Connect toointegrate usługi Azure AD i środowiska usługi Active Directory. Który omówiono poniżej w **krok 2**.
7. Kliknij przycisk **kolekcji RemoteApp Utwórz**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Krok 2: Konfigurowanie synchronizacji katalogów usługi Active Directory (opcjonalnie)
Jeśli chcesz toouse usługi Active Directory, usługi Azure RemoteApp wymaga Synchronizacja katalogu usługi Azure Active Directory i lokalnej usługi Active Directory toosynchronize użytkowników, kontaktów i dzierżawy usługi Azure Active Directory tooyour hasła. Zobacz [Konfigurowanie usługi Active Directory dla usługi Azure RemoteApp](remoteapp-ad.md) informacje dotyczące planowania. Można także przejść bezpośrednio za[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) informacji.

## <a name="step-3-publish-apps"></a>Krok 3: Publikowanie aplikacji
Aplikacja Azure RemoteApp jest aplikacji hello lub program, aby zapewnić użytkownikom tooyour. Znajduje się on w obrazu szablonu hello, który został przekazany do kolekcji hello. Gdy użytkownik uzyskuje dostęp do, aplikacji, aplikacji hello jest wyświetlany toorun w środowisku lokalnym, ale rzeczywiście jest uruchomiona na maszynie wirtualnej na platformie Azure. 

Aby użytkownicy mają dostęp do aplikacji, musisz toopublish hello ich — publikowania aplikacji umożliwia użytkownikom dostęp do aplikacji hello przy użyciu klienta pulpitu zdalnego.

Możesz opublikować wiele aplikacji tooyour kolekcji usługi Azure RemoteApp. Ze strony publikowania hello, kliknij przycisk **publikowania** tooadd programu. Możesz opublikować z hello **Start** menu obrazu szablonu hello lub określ ścieżkę hello na powitania obrazu szablonu dla aplikacji hello. Jeśli wybierzesz tooadd z hello **Start** menu, wybierz toopublish aplikacji hello. Jeśli wybierzesz tooprovide hello ścieżki toohello aplikacji, podaj nazwę dla aplikacji hello i toowhere ścieżka hello, jest zainstalowana na powitania obrazu szablonu.

## <a name="step-4-configure-user-access"></a>Krok 4: Konfigurowanie dostępu użytkowników
Po utworzeniu kolekcji, trzeba tooadd hello użytkownicy będą mogli toouse toobe zasobów zdalnych. Jeśli korzystasz z usługi Active Directory, użytkownicy hello tooexist tooneed dostępu w dzierżawie usługi Active Directory hello skojarzone z subskrypcją hello, musisz podać używane toocreate tej kolekcji.

1. Ze strony Szybki Start powitania kliknij **Konfigurowanie dostępu użytkowników**. 
2. Wprowadź konto służbowe hello (z usługi Active Directory) lub konta Microsoft interesujące toogrant dostępu.
   
   **Uwagi:** 
   
   Upewnij się, że używasz hello  *user@domain.com*  format.
   
   Jeśli używasz usługi Office 365 ProPlus w kolekcji, należy użyć hello tożsamości usługi Active Directory dla użytkowników. Dzięki temu można sprawdzić poprawności licencji. 
3. Po zweryfikowaniu hello użytkowników, kliknij przycisk **zapisać**.

## <a name="next-steps"></a>Następne kroki
To wszystko — pomyślnie utworzone i wdrożone z kolekcji w chmurze Azure RemoteApp. Witaj następnym krokiem jest toohave użytkowników, Pobierz i zainstaluj powitania klienta pulpitu zdalnego. Adres URL hello powitania klienta można znaleźć na stronie Szybki Start usługi Azure RemoteApp hello. Następnie mają użytkownicy logują się na powitania klienta i uzyskiwać dostęp do aplikacji hello, która została opublikowana.

### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że w toorating dodanie ten artykuł i dodać komentarze poniżej, możesz wprowadzić samym artykule toohello zmiany? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij przycisk **Edytuj w serwisie GitHub** zmiany toomake - te modyfikacje zostaną toous do przeglądu, a następnie, zatwierdzeniu na nich, zostanie wyświetlone Twoje zmiany i udoskonalenia tutaj.

