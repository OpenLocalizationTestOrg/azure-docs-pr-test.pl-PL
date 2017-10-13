---
title: "Tworzenie projektu usługi w chmurze Azure z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się teraz utworzyć projekt usługi w chmurze Azure z programem Visual Studio"
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Tworzenie projektu usługi w chmurze Azure z programem Visual Studio
Azure Tools dla programu Visual Studio zawiera szablon projektu umożliwiający tworzenie usługi w chmurze Azure. Po utworzeniu projektu programu Visual Studio umożliwia konfigurowanie, debugowania i wdrożyć usługę w chmurze na platformie Azure.

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>Kroki, aby utworzyć projekt usługi w chmurze platformy Azure w programie Visual Studio
Ta sekcja przeprowadzi Cię przez proces tworzenia projektu usługi w chmurze platformy Azure w programie Visual Studio z co najmniej jedną rolę sieci web.  

1. Uruchom program Visual Studio jako administrator.

1. W menu głównym wybierz **pliku** > **nowy** > **projektu**.

1. Wybierz **chmury** z Visual C# lub Visual Basic projektu węzłów szablonu, a następnie wybierz **usługi w chmurze Azure** z listy szablonów.

    ![Nowa usługa w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Określenie, której wersji programu .NET Framework ma być używany do tworzenia projektu.

1. Wprowadź nazwę i lokalizację projektu i nazwy dla rozwiązania. 

1. Kliknij przycisk **OK**.

1. W **nową usługę w chmurze Azure Microsoft** okno dialogowe, wybierz role, które chcesz dodać, a następnie kliknij przycisk strzałki w prawo, aby dodać je do rozwiązania.

    ![Wybierz nowe role usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. Aby zmienić nazwę roli, do której dodano, umieść kursor na rolę w **nową usługę w chmurze Azure Microsoft** okna dialogowego i z menu kontekstowego wybierz **Zmień nazwę**. Można również zmienić nazwy roli w ramach rozwiązania (w **Eksploratora rozwiązań**) po został dodany.

    ![Zmień nazwę roli usługi w chmurze Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Projektu programu Visual Studio Azure ma skojarzenia do roli projektów w rozwiązaniu. Projekt zawiera również *pliku definicji usługi* i *pliku konfiguracji usługi*:

- **Plik definicji usługi** — definiuje ustawienia środowiska uruchomieniowego dla aplikacji, w tym, jakie role są wymagane, punktów końcowych i rozmiar maszyny wirtualnej. 
- **Plik konfiguracji usługi** — konfiguruje liczbę wystąpień roli są wykonane i wartości ustawienia zdefiniowane dla roli. 

Aby uzyskać więcej informacji o tych plikach, zobacz [konfigurowania ról dla usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Następne kroki
- [Zarządzanie rolami w projekty usługi w chmurze Azure z programem Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
