---
title: "Szyfrowanie dysków Azure — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera odpowiedzi na często zadawane pytania dotyczące Microsoft Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 0d15bf42c156ea7a72c54d690f4016877913efe4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Szyfrowanie dysków Azure — często zadawane pytania (FAQ)

Często zadawane pytania odpowiedzi na pytania dotyczące szyfrowania dysków Azure dla systemu Windows i Linux maszyn wirtualnych IaaS, aby uzyskać więcej informacji na temat tej usługi, przeczytaj [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Pytania ogólne
**PYTANIE** Jaki jest szyfrowania dysków Azure w GA?

**Odpowiedź:** szyfrowania dysków Azure dla systemu Windows oraz maszyny wirtualne IaaS systemu Linux jest dostępna w GA we wszystkich regionach publicznej Azure.

**Pytanie:** napotyka użytkownika są dostępne w przypadku szyfrowania dysków Azure?

**Odpowiedź:** GA szyfrowania dysków Azure obsługuje szablony usługi Azure Resource Manager, programu Azure PowerShell, interfejsu wiersza polecenia Azure. Zapewnia dużą elastyczność w tym ma trzy różne opcje dotyczące włączania szyfrowania dysku dla maszyn wirtualnych IaaS. Więcej informacji na temat środowiska użytkownika i wskazówki krok po kroku są dostępne w scenariuszach wdrażania szyfrowania dysków Azure i środowiska.

**Pytanie:** ile kosztuje szyfrowania dysków Azure?

**Odpowiedź:** bezpłatnie szyfrowania dysków maszyny Wirtualnej przy użyciu szyfrowania dysków Azure nie istnieje.

**Pytanie:** jakie warstwy maszyny wirtualnej można używać szyfrowania dysków Azure z?

**Odpowiedź:** szyfrowania dysków Azure jest dostępna tylko w standardowej warstwie maszyn wirtualnych w tym [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) i tak dalej maszyn wirtualnych IaaS serii maszyn wirtualnych w tym z magazyn w warstwie premium. Nie jest dostępna na podstawowych maszynach wirtualnych warstwy.

**Pytanie:** dystrybucje systemu Linux co to są obsługiwane przez szyfrowanie dysków Azure?

**Odpowiedź:** szyfrowania dysków Azure jest obsługiwane w następujących dystrybucje serwera systemu Linux i wersji:

| Dystrybucja systemu Linux | Wersja | Typ woluminu obsługiwany w przypadku szyfrowania|
| --- | --- |--- |
| Ubuntu | 16.04 — CODZIENNIE LTS | Dysk systemu operacyjnego i danych |
| Ubuntu | 14.04.5-DAILY-LTS | Dysk systemu operacyjnego i danych |
| RHEL | 7.3 | Dysk systemu operacyjnego i danych |
| RHEL | 7.2 | Dysk systemu operacyjnego i danych |
| RHEL | 6.8 | Dysk systemu operacyjnego i danych |
| RHEL | 6.7 | Dysk z danymi |
| CentOS | 7.3 | Dysk systemu operacyjnego i danych |
| CentOS | 7.2n | Dysk systemu operacyjnego i danych |
| CentOS | 6.8 | Dysk systemu operacyjnego i danych |
| CentOS | 7.1 | Dysk z danymi |
| CentOS | 7.0 | Dysk z danymi |
| CentOS | 6.7 | Dysk z danymi |
| CentOS | 6.6 | Dysk z danymi |
| CentOS | 6.5 | Dysk z danymi |
| openSUSE | 13.2 | Dysk z danymi |
| SLES | 12 Z DODATKIEM SP1 | Dysk z danymi |
| SLES | Priorytet: 12-z dodatkiem SP1 | Dysk z danymi |
| SLES | HPC 12 | Dysk z danymi |
| SLES | Priorytet: 11-SP4 | Dysk z danymi |
| SLES | 11 Z DODATKIEM SP4 | Dysk z danymi |

**Pytanie:** jak I rozpoczęcie pracy przy użyciu szyfrowania dysków Azure?

**Odpowiedź:** klientów można dowiedzieć się, jak rozpocząć odczytując w dokumencie szyfrowania dysków Azure znajduje się [tutaj](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**Pytanie:** można zaszyfrować woluminów zarówno rozruchu i danych za pomocą szyfrowania dysków Azure?

**Odpowiedź:** tak, można zaszyfrować woluminy rozruchowe i danych systemu Windows i maszyn wirtualnych systemu Linux IaaS. Dla maszyn wirtualnych systemu Windows nie można zaszyfrować dane bez pierwszy encrpting woluminu systemu operacyjnego. Dla maszyn wirtualnych systemu Linux można zaszyfrować najpierw ilość danych bez woluminu encryptinng systemu operacyjnego. Gdy wolumin systemu operacyjnego zostały zaszyfrowane na klastrach, wyłączenie szyfrowania na woluminie systemu operacyjnego dla maszyn wirtualnych systemu Linux IaaS nie jest obsługiwane

**Pytanie:** włączone jest szyfrowanie dysków Azure "bring your own key" (BYOK) możliwości?

**Odpowiedź:** tak, możesz podać własne klucze szyfrowania kluczy. Te klucze są chronione w usłudze Azure Key Vault, która jest magazynu kluczy do szyfrowania dysków Azure. Więcej szczegółów w scenariuszach Obsługa kluczy szyfrowania zapoznaj się z szyfrowania dysków Azure wdrożeń i środowisk

**Pytanie:** można użyć klucza szyfrowania kluczy Azure utworzonych?

**Odpowiedź:** tak, można użyć usługi Azure Key vault do wygenerowania klucza szyfrowania do użycia szyfrowania dysków Azure. Te klucze są chronione w usłudze Azure Key Vault, która jest magazynu kluczy do szyfrowania dysków Azure. Więcej szczegółów w scenariuszach Obsługa kluczy szyfrowania zapoznaj się z szyfrowania dysków Azure wdrożeń i środowisk

**Pytanie:** można użyć usługi zarządzania kluczami lokalnymi/HSM w celu ochrony kluczy szyfrowania?

**Odpowiedź:** usługi zarządzania kluczami lokalnymi/HSM nie można użyć do ochrony kluczy szyfrowania przy użyciu szyfrowania dysków Azure. Usługi magazynu kluczy Azure służy tylko do ochrony kluczy szyfrowania. Więcej szczegółów w scenariuszach Obsługa kluczy szyfrowania zapoznaj się z szyfrowania dysków Azure wdrożeń i środowisk

**Pytanie:** szyfrowanie dysków jakie są wymagania wstępne, aby skonfigurować Azure?

**Odpowiedź:** Azure dysku szyfrowania wymagań wstępnych skrypt programu PowerShell do tworzenia aplikacji w usłudze AAD, utworzyć nowego magazynu kluczy lub Instalator istniejącego magazynu kluczy dla dostępu do szyfrowania dysku włączyć szyfrowanie i ochronę kluczy tajnych i klucza.  Więcej szczegółów w scenariuszach Obsługa kluczy szyfrowania Zobacz wymagań wstępnych szyfrowania dysków Azure i wdrożeń i środowisk

**Pytanie:** gdzie można uzyskać więcej informacji na temat sposobu konfigurowania szyfrowania dysków Azure przy użyciu programu PowerShell?

**Odpowiedź:** mamy niektóre dużą artykuły, w jaki sposób można wykonywać podstawowe zadania szyfrowania dysków Azure, a także bardziej zaawansowanych scenariuszy. Do podstawowych zadań, zapoznaj się z Eksploruj [szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Aby uzyskać bardziej zaawansowanych scenariuszy, zobacz Eksploruj [szyfrowania dysków Azure przy użyciu programu Azure PowerShell — część 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**Pytanie:** jakiej wersji programu Azure PowerShell jest obsługiwana przez szyfrowanie dysków Azure?

**Odpowiedź:** używać najnowszej wersji wersji zestawu SDK usługi Azure PowerShell do konfigurowania szyfrowania dysków Azure. Pobierz najnowszą wersję [programu Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Szyfrowanie dysków Azure nie jest obsługiwana przez zestaw Azure SDK w wersji 1.1.0.

> [!NOTE]
> Rozszerzenie podglądu szyfrowania dysku systemu Linux platformy Azure jest przestarzały. Aby uzyskać więcej informacji, zapoznaj się dokumentacją [tutaj](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**Pytanie:** I zastosować szyfrowanie dysków Azure na mój niestandardowego obrazu systemu Linux?

**Odpowiedź:** szyfrowania dysków Azure nie można zastosować do niestandardowego obrazu systemu Linux. Firma Microsoft obsługuje tylko obrazy Linux galerii dla obsługiwanych dystrybucjach wymienione powyżej. Obecnie nie jest obsługiwana niestandardowych obrazów systemu Linux

**Pytanie:** I aktualizacje można stosować do Red Hat Maszynę wirtualną systemu Linux przy użyciu Yum aktualizacji?

**Odpowiedź:** tak, można wykonać operacji aktualizacji i lub poprawka Red Hat Linnux maszyny Wirtualnej zgodnie ze wskazówkami podanymi [tutaj](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**Pytanie:** I gdzie mogą aby zadać pytanie lub Prześlij opinię

**Odpowiedź:** zapewniają zadać pytania lub opinie na forum szyfrowania dysków Azure [tutaj](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono więcej informacji na temat najczęstsze pytania dotyczące szyfrowania dysków Azure, aby uzyskać więcej informacji na temat tej usługi i jego możliwości odczytu:

- [Zastosuj szyfrowanie dysków w Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Szyfrowanie maszyny wirtualnej platformy Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Danych Azure szyfrowania na Rest](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
