---
title: "aaaProtecting maszyn wirtualnych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Adresy tego dokumentu, zalecenia w Centrum zabezpieczeń Azure, które ułatwiają ochronę maszyn wirtualnych i pozostać zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure
Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure. Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.  Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i aplikacji.

W tym artykule opisano zaleceń, które są stosowane tooVMs.  Maszyna wirtualna zaleceń Centrum wokół zbierania danych, stosowanie aktualizacji systemu, inicjowanie obsługi ochrony przed złośliwym kodem, szyfrowania dysków maszyny Wirtualnej i inne.  Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć hello dostępne zalecenia dotyczące maszyny Wirtualnej i co każdej z nich zrobić w przypadku zastosowania.

## <a name="available-vm-recommendations"></a>Dostępne zalecenia dotyczące maszyny Wirtualnej
| Zalecenie | Opis |
| --- | --- |
| [Włącz zbieranie danych dla subskrypcji](security-center-enable-data-collection.md) |Zaleca się włączenie funkcji zbierania danych w zasadach zabezpieczeń powitania dla każdej subskrypcji i wszystkich maszynach wirtualnych (VM) w subskrypcji. |
| [Włącz szyfrowanie dla konta magazynu Azure](security-center-enable-encryption-for-storage-account.md) | Zaleca się, Włącz szyfrowanie usługi Magazyn Azure dla przechowywanych danych. Szyfrowanie usługi Magazyn (SSE) działa hello dane są szyfrowane podczas ich zapisywania tooAzure magazynu i odszyfrowuje przed pobierania. SSE jest obecnie dostępny tylko dla hello usługi obiektów Blob platformy Azure i może służyć do blokowe i stronicowe obiekty BLOB i uzupełnialnych obiektów blob. toolearn więcej, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](../storage/common/storage-service-encryption.md).</br>SSE jest obsługiwana tylko na kontach magazynu Menedżera zasobów. Klasycznych kont magazynu nie są obecnie obsługiwane. hello toounderstand klasycznego i modeli wdrażania usługi Resource Manager, zobacz [modele wdrażania Azure](../azure-classic-rm.md). |
| [Koryguj luki w zabezpieczeniach systemu operacyjnego](security-center-remediate-os-vulnerabilities.md) |Zaleca wyrównania konfiguracje systemu operacyjnego z hello zalecane reguły konfiguracji, np. nie zezwalają na toobe hasła zapisane. |
| [Zastosuj aktualizacje systemu](security-center-apply-system-updates.md) |Zaleca się wdrożenie Brak zabezpieczenia systemu i tooVMs aktualizacje krytyczne. |
| [Zastosuj Just In Time kontroli dostępu do sieci](security-center-just-in-time.md) | Zaleca się zastosowanie tylko w dostęp maszyny Wirtualnej. Witaj tylko w funkcji czasu jest w wersji zapoznawczej i jest dostępny na powitania warstwy standardowa, Centrum zabezpieczeń. Zobacz [cennik](security-center-pricing.md) toolearn więcej informacji na temat Centrum zabezpieczeń firmy warstw cenowych. |
| [Uruchom ponownie po zaktualizowaniu systemu](security-center-apply-system-updates.md#reboot-after-system-updates) |Zaleca się ponowne uruchomienie procesu hello wirtualna toocomplete stosowanie aktualizacji systemu. |
| [Zainstaluj punkt końcowy](security-center-install-endpoint-protection.md) |Zaleca się, że alokowanie tooVMs programy chroniące przed złośliwym kodem (tylko maszyn wirtualnych systemu Windows). |
| [Rozwiąż alerty dotyczące kondycji punktu końcowego](security-center-resolve-endpoint-protection-health-alerts.md) |Zaleca rozwiązanie problemów dotyczących ochrony punktów końcowych. |
| [Włącz agenta maszyny wirtualnej](security-center-enable-vm-agent.md) |Umożliwia toosee możesz maszyny wirtualne wymagające hello agenta maszyny Wirtualnej. Witaj agenta maszyny Wirtualnej musi być zainstalowany na maszynach wirtualnych w kolejności tooprovision poprawki skanowanie skanowanie linii bazowej i programy chroniące przed złośliwym kodem. Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace. Artykuł Hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) zawiera informacje na temat sposobu tooinstall hello agenta maszyny Wirtualnej. |
| [Zastosuj szyfrowanie dysków](security-center-apply-disk-encryption.md) |Zaleca szyfrowanie dysków maszyny wirtualnej przy użyciu usługi Azure Disk Encryption (maszyny wirtualne z systemami Windows i Linux). Szyfrowanie jest zalecane dla hello systemu operacyjnego i woluminów danych na maszynie Wirtualnej. |
| [Aktualizacja wersji systemu operacyjnego](security-center-update-os-version.md) |Zaleca się, zaktualizuj wersję systemu operacyjnego (OS) hello usługi w chmurze toohello najnowszej wersji dostępnej w do Twojej rodziny systemów operacyjnych.  toolearn więcej informacji na temat usługi w chmurze, zobacz hello [Omówienie usługi w chmurze](../cloud-services/cloud-services-choose-me.md). |
| [Funkcja oceny luk w zabezpieczeniach nie jest zainstalowana](security-center-vulnerability-assessment-recommendations.md) |Zaleca się zainstalowanie na maszynie wirtualnej rozwiązania do oceny luk w zabezpieczeniach. |
| [Korygowanie luk w zabezpieczeniach](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Umożliwia toosee systemu i aplikacji luk w zabezpieczeniach wykrywanych przez rozwiązanie do oceny luk w zabezpieczeniach hello zainstalowany na maszynie Wirtualnej. |

## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:

* [Ochrona aplikacji w Centrum zabezpieczeń Azure](security-center-application-recommendations.md)
* [Ochrona sieci w Centrum zabezpieczeń Azure](security-center-network-recommendations.md)
* [Ochrona usługi Azure SQL w Centrum zabezpieczeń Azure](security-center-sql-service-recommendations.md)

toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
