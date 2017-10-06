---
title: "aaaUse agentów maszyny Wirtualnej platformy Azure dla ciągłej integracji z Wpięć."
description: "Agenty maszyn wirtualnych platformy Azure jako elementy podrzędne usługi Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Używanie agentów maszyn wirtualnych platformy Azure w celu zapewnienia ciągłej integracji z usługą Jenkins.

Ta opcja szybkiego startu pokazuje, jak toouse hello toocreate wtyczki Wpięć Azure VM agentów na żądanie agenta systemu Linux (Ubuntu) na platformie Azure.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego przewodnika Szybki Start:

* Jeśli nie masz już wzorca Wpięć, można uruchomić z poziomu hello [szablon rozwiązania](install-jenkins-solution-template.md) 
* Odwołuje się zbyt[Tworzenie nazwy głównej usługi Azure Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) Jeśli nie masz już nazwę główną usługi Azure.

## <a name="install-azure-vm-agents-plugin"></a>Instalowanie wtyczki agentów maszyn wirtualnych platformy Azure

Jeśli zostanie uruchomione z hello [szablon rozwiązania](install-jenkins-solution-template.md), hello wtyczki Agent maszyny Wirtualnej jest zainstalowany w hello Wpięć wzorca.

W przeciwnym razie zainstaluj hello **agentów maszyny Wirtualnej Azure** wtyczki z wewnątrz pulpitu nawigacyjnego Wpięć hello.

## <a name="configure-hello-plugin"></a>Skonfiguruj wtyczkę hello

* W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Wpięć Zarządzanie -> skonfiguruj System ->**. Przewiń toohello u dołu strony hello i Znajdź sekcję hello z listy rozwijanej hello **Dodaj nowe chmury**. Wybierz z hello menu **agentów programu Microsoft Azure maszyny Wirtualnej**
* Wybierz istniejące konto z listy rozwijanej poświadczenia Azure hello.  tooadd nowy **nazwy głównej usługi Azure firmy Microsoft,** wprowadź hello następujące wartości: identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0.

![Poświadczenia platformy Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Kliknij przycisk **konfiguracji Sprawdź** toomake się, że hello profilu konfiguracji są poprawne.
* Zapisz konfigurację hello i kontynuować toohello następnego kroku.

## <a name="template-configuration"></a>Konfigurowanie szablonu

### <a name="general-configuration"></a>Konfiguracja ogólna
Skonfiguruj szablon do użycia toodefine agenta maszyny Wirtualnej platformy Azure. 

* Kliknij przycisk **Dodaj** tooadd szablonu. 
* Wpisz nazwę nowego szablonu. 
* Etykiety hello wprowadź "ubuntu." Etykieta jest używany podczas konfigurowania zadania hello.
* Wybierz odpowiedni region hello z hello pola kombi.
* Witaj wybierz żądany rozmiar maszyny Wirtualnej.
* Określ nazwę konta usługi Azure Storage hello lub pozostaw nazwę domyślną hello puste toouse "jenkinsarmst."
* Określ czas przechowywania hello w minutach. To ustawienie określa hello liczbę minut oczekiwania przez Wpięć przed usunięciem automatycznie bezczynności agenta. Określ 0, jeśli nie chcesz toobe bezczynności agentów automatycznie usuwane.

![Konfiguracja ogólna](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Konfiguracja obrazu

Wybierz toocreate agenta systemu Linux (Ubuntu), **obrazu odniesienia** i użyj powitania po konfiguracji, na przykład. Odwołuje się zbyt[portalu Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) hello Azure najnowsze obsługiwanych obrazów.

* Image Publisher: Canonical
* Image Offer: UbuntuServer
* Image Sku: 14.04.5-LTS
* Image version: latest
* OS Type: Linux
* Launch method: SSH
* Wprowadź poświadczenia administratora
* W przypadku skryptu inicjowania maszyny wirtualnej wpisz:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Konfiguracja obrazu](./media/jenkins-azure-vm-agents/image-config.png)

* Kliknij przycisk **Sprawdź szablon** tooverify hello konfiguracji.
* Kliknij pozycję **Zapisz**.

## <a name="create-a-job-in-jenkins"></a>Tworzenie zadania w usłudze Jenkins

* W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **nowy element**. 
* Wprowadź nazwę, wybierz **Freestyle project** (Projekt Freestyle) i kliknij przycisk **OK**.
* W hello **ogólne** kartę, wybierz "Ograniczenia, gdzie można uruchomić projektu" i typie "ubuntu" w wyrażeniu etykiety. Pojawi się "ubuntu" w hello listy rozwijanej.
* Kliknij pozycję **Zapisz**.

![Konfigurowanie zadania](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Tworzenie nowego projektu

* Wrócić do poprzedniej strony pulpitu nawigacyjnego Wpięć toohello.
* Utworzono nowe zadanie powitania kliknij prawym przyciskiem myszy, kliknij przycisk **kompilacji teraz**. Rozpocznie się kompilowanie. 
* Po zakończeniu kompilacji hello Przejdź zbyt**dane wyjściowe konsoli**. Możesz sprawdzić, czy hello kompilacji została wykonana zdalnie na platformie Azure.

![Dane wyjściowe konsoli](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Dokumentacja

* Wideo z cyklu „Piątek z Azure”: [Ciągła integracja z usługą Jenkins przy użyciu agentów maszyn wirtualnych platformy Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* Informacje uzupełniające i opcje konfiguracji: [Wiki wtyczki agentów maszyn wirtualnych platformy Azure dla usługi Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

