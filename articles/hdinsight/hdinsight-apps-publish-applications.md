---
title: "aplikacje usługi HDInsight aaaPublish - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i publikowanie aplikacji usługi HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Publikowanie aplikacji usługi HDInsight w hello Azure Marketplace
Aplikacja usługi HDInsight to aplikacja, którą użytkownicy mogą zainstalować w klastrze usługi HDInsight opartym na systemie Linux. Te aplikacje mogą być opracowane przez firmę Microsoft, niezależnych dostawców oprogramowania (ISV) lub samodzielnie. W tym artykule dowiesz się, jak toopublish aplikację usługi HDInsight w hello Azure Marketplace.  Aby uzyskać ogólne informacje o publikowaniu w hello Azure Marketplace, zobacz [publikowania toohello oferta portalu Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

Aplikacje usługi HDInsight korzystają hello *Bring Your Own License (BYOL)* modelu, w którym dostawca aplikacji jest odpowiedzialny za Licencjonowanie aplikacji hello tooend — użytkownicy i użytkownicy końcowi są naliczane tylko wtedy przez platformę Azure zasobów hello one Utwórz, takich jak klaster usługi HDInsight hello i jej maszyny wirtualne/węzły. Obecnie rozliczenia dotyczące samej aplikacji hello nie odbywa się za pośrednictwem platformy Azure.

Inny artykuł z powiązanych aplikacji usługi HDInsight:

* [Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): Dowiedz się, jak klastrów tooinstall tooyour aplikacji usługi HDInsight.
* [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak tooinstall i testowania niestandardowych aplikacji usługi HDInsight.

## <a name="prerequisites"></a>Wymagania wstępne
toosubmit Twojej aplikacji niestandardowej toohello witryny marketplace, musisz mieć utworzone i przetestowane niestandardową aplikację. Zobacz następujące artykuły hello:

* [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak tooinstall i testowania niestandardowych aplikacji usługi HDInsight.

Należy również zarejestrowano konta dewelopera. Zobacz [publikowania toohello oferta portalu Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) i [Utwórz konto Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Definiowanie aplikacji
Obejmuje dwa kroki publikowania aplikacji toohello portalu Azure Marketplace.  Najpierw należy zdefiniować **createUiDef.json** tooindicate pliku, który klastrami dana aplikacja jest zgodna z; a następnie opublikować hello szablonu z hello portalu Azure. Po sekcji Hello jest przykładowy plik createUiDef.json.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Pole | Opis | Możliwe wartości |
| --- | --- | --- |
| types (typy) |typy klastrów Hello, które aplikacja hello jest zgodna z. |Hadoop, HBase, Storm, Spark (lub dowolna ich kombinacja) |
| tiers (warstwy) |Witaj warstwy klastrów, z którymi aplikacja hello jest zgodna z. |Standard, Premium (lub obie) |
| versions (wersje) |Witaj typy klastrów usługi HDInsight, z którymi aplikacja hello jest zgodna z. |3.4 |

## <a name="application-install-script"></a>Skrypt instalacji aplikacji
Zawsze, gdy aplikacja jest zainstalowana w klastrze (istniejącego lub nowego), jest tworzony węzeł krawędzi i skrypt instalacji aplikacji hello jest uruchamiany na nim.
  > [!IMPORTANT]
  > Nazwa Hello nazw skryptu instalacji aplikacji hello musi być unikatowa dla danego klastra z hello zgodny z formatem.
  > 
  > nazwa": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Należy zauważyć, że istnieją trzy Nazwa skryptu toohello części:
  > 
  > 1. Prefiks nazwy skryptu, który powinien zawierać nazwę aplikacji hello lub aplikacji toohello odpowiednie nazwy.
  > 2. Łącznik "-" dla czytelności.
  > 3. Funkcję unikatowego ciągu z nazwą aplikacji hello jako hello parametru.
  > 
  > Przykładem jest hello powyżej kończy się stać się: hue-install-v0-4wkahss55hlas hello utrwalone liście akcji skryptu. Przykładowy ładunek JSON można znaleźć pod adresem [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
skrypt instalacji Hello musi mieć hello następujące cechy:
1. Upewnij się, że skrypt hello jest idempotentności. Wiele wywołań toohello skryptu powinny wywoływać hello takiego samego wyniku.
2. skrypt Hello powinna być poprawnie numerów wersji. Użyj innej lokalizacji dla skryptu hello podczas uaktualniania i testowanie zmian, aby nie dotyczy użytkowników, które próbujesz tooinstall hello aplikacji. 
3. Dodaj odpowiednie rejestrowania toohello skryptów w każdym punkcie. Zazwyczaj hello skryptu dzienniki są hello tylko sposób toodebug problemy z instalacją aplikacji.
4. Sprawdź, czy usługi tooexternal wywołania lub zasoby mają odpowiednie ponownych prób tak, aby instalacja hello nie ma wpływu na przejściowe problemy z siecią.
5. Jeśli skrypt jest uruchamiany usługi na węzłach hello, upewnij się, czy usługi hello są monitorowane i skonfigurować toostart automatycznie w przypadku ponownego uruchomienia węzłów.

## <a name="package-application"></a>Tworzenie pakietu aplikacji
Utwórz plik zip, który zawiera wszystkie wymagane pliki instalacyjne aplikacji usługi HDInsight. Należy hello pliku zip w [publikowanie aplikacji](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Zobacz przykład w artykule [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md).
* Wszystkie wymagane skrypty.

> [!NOTE]
> Witaj pliki aplikacji (w tym pliki aplikacji sieci web, jeśli istnieje) może znajdować się na dowolnym publicznie dostępnym punkcie końcowym.
> 

## <a name="publish-application"></a>Publikowanie aplikacji
Wykonaj następujące kroki toopublish aplikacji usługi HDInsight hello:

1. Zaloguj się na toohello [portalu Azure Publishing](https://publish.windowsazure.com/).
2. Kliknij przycisk **szablony rozwiązań** z toocreate po lewej stronie powitania nowy szablon rozwiązania.
3. Wprowadź tytuł, a następnie kliknij pozycję **Create a new solution template** (Utwórz nowy szablon rozwiązania).
4. Kliknij przycisk **konto Centrum deweloperów Utwórz i Dołącz do programu Azure hello** tooregister firmy, jeśli nie zostało to jeszcze zrobione.  Zobacz temat [Tworzenie konta dewelopera Microsoft](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Kliknij przycisk **zdefiniować niektóre topologiami tooget uruchomiono**. Szablon rozwiązania jest tooall "nadrzędnej" jego topologii. Można zdefiniować wiele topologii w jednym szablonie oferty/rozwiązania. Gdy oferta zostanie przeniesiona toostaging, spoczywa z jego topologii. 
6. Wprowadź nazwę topologii, a następnie kliknij znak plus hello.
7. Wprowadź nową wersję, a następnie kliknij znak Plus hello.
8. Plik zip hello przekazywania przygotowany w [pakietu aplikacji](#package-application).  
9. Kliknij opcję **Request Certification** (Żądanie certyfikacji). zespół certyfikacji Microsoft Hello będzie Przejrzyj hello pliki i wystawi certyfikat topologii hello.

## <a name="next-steps"></a>Następne kroki
* [Instalowanie aplikacji usługi HDInsight](hdinsight-apps-install-applications.md): Dowiedz się, jak klastrów tooinstall tooyour aplikacji usługi HDInsight.
* [Instalowanie niestandardowych aplikacji usługi HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak toodeploy nieopublikowane tooHDInsight aplikacji usługi HDInsight.
* [Dostosowywanie klastrów usługi HDInsight opartej na systemie Linux przy użyciu akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): Dowiedz się, jak toouse akcji skryptu tooinstall dodatkowe aplikacje.
* [Tworzenie klastrów opartych na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Dowiedz się, jak toocreate szablony Menedżera zasobów toocall HDInsight clusters.
* [Użyj węzłami pusty krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md): Dowiedz się, jak toouse pustą krawędzi węzła w celu uzyskiwania dostępu do klastra usługi HDInsight, testowanie aplikacji usługi HDInsight i hosting aplikacji usługi HDInsight.

