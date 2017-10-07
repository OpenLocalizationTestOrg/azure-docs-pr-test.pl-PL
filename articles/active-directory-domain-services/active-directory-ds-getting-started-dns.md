---
title: "Azure Active Directory Domain Services: Aktualizowanie ustawień DNS dla sieci wirtualnej platformy Azure hello | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do usługi Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Włączanie usług Azure Active Directory Domain Services (wersja zapoznawcza)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Zadanie 4: aktualizowanie ustawień DNS na potrzeby hello sieci wirtualnej platformy Azure
W hello poprzedzających zadania konfiguracji została pomyślnie włączona Azure Active Directory Domain Services dla katalogu. następne zadanie Hello jest tooensure, że komputery w sieci wirtualnej hello łączyć i korzystanie z tych usług. W tym artykule należy zaktualizować ustawienia serwera DNS hello sieci wirtualnej toopoint toohello dwa adresy IP gdzie usług domenowych Azure Active Directory jest dostępny w sieci wirtualnej hello.

tooupdate hello ustawienia serwera DNS dla sieci wirtualnej hello, w której włączono usługi Azure Active Directory Domain Services, pełną hello następujące kroki:

1. Witaj **omówienie** karta zawiera zestaw **wymagane kroki konfiguracji** toobe wykonać po domeny zarządzanej jest w pełni zaaprowizowanym. pierwszym krokiem konfiguracji Hello jest **ustawienia serwera DNS aktualizacji dla sieci wirtualnej**.

    ![Usługi Domain Services — karta Przegląd po pełnej aprowizacji](./media/getting-started/domain-services-provisioned-overview.png)

2. Gdy domena zostanie w pełni zaaprowizowana, na tym kafelku będą wyświetlane dwa adresy IP. Każdy z tych adresów IP reprezentuje kontroler domeny dla domeny zarządzanej.

3. pierwszy adres IP toocopy hello tooclipboard adresów, kliknij przycisk hello kopiowania przycisku Dalej tooit. Następnie kliknij przycisk hello **serwerów DNS skonfigurować** przycisku.

4. Wklej hello pierwszego adresu IP do hello **serwer DNS dodać** textbox w hello **serwerów DNS** bloku. Przewijane w poziomie toohello toocopy hello drugiego adresu IP w lewo i wklej go do hello **serwera DNS Dodaj** pola tekstowego.

    ![Usługi Domain Services — aktualizacja usługi DNS](./media/getting-started/domain-services-update-dns.png)

5. Kliknij przycisk **zapisać** po zakończeniu serwerów DNS hello tooupdate hello sieci wirtualnej.

> [!NOTE]
> Maszyny wirtualne w sieci hello pobierają tylko nowe ustawienia DNS powitania po ponownym uruchomieniu. Jeśli potrzebne ustawienia DNS tooget hello zaktualizowane od razu, wyzwolić ponowne uruchomienie komputera przez hello portal, programu PowerShell lub hello interfejsu wiersza polecenia.
>
>

## <a name="next-step"></a>Następny krok
[Zadanie 5: Włączanie tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory](active-directory-ds-getting-started-password-sync.md)
