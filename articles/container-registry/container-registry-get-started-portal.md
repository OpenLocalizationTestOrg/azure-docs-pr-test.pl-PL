---
title: prywatne aaaCreate Docker rejestru - portalu Azure | Dokumentacja firmy Microsoft
description: "Rozpocząć tworzenie i zarządzanie nimi prywatnej rejestrów kontenera Docker z hello portalu Azure"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40f3ce44fea26e5fbeca865c9da6df55c2df9511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-portal"></a>Utwórz prywatne rejestru kontenera Docker przy użyciu hello portalu Azure
Użyj hello Azure toocreate portalu rejestru kontenera i zarządzać ustawieniami. Można również utworzyć i zarządzać nimi za pomocą hello rejestrów kontenera [poleceń Azure CLI 2.0](container-registry-get-started-azure-cli.md), [programu Azure PowerShell](container-registry-get-started-powershell.md) lub programowo hello rejestru kontenera [interfejsu API REST](https://go.microsoft.com/fwlink/p/?linkid=834376).

Tło i pojęcia dla [hello omówienie](container-registry-intro.md).

## <a name="create-a-container-registry"></a>Tworzenie rejestru kontenerów
1. W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **+ nowy**.
2. Marketplace hello wyszukiwania dla **rejestru kontenera platformy Azure**.
3. Wybierz pozycję **Azure Container Registry**, której wydawcą jest firma **Microsoft**.
    ![Usługa Container Registry w portalu Azure Marketplace](./media/container-registry-get-started-portal/container-registry-marketplace.png)
4. Kliknij przycisk **Utwórz**. Witaj **rejestru kontenera Azure** zostanie wyświetlony blok.

    ![Ustawienia usługi Container Registry](./media/container-registry-get-started-portal/container-registry-settings.png)
5. W hello **rejestru kontenera Azure** bloku, wprowadź hello następujących informacji. Po zakończeniu kliknij przycisk **Utwórz**.

    a. **Nazwa rejestru**: globalnie unikatowa nazwa domeny najwyższego poziomu dla określonego rejestru. W tym przykładzie nazwa rejestru hello jest *myRegistry01*, ale podstawić własną unikatową nazwę. Nazwa Hello może zawierać tylko litery i cyfry.

    b. **Grupa zasobów**: Wybierz istniejący [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej.

    c. **Lokalizacja**: Wybierz lokalizację centrum danych Azure, gdzie usługa hello jest [dostępne](https://azure.microsoft.com/regions/services/), takich jak **południowo-środkowe stany**.

    d. **Administrator**: należy włączyć rejestru hello tooaccess użytkownika Administrator. Można zmienić to ustawienie po utworzeniu hello rejestru.

      > [!IMPORTANT]
      > Ponadto tooproviding uzyskiwać dostęp do konta administratora, rejestrów kontenera obsługę uwierzytelniania kopii podmiotów zabezpieczeń usługi Azure Active Directory. Więcej informacji i zagadnień do rozważenia znajduje się w temacie [Authenticate with a container registry](container-registry-authentication.md) (Uwierzytelnianie za pomocą rejestru kontenerów).
      >

    e. **Konto magazynu**: Użyj hello domyślne ustawienie toocreate [konta magazynu](../storage/common/storage-introduction.md), lub wybierz istniejące konto magazynu w hello tej samej lokalizacji. Usługa Premium Storage nie jest obecnie obsługiwana.

## <a name="manage-registry-settings"></a>Zarządzanie ustawieniami rejestru
Po utworzeniu hello rejestru, Znajdź hello ustawień rejestru należy uruchomić na powitania **rejestrów kontenera** bloku w portalu hello. Na przykład może być konieczne hello toolog ustawień w rejestrze tooyour lub może być tooenable lub wyłączyć hello administrator.

1. Na powitania **rejestrów kontenera** bloku, kliknij nazwę hello rejestru.

    ![Blok rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-blade.png)
2. toomanage ustawień dostępu, kliknij przycisk **klucz dostępu**.

    ![Dostęp do rejestru kontenerów](./media/container-registry-get-started-portal/container-registry-access.png)
3. Należy zwrócić uwagę hello następujące ustawienia:

   * **Serwer logowania** -hello w pełni kwalifikowanej nazwy użyj toolog w rejestrze toohello. W tym przykładzie jest to `myregistry01.azurecr.io`.
   * **Administrator** — Przełącz tooenable lub wyłączenie konta administratora hello rejestru.
   * **Nazwa użytkownika** i **hasło** — Witaj poświadczeń konta administratora hello (jeśli jest włączona) toolog można użyć w rejestrze toohello. Opcjonalnie można ponownie wygenerować hello hasła. Dwa hasła są tworzone, dzięki czemu można zachować rejestru toohello połączenia za pomocą jednego hasła podczas ponownego generowania hello inne hasło. Zamiast tego zobacz tooauthenticate z nazwy głównej usługi [uwierzytelniony przez prywatne rejestru kontenera Docker](container-registry-authentication.md).

## <a name="next-steps"></a>Następne kroki
* [Pierwszy obraz przy użyciu interfejsu wiersza polecenia Docker hello push](container-registry-get-started-docker-cli.md)
