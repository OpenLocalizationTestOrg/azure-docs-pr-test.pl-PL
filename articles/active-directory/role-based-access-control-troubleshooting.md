---
title: aaaTroubleshoot Azure RBAC | Dokumentacja firmy Microsoft
description: "Uzyskaj pomoc dotyczącą problemy lub pytania dotyczące zasobów kontroli dostępu opartej na rolach."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Oparta na rolach kontrola dostępu do rozwiązywania problemów

W tym artykule dokumentu odpowiedzi na często zadawane pytania dotyczące hello określone prawa dostępu przyznane z rolami, aby wiedzieć, jaki tooexpect po przy użyciu hello ról w hello portalu Azure i rozwiązywać problemy z dostępem do. Te trzy role opisano wszystkie typy zasobów:

* Właściciel  
* Współautor  
* Czytelnik  

Właściciele i współautorzy mają pełny dostęp toohello zarządzania środowisko, ale współautora nie może udzielić dostępu tooother użytkowników lub grup. Rzeczy interesujący nieco z rolą czytnika hello, dlatego gdy będzie poświęcić trochę czasu. Zobacz hello [opartej na rolach kontrola dostępu get-started artykułu](role-based-access-control-configure.md) szczegółowe informacje na temat sposobu uzyskiwania dostępu toogrant.

## <a name="app-service-workloads"></a>Obciążeń usługi aplikacji
### <a name="write-access-capabilities"></a>Możliwości zapisu
Jeśli przyznasz aplikacji sieci web pojedynczego użytkownika dostęp tylko do odczytu tooa niektóre funkcje zostały wyłączone, że nie może spodziewać się. Wymagaj Hello następujące możliwości zarządzania **zapisu** dostępu do aplikacji sieci web tooa (współautora lub właściciela), a nie są dostępne w jakimkolwiek scenariuszu tylko do odczytu.

* Polecenia (na przykład Uruchom, Zatrzymaj, itp.)
* Zmiana ustawień, takich jak konfiguracja ogólna, ustawienia skalowania ustawienia kopii zapasowej i ustawienia monitorowania
* Uzyskiwanie dostępu do poświadczeń publikowania i innych informacji poufnych, takich jak ustawienia aplikacji i parametry połączenia
* Dzienniki przesyłania strumieniowego
* Dzienniki diagnostyczne konfiguracji
* W konsoli (wiersza polecenia)
* Ostatnie i Active wdrożenia (ciągłe wdrażanie lokalnej git)
* Szacowane wydatki
* Testy sieci Web
* Sieć wirtualna (tylko widoczne tooa czytnika Jeśli wcześniej skonfigurowano sieci wirtualnej przez użytkownika z uprawnieniami do zapisu).

Jeśli nie masz dostępu do żadnego z tych kafelków, należy tooask administratora dla aplikacji sieci web toohello dostępu współautora.

### <a name="dealing-with-related-resources"></a>Zajmujących się zasoby pokrewne
Aplikacje sieci Web są skomplikowane hello obecności kilka różnych zasobów, które wzajemne oddziaływanie. W tym miejscu jest grupą typowych zasobów z kilku witryn sieci Web:

![Grupa zasobów aplikacji sieci Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

W związku z tym jeśli udzielić aplikacji sieci web hello toojust dostępu ktoś większość funkcji hello na powitania bloku witryny sieci Web w portalu Azure hello jest wyłączone.

Te elementy wymagają **zapisu** dostępu toohello **planu usługi aplikacji** tooyour witryny sieci Web, który odpowiada:  

* Aplikacja sieci web hello wyświetlania obiektu cenowym (wolne lub standardowy)  
* Skala konfiguracji (liczba wystąpień, rozmiar maszyny wirtualnej, ustawienia skalowania automatycznego)  
* Przydziały (magazynu, przepustowości, procesor CPU)  

Te elementy wymagają **zapisu** toohello dostępu do całej **grupy zasobów** zawierający witryny sieci Web:  

* Certyfikaty SSL i powiązań (certyfikaty SSL może być udostępniana między lokacjami hello tej samej grupie zasobów i lokalizacja geograficzna)  
* Reguły alertów  
* Ustawienia skalowania automatycznego  
* Application insights składników  
* Testy sieci Web  

## <a name="virtual-machine-workloads"></a>Obciążenia maszyny wirtualnej
Wiele takich jak z aplikacjami sieci web, niektóre funkcje w bloku maszyny wirtualnej hello wymagają maszyny wirtualnej toohello zapisu lub tooother zasoby w grupie zasobów hello.

Maszyny wirtualne są powiązane tooDomain nazwy, sieci wirtualnych, kont magazynu i reguł alertów.

Te elementy wymagają **zapisu** dostępu toohello **maszyny wirtualnej**:

* Punkty końcowe  
* Adresy IP  
* Dyski  
* Rozszerzenia  

Wymagają one wykonywania **zapisu** hello tooboth dostępu **maszyny wirtualnej**i hello **grupy zasobów** (wraz z nazwą domeny hello) jest jego:  

* Zestaw dostępności  
* Zestawu o zrównoważonym obciążeniu  
* Reguły alertów  

Jeśli nie masz dostępu do żadnego z tych kafelków, poproś administratora dla grupy zasobów toohello dostępu współautora.

## <a name="see-more"></a>Zobacz więcej
* [Kontroli dostępu opartej na rolach](role-based-access-control-configure.md): rozpoczynanie pracy z RBAC w hello portalu Azure.
* [Wbudowane role](role-based-access-built-in-roles.md): uzyskiwanie szczegółowych informacji o rolach hello, które standardowo w RBAC.
* [Role niestandardowe w Azure RBAC](role-based-access-control-custom-roles.md): Dowiedz się, jak toofit role niestandardowe toocreate Twojego dostępu wymaga.
* [Tworzenie raportu historii zmian dostępu](role-based-access-control-access-change-history-report.md): informacje o zmieniania przypisań ról w RBAC.

