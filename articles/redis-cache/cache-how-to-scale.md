---
title: "tooScale aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooscale Azure Redis wystąpień pamięci podręcznej"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Jak tooScale Azure pamięci podręcznej Redis
Pamięć podręczna Redis Azure ma ofert różnych pamięci podręcznej, które zapewniają elastyczność w wyborze hello rozmiar pamięci podręcznej i funkcji. Po utworzeniu pamięci podręcznej można skalować hello rozmiaru i hello cenowym pamięci podręcznej hello zmiany hello wymagań aplikacji. W tym artykule opisano, jak tooscale pamięć podręczną w hello portalu Azure i za pomocą narzędzi takich jak Azure PowerShell i interfejsu wiersza polecenia Azure.

## <a name="when-tooscale"></a>Gdy tooscale
Można użyć hello [monitorowania](cache-how-to-monitor.md) funkcji toomonitor pamięć podręczna Redis Azure hello kondycję i wydajność pamięci podręcznej i ułatwić określenie, kiedy tooscale hello pamięci podręcznej. 

Można monitorować następujące hello toohelp metryki stwierdzić, czy wymagane tooscale.

* Obciążenie serwera redis
* Użycie pamięci
* Przepustowość sieci
* Użycie procesora CPU

Jeśli okaże się, czy pamięć podręczna jest już spełniający wymagania aplikacji, można skalować tooa większy lub mniejszy pamięci podręcznej cenowym, które jest odpowiednie dla aplikacji. Aby uzyskać więcej informacji na temat określania, które pamięci podręcznej toouse warstwy cenowej, zobacz [jakie oferty pamięć podręczna Redis i rozmiar użyć](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Skala pamięci podręcznej
tooscale pamięć podręczną [Przeglądaj pamięci podręcznej toohello](cache-configure.md#configure-redis-cache-settings) w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk **skali** z hello **zasobów menu**.

![Skalowanie](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Wybierz hello żądaną warstwę cenową z hello **wybierz warstwę cenową** bloku i kliknij przycisk **wybierz**.

![Warstwa cenowa][redis-cache-pricing-tier-blade]


Możesz skalować tooa inną warstwa cenowa z hello następujące ograniczenia:

* Nie można skalować z wyższej cenową warstwy tooa dolnej warstwy cenowej.
  * Nie można skalować z **Premium** pamięci podręcznej w dół tooa **standardowe** lub **podstawowe** pamięci podręcznej.
  * Nie można skalować z **standardowe** pamięci podręcznej w dół tooa **podstawowe** pamięci podręcznej.
* Możesz skalować z **podstawowe** pamięci podręcznej tooa **standardowe** pamięci podręcznej, ale nie można zmienić rozmiaru hello na powitania tym samym czasie. Jeśli potrzebujesz zmienić rozmiar należy kolejnych skalowania rozmiar toohello żądaną operację.
* Nie można skalować z **podstawowe** pamięci podręcznej bezpośrednio tooa **Premium** pamięci podręcznej. Należy skalować z **podstawowe** za**standardowe** w jednej operacji skalowania, a następnie z **standardowe** za**Premium** kolejnych skalowania Operacja.
* Nie można skalować z większego rozmiaru dół toohello **C0 (250 MB)** rozmiar.
 
Gdy hello pamięci podręcznej jest skalowanie toohello nowych cen warstwy, **skalowanie** stan jest wyświetlany w hello **pamięci podręcznej Redis** bloku.

![Skalowanie][redis-cache-scaling]

Po zakończeniu skalowanie zmiany stanu hello z **skalowanie** za**systemem**.

## <a name="how-tooautomate-a-scaling-operation"></a>Jak tooautomate operacji skalowania
W dodatku tooscaling Twojego wystąpienia pamięci podręcznej w hello portalu Azure, można skalować, za pomocą poleceń cmdlet programu PowerShell, interfejsu wiersza polecenia Azure i przy użyciu hello Microsoft Azure Management bibliotek (MAML). 

* [Skala przy użyciu programu PowerShell](#scale-using-powershell)
* [Skala przy użyciu wiersza polecenia platformy Azure](#scale-using-azure-cli)
* [Przy użyciu MAML skali](#scale-using-maml)

### <a name="scale-using-powershell"></a>Skala przy użyciu programu PowerShell
Można też skalować swoich wystąpień pamięci podręcznej Redis Azure przy użyciu programu PowerShell przy użyciu hello [AzureRmRedisCache zestaw](https://msdn.microsoft.com/library/azure/mt634518.aspx) polecenia cmdlet, gdy hello `Size`, `Sku`, lub `ShardCount` są modyfikowane właściwości. Witaj poniższy przykład przedstawia sposób tooscale pamięci podręcznej o nazwie `myCache` tooa 2,5 GB w pamięci podręcznej. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Aby uzyskać więcej informacji na temat skalowania przy użyciu programu PowerShell, zobacz [tooscale Redis pamięci podręcznej przy użyciu programu Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Skala przy użyciu wiersza polecenia platformy Azure
wywołania z wystąpień pamięć podręczna Redis Azure za pomocą interfejsu wiersza polecenia Azure, tooscale hello `azure rediscache set` polecenia i przekaż hello potrzeby zmian konfiguracji, które obejmują nowy rozmiar, jednostki sku lub rozmiar klastra, w zależności od hello żądaną operację skalowania.

Aby uzyskać więcej informacji na temat skalowania z wiersza polecenia platformy Azure, zobacz [zmienić ustawienia istniejących pamięci podręcznej Redis](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Przy użyciu MAML skali
tooscale Twojego wystąpień pamięci podręcznej Redis Azure za pomocą hello [Microsoft Azure Management bibliotek (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), hello wywołania `IRedisOperations.CreateOrUpdate` — metoda i Przekaż nowy rozmiar hello hello `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Aby uzyskać więcej informacji, zobacz hello [zarządzania pamięcią podręczną Redis przy użyciu MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) próbki.

## <a name="scaling-faq"></a>Skalowanie — często zadawane pytania
Witaj Poniższa lista zawiera toocommonly odpowiedzi zadawane pytania dotyczące skalowania pamięć podręczna Redis Azure.

* [Aby z lub w pamięci podręcznej Premium I skalowania?](#can-i-scale-to-from-or-within-a-premium-cache)
* [Po skalowania, należy toochange klucze nazwy lub dostępu do pamięci podręcznej?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Jak działa skalowania?](#how-does-scaling-work)
* [Spowoduje utratę danych z mojej pamięci podręcznej podczas skalowania?](#will-i-lose-data-from-my-cache-during-scaling)
* [Jest niestandardowe baz danych zmodyfikowane ustawienie podczas skalowania?](#is-my-custom-databases-setting-affected-during-scaling)
* [Moje pamięci podręcznej będzie dostępna podczas skalowania?](#will-my-cache-be-available-during-scaling)
* [Operacje, które nie są obsługiwane](#operations-that-are-not-supported)
* [Jak długo skalowanie podąża?](#how-long-does-scaling-take)
* [Jak sprawdzić, kiedy jest ukończone skalowania?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>Aby z lub w pamięci podręcznej Premium I skalowania?
* Nie można skalować z **Premium** pamięci podręcznej w dół tooa **podstawowe** lub **standardowe** warstwy cenowej.
* Możesz skalować z jednego **Premium** tooanother warstwy cenowej w pamięci podręcznej.
* Nie można skalować z **podstawowe** pamięci podręcznej bezpośrednio tooa **Premium** pamięci podręcznej. Użytkownik musi najpierw skali: od **podstawowe** za**standardowe** w jednej operacji skalowania, a następnie z **standardowe** za**Premium** w kolejnej Operacja skalowania.
* Jeśli włączono klaster podczas tworzenia Twojej **Premium** pamięci podręcznej, możesz [zmienić rozmiar klastra hello](cache-how-to-premium-clustering.md#cluster-size). Jeśli pamięć podręczna została utworzona bez klastra włączone, nie można skonfigurować klaster w późniejszym czasie.
  
  Aby uzyskać więcej informacji, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>Po skalowania, należy toochange klucze nazwy lub dostępu do pamięci podręcznej?
Nie, nazwa pamięci podręcznej, a klucze nie uległy zmianie podczas operacji skalowania.

### <a name="how-does-scaling-work"></a>Jak działa skalowania?
* Gdy **podstawowe** pamięci podręcznej jest skalowana tooa inny rozmiar zostanie zamknięta i nową pamięć podręczną zostanie zainicjowana przy użyciu hello nowy rozmiar. W tym czasie hello pamięci podręcznej jest niedostępna i nie zostały utracone wszystkie dane w pamięci podręcznej hello.
* Gdy **podstawowe** pamięć podręczna jest skalowana tooa **standardowe** pamięci podręcznej, zainicjowaniu obsługi pamięci podręcznej repliki i hello dane są kopiowane z hello głównej pamięci podręcznej toohello repliki w pamięci podręcznej. Witaj w pamięci podręcznej pozostaje dostępna podczas hello skalowanie procesu.
* Gdy **standardowe** pamięć podręczna jest skalowana tooa inny rozmiar lub tooa **Premium** pamięci podręcznej, jedną z replik hello jest zamknięte i ponownie zainicjowano obsługę administracyjną toohello nowego rozmiaru i hello danych przesyłanych przez, a następnie hello innych repliki wykonuje pracy awaryjnej przed ponownym zainicjowaniu obsługi administracyjnej, podobnej procedury toohello, która występuje podczas awarii jednego z węzłów pamięci podręcznej hello.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Spowoduje utratę danych z mojej pamięci podręcznej podczas skalowania?
* Gdy **podstawowe** pamięci podręcznej jest zgubienia skalowana tooa nowy rozmiar wszystkich danych i pamięci podręcznej hello jest niedostępny podczas hello operacji skalowania.
* Gdy **podstawowe** pamięć podręczna jest skalowana tooa **standardowe** pamięci podręcznej, hello dane w pamięci podręcznej hello jest zwykle zachowane.
* Gdy **standardowe** pamięć podręczna jest skalowana tooa większy rozmiar lub warstwy, lub **Premium** skalowania pamięci podręcznej tooa większy rozmiar wszystkich danych zazwyczaj są zachowywane. Podczas skalowania **standardowe** lub **Premium** pamięci podręcznej w dół tooa mniejszy rozmiar, dane mogą zostać utracone w zależności od tego, jak dużo danych jest w pamięci podręcznej hello powiązane toohello nowy rozmiar podczas jego skalowania. Jeśli dane zostaną utracone podczas skalowania, klucze są wykluczony przy użyciu hello [allkeys lru](http://redis.io/topics/lru-cache) zasady wykluczania. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>Jest niestandardowe baz danych zmodyfikowane ustawienie podczas skalowania?
Niektóre warstw cenowych mają różne [baz danych limity](cache-configure.md#databases), więc istnieją pewne kwestie dotyczące skalowania Jeśli skonfigurowana wartość niestandardową dla hello `databases` ustawienie podczas tworzenia pamięci podręcznej.

* Podczas skalowania tooa cenowym o niższej `databases` limit niż warstwa bieżąca hello:
  * Jeśli używasz hello domyślną liczbę `databases` czyli 16 dla wszystkich warstw cenowych zostały utracone żadne dane.
  * Jeśli używasz niestandardowego liczba `databases` który mieści się w granicach hello dla toowhich warstwy hello są skalowania to `databases` ustawienie jest zachowywane i nie zostały utracone żadne dane.
  * Jeśli używasz niestandardowego liczba `databases` przekraczający hello limitów hello nową warstwę, hello `databases` ustawienie jest obniżona toohello limit nową warstwę hello i wszystkich danych w bazach danych hello usunięte zostaną utracone.
* Podczas skalowania tooa cenowym z hello takie same lub wyższe `databases` limit niż warstwa bieżąca hello Twojej `databases` ustawienie jest zachowywane i nie zostały utracone żadne dane.

Zwróć uwagę, że chociaż standardowa i Premium pamięci podręcznych SLA 99,9%, dostępności, nie umowy dotyczącej poziomu usług dla utraty danych.

### <a name="will-my-cache-be-available-during-scaling"></a>Moje pamięci podręcznej będzie dostępna podczas skalowania?
* **Standardowe** i **Premium** pamięci podręcznych pozostają dostępne podczas hello operacji skalowania.
* **Podstawowe** pamięci podręcznych są w trybie offline podczas skalowania operacji tooa inny rozmiar, ale pozostają dostępne podczas skalowania z **podstawowe** za**standardowe**.

### <a name="operations-that-are-not-supported"></a>Operacje, które nie są obsługiwane
* Nie można skalować z wyższej cenową warstwy tooa dolnej warstwy cenowej.
  * Nie można skalować z **Premium** pamięci podręcznej w dół tooa **standardowe** lub **podstawowe** pamięci podręcznej.
  * Nie można skalować z **standardowe** pamięci podręcznej w dół tooa **podstawowe** pamięci podręcznej.
* Możesz skalować z **podstawowe** pamięci podręcznej tooa **standardowe** pamięci podręcznej, ale nie można zmienić rozmiaru hello na powitania tym samym czasie. Jeśli potrzebujesz zmienić rozmiar należy kolejnych skalowania rozmiar toohello żądaną operację.
* Nie można skalować z **podstawowe** pamięci podręcznej bezpośrednio tooa **Premium** pamięci podręcznej. Użytkownik musi najpierw skali: od **podstawowe** za**standardowe** w jednej operacji skalowania, a następnie z **standardowe** za**Premium** w kolejnej Operacja skalowania.
* Nie można skalować z większego rozmiaru dół toohello **C0 (250 MB)** rozmiar.

W przypadku niepowodzenia operacji skalowania usługi hello ponowi operację hello toorevert i hello pamięci podręcznej zostanie przywrócony oryginalny rozmiar toohello.

### <a name="how-long-does-scaling-take"></a>Jak długo skalowanie podąża?
Skalowanie trwa około 20 minut w zależności od tego, jak dużo danych jest w pamięci podręcznej hello.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Jak sprawdzić, kiedy jest ukończone skalowania?
W portalu Azure hello widać hello skalowanie operację w toku. Po zakończeniu skalowanie hello stanu zmiany pamięci podręcznej hello zbyt**systemem**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



