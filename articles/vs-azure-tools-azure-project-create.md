---
title: "aaaCreating projekt usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz toocreate projekt usługi w chmurze Azure z programem Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Tworzenie projektu usługi w chmurze Azure z programem Visual Studio
Hello Azure Tools dla programu Visual Studio zawiera szablon projektu umożliwiający tworzenie usługi w chmurze Azure. Po utworzeniu hello projektu programu Visual Studio umożliwia tooconfigure, debugowania i wdrażania tooAzure usługi chmury hello.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Kroki toocreate projekt usługi w chmurze platformy Azure w programie Visual Studio
Ta sekcja przeprowadzi Cię przez proces tworzenia projektu usługi w chmurze platformy Azure w programie Visual Studio z co najmniej jedną rolę sieci web.  

1. Uruchom program Visual Studio jako administrator.

1. W menu głównym hello wybierz **pliku** > **nowy** > **projektu**.

1. Wybierz **chmury** z hello Visual C# lub Visual Basic projektu węzłów szablonu, a następnie wybierz **usługi w chmurze Azure** z hello listę szablonów.

    ![Nowa usługa w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Określ wersję hello .NET Framework ma toouse toodevelop Twojego projektu.

1. Wprowadź nazwę i lokalizację projektu i nazwę hello rozwiązania. 

1. Kliknij przycisk **OK**.

1. W hello **nową usługę w chmurze Azure Microsoft** okno dialogowe, wybierz hello role mają tooadd i wybierz tooadd przycisk strzałki w prawo hello ich tooyour rozwiązania.

    ![Wybierz nowe role usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename roli zostały dodane, aktywowania roli hello w hello **nową usługę w chmurze Azure Microsoft** okna dialogowego i wybierz z menu kontekstowego hello, **zmienić**. Można również zmienić nazwy roli w ramach rozwiązania (w hello **Eksploratora rozwiązań**) po został dodany.

    ![Zmień nazwę roli usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Projekt programu Visual Studio Azure Hello ma skojarzenia toohello roli projektów w rozwiązaniu hello. Projekt Hello zawiera również hello *pliku definicji usługi* i *pliku konfiguracji usługi*:

- **Plik definicji usługi** — definiuje ustawienia środowiska uruchomieniowego hello aplikacji, w tym, jakie role są wymagane, punktów końcowych i rozmiar maszyny wirtualnej. 
- **Plik konfiguracji usługi** — konfiguruje liczbę wystąpień roli są uruchamiane i hello wartości hello ustawienia zdefiniowane dla roli. 

Aby uzyskać więcej informacji o tych plikach, zobacz [konfigurowania ról hello na potrzeby usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Następne kroki
- [Zarządzanie rolami w projekty usługi w chmurze Azure z programem Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
