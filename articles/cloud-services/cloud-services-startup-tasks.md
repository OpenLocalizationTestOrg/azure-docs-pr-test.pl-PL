---
title: "Uruchamianie zadań w usług Azure Cloud Services aaaRun | Dokumentacja firmy Microsoft"
description: "Zadania uruchamiania pomóc w przygotowaniu środowiska usługi chmury dla aplikacji. To jest przedstawienie sposobu uruchamiania zadań pracy i w jaki sposób toomake ich"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Sposób uruchamiania tooconfigure i uruchom zadania dla usługi w chmurze
Przed rozpoczęciem rolę, można użyć operacji tooperform zadania uruchamiania. Operacje można tooperform obejmują instalowania składnika, rejestrowanie składników modelu COM, ustawienie kluczy rejestru lub uruchamia proces wymagającą dużo czasu.

> [!NOTE]
> Zadania uruchamiania nie są stosowane tooVirtual maszyny, tylko tooCloud usługi sieci Web i proces roboczy.
> 
> 

## <a name="how-startup-tasks-work"></a>Sposób działania uruchamiania zadań
Uruchamianie zadania są działaniach wykonywanych przed rozpocząć role są definiowane w hello [ServiceDefinition.csdef] pliku przy użyciu hello [zadań] elementu w obrębie hello [uruchamiania]elementu. Często uruchomienia zadania są pliki wsadowe, ale można je również aplikacji konsoli lub pliki wsadowe, które uruchomić skrypty programu PowerShell.

Zmienne środowiskowe przekazywania informacji do uruchomienia zadania, a Magazyn lokalny może być używane toopass informacji poza zadanie uruchamiania. Na przykład, wartość zmiennej środowiskowej można określić hello ścieżki tooa program ma tooinstall i toolocal magazynu, który można następnie zostać odczytany później przez role można zapisywać pliki.

Zadania uruchamiania można rejestrować informacje i błędy toohello katalogu określonego przez hello **TEMP** zmiennej środowiskowej. W trakcie zadania uruchamiania hello hello **TEMP** zmiennej środowiskowej rozpoznaje toohello *C:\\zasobów\\temp\\[identyfikator guid]. [ rolename]\\RoleTemp* katalogu podczas uruchamiania w chmurze hello.

Uruchamianie zadania mogą być również wykonywane kilka razy między ponownego uruchomienia. Na przykład hello uruchamiania zadanie zostanie uruchomione zawsze, gdy rola hello jest odtwarzana i odtwarza roli nie może zawierać zawsze ponowne uruchomienie komputera. Uruchamianie zadania mają być zapisywane w sposób umożliwiający ich toorun bez problemów.

Zadania uruchamiania musi kończyć się **errorlevel** (lub kod zakończenia) o wartości zero dla hello uruchomienia procesu toocomplete. Jeśli zadanie uruchamiania kończy się na inną niż zero **errorlevel**, hello roli nie zostaną uruchomione.

## <a name="role-startup-order"></a>Kolejność uruchamiania roli
Hello poniżej przedstawiono procedury uruchamiania roli hello na platformie Azure:

1. wystąpienie Hello jest oznaczony jako **uruchamianie** i nie odbiera ruch.
2. Wszystkie zadania uruchamiania są wykonywane zgodnie z tootheir **taskType** atrybutu.
   
   * Witaj **proste** zadania są wykonywane synchronicznie, pojedynczo.
   * Witaj **tła** i **pierwszego planu** zadania są toohello wprowadzenie asynchronicznie, równoległe uruchomienia zadania.  
     
     > [!WARNING]
     > Usługi IIS może nie być pełni skonfigurowany na etapie hello uruchamiania zadań w procesie uruchamiania hello, dlatego dane specyficzne dla roli nie może być dostępne. Uruchamianie zadań, które wymagają dane specyficzne dla roli, należy użyć [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. Proces hosta roli Hello jest uruchomiona i hello witryny w usługach IIS.
4. Witaj [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) metoda jest wywoływana.
5. wystąpienie Hello jest oznaczony jako **gotowe** i ruch jest kierowany toohello wystąpienia.
6. Witaj [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda jest wywoływana.

## <a name="example-of-a-startup-task"></a>Przykład zadania uruchamiania
Uruchamianie zadania są definiowane w hello [ServiceDefinition.csdef] pliku w hello **zadań** elementu. Witaj **commandLine** atrybut określa nazwę hello oraz parametry partii uruchamiania hello plików lub konsoli polecenie hello **executionContext** atrybut określa poziom uprawnień hello hello uruchamiania zadania i hello **taskType** atrybut określa, jak hello zadania zostaną wykonane.

W tym przykładzie wartość zmiennej środowiskowej **MyVersionNumber**, jest tworzony dla hello uruchomienia zadania i ustaw wartość toohello "**1.0.0.0**".

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

W hello poniższy przykład, hello **Startup.cmd** plik wsadowy zapisuje wiersz powitania "hello bieżąca wersja to 1.0.0.0" toohello StartupLog.txt pliku w katalogu hello określonej przez zmienną środowiskową TEMP hello. Witaj `EXIT /B 0` wiersza zapewnia kończy zadanie uruchamiania tego hello **errorlevel** o wartości zero.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> W programie Visual Studio hello **skopiuj tooOutput katalogu** właściwości uruchamiania pliku wsadowego należy ustawić wartość zbyt**zawsze Kopiuj** toobe się, że plik wsadowy uruchamiania jest prawidłowo wdrożony tooyour projektu na platformie Azure (**approot\\bin** dla ról sieć Web i **approot** dla roli proces roboczy).
> 
> 

## <a name="description-of-task-attributes"></a>Opis zadania atrybutów
Witaj poniżej opisano atrybuty hello hello **zadań** element hello [ServiceDefinition.csdef] pliku:

**commandLine** — Określa wiersz polecenia hello hello uruchomienia zadania:

* Hello polecenie z parametry opcjonalne wiersza polecenia, który zaczyna się hello uruchamiania zadań.
* Jest to często filename hello pliku wsadowego cmd i bat.
* zadanie Hello jest względna toohello AppRoot\\folder Bin hello wdrożenia. Zmienne środowiskowe nie są rozwijane w określeniu ścieżki hello i hello zadania. Jeśli rozszerzania środowiska jest wymagana, można utworzyć skrypt .cmd małych wywołującą zadania uruchamiania.
* Może być aplikacji konsoli lub pliku wsadowego, który rozpoczyna się [skrypt programu PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** — określa poziom uprawnień hello hello uruchomienia zadania. poziom uprawnień Hello może być ograniczony lub z podwyższonym poziomem uprawnień:

* **ograniczone**  
  zadanie uruchamiania Hello jest uruchamiany z hello takie same uprawnienia w roli hello. Gdy hello **executionContext** atrybutu hello [środowiska uruchomieniowego] element jest również **ograniczone**, uprawnienia użytkownika będą używane.
* **z podwyższonym poziomem uprawnień**  
  zadanie uruchamiania Hello jest uruchamiany z uprawnieniami administratora. Dzięki temu zadania uruchamiania programów tooinstall, wprowadzić zmiany w konfiguracji usług IIS, wykonywanie zmiany w rejestrze i innych zadań poziomu administratora bez zwiększania hello poziom uprawnień roli hello, sama.  

> [!NOTE]
> Witaj poziom uprawnień zadania uruchamiania nie jest konieczne toobe hello sam rolę hello samej siebie.
> 
> 

**taskType** — określa sposób uruchamiania zadań hello jest wykonywana.

* **proste**  
  Zadania są wykonywane synchronicznie, pojedynczo, w kolejności hello określone w hello [ServiceDefinition.csdef] pliku. Gdy dla jednego **proste** kończy zadanie uruchamiania **errorlevel** zero, obok hello **proste** jest wykonywane zadanie uruchamiania. Jeśli nie ma już **proste** uruchamiania zadań tooexecute, następnie roli hello, sama zostanie uruchomiony.   
  
  > [!NOTE]
  > Jeśli hello **proste** zadań kończy się na inną niż zero **errorlevel**, wystąpienie hello zostanie zablokowana. Kolejne **proste** uruchamiania zadań i roli hello, nie zostaną uruchomione.
  > 
  > 
  
    tooensure, który plik wsadowy kończy się wyrazem **errorlevel** zero, wykonaj polecenie hello `EXIT /B 0` na końcu hello procesu pliku wsadowego.
* **tła**  
  Zadania są wykonywane asynchronicznie, równolegle z hello uruchamiania hello roli.
* **pierwszego planu**  
  Zadania są wykonywane asynchronicznie, równolegle z hello uruchamiania hello roli. Witaj Najważniejsza różnica między **pierwszego planu** i **tła** zadania oznacza, że **pierwszego planu** zadań uniemożliwia hello rolę z lub do czasu hello zadania zamykania zakończone. Witaj **tła** zadania nie ma to ograniczenie.

## <a name="environment-variables"></a>Zmienne środowiskowe
Zmienne środowiskowe to sposób toopass informacji tooa uruchomienia zadania. Na przykład możesz umieścić hello ścieżki tooa blob zawierający program tooinstall, lub numery portów, które będzie używać swojej roli lub funkcji toocontrol ustawienia zadania uruchamiania.

Istnieją dwa rodzaje zmiennych środowiskowych dla zadania uruchamiania; zmienne środowiskowe statyczne i zmiennych środowiskowych na podstawie elementów członkowskich z hello [ RoleEnvironment] klasy. Są w hello [środowiska] sekcji hello [ServiceDefinition.csdef] pliku, a oba hello użyj [zmiennej] elementu i **nazwa** atrybut.

Witaj używa zmiennych statycznych środowiska **wartość** atrybutu hello [zmiennej] elementu. w powyższym przykładzie Hello tworzy zmienną środowiskową hello **MyVersionNumber** , który ma wartość statyczny "**1.0.0.0**". Innym przykładem może być toocreate **StagingOrProduction** zmiennej środowiskowej, którą można ręcznie ustawić toovalues z "**przemieszczania**"lub"**produkcji**" tooperform uruchamianie różnych działań na podstawie hello wartości hello **StagingOrProduction** zmiennej środowiskowej.

Zmienne środowiskowe oparte na elementach członkowskich klasy RoleEnvironment hello nie używaj hello **wartość** atrybutu hello [zmiennej] elementu. Zamiast tego hello [RoleInstanceValue] elementu podrzędnego z odpowiednią hello **XPath** wartość atrybutu, są używane toocreate zmienną środowiskową oparte na elemencie członkowskim hello [ RoleEnvironment] klasy. Wartości hello **XPath** różnych atrybutów tooaccess [ RoleEnvironment] wartości można znaleźć [tutaj](cloud-services-role-config-xpath.md).

Na przykład toocreate zmienną środowiskową, który jest "**true**" gdy wystąpienie hello działa w emulatorze obliczeń hello, i "**false**" podczas uruchamiania w chmurze hello, użyj następujących hello [zmiennej] i [RoleInstanceValue] elementy:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak tooperform niektórych [typowe zadania uruchamiania](cloud-services-startup-tasks-common.md) z usługi w chmurze.

[Pakiet](cloud-services-model-and-package.md) usługi w chmurze.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[zadań]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[uruchamiania]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[środowiska uruchomieniowego]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[środowiska]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[zmiennej]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
