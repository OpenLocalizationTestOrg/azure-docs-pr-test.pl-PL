---
title: "wgląd w aaaGet z Centrum zabezpieczeń Azure za pomocą usługi Power BI | Dokumentacja firmy Microsoft"
description: "Witaj pakiet zawartości usługi Power BI Centrum zabezpieczeń Azure umożliwia łatwe toofind alertów zabezpieczeń, zaleceń, zaatakowanych zasobów i trendów, opartych na zestawu danych, który został utworzony na potrzeby raportu."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Uzyskiwanie szczegółowych informacji z Centrum zabezpieczeń Azure za pomocą usługi Power BI
Witaj [pulpitu nawigacyjnego programu Power BI](http://aka.ms/azure-security-center-power-bi) dla Centrum zabezpieczeń Azure umożliwia toovisualize, analizowanie i filtrowanie zaleceń oraz alertów zabezpieczeń z dowolnego miejsca, w tym urządzeniu przenośnym. Użyj trendów tooreveal pulpit nawigacyjny usługi Power BI hello i wyświetlać alerty zabezpieczeń według zasobu lub adresu IP źródła oraz nierozwiązane zagrożenia bezpieczeństwa według zasobu lub wieku wzorców ataków..

Można również w różny sposób łączyć alerty zabezpieczeń i zalecenia z usługi Security Center z innymi danymi, na przykład korzystając z [dzienników inspekcji platformy Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) i usługi [Azure SQL Database Auditing](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Dostępne pulpity nawigacyjne programu Power BI, a można również wyeksportować tego tooExcel danych na łatwe raportowanie stanu zabezpieczeń hello zasobów w chmurze.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Przy użyciu Centrum zabezpieczeń Azure tooaccess pulpit nawigacyjny usługi Power BI
Można również użyć raportów usługi Power BI tooaccess pulpit nawigacyjny Centrum zabezpieczeń Azure hello. Wykonaj to zadanie hello tooperform kroki:

1. W hello **Centrum zabezpieczeń Azure** pulpitu nawigacyjnego, kliknij przycisk **usługi Power BI** przycisku.

    ![Połącz przy użyciu usługi Power BI Centrum zabezpieczeń tooAzure](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Witaj **usługi Power BI** zostanie otwarty blok hello prawej strony pokazane na powitania po ekranu:

    ![Połącz przy użyciu usługi Power BI Centrum zabezpieczeń tooAzure](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Jeśli tworzysz pulpit nawigacyjny usługi Power BI hello na powitania po raz pierwszy, można wybrać jedną z następujących hello opcje w hello **Eksplorowanie w usłudze Power BI** bloku:

   * **Pulpit nawigacyjny szczegółowych informacji o zabezpieczeniach**: Wybierz tę opcję, jeśli chcesz toocreate pulpit nawigacyjny, który zawiera stan zabezpieczeń, wątki i wykrycia zagrożeń. Jest to częściej stosowana opcja dla roli DevOps, która odpowiada za analizowanie stanu ochrony oraz wykrytych alertów w subskrypcjach.
   * **Pulpit nawigacyjny zarządzania zasadami**: Wybierz tę opcję, jeśli chcesz tooexplore zarządzania i wymuszania zasad.  Jest to opcja częściej stosowana w centralnym dziale IT, który skupia się na zagadnieniach związanych z zarządzaniem. Będzie mógł używać tego pulpitu nawigacyjnego toogain widoczności i szczegółowe informacje na temat przestrzegania zasad zabezpieczeń w organizacji.
   * Jeśli masz już pulpit nawigacyjny usługi Power BI, kliknij przycisk **Przejdź tooyour bieżącego pulpitu nawigacyjnego usługi Power BI**.
4. Na przykład kliknij opcję **Pulpit nawigacyjny Szczegółowe informacje o zabezpieczeniach**. Jeśli jest to powitania po raz pierwszy, tworzysz pulpit nawigacyjny usługi Power BI dla Centrum zabezpieczeń jest pakiet zawartości hello tooinstall zostanie wyświetlony monit. Kliknij przycisk **uzyskać** przycisku na powitania **zawartości pakietów dla usługi Power BI** okna, jak pokazano w po ekranie powitania:

    ![Pulpit nawigacyjny szczegółowych informacji o zabezpieczeniach Centrum zabezpieczeń Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Witaj **połączyć tooAzure szczegółowych informacji o zabezpieczeniach Centrum zabezpieczeń** wyświetlenie okna. Upewnij się, że hello **uwierzytelniania** jest metoda **oAuth2** w sposób przedstawiony poniżej i kliknij przycisk **Zaloguj** przycisku.

    ![Authentication](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. Użytkownik może zostać poproszony tooauthenticate ponownie przy użyciu poświadczeń platformy Azure. Po uwierzytelnieniu pulpit nawigacyjny zostanie utworzony. Po utworzeniu pulpitu nawigacyjnego hello pokazane na powitania po ekranie zostanie wyświetlony raport o strukturze podobnej hello:

    ![Pulpit nawigacyjny usługi Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Odświeżanie raportu hello jest zaplanowane tootake miejsce codziennie. W przypadku, gdy wystąpi błąd podczas odświeżania tego odczytu [potencjalne problemy z usługi Power BI Centrum zabezpieczeń Azure hello odświeżaniem](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), aby uzyskać więcej informacji na temat tootroubleshoot.
>
>

Tutaj można zobaczyć liczbę hello alerty zabezpieczeń i zalecenia, a także hello liczbę maszyn wirtualnych, baz danych Azure SQL i zasobów sieciowych, które są monitorowane przez Centrum zabezpieczeń Azure.

Łącze tooAzure Centrum zabezpieczeń przekierowuje toohello portalu Azure. Wykresy Hello była łatwe toovisualize informacji o zaleceniach dotyczących zabezpieczeń i alertów, w tym:

* Stan zabezpieczeń zasobów
* Oczekujące zalecenia
* Zalecenia dotyczące maszyny wirtualnej
* Alerty w czasie
* Zaatakowane zasoby
* Zaatakowane adresy IP

Każdy wykres zawiera dodatkowe informacje szczegółowe. Wybierz toosee kafelka więcej informacji. Na przykład Witaj **stan zabezpieczeń zasobów** kafelka przedstawia dodatkowe informacje na temat oczekujących zaleceń według zasobów pokazane na powitania po ekranie:

![Zalecenia](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Po kliknięciu każdego wiersza wykresu hello inne osoby będą toogray wychodzących i skupić się tylko na powitania jednego wybranego. tooreturn toohello pulpitu nawigacyjnego, kliknij przycisk **Centrum zabezpieczeń Azure** w obszarze hello **pulpity nawigacyjne** opcji w okienku po lewej stronie powitania tej strony.

> [!NOTE]
> Jeśli chcesz toocustomize raportów przez dodanie dodatkowych pól lub zmianę istniejących elementów wizualnych, można edytować hello raportu. Przeczytaj temat [Interakcja z raportem w widoku do edycji programu Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/), aby uzyskać więcej informacji.
>
>

Witaj **alerty w czasie, zaatakowane zasoby** i **adresy IP osoby atakującej** Kafelki będzie miał hello podobne dane wyjściowe po kliknięciu kolejno poszczególne go. Wynika to z faktu hello raport agreguje informacje dotyczące wszystkich trzech zmiennych i określa je **zaatakowane zasoby** pokazane na powitania po ekranu:

![Zaatakowane zasoby](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

W tym momencie można także zapisać kopię tego raportu, wydrukować go lub opublikować w sieci web hello przy użyciu opcji hello dostępnych w hello **pliku** menu.

![Menu Plik](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Eksplorowanie danych w Centrum zabezpieczeń Azure za pomocą usług Power BI
Połącz toohello [Power BI Content Pack Services](https://msit.powerbi.com/groups/me/getdata/services) w usłudze Power BI i wykonaj następujące kroki hello:

1. W hello **pakiet zawartości usługi Power BI** zostaną wyświetlone dwie opcje, jak pokazano poniżej.

    ![Pakiet zawartości usługi Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Jeśli już wykonane hello pierwszej części tego artykułu, zostanie wyświetlony tylko jedną opcję, która jest zarządzanie zasadami Centrum zabezpieczeń Azure.
   >
   >
2. W celu hello tego przykładu kliknij **uzyskać** w hello **Zarządzanie zasadami Centrum zabezpieczeń Azure** kafelka.
3. W hello **połączyć tooAzure Zarządzanie zasadami Centrum zabezpieczeń** okna, upewnij się, że tooselect **oAuth2** w obszarze **metodę uwierzytelniania** liście rozwijanej, jak pokazano poniżej, a następnie kliknij przycisk **Zaloguj** przycisku.

    ![Okno Zarządzanie zasadami](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Będzie przekierowanego tooan stronę uwierzytelniania, gdzie należy wpisać poświadczenia hello używasz Centrum zabezpieczeń tooAzure tooconnect. Po zakończeniu procesu uwierzytelniania hello usługi Power BI rozpocznie importowanie danych toobuild raportów. W tym czasie może zostać wyświetlony powitania po wiadomość hello prawym górnym rogu przeglądarki:

    ![Połącz przy użyciu usługi Power BI Centrum zabezpieczeń tooAzure](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Po hello pulpit nawigacyjny jest tworzony na powitania po raz pierwszy może trwać dłużej niż zwykle — szczególnie w przypadku scenariuszy z wieloma subskrypcjami.
   >
   >
5. Po zakończeniu procesu hello pulpit nawigacyjny usługi Power BI Centrum zabezpieczeń Azure zostanie załadowany z hello **Zarządzanie zasadami** raport podobny toohello, co przedstawiono poniżej:

    ![Pulpit nawigacyjny Zarządzanie zasadami](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób toouse usługi Power BI w Centrum zabezpieczeń Azure. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Przewodnik planowania Centrum zabezpieczeń Azure i obsługi](security-center-planning-and-operations-guide.md) — Dowiedz się jak tooplan wdrożenia Centrum zabezpieczeń Azure.
* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się jak tooconfigure ustawienia zabezpieczeń w Centrum zabezpieczeń Azure
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiedź
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure
