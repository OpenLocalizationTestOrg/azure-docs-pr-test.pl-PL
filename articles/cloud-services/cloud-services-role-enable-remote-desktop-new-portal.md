---
title: "Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować aplikację usługi chmury azure, aby umożliwić połączenia pulpitu zdalnego"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: b9ae4442f57170746eb0de94849b09625be51264
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure
> [!div class="op_single_selector"]
> * [Azure portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Program PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Program Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Pulpit zdalny umożliwia dostęp do pulpitu z poziomu roli uruchomionej w systemie Azure. Podłączanie pulpitu zdalnego umożliwia rozwiązywanie problemów i diagnozowanie problemów z aplikacją, gdy jest on uruchomiony.

Umożliwia Podłączanie pulpitu zdalnego w roli podczas tworzenia przez moduły pulpitu zdalnego w tym w definicji usługi lub można włączyć pulpitu zdalnego za pomocą rozszerzenia usług pulpitu zdalnego. Jest to preferowane rozwiązanie próbę użycia rozszerzenia usług pulpitu zdalnego, jak można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji bez konieczności ponownego wdrażania aplikacji.

## <a name="configure-remote-desktop-from-the-azure-portal"></a>Konfigurowanie pulpitu zdalnego z portalu Azure
Portalu Azure używa metody rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji. **Pulpitu zdalnego** bloku dla usługi w chmurze pozwala na włączenie pulpitu zdalnego, zmień konta administratora lokalnego używanego do łączenia się z maszynami wirtualnymi, certyfikat używane podczas uwierzytelniania oraz ustawianie daty wygaśnięcia.

1. Kliknij przycisk **usługi w chmurze**, kliknij nazwę usługi w chmurze, a następnie kliknij przycisk **pulpitu zdalnego**.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Wybierz, czy chcesz włączyć Pulpit zdalny dla poszczególnych ról lub dla wszystkich ról, a następnie zmień wartość przełącznik do **włączone**.

3. Wypełnij wymagane pola dla nazwy użytkownika, hasła, wygaśnięcia i certyfikatów.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Wszystkie wystąpienia roli zostanie ponownie uruchomiony, gdy najpierw włączyć pulpitu zdalnego i kliknij przycisk OK (znacznikiem wyboru). Aby uniknąć ponownego uruchomienia systemu, certyfikat używany do szyfrowania hasła musi być instalowany w roli. Aby uniknąć ponownego uruchomienia, [Prześlij certyfikat usługi w chmurze](cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate) , a następnie wróć do tego okna dialogowego.
   >
   >
3. W **ról**, wybierz rolę, aby zaktualizować lub wybierz **wszystkie** dla wszystkich ról.

4. Po zakończeniu aktualizacji konfiguracji, kliknij przycisk **zapisać**. Potrwa kilka minut przed wystąpienia roli są gotowe do odbierania połączeń.

## <a name="remote-into-role-instances"></a>Zdalne do wystąpień roli
Po włączeniu ról usług pulpitu zdalnego może zainicjować połączenie bezpośrednio z portalu Azure:

1. Kliknij przycisk **wystąpień** otworzyć **wystąpień** bloku.
2. Wybierz wystąpienia roli, który ma pulpitu zdalnego skonfigurowane.
3. Kliknij przycisk **Connect** można pobrać pliku RDP dla wystąpienia roli.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Kliknij przycisk **Otwórz** , a następnie **Connect** nawiązaniu połączenia pulpitu zdalnego.

>[!NOTE]
> Usługi w chmurze jest działo za grupy NSG, może być konieczne utworzenie reguły zezwalające na ruch na portach **3389** i **20000**.  Pulpit zdalny używa portu **3389**.  Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować którego wystąpienia, aby nawiązać połączenie.  *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i umożliwić klientom wysyłanie plików cookie protokołu RDP i określ poszczególne wystąpienia do nawiązania połączenia.  *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.

## <a name="additional-resources"></a>Zasoby dodatkowe

[Jak skonfigurować usługi w chmurze](cloud-services-how-to-configure-portal.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)
