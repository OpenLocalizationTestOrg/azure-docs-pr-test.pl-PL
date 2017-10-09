---
title: "aaaReliable serializacji obiektu kolekcji w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Azure serializacji obiektu kolekcji niezawodnej sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="f777d-103">Niezawodne serializacji obiektu kolekcji w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="f777d-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="f777d-104">Niezawodne kolekcje replikacji i utrwalić ich elementów toomake się, że są one trwałego na błędy maszyn i awarie zasilania.</span><span class="sxs-lookup"><span data-stu-id="f777d-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="f777d-105">Elementy zarówno tooreplicate i toopersist, niezawodne kolekcje muszą tooserialize je.</span><span class="sxs-lookup"><span data-stu-id="f777d-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="f777d-106">Niezawodne kolekcje Pobierz hello odpowiedni serializator dla danego typu z niezawodnej Menedżer stanów.</span><span class="sxs-lookup"><span data-stu-id="f777d-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="f777d-107">Menedżer stanu niezawodny zawiera wbudowane serializatorów i umożliwia toobe serializatorów niestandardowych zarejestrowany dla danego typu.</span><span class="sxs-lookup"><span data-stu-id="f777d-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="f777d-108">Wbudowane serializatorów</span><span class="sxs-lookup"><span data-stu-id="f777d-108">Built-in Serializers</span></span>

<span data-ttu-id="f777d-109">Menedżer stanu niezawodny obejmuje wbudowane serializatora dla niektórych typowych tak, aby serializować wydajnie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="f777d-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="f777d-110">Dla innych typów, Menedżer stanu niezawodnej powraca toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="f777d-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="f777d-111">Wbudowane serializatorów są bardziej wydajne, ponieważ wiedzieli, nie można zmienić ich typów i nie potrzebują oni tooinclude informacje o typie hello, takie jak jego nazwa typu.</span><span class="sxs-lookup"><span data-stu-id="f777d-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="f777d-112">Menedżer stanu niezawodny ma wbudowane serializatora dla następujących typów:</span><span class="sxs-lookup"><span data-stu-id="f777d-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="f777d-113">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="f777d-113">Guid</span></span>
- <span data-ttu-id="f777d-114">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="f777d-114">bool</span></span>
- <span data-ttu-id="f777d-115">Bajtów</span><span class="sxs-lookup"><span data-stu-id="f777d-115">byte</span></span>
- <span data-ttu-id="f777d-116">sbyte —</span><span class="sxs-lookup"><span data-stu-id="f777d-116">sbyte</span></span>
- <span data-ttu-id="f777d-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="f777d-117">byte[]</span></span>
- <span data-ttu-id="f777d-118">char</span><span class="sxs-lookup"><span data-stu-id="f777d-118">char</span></span>
- <span data-ttu-id="f777d-119">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f777d-119">string</span></span>
- <span data-ttu-id="f777d-120">Decimal</span><span class="sxs-lookup"><span data-stu-id="f777d-120">decimal</span></span>
- <span data-ttu-id="f777d-121">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="f777d-121">double</span></span>
- <span data-ttu-id="f777d-122">Float</span><span class="sxs-lookup"><span data-stu-id="f777d-122">float</span></span>
- <span data-ttu-id="f777d-123">int</span><span class="sxs-lookup"><span data-stu-id="f777d-123">int</span></span>
- <span data-ttu-id="f777d-124">uint</span><span class="sxs-lookup"><span data-stu-id="f777d-124">uint</span></span>
- <span data-ttu-id="f777d-125">długa</span><span class="sxs-lookup"><span data-stu-id="f777d-125">long</span></span>
- <span data-ttu-id="f777d-126">ulong</span><span class="sxs-lookup"><span data-stu-id="f777d-126">ulong</span></span>
- <span data-ttu-id="f777d-127">krótki</span><span class="sxs-lookup"><span data-stu-id="f777d-127">short</span></span>
- <span data-ttu-id="f777d-128">ushort</span><span class="sxs-lookup"><span data-stu-id="f777d-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="f777d-129">Niestandardowej serializacji</span><span class="sxs-lookup"><span data-stu-id="f777d-129">Custom Serialization</span></span>

<span data-ttu-id="f777d-130">Serializatorów niestandardowe są często używane tooincrease wydajności lub tooencrypt hello danych za pośrednictwem hello przewodowy i na dysku.</span><span class="sxs-lookup"><span data-stu-id="f777d-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="f777d-131">Wśród innych przyczyn serializatorów niestandardowe są często bardziej efektywne niż ogólny serializator, ponieważ nie potrzebują tooserialize informacje o typie hello.</span><span class="sxs-lookup"><span data-stu-id="f777d-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="f777d-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) jest używane tooregister niestandardowego programu szeregującego dla danego typu T. hello Rejestracja powinno się zdarzyć w konstrukcji hello hello StatefulServiceBase tooensure czy przed rozpoczęciem odzyskiwania, wszystkie kolekcje niezawodnej mają dostęp do tooread odpowiedni serializator toohello utrwalonych danych.</span><span class="sxs-lookup"><span data-stu-id="f777d-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="f777d-133">Niestandardowe serializatorów są pierwszeństwo nad serializatorów wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="f777d-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="f777d-134">Na przykład po zarejestrowaniu niestandardowego programu szeregującego dla int jest liczb całkowitych tooserialize używane zamiast hello wbudowanych serializatora dla int.</span><span class="sxs-lookup"><span data-stu-id="f777d-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="f777d-135">Jak tooimplement serializatora niestandardowego</span><span class="sxs-lookup"><span data-stu-id="f777d-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="f777d-136">Serializatora niestandardowego wymaga tooimplement hello [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfejsu.</span><span class="sxs-lookup"><span data-stu-id="f777d-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="f777d-137">IStateSerializer<T> zawiera przeciążenia dla zapisu i odczytu, która przyjmuje w dodatkowych T jako wartości podstawowej.</span><span class="sxs-lookup"><span data-stu-id="f777d-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="f777d-138">Ten interfejs API jest różnicowej serializacji.</span><span class="sxs-lookup"><span data-stu-id="f777d-138">This API is for differential serialization.</span></span> <span data-ttu-id="f777d-139">Obecnie funkcja różnicowej serializacji nie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="f777d-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="f777d-140">W związku z tym te dwa przeciążenia nie są nazywane, dopóki różnicowej serializacji jest widoczne i włączone.</span><span class="sxs-lookup"><span data-stu-id="f777d-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="f777d-141">Poniżej przedstawiono przykład typu niestandardowego o nazwie OrderKey, który zawiera cztery właściwości</span><span class="sxs-lookup"><span data-stu-id="f777d-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="f777d-142">Poniżej przedstawiono przykład stosowania IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="f777d-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="f777d-143">Należy pamiętać, że odczytywanie i zapisywanie przeciążeń, które przyjmują w baseValue, wywołania ich odpowiednich przeciążenia dla zgodności wyszukiwanie do przodu.</span><span class="sxs-lookup"><span data-stu-id="f777d-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="f777d-144">Możliwość</span><span class="sxs-lookup"><span data-stu-id="f777d-144">Upgradability</span></span>
<span data-ttu-id="f777d-145">W [aplikacji uaktualnienia stopniowego](service-fabric-application-upgrade.md), uaktualnienie hello jest stosowane tooa podzbioru węzłów, domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="f777d-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="f777d-146">W trakcie tego procesu będzie niektórych domen uaktualnienia w nowszej wersji aplikacji hello, a niektóre domen uaktualnienia musi być na powitania starszej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f777d-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="f777d-147">Podczas fazy hello hello nowej wersji aplikacji musi być możliwe tooread hello starą wersję danych, a hello starą wersję aplikacji musi być możliwe tooread hello nowej wersji danych.</span><span class="sxs-lookup"><span data-stu-id="f777d-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="f777d-148">Jeśli format danych hello nie jest zgodny, uaktualnienie hello do przodu i do tyłu może zakończy się awarią lub gorsza, dane mogą być utracone lub uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="f777d-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="f777d-149">Jeśli korzystasz z wbudowanych serializator, nie masz tooworry o zgodności.</span><span class="sxs-lookup"><span data-stu-id="f777d-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="f777d-150">Jednak jeśli używasz niestandardowego programu szeregującego lub hello DataContractSerializer hello danych ma toobe nieograniczonej Wstecz i przekazuje zgodne.</span><span class="sxs-lookup"><span data-stu-id="f777d-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="f777d-151">Innymi słowy każda wersja programu szeregującego wymaga tooserialize stanie toobe oraz zdeserializować dowolnej wersji hello typu.</span><span class="sxs-lookup"><span data-stu-id="f777d-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="f777d-152">Użytkownicy kontraktu danych powinien być zgodny hello reguły dobrze zdefiniowany kontroli wersji, dodawanie, usuwanie i zmiana pola.</span><span class="sxs-lookup"><span data-stu-id="f777d-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="f777d-153">Kontrakt danych ma również obsługę zajmujących się nieznany pól, przechwytywanie procesem hello serializacji i deserializacji i zajmujących się dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="f777d-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="f777d-154">Aby uzyskać więcej informacji, zobacz [kontraktu danych przy użyciu](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="f777d-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="f777d-155">Użytkownicy niestandardowego programu szeregującego przestrzegać toohello wytycznymi serializator hello używają toomake się, że jest Wstecz i przekazuje zgodne.</span><span class="sxs-lookup"><span data-stu-id="f777d-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="f777d-156">Typowy sposób obsługi wszystkich wersji jest dodawanie informacji o rozmiarze na początku hello i tylko dodanie właściwości opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="f777d-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="f777d-157">W ten sposób każdej wersji mogą odczytywać, jaka może i przejść przez hello pozostała część hello strumienia.</span><span class="sxs-lookup"><span data-stu-id="f777d-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f777d-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f777d-158">Next steps</span></span>
  * [<span data-ttu-id="f777d-159">Serializacja i uaktualniania</span><span class="sxs-lookup"><span data-stu-id="f777d-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="f777d-160">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="f777d-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="f777d-161">[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f777d-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="f777d-162">[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f777d-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="f777d-163">Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="f777d-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="f777d-164">Dowiedz się, jak toouse zaawansowanych funkcji podczas uaktualniania aplikacji, odnosząc się zbyt[Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="f777d-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="f777d-165">Rozwiązywania typowych problemów w aplikacji uaktualnień, odnosząc się kroki toohello [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f777d-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
