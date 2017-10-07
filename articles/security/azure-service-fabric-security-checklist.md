---
title: "aaaAzure usługi sieci szkieletowej — Lista kontrolna zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw Lista kontrolna zabezpieczeń zabezpieczeń sieci szkieletowej Azure."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Lista kontrolna zabezpieczeń platformy Azure sieci szkieletowej usług
Ten artykuł zawiera listę kontrolną łatwy w użyciu, które mogą pomóc w zabezpieczeniu środowiska sieć szkieletowa usług Azure.

## <a name="introduction"></a>Wprowadzenie
Sieć szkieletowa usług Azure to platforma systemów rozproszonych, dzięki którym toopackage łatwe, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne. Sieć szkieletowa usług dotyczy również hello znaczne trudności w tworzenie i zarządzanie aplikacjami w chmurze. Deweloperzy i administratorzy mogą uniknąć złożonych problemów związanych z infrastrukturą i skoncentrować się na implementowaniu wymagających obciążeń o znaczeniu strategicznym, które są skalowalne, niezawodne i łatwe w zarządzaniu.

## <a name="checklist"></a>Lista kontrolna
Użyj powitania po toohelp listy kontrolnej, należy upewnić się, że nie pomijane wszelkie istotne problemy w zarządzania i konfiguracji bezpieczna sieć szkieletowa usług Azure.


|Lista kontrolna kategorii| Opis |
| ------------ | -------- |
|[Kontrola dostępu oparta na rolach (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>Kontrola dostępu umożliwia hello klastra administrator toolimit dostępu toocertain klastra operacje dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.</li><li>Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). </li><li>   Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.</li></ul>|
|[Certyfikaty X.509 i sieci szkieletowej usług](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>[Certyfikaty](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates) używane w klastrach uruchomionych obciążeń produkcyjnych powinny zostać utworzone przy użyciu poprawnie skonfigurowanej usługi certyfikatów systemu Windows Server lub uzyskane z zatwierdzonych [urzędu certyfikacji,](https://en.wikipedia.org/wiki/Certificate_authority).</li><li>Nigdy nie używaj żadnego [tymczasowego lub certyfikaty testów](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development) w środowisku produkcyjnym, które są tworzone przy użyciu narzędzi, takich jak [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx). </li><li>Można użyć [certyfikatu z podpisem własnym](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) jednak zrobić to dla klastrów testowych, a nie w środowisku produkcyjnym.</li></ul>|
|[Zabezpieczenia klastra](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>zabezpieczenia węzła do węzła, węzeł klient zabezpieczenia, są następujące scenariusze zabezpieczeń klastra Hello [kontroli dostępu opartej na rolach (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles).</li></ul>|
|[Uwierzytelnianie klastra](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Uwierzytelnia [komunikacji między węzłami](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md) dla Federacji klastra. </li></ul>|
|[Uwierzytelnianie serwera](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>Uwierzytelnia hello [klastra zarządzania punkty końcowe](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal) tooa zarządzania klienta.</li></ul>|
|[Zabezpieczenia aplikacji](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>Szyfrowanie i odszyfrowywanie wartości konfiguracji aplikacji.</li><li> Szyfrowanie danych w węzłach podczas replikacji.</li></ul>|
|[Certyfikat klastra](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>Ten certyfikat jest wymagany toosecure hello komunikacji między węzłami hello w klastrze.</li><li>  Ustaw dodatkowej w zmiennych ThumbprintSecondary hello hello odcisk palca hello podstawowego certyfikatu w hello sekcji odcisk palca i który hello.</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>Ten certyfikat jest widoczne toohello klienta po próbie tooconnect toothis klastra. Do uaktualnienia, można użyć dwóch różnych certyfikatów, podstawowego i pomocniczego.</li></ul>|
|ClientCertificateThumbprints| <ul><li>Jest to zestaw certyfikatów, które mają tooinstall na klientach hello uwierzytelniony. </li></ul>|
|ClientCertificateCommonNames| <ul><li>Ustaw nazwa pospolita hello hello pierwszego certyfikatu klienta na powitania CertificateCommonName. Witaj CertificateIssuerThumbprint jest hello odcisk palca wystawcy hello tego certyfikatu. </li></ul>|
|ReverseProxyCertificate| <ul><li>Jest opcjonalny certyfikat, który może być określony, jeśli chcesz, aby toosecure Twojego [wstecznego Proxy](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy). </li></ul>|
|Usługa Key Vault| <ul><li>Używane certyfikaty toomanage w klastrach usługi sieć szkieletowa na platformie Azure.  </li></ul>|


## <a name="next-steps"></a>Następne kroki
- [Proces uaktualniania klastra sieci szkieletowej usług oraz oczekiwań od użytkownika](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [Zarządzanie aplikacji usługi Service Fabric w programie Visual Studio](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio).
- [Wprowadzenie modelu kondycji sieci szkieletowej usług](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction).
