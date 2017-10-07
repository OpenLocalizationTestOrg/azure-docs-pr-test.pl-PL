---
title: "aaaMigrating BizTalk Server — rozwiązania dotyczące EDI tooBizTalk podręcznik techniczny usług | Dokumentacja firmy Microsoft"
description: "Migrowanie EDI tooMABS; Usługi BizTalk Services dla platformy Microsoft Azure"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Migracja usług tooBizTalk BizTalk Server — rozwiązania dotyczące EDI: Podręcznik techniczny

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Autor: Wieman Timowi i Nitin Mehrotra

Recenzenci: Karthik Bharthy

Napisane przy użyciu: usługi BizTalk platformy Microsoft Azure — luty 2014 wersji.

## <a name="introduction"></a>Wprowadzenie
(Lub grupy użytkowników) jest jednym z najbardziej rozpowszechnionych środków hello, za pomocą którego firm wymiany danych elektronicznie, określane również jako Business-to-Business lub B2B transakcji. BizTalk Server wystąpiła Obsługa EDI za pośrednictwem dekadę od początkowego wydania BizTalk Server hello. Usługi BizTalk Microsoft nadal hello obsługę EDI rozwiązania na platformie Microsoft Azure hello. Transakcje B2B są przeważnie zewnętrznych tooan organizacji i stąd jest łatwiejsze tooimplement Jeśli został wdrożony na platformie chmury. Microsoft Azure obsługuje tę funkcję za pomocą usługi BizTalk Services.

Gdy niektórzy klienci przyjrzeć się usługi BizTalk Services jako platforma "greenfield" dla nowych rozwiązań EDI, wielu klientów ma bieżącego rozwiązań BizTalk Server EDI one być toomigrate tooAzure. Ponieważ EDI usługi BizTalk jest zaprojektowanej architektury hello na podstawie klucza jednostki jako architektura BizTalk Server EDI (partnerów, jednostek, umów handlowych), jest możliwe toomigrate BizTalk Server EDI artefakty tooBizTalk usług.

W tym dokumencie omówiono niektóre różnice hello z Migrowanie tooBizTalk artefakty BizTalk Server EDI usług. Ten dokument zakłada praktyczną znajomość i umów z partnerami handlowymi BizTalk Server EDI przetwarzania. Aby uzyskać więcej informacji dotyczących BizTalk Server EDI, zobacz [handlowymi partnera zarządzania przy użyciu BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>Której wersji programu BizTalk Server EDI artefakty mogą być migrowane tooBizTalk usług?
Hello BizTalk Server EDI modułu zostały znacznie rozszerzone dla BizTalk Server 2010, gdy był remodeled tooinclude partnerów, profilów i umów. Używa usługi BizTalk hello samą powitalnych tooorganize modelu partnerami handlowymi i hello oddziałów firm w ramach tych partnerami handlowymi. W związku z tym artefaktów z BizTalk Server 2010 i nowszych wersjach tooBizTalk migracji EDI usługi, jest procesem bardziej bezpośrednio do przodu. toomigrate EDI artefakty skojarzone z tooBizTalk wcześniejsze wersje Server 2010, należy najpierw uaktualnić tooBizTalk Server 2010, a następnie przeprowadzić migrację z artefakty EDI tooBizTalk usług.

## <a name="scenariosmessage-flow"></a>Przepływ scenariusze/komunikatów
Jako z BizTalk Server EDI przetwarzania w usługi BizTalk Services opiera się rozwiązania zarządzania handlowymi partnera (TPM). Witaj rozwiązania modułu TPM ma hello następujące najważniejsze składniki:

* Partnerami handlowymi, które reprezentują organizacji w ramach transakcji B2B.
* Profile, które reprezentują oddziałami partnerem handlowym.
* Handlowymi umów z partnerami (lub umów) reprezentujący hello umowy biznesowych między dwoma partnerami/profile.

Hello następującej ilustracji przedstawiono podobieństwa hello, a także różnice między rozwiązań BizTalk Server EDI i EDI usługi BizTalk rozwiązania:

![][EDImessageflow]

Witaj podstawowe różnice i podobieństwa przepływ rozwiązania EDI w BizTalk Server i usługi BizTalk Services to:

* Tak samo, jak BizTalk Server używa tooreceive potoku EDIReceive wiadomości EDI i toosend potoku EDISend wiadomości EDI, usługi BizTalk Services używa odbierania EDI tooreceive mostek i wysłać EDI toosend Mostek EDI wiadomości. BizTalk Server potoki hello są skojarzone z umowy przy użyciu wysyłania lub portów odbioru. W usługi BizTalk Services samej umowy hello oznacza hello wysyłanie lub odbieranie mostek.
* W BizTalk Server po hello EDIReceive potoku procesów hello wiadomości EDI wiadomość hello jest zrzut tooa bazy danych programu SQL Server. potok EdiSend Hello następnie przejmuje wiadomość hello z bazy danych programu SQL Server hello, procesy i następnie wysyła on toohello partnera handlowego.
  
    W usługach BizTalk po hello EDI komunikat Mostek procesów hello EDI, kieruje procesu zewnętrznego tooan wiadomość hello. Proces zewnętrzny Hello może być uruchomiona w Microsoft Azure lub lokalnie. Proces zewnętrzny Hello powinny kierować toohello wiadomość hello EDI wysyłania Mostek; Mostek wysyłania Hello z założenia nie będzie ściągać wiadomość hello. Po wiadomość hello przetwarzania hello EDI wysyłania Mostek kieruje partnerem handlowym toohello wiadomość hello.

Usługi BizTalk Services zapewnia konfiguracji łatwy w użyciu środowisko tooquickly tworzenie i wdrażanie umowę B2B między partnerami handlowymi bez konfigurowania żadnych Microsoft rozwiązań usługi obliczenia Azure wystąpienia (role sieci Web lub procesu roboczego), żadnych baz danych SQL Azure firmy Microsoft lub dowolną Konta magazynu Microsoft Azure. Wymaga bardziej złożonymi scenariuszami wiązania w przepływach pracy lub innego typu przetwarzania usługi "wokół krawędzi hello" Umowy handlowymi partnera, oznacza to, że przed lub po zakończeniu przetwarzania Mostek handlowymi EDI umowę partnera. Szczegółowe hello poniższa sekwencja zdarzeń wystąpić podczas przetwarzania w usługi BizTalk Services komunikatów EDI.

1. Komunikat EDI zostało odebrane od partnera, Fabrikam handlowego.  Odbieranie komunikatów EDI z partnerami handlowymi, protokołów, takich jak FTP, SFTP AS2 i HTTP/S. obsługuje usługi BizTalk Services
2. Witaj handlowymi przetwarzania po stronie odbierającej umowę partnera rozkłada hello EDI tooXML formatu.  Można przekierować hello dezasemblowania EDI komunikatów (w formacie XML) tooService magistrali końcowych, takie jak punkt końcowy przekaźnik magistrali usług, temat magistrali usług, kolejką usługi Service Bus lub mostka usługi BizTalk Services.
3. Witaj asemblerze XML można następnie można odbierać wiadomości z punktu końcowego hello w celu dalszego przetwarzania niestandardowego.  Te punkty końcowe może być przetworzone przez składnik lokalnymi lub rozwiązań usługi obliczenia Azure Microsoft wystąpienia toofurther procesu hello komunikatu za pośrednictwem usługi Windows przepływu pracy (WF) lub usługi Windows Communication Foundation (WCF), np.
4. Witaj "po stronie wysyłania przetwarzanie" hello umowy z partnerem handlowym następnie składana wiadomości powitania XML do formatu EDI i wysyła je tootrading partnera, Contoso.  Do wysyłania wiadomości EDI tootrading partnerów, usługi BizTalk Services obsługuje protokoły takie same jak te używane do odbierania wiadomości EDI hello.

Dalej w tym dokumencie znajdują się ogólne wskazówki dotyczące migracji niektórych hello różnych BizTalk Server EDI artefakty tooBizTalk usług.

## <a name="sendreceive-ports-tootrading-partners"></a>Porty wysyłania i odbierania tooTrading partnerów
BizTalk Server umożliwia zdefiniowanie odbierania lokalizacje i porty Odbierz tooreceive EDI/XML wiadomości z partnerami handlowymi i skonfigurować porty wysyłania toosend EDI/XML wiadomości tootrading partnera. Następnie powiązać się te tooa porty handlowymi za pomocą konsoli administracyjnej serwera BizTalk hello umowy z partnerem. W usługach BizTalk otrzymywania wiadomości z partnerami i której wysyłane wiadomości tootrading partnerów są skonfigurowane jako część hello handlowymi umowy z partnerem, sama (jako część ustawienia transportu) w lokalizacji hello hello Portal usługi BizTalk .  Dlatego nie naprawdę masz hello pojęcie "Wyślij porty" i "otrzymywać lokalizacje", per se w usługi BizTalk Services. Aby uzyskać więcej informacji, zobacz [Tworzenie umów](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Potoki (mostków)
BizTalk Server EDI potoki są jednostki przetwarzania komunikatów, które mogą również obejmować niestandardową logikę na potrzeby przetwarzania określonych funkcji, zgodnie z wymaganiami aplikacji hello. Usługi BizTalk hello równoważne czy Mostek EDI. Jednak w usługi BizTalk Services obecnie mostków EDI hello są "zamknięte".  Oznacza to, że nie można dodać własne Mostek EDI tooan działań niestandardowych. Poza Mostek EDI hello w aplikacji, należy wszelkie niestandardowe przetwarzania przed lub po wiadomość hello wprowadza Mostek hello skonfigurowany jako część hello umowy z partnerem obrotu. Mostków EAI ma hello opcja toodo niestandardowych przetwarzania. Jeśli chcesz przetwarzania niestandardowego służy mostków EAI przed lub po wiadomość hello jest przetwarzany przez mostek EDI hello. Aby uzyskać więcej informacji, zobacz [jak tooInclude niestandardowy kod mostków](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Możesz wstawić przepływem publikowania/subskrypcji z niestandardowych kodów i/lub przy użyciu usługi Service Bus do obsługi komunikatów kolejek i tematów przed hello handlowymi umowy z partnerem odbiera wiadomość hello lub po umowy hello przetwarza wiadomość hello i kieruje je tooa punktu końcowego Service Bus.

Zobacz **przepływ scenariusze/komunikatów** w tym temacie hello przepływu komunikatów.

## <a name="agreements"></a>Umowy
Jeśli znasz hello BizTalk Server 2010 handlowi partnera umów używana w przypadku przetwarzania EDI usługi BizTalk Services umów z partnerami handlowymi wyglądać bardzo znajomo. Większość umowy hello ustawienia są hello tego samego i użyj hello tą samą terminologię. W niektórych przypadkach hello umowy ustawienia są dużo prostsze toohello w porównaniu z tych samych ustawień w BizTalk Server. Usługi BizTalk platformy Microsoft Azure obsługuje X12, EDIFACT i AS2 transportu.

Usługi BizTalk platformy Microsoft Azure udostępnia **migracji danych modułu TPM** narzędzia partnerami handlowymi toomigrate i umów partnera handlowymi BizTalk Server modułu tooBizTalk Portal usługi. Narzędzie migracji danych modułu TPM Hello jest dostępne jako część pakietu narzędzi, który można pobrać z hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). Pakiet HELLO zawiera również plik readme, który zawiera instrukcje dotyczące jak narzędzie hello toouse i podstawowe informacje dotyczące rozwiązywania problemów dla hello narzędzia.

## <a name="schemas"></a>Schematy
Usługi BizTalk Services zawiera schematów EDI, które mogą być używane w rozwiązaniach usługi BizTalk Services.  Ponadto schematów EDI serwera BizTalk można również można użyć z usługi BizTalk Services, ponieważ węzeł główny hello schematów EDI hello jest taka sama w BizTalk Server, a także usługi BizTalk. W związku z tym będzie można podjęcia stanie toodirectly Twojego schematów EDI serwera BizTalk i używać ich w hello EDI rozwiązania, które za pomocą usługi BizTalk Services. Możesz również pobrać hello schematów z hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Mapy (transformacji)
Mapy w BizTalk Server są nazywane transformacje w usługi BizTalk Services. Migrowanie mapy z tooBizTalk BizTalk Server, usługi może być jedną z hello bardziej złożonych zadań tooachieve (w zależności od złożoności mapy). Hello mapowania narzędziem używanym do usługi BizTalk Services jest inna niż hello BizTalk mapowania. Nawet jeśli wygląda mapowania hello przede wszystkim hello takie same, różni się hello podstawowy format mapy. Witaj functoids (o nazwie **operacji mapy** w usługi BizTalk Services) również użytkowników toohello dostępne są różne.  W efekcie nie mogą bezpośrednio używać mapy BizTalk w usługach BizTalk. Ponadto nie wszystkie dostępne w BizTalk Server functoids hello są dostępne jako operacje mapy w usługi BizTalk Services.

### <a name="new-transform-operations"></a>Nowe operacje transformacji
Chociaż hello listę operacji mapy przekształcania może wydawać się bardzo różne hello mapowania BizTalk Server, przekształca usługi BizTalk ma nowych sposobów hello te same zadania. Na przykład mieć przekształca usługi BizTalk **listę operacji** dostępne. To nie jest dostępna w hello BizTalk mapowania.  Witaj **listę operacji** pozwalają toocreate i działają na "List", w przypadku, gdy lista jest zbiór elementów (znanej także jako "wiersze"), a każdy element może mieć wiele elementów członkowskich (znanej także jako "kolumny").  Można sortować hello listy elementów select oparte na stanie itp.

Innym przykładem nowych funkcji w programie przekształca usługi BizTalk są hello **operacji pętli**.  Jest trudne toocreate zagnieżdżone pętli w hello mapowania BizTalk Server.  W związku z tym hello pętli mapy operacji zostaną dodane hello przekształca usługi BizTalk.

Jeszcze innym przykładem jest hello **If-to-inaczej** operacji mapy wyrażenia.  Wykonuje operację if to inaczej było możliwe w hello BizTalk mapowania, ale wymaga ona wiele tooaccomplish functoids pozornie prostym zadaniem.

### <a name="migrating-biztalk-server-maps"></a>Migrowanie serwera BizTalk mapy
Usługi BizTalk platformy Microsoft Azure oferuje toomigrate narzędzie BizTalk Server mapuje tooBizTalk transformacje usług. Witaj **BTMMigrationTool** jest dostępna jako część hello **narzędzia** pakietu podaną w hello [pobierania zestawu SDK usługi BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkId=235057). Aby uzyskać więcej informacji o narzędziu hello, zobacz [przekonwertować tooa mapy BizTalk, Przekształć usługi BizTalk](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

Można również przyjrzeć się próbkę przez Sandro Pereira, BizTalk MVP na sposób zbyt[migracji BizTalk Server mapy tooBizTalk usług transformacje](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Orchestrations
Toomigrate tooMicrosoft przetwarzania aranżacji BizTalk Server Azure należy hello orchestrations potrzebny toobe napisany od nowa, ponieważ Microsoft Azure nie obsługuje uruchomionych orchestrations BizTalk Server.  Można zmodyfikować hello funkcji aranżacji w usłudze Windows Workflow Foundation 4.0 (WF4).  Powinien to być ukończone ponownego zapisywania, ponieważ nie ma obecnie nie migracji z tooWF4 orchestrations BizTalk Server. Oto kilka zasobów dla przepływu pracy systemu Windows:

* [*Jak toointegrate przepływu pracy WCF usługi z tematów i kolejek usługi Service Bus* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) przez Paolo Salvatori. 
* [*Kompilowanie aplikacji za pomocą programu Windows Workflow Foundation i Azure* sesji](http://go.microsoft.com/fwlink/p/?LinkId=237314) z konferencji hello 2011 kompilacji.
* [*Centrum deweloperów systemu Windows Workflow Foundation* ](http://go.microsoft.com/fwlink/p/?LinkId=237315) w witrynie MSDN.
* [*Dokumentacja Windows Workflow Foundation 4 (WF4)* ](https://msdn.microsoft.com/library/dd489441.aspx) w witrynie MSDN.

## <a name="other-considerations"></a>Inne zagadnienia
Poniżej przedstawiono kilka kwestii, które należy wykonać podczas korzystania z usługi BizTalk Services.

### <a name="fallback-agreements"></a>Rezerwowy umów
BizTalk Server EDI przetwarzania ma hello pojęcie "Umów powrotu".  Usługi BizTalk Services jest **nie** ma koncepcji umowy powrotu do tej pory.  Zobacz tematy dokumentacji BizTalk [hello roli umów w przetwarzaniu EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) i [Konfigurowanie globalnym, ani właściwości umowy powrotu](https://msdn.microsoft.com/library/bb245981.aspx) Aby uzyskać informacje dotyczące używania umów rezerwowe w BizTalk Serwer.

### <a name="routing-toomultiple-destinations"></a>Routingu toomultiple miejsc docelowych.
Mostków usługi BizTalk Services w jego bieżącym stanie nie obsługuje routingu wiadomości toomultiple miejsc docelowych przy użyciu publikowanie-subskrypcji modelu. Zamiast tego można przekierować wiadomości z usługi BizTalk Services Mostek tooa tematu usługi Service Bus, które mogą mieć wiele wiadomość hello tooreceive subskrypcje w więcej niż jednym punkcie końcowym.

## <a name="conclusion"></a>Podsumowanie
Usługi BizTalk platformy Microsoft Azure są aktualizowane w regularnych punktów kontrolnych tooadd więcej funkcji i możliwości. Przy każdej aktualizacji mamy nadzieję toosupporting zwiększyć toofacilitate funkcji tworzenia rozwiązań na trasie przy użyciu usługi BizTalk Services i innych technologii Azure.

## <a name="see-also"></a>Zobacz też
[Tworzenie aplikacji przedsiębiorstwa z platformy Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
