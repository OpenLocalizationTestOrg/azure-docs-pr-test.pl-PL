---
title: "aaaAzure Centrum zabezpieczeń szybki start-Podręcznik | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomaga szybko rozpocząć pracę z Centrum zabezpieczeń Azure przeprowadzi Cię hello składniki monitorowania zabezpieczeń i zasad zarządzania i podano linki toonext czynności."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Przewodnik Szybki start dotyczący usługi Azure Security Center
Ten artykuł pomaga szybko rozpocząć pracę z Centrum zabezpieczeń Azure pomocne hello składniki monitorowania zabezpieczeń i zasad zarządzania Centrum zabezpieczeń.

> [!NOTE]
> Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Wymagania wstępne
wprowadzenie do Centrum zabezpieczeń tooget, musi mieć tooMicrosoft subskrypcji Azure. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnego konta](https://azure.microsoft.com/pricing/free-trial/).

Warstwa bezpłatna Hello Centrum zabezpieczeń jest włączane automatycznie w ramach subskrypcji i zapewnia wgląd w hello stan zabezpieczeń zasobów platformy Azure. Zapewnia to podstawowe zarządzanie zasadami zabezpieczeń, zaleceniami dotyczącymi zabezpieczeń i integrację z dotyczącymi zabezpieczeń produktami i usługami partnerów platformy Azure.

Dostęp do Centrum zabezpieczeń hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). toolearn więcej informacji na temat hello portalu Azure, zobacz hello [dokumentację portalu](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Uprawnienia
W Centrum zabezpieczeń widoczne są tylko informacje dotyczące tooan zasobów platformy Azure po przypisaniu roli hello właściciela, współautora lub czytelnika dla grupy zasobów lub subskrypcji hello należącą do zasobu. Zobacz [uprawnienia w Centrum zabezpieczeń Azure](security-center-permissions.md) toolearn więcej informacji na temat ról i akcji dozwolonych w Centrum zabezpieczeń.

## <a name="data-collection"></a>Zbieranie danych
Centrum zabezpieczeń zbiera dane z Twojego tooassess maszynach wirtualnych (VM) stanu zabezpieczeń, podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. Po pierwszym uzyskaniu dostępu do usługi Security Center zbieranie danych jest włączone na wszystkich maszynach wirtualnych w ramach subskrypcji. Centrum zabezpieczeń przepisy hello Microsoft Monitoring Agent na wszystkich istniejących obsługiwane maszyny wirtualne platformy Azure i nowe pliki, które są tworzone. Zobacz [Włącz zbieranie danych](security-center-enable-data-collection.md) toolearn więcej informacji na temat działania zbierania danych.

Zbieranie danych jest zalecane. Jeśli używasz hello warstwę bezpłatna Centrum zabezpieczeń można wyłączyć zbieranie danych z maszyn wirtualnych przez wyłączenie zbierania danych w zasadach zabezpieczeń hello. Zbieranie danych jest wymagane dla subskrypcji w warstwie standardowa hello Centrum zabezpieczeń. Zobacz [cennik Centrum zabezpieczeń](security-center-pricing.md) hello toolearn więcej informacji o wolnym i Standard warstw cenowych.

Hello następujące kroki opisują sposób tooaccess i użyj hello składniki z Centrum zabezpieczeń. W tych krokach zostanie przedstawiony zostanie sposób tooturn wyłączyć zbieranie danych po wybraniu tooopt wychodzących.

> [!NOTE]
> W tym artykule przedstawiono hello usługi za pomocą przykładowego wdrożenia. Ten artykuł nie jest przewodnikiem krok po kroku.
>
>

## <a name="access-security-center"></a>Dostęp do usługi Security Center
W portalu hello wykonaj te kroki tooaccess Centrum zabezpieczeń:

1. Na powitania **Microsoft Azure** menu, wybierz opcję **Centrum zabezpieczeń**.

   ![Azure menu][1]
2. Jeśli uzyskujesz dostęp do Centrum zabezpieczeń dla powitania po raz pierwszy, hello **powitalnej** zostanie otwarty blok. Wybierz **Centrum zabezpieczeń uruchamiania** tooopen hello **Centrum zabezpieczeń** bloku i tooenable zbierania danych.
   ![Ekran powitalny][10]
3. Po uruchomić Centrum zabezpieczeń z bloku-Zapraszamy hello lub Centrum zabezpieczeń, wybierz z menu Microsoft Azure hello hello **Centrum zabezpieczeń** zostanie otwarty blok. Dla toohello łatwy dostęp **Centrum zabezpieczeń** bloku w hello hello przyszłych, wybierz pozycję **toodashboard bloku kodu Pin** opcji (prawym górnym rogu).
   ![Opcja toodashboard bloku kodu PIN][2]

## <a name="use-security-center"></a>Korzystanie z usługi Security Center
Skonfigurować można zasady zabezpieczeń dla subskrypcji i grup zasobów platformy Azure. Skonfigurujmy zasady zabezpieczeń dla subskrypcji:

1. Na powitania **Centrum zabezpieczeń** bloku, wybierz hello **zasad** kafelka.
2. Na powitania **zasady zabezpieczeń — Zdefiniuj zasady dla subskrypcji** bloku, wybierz subskrypcję.
3. Na powitania **zasady zabezpieczeń** bloku **zbierania danych** jest włączone tooautomatically zbieranie dzienników. rozszerzenie dotyczące monitorowania Hello jest inicjowana na wszystkie bieżące oraz nowe maszyny wirtualne w subskrypcji hello. (Na powitania warstwę bezpłatna Centrum zabezpieczeń, możesz zrezygnować z funkcji zbierania danych przez ustawienie **zbierania danych** za**poza**. Ustawienie **zbierania danych** za**poza** uniemożliwia umożliwiając alertów zabezpieczeń i zaleceń Centrum zabezpieczeń.)
4. Na powitania **zasady zabezpieczeń** bloku, wybierz opcję **zasady zapobiegania**. Spowoduje to otwarcie hello **zasady zapobiegania** bloku.
5. Na powitania **zasady zapobiegania** bloku włączaj zalecenia hello mają toosee jako część zasad zabezpieczeń. Przykłady:

   * Ustawienie **aktualizacji systemu** za**na** skanowanie wszystkich obsługiwanych maszyn wirtualnych dla brakujących aktualizacji systemu operacyjnego.
   * Ustawienie **luk w zabezpieczeniach systemu operacyjnego** za**na** skanowanie wszystkich obsługiwanych maszyn wirtualnych tooidentify konfiguracji systemu operacyjnego, które może uniemożliwić hello maszyna wirtualna będzie bardziej narażona tooattack.

### <a name="view-recommendations"></a>Wyświetlanie zaleceń
1. Zwraca toohello **Centrum zabezpieczeń** bloku i wybierz hello **zalecenia** kafelka. Centrum zabezpieczeń okresowo analizuje stan zabezpieczeń hello zasobów platformy Azure. Gdy Centrum zabezpieczeń identyfikuje potencjalnych luk w zabezpieczeniach, zawiera zalecenia na powitania **zalecenia** bloku.
   ![Zalecenia w usłudze Azure Security Center][5]
2. Wybierz zalecenie dotyczące hello **zalecenia** wystawiać więcej informacji i/lub tootake hello akcji w tooresolve tooview bloku.

### <a name="view-hello-security-state-of-your-resources"></a>Wyświetl hello stan zabezpieczeń zasobów
1. Zwraca toohello **Centrum zabezpieczeń** bloku. Witaj **zapobiegania** sekcja hello pulpit nawigacyjny zawiera wskaźniki stanu zabezpieczeń powitania dla maszyn wirtualnych, sieci, danych i aplikacji.
2. Wybierz **obliczeniowe** tooview więcej informacji. Witaj **obliczeniowe** zostanie otwarty blok przedstawiający trzy karty:

  - **Omówienie** — zawiera, monitorowania i zalecenia dotyczące maszyny Wirtualnej.
  - **Maszyny wirtualne** — zawiera listę wszystkich maszyn wirtualnych i bieżących informacji zabezpieczających stanów.
  - **Usługi w chmurze** — zawiera listę ról sieci web i proces roboczy, które są monitorowane przez Centrum zabezpieczeń.

    ![Witaj Kafelek kondycja zasobów w Centrum zabezpieczeń Azure][6]

3. Na powitania **omówienie** , a następnie wybierz zalecenie, w obszarze **zalecenia dotyczące maszyny WIRTUALNEJ** tooview więcej informacji i/lub podjęcia działań tooconfigure niezbędnych opcji.
4. Na powitania **maszyn wirtualnych** , a następnie wybierz dodatkowe szczegóły tooview maszyny Wirtualnej.

### <a name="view-security-alerts"></a>Wyświetlanie alertów zabezpieczeń
1. Zwraca toohello **Centrum zabezpieczeń** bloku i wybierz hello **alerty zabezpieczeń** kafelka. Witaj **alerty zabezpieczeń** bloku otwiera i wyświetla listę alertów. Witaj analizy Centrum zabezpieczeń uwzględniającej dzienniki zabezpieczeń i aktywność sieci generuje te alerty. Uwzględniane są alerty zintegrowanych rozwiązań partnerskich.
   ![Alerty zabezpieczeń w usłudze Azure Security Center][7]

   > [!NOTE]
   > Alerty zabezpieczeń są dostępne tylko po włączeniu warstwy standardowa hello Centrum zabezpieczeń. 60-dniowa bezpłatna wersja próbna warstwy standardowa hello jest dostępna. Zobacz [następne kroki](#next-steps) Aby uzyskać informacje dotyczące sposobu tooget hello Standard warstwy.
   >
   >
2. Wybierz dodatkowe informacje tooview alertu. W tym przykładzie wybierzmy pozycję **Wykryto zmodyfikowany plik binarny systemu**. Spowoduje to otwarcie bloków, które zawierają dodatkowe szczegóły dotyczące alertu hello.
   ![Szczegóły alertów zabezpieczeń w usłudze Azure Security Center][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Widok hello kondycji rozwiązań partnerskich
1. Zwraca toohello **Centrum zabezpieczeń** bloku. Witaj **rozwiązania partnerskie** kafelka umożliwia monitorowanie, w skrócie, hello stanu kondycji rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure.
2. Wybierz hello **rozwiązania partnerskie** kafelka. Zostanie otwarty blok i wyświetla listę rozwiązań partnerskich połączone tooSecurity Center.
   ![Rozwiązania partnerskie][9]
3. Wybierz rozwiązanie partnerskie. W tym przykładzie załóżmy wybierz hello **QualysVa1** rozwiązania.  Otwiera i pokazuje stan hello rozwiązaniem partnerskim hello i rozwiązania hello skojarzonych zasobów. Wybierz **Konsola rozwiązań** Zarządzanie partnerami hello tooopen środowisko dla tego rozwiązania.

## <a name="next-steps"></a>Następne kroki
W tym artykule wprowadzono toohello składniki monitorowania zabezpieczeń i zasad zarządzania Centrum zabezpieczeń. Teraz, kiedy znasz Centrum zabezpieczeń, spróbuj hello następujące kroki:

* Skonfiguruj zasady zabezpieczeń dla subskrypcji platformy Azure. toolearn więcej, zobacz [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md).
* Użyj hello zalecenia w Centrum zabezpieczeń toohelp ochronę zasobów platformy Azure. toolearn więcej, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md).
* Przejrzyj bieżące alerty zabezpieczeń i zarządzaj nimi. toolearn więcej, zobacz [toosecurity zarządzanie i odpowiada alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md).
- [Bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md) — Dowiedz się, jak dane są zarządzane i w Centrum zabezpieczeń.
* Dowiedz się więcej o hello [zaawansowane funkcje wykrywania zagrożeń](security-center-detection-capabilities.md) pochodzące z hello [warstwy standardowa](security-center-pricing.md) Centrum zabezpieczeń. warstwy standardowa Hello jest oferowane bezpłatnie dla hello pierwsze 60 dni.
* Jeśli masz pytania dotyczące korzystania z Centrum zabezpieczeń, zobacz hello [często zadawane pytania dotyczące usługi Azure Security Center](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
