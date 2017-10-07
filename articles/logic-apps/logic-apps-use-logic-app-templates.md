---
title: "przepływy pracy aaaCreate z szablonów - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wprowadzenie — szybkie tworzenie przepływów pracy za pomocą aplikacji tooconnect szablonów aplikacji logiki platformy Azure i integrowanie danych."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>Konfigurowanie przepływu pracy za pomocą wbudowanych szablonów lub tooget wzorzec szybko rozpocząć pracę

## <a name="what-are-logic-app-templates"></a>Co to są szablony aplikacji logiki
Szablon aplikacji logiki jest aplikacji logiki wbudowanych służy tooquickly rozpocząć tworzenie własnych przepływu pracy. 

Te szablony są toodiscover dobrze różnych wzorców, które mogą zostać skompilowane przy użyciu aplikacji logiki. Możesz użyć tych szablonów jako- lub zmodyfikować je toofit Twojego scenariusza.

## <a name="overview-of-available-templates"></a>Omówienie dostępnych szablonów
Istnieje wiele dostępnych szablonów, w obecnie opublikowanych hello logiki aplikacji platformy. Poniżej przedstawiono niektóre kategorie przykład, jak również typ hello łączników używane w nich.

### <a name="enterprise-cloud-templates"></a>Szablony Enterprise chmury
Szablony, które integracji usługi Dynamics CRM, Salesforce pole, obiektów Blob platformy Azure i inne łączniki do potrzeb chmury przedsiębiorstwa. Przykłady co można zrobić za pomocą te szablony obejmują organizowanie potencjalnych klientów i tworzenie kopii zapasowej danych plików firmowych.

### <a name="enterprise-integration-pack-templates"></a>Szablony pakietów integracji przedsiębiorstwa
Konfiguracje VETER (Sprawdzanie poprawności, extract, transform, uzupełnić, trasy) potoki odbieranie X12 EDI dokumentów za pośrednictwem AS2 i przekształcania tooXML, jak również komunikat X12 i AS2 obsługi.

### <a name="protocol-pattern-templates"></a>Protokół wzorzec szablonów
Te szablony składają się z aplikacji logiki, które zawierają protokołu wzorców, takich jak żądanie odpowiedź za pośrednictwem protokołu HTTP, a także integracji między FTP i SFTP. Użyj tych istniejących lub jako podstawy do tworzenia bardziej złożonych wzorców protokołu.  

### <a name="personal-productivity-templates"></a>Szablony produktywność
Wzorce toohelp zwiększyć produktywność obejmują szablonów, które ustawić codzienne przypomnienia, Włącz elementów roboczych ważne do listy zadań do wykonania i automatyzowania zadań długich dół krok zatwierdzenia tooa jednego użytkownika.

### <a name="consumer-cloud-templates"></a>Szablony konsumentów chmury
Proste szablonów, które integrują się z usługami mediów społecznościowych, takich jak usługi Twitter, zapas czasu i poczty e-mail, ostatecznie stanie wzmocnienia mediów społecznościowych marketingu inicjatyw. Obejmują one również szablony taką jak kopiowanie mętna, co może pomóc zwiększyć wydajność, aby zaoszczędzić czas tradycyjnie powtarzających się zadań. 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>Jak toocreate aplikacji logiki przy użyciu szablonu
tooget uruchomiony przy użyciu szablonu aplikacji logiki, przejdź do projektanta aplikacji logiki hello. Jeśli wprowadzasz hello projektanta, otwierając istniejących aplikacji logiki, aplikację logiki hello automatycznie ładuje w widoku projektanta. Jednak jeśli tworzysz nową aplikację logiki, zobacz hello ekranu poniżej.  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

Na tym ekranie można wybrać toostart z aplikacji logiki puste lub wcześniej utworzonego szablonu. W przypadku wybrania jednego z szablonów hello podano dodatkowe informacje. W tym przykładzie używamy hello *podczas tworzenia nowego pliku w Dropbox, skopiuj go tooOneDrive* szablonu.  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

Jeśli wybierzesz szablon hello toouse, wystarczy zaznaczyć hello *użyć tego szablonu* przycisku. Zostanie wyświetlony monit toosign oparte na szablon hello łączników, który korzysta z konta tooyour. Lub, jeśli zostało wcześniej ustanowione połączenie z tych łączników, możesz wybrać kontynuować, jak pokazano poniżej.  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

Po ustanowieniu połączenia hello i wybraniu *kontynuować*, aplikację logiki hello otwiera się w widoku projektanta.  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

W powyższym przykładzie hello podobnie jak przypadku hello wiele szablonów, niektóre pola obowiązkowej właściwości hello może zostać wypełnione w łączniki hello; Jednak niektóre mogą nadal wymagana była wartość aby można było tooproperly wdrażanie hello logiki aplikacji. Jeśli spróbujesz toodeploy bez wprowadzania niektórych hello brakujące pola, zostanie wyświetlone powiadomienie z komunikatem o błędzie.

Jeśli chcesz, aby Podgląd szablonu toohello tooreturn, wybierz hello *szablony* przycisk hello górnym pasku nawigacyjnym. Przełączanie podglądu szablonu toohello Wstecz, utracisz niezapisane postępu. Wcześniejsze tooswitching do podglądu szablonu, zobaczysz komunikat ostrzegawczy informujący o tym.  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>Jak toodeploy aplikacji logiki utworzonych na podstawie szablonu
Po ładowany szablon i żądane zmiany wprowadzone w hello lewym górnym rogu wybierz hello przycisk zapisywania. Spowoduje to zapisanie i publikuje aplikacji logiki.  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

Jeśli będzie więcej informacji na temat sposobu tooadd więcej kroki do istniejącego szablonu aplikacji logiki, takich jak lub dokonaj edycji ogólnie rzecz biorąc, Dowiedz się więcej o [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

