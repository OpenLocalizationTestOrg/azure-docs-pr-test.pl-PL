---
title: tooauthentication aaaIntro automatyzacji Azure | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera przegląd zabezpieczeń automatyzacji i hello różnych metod uwierzytelniania dostępne dla kont automatyzacji w automatyzacji Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "zabezpieczenia usługi automation, bezpieczna usługa automation, uwierzytelnianie usługi automation"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Wprowadzenie tooauthentication automatyzacji Azure  
Automatyzacja Azure umożliwia tooautomate zadania w odniesieniu do zasobów na platformie Azure i lokalnego i z innych dostawców chmury, takich jak Amazon usług sieci Web (AWS).  Aby runbook tooperform żądane działania, musi mieć uprawnienia toosecurely dostępu hello zasobów z hello minimalnym poziomem uprawnień wymaganych w ramach subskrypcji hello.

W tym artykule opisano hello obsługiwane różne scenariusze uwierzytelniania usługi Automatyzacja Azure i Pokaż sposób uruchamiania tooget oparty na środowisku hello lub środowisk można będzie toomanage.  

## <a name="automation-account-overview"></a>Konto usługi Automation — omówienie
Po ponownym uruchomieniu usługi Automatyzacja Azure dla powitania po raz pierwszy, należy utworzyć co najmniej jedno konto automatyzacji. Konta automatyzacji pozwalają tooisolate zasobami automatyzacji (elementy runbook, zasoby, konfiguracje) z hello zasoby zawarte na inne konta automatyzacji. Zasoby tooseparate kont automatyzacji można użyć do oddzielnych środowisk logiczne. Na przykład jednego konta można użyć dla środowiska rozwojowego, innego dla produkcyjnego, a jeszcze innego dla lokalnego.  Konto usługi Azure Automation różni się od konta Microsoft lub kont utworzonych w ramach subskrypcji platformy Azure.

Hello automatyzacji zasobów dla każdego konta automatyzacji skojarzonych z pojedynczym regionie Azure, ale kont automatyzacji mogą zarządzać wszystkie zasoby hello w ramach subskrypcji. kont automatyzacji toocreate główną przyczyną Hello w różnych regionach będzie, jeśli masz zasady, które wymagają danych i zasobów toobe tooa izolowanego określonego regionu.

> [!NOTE]
> Konta automatyzacji i zasoby hello zawierają, które są tworzone w portalu Azure hello, nie można uzyskać dostępu do hello klasycznego portalu Azure. Jeśli chcesz toomanage te konta lub ich zasobów przy użyciu programu Windows PowerShell, należy użyć hello modułów usługi Azure Resource Manager.
>

Wszystkie zadania hello, które należy wykonać przed zasobów za pomocą usługi Azure Resource Manager i hello poleceń cmdlet systemu Azure w usłudze Automatyzacja Azure musi uwierzytelniać tooAzure przy użyciu uwierzytelniania opartego na poświadczeń organizacyjnych tożsamości usługi Azure Active Directory.  Uwierzytelnianie oparte na certyfikatach był hello oryginalnej metody uwierzytelniania w trybie zarządzania usługami Azure, ale było skomplikowane toosetup.  Uwierzytelnianie tooAzure z użytkownikiem usługi Azure AD zostało wprowadzone ponownie 2014 toonot tylko uprościć hello tooconfigure proces uwierzytelniania konta, ale także możliwość hello pomocy technicznej toonon interakcyjnego uwierzytelniania tooAzure przy użyciu konta jednego użytkownika, który pracuje z usługi Azure Resource Manager i zasoby klasyczne.   

Obecnie tworząc nowe konto usługi Automatyzacja w portalu Azure hello, automatycznie tworzy:

* Konto Uruchom jako, które tworzy nową główną nazwę usługi w usłudze Azure Active Directory, certyfikat i przypisuje hello współautora opartej na rolach kontroli dostępu (RBAC), które będą używane zasoby usługi Resource Manager toomanage używanie elementów runbook.
* Klasycznym konto Uruchom jako, przekazując certyfikat zarządzania, który będzie można używane toomanage zarządzania usługą Azure lub klasycznego zasobów przy użyciu elementów runbook.  

Kontrola dostępu oparta na rolach jest dostępna z usługi Azure Resource Manager toogrant dozwolone konto użytkownika usługi Azure AD tooan akcje i konta Uruchom jako, a uwierzytelniania tej nazwy głównej usługi.  Przeczytaj [kontroli dostępu opartej na rolach w artykule usługi Automatyzacja Azure](automation-role-based-access-control.md) dalsze informacje toohelp opracować modelu do zarządzania uprawnieniami automatyzacji.  

Elementów Runbook uruchomionych na hybrydowego procesu roboczego elementu Runbook w centrum danych lub usług AWS obliczeniowych nie można Użyj hello sama metoda, która jest zazwyczaj używana w przypadku uwierzytelniania zasobów tooAzure elementów runbook.  Jest to spowodowane te zasoby są uruchomione poza platformą Azure i w związku z tym będzie wymagać ich poświadczenia zabezpieczeń zdefiniowane w tooresources tooauthenticate automatyzacji, który będzie uzyskiwać lokalnie.  

## <a name="authentication-methods"></a>Metody uwierzytelniania
Witaj Poniższa tabela zawiera podsumowanie hello różnych metod uwierzytelniania dla każdego środowiska obsługiwane przez usługi Automatyzacja Azure i hello artykuł opisujący sposób uwierzytelniania toosetup elementy runbook.

| Metoda | Środowisko | Artykuł |
| --- | --- | --- |
| Konto użytkownika usługi Azure AD |Azure Resource Manager i Azure Service Management |[Uwierzytelnianie elementów Runbook przy użyciu konta użytkownika usługi Azure AD](automation-create-aduser-account.md) |
| Konto Uruchom jako platformy Azure |Azure Resource Manager |[Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md) |
| Klasyczne konto Uruchom jako platformy Azure |Usługa Azure Service Management |[Uwierzytelnianie elementów Runbook przy użyciu konta Uruchom jako platformy Azure](automation-sec-configure-azure-runas-account.md) |
| Uwierzytelnianie systemu Windows |Lokalne centrum danych |[Uwierzytelnianie elementów Runbook dla hybrydowych procesów roboczych Runbook](automation-hybrid-runbook-worker.md) |
| Poświadczenia AWS |Amazon Web Services |[Uwierzytelnianie elementów Runbook w usłudze Amazon Web Services](automation-config-aws-account.md) |
