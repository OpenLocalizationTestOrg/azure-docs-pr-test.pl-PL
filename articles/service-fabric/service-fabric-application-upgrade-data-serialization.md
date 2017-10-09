---
title: 'Uaktualnianie aplikacji: serializacja danych | Dokumentacja firmy Microsoft'
description: "Najlepsze rozwiązania dla serializacji danych i jak wpływa na uaktualnienia równoległe aplikacji."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Jak serializacja danych wpływa na uaktualnienia aplikacji
W [aplikacji uaktualnienia stopniowego](service-fabric-application-upgrade.md), uaktualnienie hello jest stosowane tooa podzbioru węzłów, domeny uaktualnienia pojedynczo. W trakcie tego procesu niektórych domen uaktualnienia znajdują się na powitania nowsza wersja aplikacji, a niektórych domen uaktualnienia znajdują się na powitania starszej wersji aplikacji. Podczas fazy hello hello nowej wersji aplikacji musi być możliwe tooread hello starą wersję danych, a hello starą wersję aplikacji musi być możliwe tooread hello nowej wersji danych. Jeśli format danych hello nie jest zgodny, uaktualnienie hello do przodu i do tyłu może zakończy się awarią lub gorsza, dane mogą być utracone lub uszkodzony. W tym artykule opisano, co stanowi formatu danych i oferuje najlepsze rozwiązania dotyczące zapewnienie, że dane są do przodu i do tyłu zgodne.

## <a name="what-makes-up-your-data-format"></a>Co tworzą formatu danych?
W sieci szkieletowej usług Azure dane hello jest utrwalenia i replikacji pochodzi z klasy C#. Dla aplikacji używających [niezawodnej kolekcje](service-fabric-reliable-services-reliable-collections.md), że dane są obiekty hello w hello niezawodnej słowniki i kolejek. Dla aplikacji używających [Reliable Actors](service-fabric-reliable-actors-introduction.md), czyli hello kopii stan hello aktora. Te klasy C#, muszą podlegać serializacji toobe utrwalenia i replikacji. W związku z tym hello format danych został zdefiniowany przez hello pola i właściwości, które są serializowane, a także jak ich są serializowane. Na przykład w `IReliableDictionary<int, MyClass>` hello dane są serializowane `int` i serializacji `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Wynik zmianę formatu danych zmiany kodu
Ponieważ hello format danych jest określana przez klas C#, klas toohello zmian może spowodować zmianę formatu danych. Należy zachować ostrożność tooensure, który może obsługiwać uaktualnienia stopniowego zmianę formatu danych hello. Przykłady, które mogą powodować zmiany formatowania danych:

* Dodawanie lub usuwanie pól lub właściwości
* Zmiana nazwy pola lub właściwości
* Zmienianie typów hello pól lub właściwości
* Zmiana nazwy klasy hello lub przestrzeni nazw

### <a name="data-contract-as-hello-default-serializer"></a>Kontrakt danych jako domyślnego elementu serializującego hello
Serializator Hello jest zazwyczaj odpowiedzialny za odczytywanie danych hello i deserializację go do wersji bieżącej hello, nawet jeśli dane hello jest w starszej lub *nowszej* wersji. Witaj domyślnym elementem serializującym jest hello [serializator kontraktu danych](https://msdn.microsoft.com/library/ms733127.aspx), który zawiera reguły dobrze zdefiniowany kontroli wersji. Kolekcje niezawodnej Zezwalaj toobe serializator hello zastąpiona, ale Reliable Actors aktualnie nie. Serializator danych Hello odgrywa ważną rolę w naprawieniu uaktualnienia równoległe. serializator kontraktu danych Hello jest serializator hello, zalecany dla aplikacji sieci szkieletowej usług.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Jak hello format danych wpływa na uaktualnienia stopniowego
Podczas uaktualnienia stopniowego, istnieją dwa główne scenariusze, w którym serializator hello napotkać starszej lub *nowszej* wersji danych:

1. Po węzeł zostanie uaktualniony i uruchamia tworzenie kopii zapasowej, nowe serializator hello załaduje hello danych, które były toodisk utrwalonego za stara wersja hello.
2. Podczas uaktualnienia stopniowego hello hello klastra będzie zawierać kombinację hello starej i nowej wersji kodu. Ponieważ replik może znajdować się w różnych domenach uaktualnienia i replik wysyłania danych tooeach innych, hello nowego lub starego wersji danych może napotkać hello stary i/lub nowych wersji programu szeregującego.

> [!NOTE]
> Witaj, "Nowa wersja" i "starą wersję" w tym miejscu można znaleźć wersji toohello swój kod, który jest uruchomiony. Hello "nowe serializatora" odwołuje się toohello serializator kodu, który jest wykonywany w nowej wersji aplikacji hello. Hello "nowe dane" odnosi się toohello serializacji C# klasy z hello nowej wersji aplikacji.
> 
> 

Witaj dwie wersje kodu i musi mieć format danych, zarówno do przodu i do tyłu zgodne. Jeśli nie są zgodne, hello uaktualnienia stopniowego może zakończyć się niepowodzeniem lub dane mogą zostać utracone. uaktualnienie stopniowe Hello może zakończyć się niepowodzeniem, ponieważ kod hello lub serializator może zgłaszać wyjątków lub fault po napotkaniu hello innych wersji. Dane mogą zostać utracone, jeśli na przykład dodano nową właściwość, ale odrzuca je podczas deserializacji serializator starego hello.

Kontrakt danych jest hello zalecane rozwiązania za zapewnienie, że dane są zgodne. Ma ona versioning dobrze zdefiniowane zasady Dodawanie, usuwanie i zmiana pola. Ma również obsługę zajmujących się nieznany pól, przechwytywanie procesem hello serializacji i deserializacji i zajmujących się dziedziczenia klas. Aby uzyskać więcej informacji, zobacz [kontraktu danych przy użyciu](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Następne kroki
[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.

[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.

Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).

Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).

Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji ](service-fabric-application-upgrade-troubleshooting.md).

