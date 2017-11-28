---
title: aaaOptimizing kodu platformy Azure w programie Visual Studio | Dokumentacja firmy Microsoft
description: "Informacje dotyczące sposobu Azure kodu optymalizacji narzędzia w programie Visual Studio sprawić, że kod bardziej niezawodny i lepszego wykonywania."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="8c0c8-103">Optymalizacja kodu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8c0c8-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="8c0c8-104">W przypadku programowania aplikacji, które używają programu Microsoft Azure, istnieją pewne praktyk kodowania, należy wykonać toohelp uniknąć problemów z aplikacji, skalowalność, zachowania i wydajności w środowisku chmury.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="8c0c8-105">Firma Microsoft udostępnia narzędzia do analizy kodu platformy Azure, która rozpoznaje i identyfikuje niektóre z tych często napotkał problemy i ułatwia ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="8c0c8-106">Możesz pobrać narzędzie hello w programie Visual Studio za pośrednictwem pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="8c0c8-107">Azure reguł analizy kodu</span><span class="sxs-lookup"><span data-stu-id="8c0c8-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="8c0c8-108">Narzędzie do analizy kodu Azure Hello używa hello reguły tooautomatically Flaga Azure kodu, gdy znajdzie znanych problemów wpływających na wydajność.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="8c0c8-109">Wykryto problemy występują jako ostrzeżenia lub błędy kompilatora.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="8c0c8-110">Kod poprawki lub sugestie tooresolve hello ostrzeżenia lub błędu często są realizowane za pośrednictwem ikoną żarówki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="8c0c8-111">Unikaj używania domyślny tryb stanu sesji (w trakcie)</span><span class="sxs-lookup"><span data-stu-id="8c0c8-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-112">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-112">ID</span></span>
<span data-ttu-id="8c0c8-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-114">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-114">Description</span></span>
<span data-ttu-id="8c0c8-115">Jeśli używasz tryb stanu sesji (w trakcie) domyślnego powitania dla aplikacji w chmurze, zostaną utracone stanu sesji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="8c0c8-116">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-117">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-117">Reason</span></span>
<span data-ttu-id="8c0c8-118">Domyślnie tryb stanu sesji hello określone w pliku web.config hello jest w trakcie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="8c0c8-119">Ponadto jeśli żadnego wpisu określony w pliku konfiguracji hello, tryb stanu sesji hello domyślnie tooin procesu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="8c0c8-120">Witaj w trakcie tryb zapisuje stan sesji w pamięci na powitania serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="8c0c8-121">Po uruchomieniu wystąpienia lub nowe wystąpienie jest używana do równoważenia obciążenia lub obsługi trybu failover, stan sesji hello przechowywane w pamięci na serwerze sieci web hello nie są zapisywane.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="8c0c8-122">Taka sytuacja uniemożliwia aplikacji hello jest skalowalna na powitania chmury.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="8c0c8-123">Stan sesji ASP.NET obsługuje kilka opcji innego magazynu dla danych stanu sesji: InProc, StateServer, SQLServer, niestandardowe i Off.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="8c0c8-124">Zaleca się używanie niestandardowy tryb toohost danych w zewnętrznym sklepie stanu sesji, takie jak [dostawcę stanu sesji Azure Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-125">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-125">Solution</span></span>
<span data-ttu-id="8c0c8-126">Jedno rozwiązanie zalecane jest toostore stanu sesji na usługi zarządzana pamięć podręczna.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="8c0c8-127">Dowiedz się, jak toouse [dostawcę stanu sesji Azure Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore Twojego stanu sesji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="8c0c8-128">Użytkownik może również magazynu sesji stanu w innych miejscach tooensure się, że aplikacja jest skalowalna na powitania chmury.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="8c0c8-129">więcej informacji na temat rozwiązań alternatywnych, przeczytaj toolearn [trybów stanu sesji](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="8c0c8-130">Uruchom metody nie powinna być asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="8c0c8-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-131">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-131">ID</span></span>
<span data-ttu-id="8c0c8-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-133">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-133">Description</span></span>
<span data-ttu-id="8c0c8-134">Tworzenie metod asynchronicznych (takich jak [await](https://msdn.microsoft.com/library/hh156528.aspx)) poza hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody, a następnie wywołań metod asynchronicznych hello z [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="8c0c8-135">Deklarowanie hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda async powoduje, że proces roboczy hello tooenter roli pętli ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="8c0c8-136">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-137">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-137">Reason</span></span>
<span data-ttu-id="8c0c8-138">Wywołanie metod asynchronicznych wewnątrz hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metoda powoduje roli procesu roboczego hello toorecycle środowiska uruchomieniowego hello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="8c0c8-139">Podczas uruchamiania roli proces roboczy, wszystkie wykonywania programu ma miejsce w obrębie hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="8c0c8-140">Witaj istniejącym [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) — metoda powoduje, że proces roboczy hello toorestart roli.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="8c0c8-141">Gdy środowiska uruchomieniowego roli procesu roboczego hello trafi hello metoda asynchroniczna, wywołuje wszystkie operacje po metodzie asynchronicznej hello, a następnie zwraca.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="8c0c8-142">Powoduje to, że proces roboczy hello tooexit roli z hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) — metoda i uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="8c0c8-143">W następnej iteracji hello wykonywania roli procesu roboczego hello trafień ponownie metody asynchronicznej hello i ponowne uruchomienia, powoduje także ponownie toorecycle roli procesu roboczego hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-144">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-144">Solution</span></span>
<span data-ttu-id="8c0c8-145">Umieść wszystkie operacje asynchroniczne poza hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="8c0c8-146">Wywoływać metody asynchronicznej hello refaktoryzowane z wewnątrz hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metody, takiej jak RunAsync .wait ().</span><span class="sxs-lookup"><span data-stu-id="8c0c8-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="8c0c8-147">Narzędzie do analizy kodu Azure Hello może pomóc rozwiązać ten problem.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="8c0c8-148">powitania po fragment kodu przedstawia hello kodu poprawkę dotyczącą tego problemu:</span><span class="sxs-lookup"><span data-stu-id="8c0c8-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="8c0c8-149">Sygnatura dostępu współdzielonego magistrali usługi uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="8c0c8-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-150">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-150">ID</span></span>
<span data-ttu-id="8c0c8-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-152">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-152">Description</span></span>
<span data-ttu-id="8c0c8-153">Dostęp do sygnatury dostępu Współdzielonego jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="8c0c8-154">Usługi kontroli dostępu (ACS) jest przestarzałe uwierzytelniania magistrali usługi.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="8c0c8-155">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-156">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-156">Reason</span></span>
<span data-ttu-id="8c0c8-157">Aby zwiększyć bezpieczeństwo Azure Active Directory zastępuje ACS uwierzytelniania przy użyciu uwierzytelniania sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="8c0c8-158">Zobacz [usługi Azure Active Directory jest hello przyszłych usług ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) informacji na powitania planu migracji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-159">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-159">Solution</span></span>
<span data-ttu-id="8c0c8-160">Korzystanie z uwierzytelniania sygnatury dostępu Współdzielonego w aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="8c0c8-161">Witaj poniższy przykład pokazuje, jak toouse istniejących tooaccess tokenu sygnatury dostępu Współdzielonego usługi magistrali przestrzeni nazw lub jednostki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="8c0c8-162">Zobacz hello następujące tematy, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="8c0c8-163">Aby uzyskać ogólne informacje, zobacz [uwierzytelniania podpisu dostępu udostępnionych za pomocą usługi Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="8c0c8-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="8c0c8-164">Jak toouse uwierzytelniania podpisu dostępu do udostępnionych z usługą Service Bus</span><span class="sxs-lookup"><span data-stu-id="8c0c8-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="8c0c8-165">Aby uzyskać przykładowy projekt, zobacz [uwierzytelniania przy użyciu dostępu sygnatury dostępu Współdzielonego z subskrypcji magistrali usług](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="8c0c8-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="8c0c8-166">Należy rozważyć użycie tooavoid metody OnMessage "pętlę odbierania"</span><span class="sxs-lookup"><span data-stu-id="8c0c8-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-167">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-167">ID</span></span>
<span data-ttu-id="8c0c8-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="8c0c8-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-169">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-169">Description</span></span>
<span data-ttu-id="8c0c8-170">tooavoid, przechodząc do "otrzymywać pętli" hello wywoływania **OnMessage** metoda jest lepszym rozwiązaniem do odbierania wiadomości niż hello wywoływania **Receive** — metoda.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="8c0c8-171">Jednak jeśli musisz użyć hello **Receive** metoda i określ serwer z systemem innym niż domyślny czas oczekiwania, upewnij się, czas oczekiwania serwera hello jest więcej niż jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="8c0c8-172">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-173">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-173">Reason</span></span>
<span data-ttu-id="8c0c8-174">Podczas wywoływania metody **OnMessage**, powitania klienta uruchamia pompę wewnętrzny komunikat, który sonduje stale kolejki hello lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="8c0c8-175">To przekazywanie komunikatów zawiera nieskończoną pętlę, która wystawia wywołanie tooreceive wiadomości.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="8c0c8-176">Jeśli upłynie limit czasu wywołania hello, wystawia nowe połączenie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="8c0c8-177">Witaj — interwał limitu czasu jest określany przez wartość hello hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) właściwości hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)który jest używany.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="8c0c8-178">Witaj zaletą używania **OnMessage** porównaniu zbyt**Receive** jest, że użytkownicy nie mają toomanually sondować komunikatów, obsługa wyjątków przetwarzać wiele komunikatów równolegle i ukończyć powitalnych komunikaty.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="8c0c8-179">Jeśli należy wywołać **Receive** bez użycia wartość domyślną, należy się hello *ServerWaitTime* wartość jest więcej niż jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="8c0c8-180">Ustawienie *ServerWaitTime* toomore niż minuta uniemożliwia limit czasu, zanim pełni odbioru wiadomości powitania powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-181">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-181">Solution</span></span>
<span data-ttu-id="8c0c8-182">Zobacz hello następujące przykłady kodu dla zalecane użycia.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="8c0c8-183">Aby uzyskać więcej informacji, zobacz [QueueClient.OnMessage — metoda (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)i [QueueClient.Receive — metoda (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="8c0c8-184">wydajność hello tooimprove hello Azure infrastruktury obsługi wiadomości, zobacz wzorca projektowego hello [asynchroniczne Elementarz wiadomości](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="8c0c8-185">Witaj poniżej przedstawiono przykład użycia **OnMessage** tooreceive wiadomości.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="8c0c8-186">Witaj poniżej przedstawiono przykład użycia **Receive** czas oczekiwania, hello domyślnego serwera.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="8c0c8-187">Witaj poniżej przedstawiono przykład użycia **Receive** z serwerem z systemem innym niż domyślny czas oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="8c0c8-188">Należy rozważyć użycie metod asynchronicznych usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="8c0c8-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-189">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-189">ID</span></span>
<span data-ttu-id="8c0c8-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="8c0c8-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-191">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-191">Description</span></span>
<span data-ttu-id="8c0c8-192">Za pomocą asynchroniczne wydajności tooimprove metod usługi Service Bus obsługiwanych przez brokera obsługi komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="8c0c8-193">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-194">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-194">Reason</span></span>
<span data-ttu-id="8c0c8-195">Używanie metod asynchronicznych umożliwia współbieżności program aplikacji, ponieważ wykonywania każdego wywołania nie blokuje hello głównego wątku.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="8c0c8-196">Korzystając z usługi Service Bus metod do obsługi komunikatów, wykonywania operacji (wysyłanie, odbierania, usuwanie, itp.) jest czasochłonne.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="8c0c8-197">Teraz obejmuje hello przetwarzania operacji hello przez hello usługi Service Bus opóźnienia toohello dodanie hello żądania i odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="8c0c8-198">tooincrease hello liczbę operacji na czas, operacji musi być wykonywany współbieżnie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="8c0c8-199">Aby uzyskać więcej informacji można znaleźć zbyt[najlepsze rozwiązania dotyczące wydajności ulepszenia przy użyciu usługi magistrali obsługiwanych przez brokera obsługi komunikatów](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-200">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-200">Solution</span></span>
<span data-ttu-id="8c0c8-201">Zobacz [QueueClient klasy (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) uzyskać informacji na temat sposobu toouse hello zalecane metody asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="8c0c8-202">wydajność hello tooimprove hello Azure infrastruktury obsługi wiadomości, zobacz wzorca projektowego hello [asynchroniczne Elementarz wiadomości](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="8c0c8-203">Należy wziąć pod uwagę partycjonowania tematów i kolejek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="8c0c8-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-204">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-204">ID</span></span>
<span data-ttu-id="8c0c8-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="8c0c8-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-206">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-206">Description</span></span>
<span data-ttu-id="8c0c8-207">Partycji usługi Service Bus kolejek i tematów w celu poprawy wydajności z komunikatów usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="8c0c8-208">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-209">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-209">Reason</span></span>
<span data-ttu-id="8c0c8-210">Partycjonowanie tematów i kolejek usługi Service Bus zwiększa dostępność przepływności i usługi wydajności, ponieważ hello ogólną przepustowość partycjonowanej kolejka lub temat nie jest już ograniczone przez wydajności hello brokera komunikatów pojedynczego lub magazynie obsługi komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="8c0c8-211">Ponadto tymczasowego awaria magazynie obsługi komunikatów nie należy partycjonowanej kolejka lub temat niedostępny.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="8c0c8-212">Aby uzyskać więcej informacji, zobacz [partycjonowania jednostek obsługi komunikatów](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-213">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-213">Solution</span></span>
<span data-ttu-id="8c0c8-214">Witaj następującego kodu fragment kodu przedstawia sposób toopartition jednostki do obsługi komunikatów.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="8c0c8-215">Aby uzyskać więcej informacji, zobacz [podzielona na partycje kolejek usługi Service Bus i tematy | Blog usługi Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) i wyewidencjonowania hello [Microsoft Azure na partycje kolejką usługi Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) próbki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="8c0c8-216">Nie ustawiaj SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="8c0c8-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-217">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-217">ID</span></span>
<span data-ttu-id="8c0c8-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="8c0c8-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-219">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-219">Description</span></span>
<span data-ttu-id="8c0c8-220">Należy unikać używania SharedAccessStartTimeset toohello bieżącym uruchomieniu tooimmediately hello zasad dostępu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="8c0c8-221">Wystarczy tooset tej właściwości Jeśli zasady dostępu udostępnionego hello toostart w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="8c0c8-222">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-223">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-223">Reason</span></span>
<span data-ttu-id="8c0c8-224">Synchronizacja zegara powoduje, że czas niewielkie różnice centrów danych.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="8c0c8-225">Na przykład można logicznie się spodziewać czas rozpoczęcia hello ustawienia magazynu zasad sygnatury dostępu Współdzielonego jako hello bieżący czas za pomocą DateTime.Now lub podobnej metody spowoduje, że hello SAS zasad tootake obowiązywać natychmiast.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="8c0c8-226">Jednak hello czasu niewielkie różnice między centrami danych może spowodować problemy z tym, ponieważ sytuacje centrum danych mogą być nieco później niż czas rozpoczęcia hello, podczas gdy inne wcześniejsze go.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="8c0c8-227">W związku z tym hello SAS zasad można wygaśnie szybko (lub nawet natychmiast) Jeśli okres istnienia zasad hello jest zbyt krótki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="8c0c8-228">Aby uzyskać więcej pomocy na temat używania sygnatura dostępu współdzielonego w magazynie Azure, zobacz [wprowadzenie tabeli SAS (Shared Access Signature), SAS kolejki i tooBlob aktualizacji SAS - Microsoft Azure Blog zespołu usługi Magazyn — strona główna — lokacji blogi MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-229">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-229">Solution</span></span>
<span data-ttu-id="8c0c8-230">Usuń hello instrukcja, która ustawia czas rozpoczęcia hello hello udostępnionych zasad dostępu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="8c0c8-231">Narzędzie do analizy kodu Azure Hello przedstawiono rozwiązanie tego problemu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="8c0c8-232">Aby uzyskać więcej informacji dotyczących zarządzania zabezpieczeniami, zobacz wzorca projektowego hello [wzorzec klucza Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="8c0c8-233">Witaj następującego fragmentu kodu pokazuje hello kodu poprawkę dotyczącą tego problemu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="8c0c8-234">Udostępnione czas wygaśnięcia musi być przeprowadzona ponad pięć minut zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="8c0c8-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-235">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-235">ID</span></span>
<span data-ttu-id="8c0c8-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="8c0c8-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-237">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-237">Description</span></span>
<span data-ttu-id="8c0c8-238">Może istnieć jak pięciu minut różnica w zegary między centrami danych w różnych lokalizacjach powodu warunku tooa znana jako "przesunięcia czasowego zegara."</span><span class="sxs-lookup"><span data-stu-id="8c0c8-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="8c0c8-239">tooprevent hello SAS zasady wygaśnięcia wcześniej niż ustawić token toobe czas wygaśnięcia hello więcej niż pięć minut.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="8c0c8-240">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-241">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-241">Reason</span></span>
<span data-ttu-id="8c0c8-242">Synchronizuj centrów danych w różnych miejscach na całym świecie hello sygnał zegara.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="8c0c8-243">Ponieważ czas dla lokalizacji toodifferent tootravel sygnał zegara, może istnieć wariancji czas między centrami danych w różnych lokalizacjach geograficznych mimo wszystko, co prawdopodobnie jest zsynchronizowany.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="8c0c8-244">Ta różnica czasu może mieć wpływ na powitania dostęp współdzielony początkowy czas i wygaśnięcia interwał zasad.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="8c0c8-245">W związku z tym tooensure zasad udostępnionych dostępu ma efekt natychmiastowy, nie podaje godziny rozpoczęcia hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="8c0c8-246">Ponadto upewnij się, że czas wygaśnięcia hello jest większa niż 5 minut tooprevent wczesne przekroczenia limitu czasu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="8c0c8-247">Aby uzyskać więcej informacji o korzystaniu z sygnaturą dostępu współdzielonego w magazynie Azure, zobacz [wprowadzenie tabeli SAS (Shared Access Signature), SAS kolejki i tooBlob aktualizacji SAS - Microsoft Azure Blog zespołu usługi Magazyn — strona główna — lokacji blogi MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-248">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-248">Solution</span></span>
<span data-ttu-id="8c0c8-249">Aby uzyskać więcej informacji dotyczących zarządzania zabezpieczeniami, zobacz wzorca projektowego hello [wzorzec klucza Valet](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="8c0c8-250">Hello poniżej znajduje się przykład nieokreślenie godzinę rozpoczęcia zasad dostępu udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="8c0c8-251">Witaj poniżej znajduje się przykład określenia godziny rozpoczęcia zasad dostęp współdzielony z okresem ważności zasady więcej niż pięć minut.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="8c0c8-252">Aby uzyskać więcej informacji, zobacz [tworzenia i używania sygnaturę dostępu współdzielonego](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="8c0c8-253">Użyj CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="8c0c8-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-254">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-254">ID</span></span>
<span data-ttu-id="8c0c8-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-256">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-256">Description</span></span>
<span data-ttu-id="8c0c8-257">Przy użyciu hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) klasy dla projektów, takie jak witryny sieci Web Azure i usług Azure mobile services nie będzie powodować problemy środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="8c0c8-258">Najlepszym rozwiązaniem jest jednak dobrze toouse chmury[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) jako jednolity sposób zarządzania konfiguracjami dla wszystkich aplikacji w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="8c0c8-259">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-260">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-260">Reason</span></span>
<span data-ttu-id="8c0c8-261">CloudConfigurationManager odczytuje hello konfiguracji pliku właściwe toohello aplikacji środowiska.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="8c0c8-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="8c0c8-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="8c0c8-263">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-263">Solution</span></span>
<span data-ttu-id="8c0c8-264">Refaktoryzuj hello toouse Twojego kodu [klasa CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="8c0c8-265">Kod poprawkę dotyczącą tego problemu są udostępniane przez narzędzie do analizy kodu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="8c0c8-266">Witaj następującego fragmentu kodu pokazuje hello kodu poprawkę dotyczącą tego problemu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="8c0c8-267">Replace</span><span class="sxs-lookup"><span data-stu-id="8c0c8-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="8c0c8-268">Z</span><span class="sxs-lookup"><span data-stu-id="8c0c8-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="8c0c8-269">Poniżej przedstawiono przykład sposobu toostore hello ustawienie konfiguracji w pliku App.config lub Web.config.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="8c0c8-270">Dodaj hello ustawienia toohello sekcji appSettings pliku konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="8c0c8-271">Oto Hello hello pliku Web.config dla hello poprzednim przykładzie kodu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="8c0c8-272">Unikaj używania ciągów połączenia stałe</span><span class="sxs-lookup"><span data-stu-id="8c0c8-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-273">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-273">ID</span></span>
<span data-ttu-id="8c0c8-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="8c0c8-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-275">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-275">Description</span></span>
<span data-ttu-id="8c0c8-276">Jeśli używasz parametry połączenia ustalony i trzeba tooupdate je później, należy mieć kod źródłowy tooyour zmiany toomake i ponowne skompilowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="8c0c8-277">Jednak jeśli parametry połączenia są przechowywane w pliku konfiguracji, można zmienić je później, po prostu aktualizując hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="8c0c8-278">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-279">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-279">Reason</span></span>
<span data-ttu-id="8c0c8-280">Koduj parametrów połączenia jest zła rozwiązaniem, ponieważ wprowadza ona problemów, jeśli parametry połączenia muszą toobe szybko zmienić.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="8c0c8-281">Ponadto jeśli hello projektu musi toobe zaznaczone w formancie toosource, parametry połączenia ustalony wprowadzić luk w zabezpieczeniach, ponieważ ciągi hello można wyświetlić w kodzie źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-282">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-282">Solution</span></span>
<span data-ttu-id="8c0c8-283">Przechowywanie parametrów połączenia w plikach konfiguracji hello lub środowisk Azure.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="8c0c8-284">Dla aplikacji autonomicznej należy użyć ustawień parametrów połączenia toostore app.config.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="8c0c8-285">Dla aplikacji hostowanych przez usługi IIS sieci web Użyj parametrów połączenia toostore pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="8c0c8-286">Dla aplikacji vNext ASP.NET Użyj parametrów połączenia toostore configuration.json.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="8c0c8-287">Informacje na temat używania plików konfiguracji, takich jak plik web.config lub app.config, zobacz [wskazówki dotyczące konfigurowania sieci Web ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="8c0c8-288">Uzyskać informacji na temat sposobu Azure pracy zmiennych środowiska, zobacz [Azure Web Sites: jak ciągi aplikacji i działać ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="8c0c8-289">Aby uzyskać informacje na przechowywanie parametrów połączenia w kontroli źródła, zobacz [należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytorium kodu źródłowego](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="8c0c8-290">Użyj pliku konfiguracji diagnostyki</span><span class="sxs-lookup"><span data-stu-id="8c0c8-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-291">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-291">ID</span></span>
<span data-ttu-id="8c0c8-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-293">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-293">Description</span></span>
<span data-ttu-id="8c0c8-294">Zamiast konfigurować ustawienia diagnostyki w kodzie, takich jak przy użyciu hello Microsoft.WindowsAzure.Diagnostics programowania interfejsu API, należy skonfigurować ustawienia diagnostyki w pliku diagnostics.wadcfg hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="8c0c8-295">(Lub diagnostics.wadcfgx, jeśli używasz 2.5 zestawu SDK platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="8c0c8-296">W ten sposób można zmienić ustawień diagnostycznych bez konieczności toorecompile kodu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="8c0c8-297">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-298">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-298">Reason</span></span>
<span data-ttu-id="8c0c8-299">Przed 2.5 zestawu SDK platformy Azure, (używający Diagnostyka Azure 1.3), Azure Diagnostics (WAD) może zostać skonfigurowany przy użyciu kilka różnych metod: dodanie go toohello konfiguracji blob w magazynie, za pomocą kodu konieczne, deklaratywne konfiguracji lub hello domyślne Konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="8c0c8-300">Jednak hello preferowane toouse plik konfiguracyjny XML (diagnostics.wadcfg lub diagnositcs.wadcfgx dla zestawu SDK, 2.5 i nowszych) w projekcie aplikacji hello jest sposób tooconfigure diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="8c0c8-301">W takie podejście plik diagnostics.wadcfg hello całkowicie definiuje konfigurację hello i aktualizowanie i wdrożone w momencie.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="8c0c8-302">Mieszanie hello użycie pliku konfiguracji diagnostics.wadcfg hello z hello metod programistycznych ustawienia konfiguracji za pomocą hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)lub [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) klas może prowadzić tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="8c0c8-303">Zobacz [zainicjować lub zmienianie konfiguracji diagnostyki Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="8c0c8-304">Począwszy od 1.3 WAD (dołączony do 2.5 zestawu SDK platformy Azure), nie jest już możliwe toouse kodu tooconfigure diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="8c0c8-305">W związku z tym można podać tylko konfiguracji hello podczas stosowania lub aktualizowania hello diagnostyki rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-306">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-306">Solution</span></span>
<span data-ttu-id="8c0c8-307">Użyj hello diagnostyki toomove projektanta ustawień diagnostycznych toohello diagnostyki konfiguracji pliku konfiguracji (diagnositcs.wadcfg lub diagnositcs.wadcfgx dla zestawu SDK, 2.5 i nowszych).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="8c0c8-308">Zaleca się zainstalowanie [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) i korzystać z najnowszych funkcji diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="8c0c8-309">W menu skrótów hello hello roli, które mają tooconfigure wybierz polecenie Właściwości, a następnie wybierz kartę Konfiguracja hello.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="8c0c8-310">W hello **diagnostyki** sekcji, upewnij się, że hello **włączyć diagnostyki** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="8c0c8-311">Wybierz hello **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-311">Choose hello **Configure** button.</span></span>

   ![Dostęp do opcji Włącz diagnostyki hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="8c0c8-313">Zobacz [Konfigurowanie diagnostyki dla usług Azure Cloud Services i maszyn wirtualnych](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="8c0c8-314">Unikaj deklarowanie obiektów DbContext jako statyczne</span><span class="sxs-lookup"><span data-stu-id="8c0c8-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="8c0c8-315">ID</span><span class="sxs-lookup"><span data-stu-id="8c0c8-315">ID</span></span>
<span data-ttu-id="8c0c8-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="8c0c8-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="8c0c8-317">Opis</span><span class="sxs-lookup"><span data-stu-id="8c0c8-317">Description</span></span>
<span data-ttu-id="8c0c8-318">pamięć toosave uniknąć deklarowanie obiektów DBContext jako statyczny.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="8c0c8-319">Udostępnij te koncepcje i opinie na [opinii analizy kodu Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="8c0c8-320">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="8c0c8-320">Reason</span></span>
<span data-ttu-id="8c0c8-321">Obiekty DBContext przechowują hello wyników zapytania z każdym wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="8c0c8-322">Obiekty DBContext statyczne nie są usuwane, dopóki nie zostanie zwolniony hello domeny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="8c0c8-323">W związku z tym statycznego obiektu DBContext może używać dużych ilości pamięci.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="8c0c8-324">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="8c0c8-324">Solution</span></span>
<span data-ttu-id="8c0c8-325">Zadeklarować zmiennej lokalnej lub pole wystąpienia niestatycznego DBContext, użyj go zadania, a następnie pozwól mu usuwane po użyciu.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="8c0c8-326">Hello następujące klasy kontrolera MVC przykładzie pokazano, jak toouse hello obiektu DBContext.</span><span class="sxs-lookup"><span data-stu-id="8c0c8-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="8c0c8-327">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8c0c8-327">Next steps</span></span>
<span data-ttu-id="8c0c8-328">toolearn więcej informacji na temat optymalizacji i rozwiązywanie problemów z aplikacjami platformy Azure, zobacz [Rozwiązywanie problemów aplikacji sieci web w usłudze Azure App Service przy użyciu programu Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8c0c8-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
