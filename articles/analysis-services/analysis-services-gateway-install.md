---
title: Brama danych lokalnych aaaInstall | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooinstall i skonfiguruj bramę danych lokalnego."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Zainstaluj i skonfiguruj bramę danych lokalnych
Brama danych lokalnych jest wymagany, jeśli co najmniej jeden serwer usług Azure Analysis Services w hello sam region połączenia tooon lokalnych źródeł danych. Zobacz toolearn więcej informacji na temat bramy hello [bramy danych lokalnych](analysis-services-gateway.md).

## <a name="prerequisites"></a>Wymagania wstępne
**Minimalne wymagania:**

* .NET 4.5 framework
* 64-bitowej wersji systemu Windows 7 / Windows Server 2008 R2 (lub nowszy)

**Zalecane:**

* 8 rdzeni procesora CPU
* 8 GB pamięci
* 64-bitowej wersji systemu Windows 2012 R2 (lub nowszy)

**Ważne kwestie:**

* Podczas instalacji przy rejestracji bramy w usłudze Azure wybrano hello domyślnego regionu dla Twojej subskrypcji. Można wybrać inny region. Jeśli masz serwery w więcej niż jeden region, należy zainstalować bramy dla każdego regionu. 
* Witaj bramy nie można zainstalować na kontrolerze domeny.
* Na jednym komputerze można zainstalować tylko jedną bramę.
* Zainstaluj bramę hello na komputerze, który pozostaje na, a nie przechodzi toosleep.
* Nie należy instalować bramy hello sieci tooyour bezprzewodowo podłączonego komputera. Wydajność może być mniejsza.


## <a name="download"></a>Pobierz
 [Pobierz hello bramy](https://aka.ms/azureasgateway)

## <a name="install"></a>Zainstaluj

1. Uruchom Instalatora.

2. Wybierz lokalizację, zaakceptuj postanowienia hello, a następnie kliknij przycisk **zainstalować**.

   ![Zainstaluj lokalizacji oraz postanowienia licencyjne](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Wybierz **lokalnych danych bramy (zalecane)**. Azure Analysis Services nie obsługuje trybu osobistych.

   ![Wybierz typ bramy](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Wprowadź konto toosign tooAzure. Witaj, konto musi być w Twojej dzierżawy usługi Azure Active Directory. To konto jest używane dla hello administratora bramy. 

   ![Wprowadź konto toosign w tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Jeśli możesz zalogować się przy użyciu konta domeny, będzie on zamapowany tooyour konto organizacyjne w usłudze Azure AD. Konta organizacyjnego będzie służyć jako administrator bramy hello hello.

## <a name="register"></a>Rejestr
W kolejności toocreate zasobu bramy na platformie Azure możesz zarejestrować hello lokalne wystąpienie instalowania z hello usługi bramy w chmurze. 

1.  Wybierz **zarejestrować nową bramę na tym komputerze**.

    ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Wpisz nazwę i odzyskiwanie klucza bramy. Domyślnie brama hello używa Twojej subskrypcji domyślnego regionu. Jeśli potrzebujesz tooselect inny region, wybierz **Region zmiany**.

   ![Zarejestruj subskrypcję](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Utwórz zasób Azure bramy
Po zainstalowaniu i zarejestrować bramę, należy toocreate zasobów bramy w Twojej subskrypcji platformy Azure. Zaloguj tooAzure z hello samo konto używane podczas rejestrowania hello bramy.

1. W portalu Azure kliknij **Utwórz nową usługę** > **integracji przedsiębiorstwa** > **bramy danych lokalnych** > **Utwórz**.

   ![Utwórz zasób bramy](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. W **Utwórz bramę połączenia**, wprowadź następujące ustawienia:

    * **Nazwa**: Wprowadź nazwę dla zasobu bramy. 

    * **Subskrypcja**: Wybierz hello tooassociate subskrypcji platformy Azure z zasobu bramy. 
    Ta subskrypcja powinna być hello tej samej subskrypcji, serwery są w.
   
      Hello Domyślna subskrypcja jest oparta na powitania konto platformy Azure, który został użyty toosign w.

    * **Grupa zasobów**: utwórz grupę zasobów lub wybierz istniejącą.

    * **Lokalizacja**: hello wybierz region zarejestrować bramy w.

    * **Nazwa instalacji**: Jeśli instalacji bramy nie została jeszcze wybrana, wybierz hello brama zarejestrowana. 

    Gdy wszystko będzie gotowe, kliknij przycisk **Utwórz**.

## <a name="connect-servers"></a>Połącz zasób bramy toohello serwerów

1. W sieci — Omówienie serwera usług Azure Analysis Services kliknij **bramy danych lokalnych**.

   ![Połącz toogateway serwera](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. W **wybierz tooconnect bramy danych lokalnego**wybierz zasób bramy, a następnie kliknij przycisk **wybranej bramy Połącz**.

   ![Połącz zasób toogateway serwera](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Jeśli brama nie ma na liście hello, serwer może nie jest w tym samym regionie co określony podczas rejestrowania bramy hello region hello hello. 

To już wszystko. Jeśli potrzebne porty tooopen lub wykonaj wszelkie rozwiązywania problemów, można się toocheck limit [bramy danych lokalnych](analysis-services-gateway.md).

## <a name="next-steps"></a>Następne kroki
* [Zarządzanie usług Analysis Services](analysis-services-manage.md)   
* [Pobieranie danych z usług Azure Analysis Services](analysis-services-connect.md)
