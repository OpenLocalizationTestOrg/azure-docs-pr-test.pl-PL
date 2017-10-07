---
title: "aaaManaging ról na platformie Azure cloud services z programem Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd i usuwanie ról na platformie Azure cloud services z programem Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Zarządzanie rolami w usług w chmurze Azure z programem Visual Studio
Po utworzeniu usługi w chmurze platformy Azure, można dodać nowe role tooit lub usuwać istniejących ról. Można także zaimportować istniejący projekt i przekonwertować go tooa roli. Można na przykład zaimportować aplikację sieci web platformy ASP.NET i wyznaczanie roli sieci web.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Dodawanie tooan roli usługi w chmurze Azure
Hello następujące kroki prowadzące przez dodawanie sieci web lub procesu roboczego roli tooan Azure projektu usługi w chmurze w programie Visual Studio.

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello

1. Kliknij prawym przyciskiem myszy hello **ról** menu kontekstowe hello toodisplay węzłów. Wybierz z menu kontekstowego hello **Dodaj**, następnie wybierz istniejącą rolę sieci web lub roli proces roboczy z bieżącego rozwiązania hello lub Utwórz projekt roli sieci web lub procesu roboczego. Można również wybrać odpowiedni projekt, takich jak projekt aplikacji sieci web platformy ASP.NET i skojarzyć go z projektu roli.

    ![Menu Opcje tooadd projektu usługi w chmurze Azure tooan roli](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Usunięcie roli z usługi w chmurze Azure
Witaj następujące kroki prowadzące przez usunięcie roli sieci web lub procesu roboczego z projektu usługi w chmurze platformy Azure w programie Visual Studio.

1. Utwórz lub Otwórz projekt usługi w chmurze platformy Azure w programie Visual Studio.

1. W **Eksploratora rozwiązań**, rozwiń węzeł projektu hello

1. Rozwiń węzeł hello **ról** węzła.

1. Kliknij prawym przyciskiem myszy hello węzła tooremove, a następnie, wybierz z menu kontekstowego hello **Usuń**. 

    ![Menu Opcje tooadd tooan roli usługi w chmurze Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Ponowne dodawanie projektu usługi w chmurze Azure tooan roli
Usuń rolę z projektu usługi w chmurze, ale później zdecyduje tooadd hello powrotem rolę toohello projektu, tylko hello roli deklaracji i Podstawowe atrybuty, takie jak punkty końcowe i informacje diagnostyczne, zostaną dodane. Nie dodatkowe zasoby lub odwołania są dodawane toohello `ServiceDefinition.csdef` pliku lub toohello `ServiceConfiguration.cscfg` pliku. Jeśli chcesz tooadd te informacje, należy toomanually go z powrotem dodać do tych plików.

Na przykład można usunąć roli usługi sieci web, a później zdecyduje tooadd kopii tej roli w ramach rozwiązania. Jeśli to zrobisz, występuje błąd. tooprevent ten błąd, masz tooadd hello `<LocalResources>` element pokazano powitania po XML z powrotem do hello `ServiceDefinition.csdef` pliku. Użyj nazwy hello hello roli usługi sieci web, która dodane do projektu hello jako część atrybut nazwy hello hello  **<LocalStorage>**  elementu. W tym przykładzie nazwa hello roli usługi sieci web hello jest **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Następne kroki
- [Konfigurowanie ról powitania dla usługi w chmurze Azure z programem Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
