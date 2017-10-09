---
title: "Ustawienia rejestru odnajdywania aplikacji dla usługi serwera Proxy aaaCloud | Dokumentacja firmy Microsoft"
description: "cel Hello tego tematu jest tooprovide program hello kroki należy dodać port hello wymagane tooset tooperform na powitania komputerach hello agenta Cloud App Discovery."
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Ustawienia funkcji cloud Discovery aplikacji rejestru dla usługi serwera Proxy
Domyślnie agenta Cloud App Discovery hello jest skonfigurowany toouse tylko porty hello 80 i 443. Jeśli planujesz zainstalowanie Cloud App Discovery w środowisku z serwera proxy, który jest używany niestandardowy port (80 ani 443), należy tooconfigure Twojego toouse agentów tego portu. Konfiguracja Hello jest oparta na klucz rejestru.

cel Hello tego tematu jest tooprovide program hello kroki należy dodać port hello wymagane tooset tooperform na powitania komputerach hello agenta Cloud App Discovery.

**toomodify hello port używany przez program hello komputerze agenta Cloud App Discovery hello, wykonaj następujące kroki hello:**

1. Uruchom Edytor rejestru hello. <br> ![Uruchom polecenie](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. Przejdź tooor utworzyć powitania po klucz rejestru: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud Discovery\Endpoint aplikacji** 
3. Utwórz nową **ciągu wielokrotnego** wartość o nazwie **porty**. ![Nowy](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. Witaj tooopen **Edytowanie ciągu wielokrotnego** okna dialogowego, kliknij dwukrotnie wartość porty hello.
5. W pole tekstowe danych wartości hello wpisz następujące wartości hello i dodać wszystkie porty niestandardowe, które są używane przez Twoją organizację: <br><br>
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
6. Kliknij przycisk **OK** tooclose hello **Edytowanie ciągu wielokrotnego** okna dialogowego.

**Dodatkowe zasoby**

* [Jak odnajdywać niezatwierdzone aplikacje w chmurze używanych mojej organizacji](active-directory-cloudappdiscovery-whatis.md) 

