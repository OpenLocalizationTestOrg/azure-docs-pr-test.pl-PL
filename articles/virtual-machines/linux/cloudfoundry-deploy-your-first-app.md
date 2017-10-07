---
title: aaaDeploy pierwszy tooCloud aplikacji Foundry w systemie Microsoft Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie aplikacji tooCloud Foundry na platformie Azure"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Wdrażanie pierwszego tooCloud aplikacji Foundry w systemie Microsoft Azure

[Chmury Foundry](http://cloudfoundry.org) jest dostępna w systemie Microsoft Azure platformy popularnych aplikacji open source. W tym artykule zostanie przedstawiony sposób toodeploy i zarządzanie nimi aplikacji w chmurze Foundry w środowisku platformy Azure.

## <a name="create-a-cloud-foundry-environment"></a>Utwórz środowisko chmury Foundry

Dostępnych jest kilka opcji tworzenia środowiska Foundry chmurze na platformie Azure:

- Użyj hello [oferta kluczową Foundry chmury] [ pcf-azuremarketplace] w hello Azure Marketplace toocreate standardowe środowisko obejmujące PCF Operations Manager i hello Azure Service Broker. Można znaleźć [wykonać instrukcje] [ pcf-azuremarketplace-pivotaldocs] wdrażania hello marketplace oferty w hello kluczową dokumentacji.
- Utwórz dostosowane środowisko przez [wdrażania ręcznego kluczową Foundry chmury][pcf-custom].
- [Wdrażanie pakietów Foundry chmury open source hello bezpośrednio] [ oss-cf-bosh] poprzez ustawienie [BOSH](http://bosh.io) dyrektora, maszynę Wirtualną, która koordynuje hello wdrożenia środowiska chmury Foundry hello.

> [!IMPORTANT] 
> Jeśli wdrażasz PCF z hello Azure Marketplace, zanotuj hello SYSTEMDOMAINURL i poświadczeń administratora hello wymagane tooaccess hello kluczową Menedżera aplikacje, które są opisanej w przewodniku wdrażania marketplace hello. One są toocomplete potrzebne w tym samouczku. W przypadku wdrożeń marketplace hello SYSTEMDOMAINURL jest https://system formularza hello. *adres ip*. cf.pcfazure.com.

## <a name="connect-toohello-cloud-controller"></a>Połącz toohello kontrolerem chmury

Hello kontrolerem chmury to hello podstawowy wpis punktu tooa Foundry chmury środowisko wdrażania aplikacji i zarządzanie nimi. core Hello chmury kontrolera interfejsu API (CCAPI) to interfejs API REST, ale nie jest dostępny za pośrednictwem różnych narzędzi. W takim przypadku możemy korzystać z niego za pośrednictwem hello [interfejsu wiersza polecenia chmury Foundry][cf-cli]. Hello interfejsu wiersza polecenia można zainstalować w systemie Linux, MacOS lub systemu Windows, ale jeśli wolisz nie tooinstall go wcale, jest dostępny wstępnie zainstalowane w hello [powłoki chmury Azure][cloudshell-docs].

dołączenie wartości toolog, `api` toohello SYSTEMDOMAINURL uzyskany z hello marketplace wdrożenia. Ponieważ hello domyślne wdrożenie używa certyfikatu z podpisem własnym, należy także uwzględnić hello `skip-ssl-validation` przełącznika.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Jesteś zostanie wyświetlony monit o toolog w toohello kontrolerem chmury. Użyj hello poświadczeń konta administratora, które uzyskane z kroki wdrażania hello marketplace.

Udostępnia chmury Foundry *organizacjami* i *spacji* jako przestrzenie nazw tooisolate hello zespołów i środowisk, w ramach wdrożenia udostępnionych. Hello PCF wdrożenia marketplace zawiera domyślne hello *systemu* organizacji i zestaw funkcji miejsca do utworzenia toocontain hello podstawowe składniki, takie jak usługi Skalowanie automatyczne hello i hello brokera usług Azure. Teraz, wybierz hello *systemu* miejsca.


## <a name="create-an-org-and-space"></a>Tworzenie schematu i miejsca

W przypadku wpisania `cf apps`, należy zapoznać się z zestawem aplikacji systemu, które zostały wdrożone w miejscu systemu hello w hello org. systemu 

Zachowaj hello *systemu* org zastrzeżone dla aplikacji systemu dlatego Utwórz toohouse organizacji i miejsca naszych przykładowej aplikacji.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Użyj hello docelowego polecenia tooswitch toohello nowej organizacji i miejsca:

```bash
cf target -o testorg -s dev
```

Teraz gdy wdrażana jest aplikacja została ona utworzona automatycznie w nowej organizacji hello i miejsca. tooconfirm, który obecnie nie istnieją żadne aplikacji w nowej organizacji hello na miejsce, typu `cf apps` ponownie.

> [!NOTE] 
> Aby uzyskać więcej informacji na temat organizacjami i spacje i jak one używane do kontroli dostępu opartej na rolach (RBAC), zobacz hello [Foundry chmury dokumentacji][cf-orgs-spaces-docs].

## <a name="deploy-an-application"></a>Wdrażanie aplikacji

Użyjmy Foundry chmury przykładową aplikację o nazwie Hello Spring chmury, co jest napisany w języku Java i oparte na powitania [Spring Framework](http://spring.io) i [rozruchu Spring](http://projects.spring.io/spring-boot/).

### <a name="clone-hello-hello-spring-cloud-repository"></a>Klonuj repozytorium chmury Spring Hello hello

Chmury Spring Hello Przykładowa aplikacja Hello jest dostępna w witrynie GitHub. Ją sklonować tooyour środowiska i zmień do nowego katalogu hello:

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Tworzenie aplikacji hello

Przy użyciu aplikacji hello kompilacji [Apache Maven](http://maven.apache.org).

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Wdrażanie aplikacji hello z cf wypychania

Większość aplikacji tooCloud Foundry można wdrożyć przy użyciu hello `push` polecenia:

```bash
cf push
```

Gdy użytkownik *wypychania* aplikacji, chmury Foundry wykrywa hello typu aplikacji (w tym przypadku aplikacji Java) i jego zależności (w przypadku platforma Spring hello) identyfikuje. Pakiety następnie wszystkie elementy wymagane toorun kodu w obrazie kontenera autonomiczny, nazywany *dropletu*. Na koniec harmonogramy Foundry chmury hello aplikacji na jednym hello dostępne maszyn w środowisku i tworzy adresu URL, na której możesz uzyskiwać dostęp, która jest dostępna w hello dane wyjściowe polecenia hello.

![Dane wyjściowe polecenia wypychania cf][cf-push-output]

toosee hello hello spring chmury aplikacji, otwórz hello podany adres URL, w przeglądarce:

![Domyślny interfejs użytkownika dla chmury Hello Spring][hello-spring-cloud-basic]

> [!NOTE] 
> więcej informacji na temat efektów podczas toolearn `cf push`, zobacz [jak aplikacje są umieszczane] [ cf-push-docs] w hello dokumentacji Foundry chmury.

## <a name="view-application-logs"></a>Wyświetl dzienniki aplikacji

Witaj CLI Foundry chmury tooview dzienników można używać do aplikacji, za pomocą nazwy:

```bash
cf logs hello-spring-cloud
```

Domyślnie program hello rejestruje używa polecenia *tail*, który wskazuje nowe dzienniki, ponieważ są one zapisywane. pojawią się nowe dzienniki toosee, Odśwież hello aplikacji hello spring chmury w przeglądarce hello.

Dzienniki tooview, które już zostały zapisane, Dodaj hello `recent` przełącznika:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>Aplikacja hello skali

Domyślnie `cf push` tworzy tylko jedno wystąpienie aplikacji. tooensure wysokiej dostępności i Włączanie skalowania dla wyższej przepustowości, zazwyczaj mają toorun więcej niż jedno wystąpienie aplikacji. Możesz łatwo skalować w poziomie już wdrożone aplikacje za pomocą hello `scale` polecenia:

```bash
cf scale -i 2 hello-spring-cloud
```

Uruchomione hello `cf app` polecenia w aplikacji hello pokazuje, czy inne wystąpienie aplikacji hello tworzy Foundry chmury. Po uruchomieniu aplikacji hello, w chmurze Foundry tooit ruchu równoważenia obciążenia jest uruchamiana automatycznie.


## <a name="next-steps"></a>Następne kroki

- [Witaj odczytu dokumentacji chmury Foundry][cloudfoundry-docs]
- [Konfigurowanie hello dodatku Visual Studio Team Services dla chmury Foundry][vsts-plugin]
- [Konfigurowanie hello końcówki Analiza dzienników Microsoft dla chmury Foundry][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png