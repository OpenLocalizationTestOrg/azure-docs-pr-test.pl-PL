---
title: "aaaEnable Podłączanie pulpitu zdalnego dla roli w usług Azure Cloud Services | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure platformy azure w chmurze usługi połączeń pulpitu zdalnego tooallow aplikacji"
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
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Program Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Pulpit zdalny umożliwia pulpitu hello tooaccess roli działające na platformie Azure. Można użyć tootroubleshoot połączenia pulpitu zdalnego i diagnozowanie problemów z aplikacją, jest uruchomiona.

Umożliwia Podłączanie pulpitu zdalnego w roli podczas tworzenia przez uwzględnienie hello modułów usług pulpitu zdalnego w definicji usługi. można też tooenable pulpitu zdalnego za pośrednictwem hello rozszerzenia usług pulpitu zdalnego. Hello preferowana metoda się toouse hello pulpitu zdalnego rozszerzenie można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello bez konieczności tooredeploy aplikacji.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Konfigurowanie pulpitu zdalnego z hello portalu Azure
Hello portalu Azure używa hello podejście rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello. Witaj **pulpitu zdalnego** bloku dla usługi w chmurze pozwala tooenable pulpitu zdalnego, zmiana konta administratora lokalnego hello używane maszyny wirtualne toohello tooconnect, hello certyfikat używany podczas uwierzytelniania i ustawić hello Data wygaśnięcia.

1. Kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **pulpitu zdalnego**.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Wybierz, czy tooenable pulpitu zdalnego dla poszczególnych ról lub dla wszystkich ról, a następnie zmienić wartości hello przełącznik hello zbyt**włączone**.

3. Wypełnij pola hello wymagane podanie nazwy użytkownika, hasła, wygaśnięcia i certyfikatów.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Wszystkie wystąpienia roli zostanie ponownie uruchomiony, gdy najpierw włączyć pulpitu zdalnego i kliknij przycisk OK (znacznikiem wyboru). tooprevent ponowne uruchomienie komputera, hello certyfikatu używane tooencrypt hello hasło musi być zainstalowany na powitania roli. tooprevent ponowne uruchomienie, [przekazywanie certyfikatu dla usługi w chmurze hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , a następnie wróć toothis okna dialogowego.
   >
   >
3. W **ról**, wybierz rolę hello tooupdate lub wybierz **wszystkie** dla wszystkich ról.

4. Po zakończeniu aktualizacji konfiguracji, kliknij przycisk **zapisać**. Potrwa kilka minut, zanim wystąpienia roli będą gotowe tooreceive połączenia.

## <a name="remote-into-role-instances"></a>Zdalne do wystąpień roli
Włączenie pulpitu zdalnego na powitania ról, możesz zainicjować połączenie bezpośrednio z hello portalu Azure:

1. Kliknij przycisk **wystąpień** tooopen hello **wystąpień** bloku.
2. Wybierz wystąpienia roli, który ma pulpitu zdalnego skonfigurowane.
3. Kliknij przycisk **Connect** toodownload RDP plik hello wystąpienia roli.

    ![Pulpit zdalny usługi w chmurze](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Kliknij przycisk **Otwórz** , a następnie **Connect** toostart hello Podłączanie pulpitu zdalnego.

>[!NOTE]
> Usługi w chmurze jest działo za grupy NSG, może być konieczne toocreate reguł, które zezwalają na ruch na portach **3389** i **20000**.  Pulpit zdalny używa portu **3389**.  Wystąpienia usługi chmury jest równoważone, więc nie można bezpośrednio kontrolować tooconnect wystąpienia, które do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów zarządzania na ruch RDP i Zezwalaj na powitania klienta toosend pliku cookie protokołu RDP i określ tooconnect poszczególnych wystąpień do.  Witaj *RemoteForwarder* i *RemoteAccess* agentów wymagają tego portu **20000*** otwarty, które mogą być zablokowane, jeśli masz grupy NSG.

## <a name="additional-resources"></a>Dodatkowe zasoby

[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)
