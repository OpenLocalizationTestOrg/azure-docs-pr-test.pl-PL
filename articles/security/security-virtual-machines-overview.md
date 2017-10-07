---
title: "funkcje zabezpieczeń aaaAzure używane z maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: " Przegląd funkcji zabezpieczeń platformy Azure core hello, które mogą być używane z maszyn wirtualnych platformy Azure. Azure maszyn wirtualnych należy podać hello swobodne korzystanie z wirtualizacji bez konieczności toobuy i obsługa hello sprzętem fizycznym, który uruchamia hello maszyny Wirtualnej. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Omówienie zabezpieczeń usługi Azure maszyny wirtualne
Usługa Azure Virtual Machines umożliwia elastyczne wdrażanie szerokiego zakresu rozwiązań obliczeniowych. Dzięki obsłudze rozwiązań Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM i SAP oraz usługi BizTalk Services na platformie Azure możesz wdrożyć dowolne obciążenie w dowolnym języku i w prawie każdym systemie operacyjnym.

Zapewnia maszyny wirtualnej platformy Azure hello swobodne korzystanie z wirtualizacji bez konieczności toobuy i obsługa hello sprzętem fizycznym, na którym działają hello maszyny wirtualnej.  Możesz skompilować i wdrożyć aplikacje z hello gwarancji, że dane są chronione i bezpieczne w naszych centrach danych w bardzo bezpieczny.

Przy użyciu platformy Azure można tworzyć rozwiązania z rozszerzonymi zabezpieczeniami, zgodne który:

* Ochrona maszyn wirtualnych przed wirusami i złośliwym oprogramowaniem
* Szyfrowanie poufnych danych
* Zabezpieczanie ruchu sieciowego
* Identyfikowanie i wykrywanie zagrożeń
* Spełnianie wymagań dotyczących zgodności

Hello celem tego artykułu jest tooprovide omówienie hello podstawowe zabezpieczeń platformy Azure funkcje, które mogą być używane z maszyn wirtualnych. Firma Microsoft udostępnia również tooarticles łącza, które podać szczegóły dotyczące każdej funkcji, aby dowiedzieć się więcej.  

Witaj podstawowej maszyny wirtualnej Azure zabezpieczeń możliwości toobe omówione w tym artykule:

* Oprogramowanie chroniące przed złośliwym kodem
* Sprzętowy moduł zabezpieczeń
* Szyfrowanie dysków maszyny wirtualnej
* Kopia zapasowa maszyny wirtualnej
* Azure Site Recovery
* Sieci wirtualne
* Zarządzanie zasadami zabezpieczeń i raportowanie
* Zgodność

## <a name="antimalware"></a>Oprogramowanie chroniące przed złośliwym kodem
Z platformy Azure używając ochrony przed złośliwym oprogramowaniem z dostawcami zabezpieczeń, takich jak Microsoft, firmy Symantec, Trend Micro i Kaspersky tooprotect maszyn wirtualnych z złośliwych plików, adware i innymi zagrożeniami. Zobacz hello Dowiedz się więcej sekcji poniżej toofind artykuły rozwiązań partnerskich.

Antimalware firmy Microsoft dla usług Azure Cloud Services i maszyn wirtualnych jest możliwość ochrony w czasie rzeczywistym, która pomaga w identyfikacji i usuwania wirusy, programy szpiegujące lub inne złośliwe oprogramowanie.  Microsoft Antimalware udostępnia można skonfigurować alerty, gdy znane tooinstall prób złośliwego lub niechcianego oprogramowania, się lub uruchomić w systemie Azure.

Microsoft Antimalware to rozwiązanie jednego agenta dla aplikacji i środowisk dzierżawy toorun zaprojektowane w tle hello bez udziału człowieka. Można wdrożyć ochrony na podstawie potrzeb hello obciążeń aplikacji, z albo podstawowe secure domyślnie lub Zaawansowane Konfiguracja niestandardowa, w tym monitorowania ochrony przed złośliwym oprogramowaniem.

Podczas wdrażania i włączyć Microsoft Antimalware hello następujące podstawowe funkcje są dostępne:

* Ochrona w czasie rzeczywistym - monitorów działania usług w chmurze i maszyn wirtualnych toodetect i blokowanie wykonywania złośliwego oprogramowania.
* Zaplanowane skanowanie - okresowo przesyła docelowe skanowania toodetect złośliwe oprogramowanie, w tym aktywnie uruchomione programy.
* Korygowania złośliwego oprogramowania — automatycznie pobiera wykrytego złośliwego oprogramowania, takich jak usuwanie lub poddawania złośliwych plików i czyszczenie wpisy rejestru złośliwe działania.
* Aktualizacje podpisu — automatycznie instaluje hello najnowsze ochrony podpisów (definicje wirusów) tooensure ochrona jest aktualne na wstępnie określoną częstotliwością.
* Aktualizacje aparatu ochrony przed złośliwym kodem — automatyczne aktualizacje hello aparat Antimalware firmy Microsoft.
* Aktualizacje platformy ochrony przed złośliwym kodem — automatyczne aktualizacje hello platformy Microsoft Antimalware.
* Active protection - raporty tooAzure telemetrii metadanych o wykrytych zagrożeń i podejrzane zasobów tooensure szybkie odpowiedzi i umożliwia w czasie rzeczywistym podpisu synchroniczne dostawy za pośrednictwem hello systemu Microsoft Active Protection (MAPS).
* Przykłady raportowania — zapewnia i raporty przykłady toohelp usługi Microsoft Antimalware toohello uściślić hello usługi i Włącz rozwiązywania problemów.
* Wykluczenia — aplikacji i tooconfigure administratorów usługi niektóre pliki, procesów i dyski tooexclude je z ochrony i skanowania, wydajności i inne przyczyny.
* Zbieranie zdarzeń ochrony przed złośliwym kodem — rejestruje hello ochrony przed złośliwym kodem usługi kondycji, podejrzanych działań i korygowania akcje wykonywane w dzienniku zdarzeń systemu operacyjnego hello i zbiera je do konta magazynu Azure powitania klienta.

Dowiedz się więcej: więcej informacji na temat tooprotect oprogramowania chroniącego przed złośliwym kodem toolearn maszyn wirtualnych, zobacz:

* [Ochrony przed złośliwym oprogramowaniem firmy Microsoft dla usług w chmurze Azure i maszyn wirtualnych](azure-security-antimalware.md)
* [Wdrażanie rozwiązań do ochrony przed złośliwym kodem na maszynach wirtualnych platformy Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Jak tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej systemu Windows](../virtual-machines/windows/classic/install-trend.md)
* [Jak tooinstall i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Rozwiązań zabezpieczeń w hello Azure Marketplace](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Zabezpieczenia sprzętowe modułu
Zabezpieczenia uwierzytelniania i szyfrowania może zostać poprawione skracając klucza zabezpieczeń. Można uprościć zarządzanie hello i bezpieczeństwo kluczy i kluczy tajnych krytyczne przez zapisanie ich w usłudze Azure Key Vault. Magazyn kluczy udostępnia hello opcja toostore klucze w standardami dotyczącymi sprzętu zabezpieczeń certyfikowanych tooFIPS modułów (HSM) 140-2 poziom 2. Klucze szyfrowania programu SQL Server do utworzenia kopii zapasowej lub [przezroczystego szyfrowania danych](https://msdn.microsoft.com/library/bb934049.aspx) wszystkie można przechowywać w magazynie kluczy z kluczy ani kluczy tajnych z aplikacji. Uprawnienia i dostęp do elementów toothese chronione są zarządzane za pośrednictwem [usługi Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Więcej informacji:

* [Co to jest usługa Azure Key Vault?](../key-vault/key-vault-whatis.md)
* [Wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md)
* [Blog Azure Key Vault](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Szyfrowanie dysków maszyny wirtualnej
Szyfrowanie dysków Azure to nowa funkcja umożliwia zaszyfrowanie dysków systemu Windows i Linux Azure Virtual Machine. Szyfrowanie dysków Azure branżowymi hello [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i hello [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i dysków z danymi hello.

rozwiązanie Hello jest zintegrowany z usługi Azure Key Vault toohelp sterowania i zarządzania hello dysku szyfrowania kluczy i kluczy tajnych w magazynie kluczy subskrypcji, przy jednoczesnym zapewnieniu, że wszystkie dane w hello dysków maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.

Więcej informacji:

* [Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Szyfrowanie dysków Azure dla maszyn wirtualnych systemu Windows i Linux](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Szyfrowanie maszyny wirtualnej](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Kopia zapasowa maszyny wirtualnej
Azure Backup to skalowalne rozwiązanie chroniące dane aplikacji, które nie wymaga żadnych inwestycji kapitałowych i cechujące się minimalnymi kosztami operacyjnymi. Błędy aplikacji mogą powodować uszkodzenia danych, a błędy użytkowników — usterki aplikacji. Kopia zapasowa Azure maszynach wirtualnych z systemem Windows i Linux są chronione.

Więcej informacji:

* [Co to jest Azure Backup?](../backup/backup-introduction-to-azure-backup.md)
* [Ścieżka szkoleniowa kopii zapasowej systemu Azure](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Usługa Kopia zapasowa Azure — często zadawane pytania](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Istotną częścią strategii BCDR organizacji jest ustaleniem, jak wystąpić tookeep firmowych obciążeń i aplikacji w górę i uruchomiona podczas planowanych i nieplanowanych przestojów. Usługa Azure Site Recovery pomaga organizowania replikacji, trybu failover i odzyskiwania obciążeń i aplikacji, tak aby były dostępne z lokalizacji dodatkowej jeśli spadnie do lokalizacji głównej.

Usługa Site Recovery:

* **Upraszcza strategii BCDR** — Usługa Site Recovery umożliwia łatwe toohandle replikacji, trybu failover i odzyskiwania wielu firmowych obciążeń i aplikacji z jednej lokalizacji. Usługa Site Recovery organizuje replikację i tryb failover, ale nie przechwytuje danych aplikacji ani nie zbiera żadnych informacji ich dotyczących.
* **Zapewnia elastyczne replikacji** — przy użyciu usługi Site Recovery może replikować obciążenia uruchomione na maszynach wirtualnych funkcji Hyper-V, maszyny wirtualne VMware i serwery fizyczne z systemem Windows lub Linux.
* **Obsługuje tryb failover i odzyskiwania** — Usługa Site Recovery zapewnia testowy tryb failover testowanie odzyskiwania po awarii toosupport bez wpływu na środowiska produkcyjne. Możesz również uruchomić planowane tryby failover (brak utraty danych) w przypadku przewidywanych przerw w działaniu lub nieplanowane tryby failover (minimalna utrata danych, zależna od częstotliwości replikacji) w przypadku nieoczekiwanych awarii. Po przejściu w tryb failover można Lokacje główne tooyour powrotu po awarii. Usługa Site Recovery zapewnia plany odzyskiwania, które mogą uwzględniać skrypty i skoroszyty automatyzacji platformy Azure. Dzięki nim możesz dostosować tryb failover i odzyskiwanie dla aplikacji wielowarstwowych.
* **Eliminuje dodatkowego centrum danych** — można replikować tooa lokacji dodatkowej lokalnymi lub tooAzure. Za pomocą platformy Azure jako miejsca docelowego dla odzyskiwania po awarii eliminuje koszty hello i z utrzymywaniem lokacji dodatkowej. Replikowane dane są przechowywane w usłudze Azure Storage.
* **Integruje się z istniejącymi technologiami BCDR** — Usługa Site Recovery współpracuje z innymi funkcjami BCDR aplikacji. Na przykład można użyć usługi Site Recovery tooprotect hello programu SQL Server zaplecza obciążeń firmowych. W tym macierzystą obsługę programu SQL Server AlwaysOn toomanage hello trybem failover grup dostępności.

Więcej informacji:

* [Co to jest Azure Site Recovery?](../site-recovery/site-recovery-overview.md)
* [Jak działa usługa Azure Site Recovery?](../site-recovery/site-recovery-components.md)
* [Jakie obciążenia są chronione przez usługę Azure Site Recovery?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Sieci wirtualne
Maszyny wirtualne muszą łączność sieciową. toosupport tego wymogu Azure wymaga toobe maszyny wirtualne podłączone tooan sieci wirtualnej platformy Azure. Sieci wirtualnej platformy Azure jest konstrukcją logiczną, rozszerzający hello fizycznej Azure sieci szkieletowej. Każdy logicznej sieci wirtualnej platformy Azure jest odizolowana od wszystkich innych sieciach wirtualnych platformy Azure. Izolacja pomaga upewnić się, że ruch sieciowy we wdrożeniach nie jest dostępny tooother klientów Microsoft Azure.

Więcej informacji:

* [Przegląd zabezpieczeń sieci platformy Azure](security-network-overview.md)
* [Omówienie sieci wirtualnej](../virtual-network/virtual-networks-overview.md)
* [Funkcje sieci i powiązań dla scenariuszy dla przedsiębiorstw](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Zarządzanie zasadami zabezpieczeń i raportowanie
Centrum zabezpieczeń Azure pomaga zapobiec, wykrywania i reagowania toothreats i zapewnia zwiększyć widoczność i kontrolę nad, hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

Centrum zabezpieczeń Azure ułatwia optymalizacji i monitorowania zabezpieczeń maszyny wirtualnej:

* Zapewnianie maszyny wirtualnej [zalecenia dotyczące zabezpieczeń](../security-center/security-center-recommendations.md) takich jak stosowanie aktualizacji systemu skonfigurować listy ACL punktów końcowych, włączanie ochrony przed złośliwym kodem, Włącz grup zabezpieczeń sieci i zastosować szyfrowanie dysku.
* Monitorowanie stanu hello maszyn wirtualnych

Więcej informacji:

* [Wprowadzenie tooAzure Centrum zabezpieczeń](../security-center/security-center-intro.md)
* [Centrum zabezpieczeń Azure — często zadawane pytania](../security-center/security-center-faq.md)
* [Planowanie Centrum zabezpieczeń Azure i operacje](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Zgodność
Maszyny wirtualne platformy Azure jest certyfikowany do FISMA, FedRAMP HIPAA, PCI DSS poziom 1 i innych programów zgodności kluczy. Certyfikat ułatwia tworzenie własnych wymagań zgodności toomeet aplikacjami platformy Azure i tooaddress Twojego biznesowych szeroką gamę krajowych i międzynarodowych przepisów wymagania.

Więcej informacji:

* [Centrum zaufania Microsoft: zgodności](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Zaufanych chmury: Microsoft Azure zabezpieczeń, prywatności i zgodności](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
