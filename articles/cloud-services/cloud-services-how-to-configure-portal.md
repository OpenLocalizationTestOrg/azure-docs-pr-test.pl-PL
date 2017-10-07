---
title: "tooconfigure aaaHow usługi w chmurze (portal) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usług w chmurze tooconfigure na platformie Azure. Dowiedz się, konfiguracji usługi w chmurze hello tooupdate i skonfiguruj wystąpień toorole dostępu zdalnego. Poniższe przykłady użycia hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>W jaki sposób tooConfigure usług w chmurze
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-configure-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-configure.md)
>
>

Usługi w chmurze hello najczęściej używane ustawienia można skonfigurować w hello portalu Azure. Lub, jeśli chcesz tooupdate plikach konfiguracyjnych bezpośrednio, Pobierz tooupdate pliku konfiguracji usługi, a następnie przekaż hello zaktualizowany plik i aktualizacji hello usługi w chmurze hello zmian konfiguracji. W obu przypadkach aktualizacji konfiguracji hello są wypychani tooall wystąpień roli.

Można również zarządzać wystąpień hello role usługi w chmurze lub pulpitu zdalnego do nich.

Azure można tylko zapewnienia dostępności usług 99,95% podczas hello aktualizacji konfiguracji Jeśli masz co najmniej dwóch wystąpień roli dla każdej roli. Umożliwiająca jednego żądania klientów tooprocess maszyny wirtualnej podczas aktualizowania hello innych. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Zmiana usługi w chmurze
Po otwierającym hello [portalu Azure](https://portal.azure.com/), przejdź tooyour usługi w chmurze. W tym miejscu możesz zarządzać wiele aspektów.

![Ustawienia strony](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Witaj **ustawienia** lub **wszystkie ustawienia** łącza spowoduje to otwarcie hello **ustawienia** bloku, w którym można zmienić hello **właściwości**, zmień hello **Konfiguracji**, zarządzanie hello **certyfikaty**, Instalator **reguły alertów**i zarządzanie nimi hello **użytkowników** mają dostęp usługi w chmurze toothis.

![Blok ustawień usługi w chmurze Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Zarządzanie wersji systemu operacyjnego gościa

Domyślnie program Azure okresowo aktualizuje użytkownika gościa obrazu systemu operacyjnego toohello najnowszych obsługiwane w ramach hello rodziny systemów operacyjnych, określoną w konfiguracji usługi (cscfg), takie jak Windows Server 2016.

Tootarget określonych wersji systemu operacyjnego, należy można ustawić w hello **konfiguracji** bloku.

![Ustaw wersję systemu operacyjnego](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Wybranie określonych wersji systemu operacyjnego spowoduje wyłączenie automatycznego systemu operacyjnego aktualizacji i umożliwia stosowanie poprawek programu odpowiedzialności. Należy upewnić się, że wystąpienia roli otrzymują aktualizacje lub może narazić Twoje luk w zabezpieczeniach toosecurity aplikacji.

## <a name="monitoring"></a>Monitorowanie
Można dodać usługi w chmurze tooyour alertów. Kliknij przycisk **ustawienia** > **reguły alertu** > **Dodaj alert**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

W tym miejscu możesz skonfigurować alert. Z hello **Metryka** listy rozwijanej, można ustawić alert hello następujące typy danych.

* Odczytu dysku
* Zapisu na dysku
* Sieci w
* Sieci limit
* Procent użycia procesora CPU

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Skonfiguruj funkcję monitorowania z metryki kafelka
Zamiast **ustawienia** > **reguły alertów**, możesz kliknąć jeden z hello metryki kafelków w hello **monitorowanie** sekcji hello **chmury Usługa** bloku.

![Monitorowanie usługi w chmurze](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

W tym miejscu można dostosować wykres hello używane z kafelka hello, lub dodać reguły alertów.

## <a name="reboot-reimage-or-remote-desktop"></a>Ponowne uruchomienie komputera, odtworzenia z obrazu lub pulpitu zdalnego
W tej chwili nie można konfigurować usługi pulpitu zdalnego przy użyciu hello **portalu Azure**. Jednak można skonfigurować go za pośrednictwem hello [klasycznego portalu Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), lub za pomocą [programu Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Najpierw kliknij w wystąpieniu usługi chmury hello.

![Wystąpienie usługi w chmurze](./media/cloud-services-how-to-configure-portal/cs-instance.png)

Z hello bloku, który zostanie otwarty, możesz zainicjować połączenie pulpitu zdalnego, zdalnie ponownie hello, lub zdalnie odtworzenia z obrazu (start z obrazem świeże) hello wystąpieniu.

![Przyciski wystąpienia usługi chmury](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Skonfiguruj ponownie Twoje .cscfg
Może być konieczne tooreconfigure usługi w chmurze za pośrednictwem hello [konfiguracji usługi (cscfg)](cloud-services-model-and-package.md#cscfg) pliku. Najpierw należy toodownload Twojego .cscfg pliku, zmodyfikuj go, a następnie przekaż go.

1. Polecenie hello **ustawienia** ikony lub hello **wszystkie ustawienia** link tooopen się hello **ustawienia** bloku.

    ![Ustawienia strony](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Polecenie hello **konfiguracji** elementu.

    ![Blok konfiguracji](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Polecenie hello **Pobierz** przycisku.

    ![Do pobrania](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Po zaktualizowaniu pliku konfiguracji usługi hello, przekazywanie i stosowania aktualizacji konfiguracji hello:

    ![Upload](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Wybierz plik .cscfg hello, a następnie kliknij przycisk **OK**.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[wdrażania usługi w chmurze](cloud-services-how-to-create-deploy-portal.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).
