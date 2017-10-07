---
title: "aaaAzure sieci szkieletowej usług w systemie Linux | Dokumentacja firmy Microsoft"
description: "Klastry usługi sieć szkieletowa obsługują systemu Linux i Java, co oznacza, że będziesz w stanie toodeploy i aplikacji sieci szkieletowej usług hosta napisany w języku Java i C# w systemie Linux."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Sieć szkieletowa usług w systemie Linux
Podgląd Hello sieci szkieletowej usług w systemie Linux pozwala toobuild, wdrażania i zarządzania wysoce skalowalne, wysoko dostępne aplikacje w systemie Linux, tak jak w systemie Windows. platformy Service Fabric Hello (Reliable Services i Reliable Actors) są dostępne w języku Java w systemie Linux w dodanie tooC # (.NET Core).  Można również tworzyć [usługi pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md) z dowolnego języka lub struktury. Ponadto hello preview obsługuje również organizowanie kontenery Docker. Kontenery docker można uruchamiać pliki wykonywalne gościa lub macierzysty usług sieci szkieletowej usług, korzystających z platformy Service Fabric hello.

Sieć szkieletowa usług w systemie Linux jest koncepcyjnie równoważne tooService sieci szkieletowej w systemie Windows (z wyjątkiem charakterystyki systemu operacyjnego i obsługa języka programowania). W związku z tym większość naszego [istniejąca dokumentacja](http://aka.ms/servicefabricdocs) ma zastosowanie w myśl należy zapoznać się z technologii hello.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Obsługiwane systemy operacyjne i języki programowania
Hello ograniczone w wersji zapoznawczej obsługuje hello tworzenia rozwoju jednego pola Ponadto klastry klastrów maszyny toomulti na platformie Azure z systemem Ubuntu Server 16.04. obsługuje podglądu Hello hello Reliable Actors i hello usługi bezstanowej niezawodnej struktury w języku Java i C# w pliki wykonywalne tooguest dodanie i organizowanie kontenery Docker.  

> [!NOTE]
> Niezawodne kolekcje nie są obsługiwane w systemie Linux jeszcze. Nie są obsługiwane tylko klastry wstrzymania albo - tylko jedno pole, jak i Azure Linux klastrach obejmujących wiele maszyn są obsługiwane w wersji zapoznawczej hello.
>
>


## <a name="supported-tooling"></a>Obsługiwane narzędzi
Podgląd Hello obsługuje interakcji z hello klastra za pomocą interfejsu wiersza polecenia usługi sieci szkieletowej. Dla deweloperów języka Java Integracja z Eclipse i narzędzia Yeoman jest dostarczany z Eclipse obsługiwane w systemie Linux i OS x. Witaj integracji systemu OS x używa Maszynę wirtualną systemu Linux pod maską hello za pośrednictwem vagrant. C# deweloperom integracji z narzędzia Yeoman podano toogenerate szablonów aplikacji.

## <a name="next-steps"></a>Następne kroki

* Zapoznaj się z hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) i [niezawodne usługi](service-fabric-reliable-services-introduction.md) programowania struktur
* [Przygotowywanie środowiska projektowego w systemie Linux](service-fabric-get-started-linux.md)
* [Przygotowywanie środowiska projektowego w systemie OSX](service-fabric-get-started-mac.md)
* [Tworzenie pierwszej aplikacji usługi sieci szkieletowej Java w systemie Linux](service-fabric-create-your-first-linux-application-with-java.md)
* [Instalator usługi sieć szkieletowa ciągłej integracji i wdrażania z Wpięć i GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Różnice w usłudze Service Fabric w systemie Windows i Linux](service-fabric-linux-windows-differences.md)
