---
title: "aaaWhat jest usługa Azure RemoteApp? | Microsoft Docs"
description: "Dowiedz się, jak urządzenie tooshare aplikacji i zasobów tooany za pośrednictwem usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Co to jest usługa Azure RemoteApp?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp łączy hello funkcjonalność programu Microsoft RemoteApp lokalne powitania obsługiwanej przez usługi pulpitu zdalnego, tooAzure. Usługa Azure RemoteApp pomaga zapewnić bezpieczny zdalny dostęp tooapplications z wielu różnych urządzeń użytkowników. Usługa Azure RemoteApp hostuje nietrwałe sesje serwera terminali w chmurze hello i pobrać toouse je i udostępniać je użytkownikom.

Za pomocą usługi Azure RemoteApp można udostępniać aplikacje i zasoby użytkownikom przy użyciu prawie każdego urządzenia. Nasze aplikacje są hostowane w chmurze hello, co oznacza, że Dbamy o hello sprzętu i skalowanie toomeet potrzeb użytkownika. Masz toodo jest przekazanie aplikacji hello mają tooshare, a następnie zachęcić toouse Twojego użytkowników tych aplikacji. [Użytkownicy uzyskują tookeep ich własnych urządzeń](remoteapp-clients.md), podczas gdy Ty zarządzasz wszystkim za pośrednictwem hello portalu Azure. Możesz nawet ma hello możliwości przy użyciu poświadczeń firmowych, dzięki czemu zapewniasz bezpieczeństwo hello aplikacji i danych.

Dowiedz się więcej na temat usługi Azure RemoteApp lub — jeśli już Cię przekonaliśmy — [od razu ją wypróbuj](https://azure.microsoft.com/services/remoteapp/).

Masz pytania dotyczące usługi Azure RemoteApp? Zapoznaj się z [często zadawanymi pytaniami](remoteapp-faq.md).

Usługa Azure RemoteApp jest częścią hello [infrastruktury pulpitów wirtualnych Microsoft](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Nowość!** Chcesz toolearn więcej informacji na temat usługi Azure RemoteApp? Lub gotowe toovalidate usługi Azure RemoteApp w skali? Dołącz do naszych cotygodniowych [poprosić ekspertów hello webinar](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Kolekcje usługi Azure RemoteApp
Istnieją dwa rodzaje [kolekcji usługi Azure RemoteApp](remoteapp-collections.md):

* A **kolekcja w chmurze** jest hostowany i przechowuje dane programów w chmurze hello. Użytkownicy mogą uzyskiwać dostęp do aplikacji, logując się przy użyciu konta Microsoft lub poświadczeń firmowych synchronizowanych lub sfederowanych z usługą Azure Active Directory.
  
    Wybierz kolekcję w chmurze ma tooshare aplikacji hello nie potrzebują zasobu tooany połączenia sieci prywatnej firmy (na przykład za pomocą urządzenia sieci VPN). Jeśli aplikacja hello używa zasobów na powitania Internet, usłudze OneDrive lub na platformie Azure, kolekcji w chmurze będzie działać dla Ciebie. Możliwe jest również toocreate najszybszy hello.
* A **kolekcji hybrydowej** jest hostowany i przechowuje dane w hello chmury Azure, ale również umożliwia użytkownikom dostęp do danych i zasobów przechowywanych w sieci lokalnej. Użytkownicy mogą uzyskiwać dostęp do aplikacji, logując się przy użyciu poświadczeń firmowych synchronizowanych lub sfederowanych z usługą Azure Active Directory.
  
    Wybierz kolekcję hybrydową, jeśli potrzebujesz tooresources połączenia, w sieci prywatnej firmy. Na przykład jeśli hello aplikacja musi uzyskiwać dostęp do tooone hello poniżej:
  
  * Serwery plików znajdujące się w intranecie
  * Program Quicken
  * Bazy danych znajdujące się za zaporą
    
    Jest to zazwyczaj bardziej użyteczna dla dużych firm z dużą ilością zasobów w sieciach prywatnych, które nie mogą być przenoszone toohello chmury.

Witaj różne kolekcje mają różne opcje, w tym sieci, dlatego zastanów się [którą kolekcję](remoteapp-collections.md) działa najlepiej dla Ciebie. 

### <a name="updating-your-collection"></a>Aktualizowanie kolekcji
Jednym z hello podstawowych różnic między kolekcjami hybrydowymi i w chmurze hello jest sposób obsługi aktualizacji oprogramowania. Z kolekcji w chmurze, która używa hello preinstalowane obrazu usługi Office 365 ProPlus lub Office 2013 nie masz tooworry o wszystkich aktualizacjach. Witaj usługa sama obsługuje i wdraża aktualizacje w sposób ciągły, tooboth aplikacji i systemu operacyjnego hello.

Kolekcje hybrydowe, a także kolekcje w chmurze, korzystających z obrazu niestandardowego szablonu są odpowiada za obsługę obrazu hello i aplikacji. Aktualizacje obrazów dołączonych do domeny można kontrolować za pomocą narzędzi takich jak Windows Update, zasady grupy lub program System Center.

Po zaktualizowaniu obrazu niestandardowego szablonu Przekaż hello nowy obraz toohello chmury Azure i następnie zaktualizuj hello kolekcji toouse hello nowy obraz. (Możesz to zrobić, korzystając z usługi Azure RemoteApp hello **Szybki Start** strony lub hello pulpitu nawigacyjnego.)

Aby uzyskać więcej informacji, zobacz [Update your collection](remoteapp-update.md) (Aktualizowanie kolekcji).

## <a name="supported-remoteapp-clients"></a>Obsługiwani klienci usługi RemoteApp
Usługa Azure RemoteApp jest obsługiwana w aplikacjach klienckich usługi RemoteApp hello systemu Windows i Windows RT, a także aplikacjach pulpitu zdalnego firmy Microsoft hello for Mac, iOS i Android. Użytkowników można używać tych aplikacji na ich mobile lub obliczeń tooaccess urządzeń hello nowych programów Azure RemoteApp.

Zobacz [podczas uzyskiwania dostępu do aplikacji w usłudze Azure RemoteApp](remoteapp-clients.md) Aby uzyskać więcej informacji o klientach hello.

## <a name="next-steps"></a>Następne kroki
Wszystko gotowe. Czas wypróbować usługę. Następujące artykuły pomogą Ci rozpocząć pracę z usługą Azure RemoteApp:

* [Jakiego rodzaju kolekcji potrzebujesz w usłudze Azure RemoteApp?](remoteapp-collections.md)
* [Tworzenie obrazu usługi Azure RemoteApp](remoteapp-imageoptions.md)
* [Jak toocreate kolekcji w chmurze Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Jak toocreate kolekcji hybrydowej usługi Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Jak działa licencjonowanie w usłudze Azure RemoteApp?](remoteapp-licensing.md)
* [Najlepsze rozwiązania dotyczące korzystania z usługi Azure RemoteApp](remoteapp-bestpractices.md)
* [Często zadawane pytania dotyczące usługi Azure RemoteApp](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Pomóż nam sobie pomóc
Czy wiesz, że w toorating dodanie ten artykuł i dodać komentarze poniżej, możesz wprowadzić samym artykule toohello zmiany? Brakuje informacji? Coś jest nie tak? Treść artykułu jest niejasna? Przewiń w górę i kliknij przycisk **Edytuj w serwisie GitHub** lub **Edytuj** zmiany toomake - te modyfikacje zostaną toous do przeglądu, a następnie, zatwierdzeniu na nich, zostanie wyświetlone Twoje zmiany i udoskonalenia tutaj.

