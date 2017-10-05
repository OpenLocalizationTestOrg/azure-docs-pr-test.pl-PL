---
title: "Ustawienia funkcji cloud App Discovery rejestru dla serwera Proxy usług | Dokumentacja firmy Microsoft"
description: "Celem tego tematu jest dostarczają czynności, które należy wykonać, aby ustawić wymaganego portu na komputerach z systemem agenta Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Ustawienia funkcji cloud Discovery aplikacji rejestru dla usługi serwera Proxy
Domyślnie agenta Cloud App Discovery jest skonfigurowany do użycia tylko porty 80 i 443. Jeśli planujesz zainstalowanie Cloud App Discovery w środowisku z serwera proxy, który jest używany niestandardowy port (80 ani 443), należy skonfigurować agentów do użycia tego portu. Konfiguracja jest oparta na kluczu rejestru.

Celem tego tematu jest dostarczają czynności, które należy wykonać, aby ustawić wymaganego portu na komputerach z systemem agenta Cloud App Discovery.

**Aby zmodyfikować port używany przez komputer z uruchomionym agentem Cloud App Discovery, wykonaj następujące czynności:**

1. Uruchom Edytor rejestru. <br> ![Uruchom polecenie](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Przejdź do lub utwórz następujący klucz rejestru: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud Discovery\Endpoint aplikacji** 
3. Utwórz nową **ciągu wielokrotnego** wartość o nazwie **porty**. ![Nowy](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Aby otworzyć **Edytowanie ciągu wielokrotnego** okna dialogowego, kliknij dwukrotnie wartość portów.
5. W polu tekstowym wartość danych wpisz następujące wartości, a następnie dodaj wszystkie porty niestandardowe, które są używane przez Twoją organizację: <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![Edytowanie ciągu wielokrotnego](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. Kliknij przycisk **OK** zamknąć **Edytowanie ciągu wielokrotnego** okna dialogowego.

**Dodatkowe zasoby**

* [Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji](active-directory-cloudappdiscovery-whatis.md) 

