---
title: "Niezawodne serializacji obiektu kolekcji w sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="35a7f-103">Niezawodne serializacji obiektu kolekcji w sieci szkieletowej usług Azure</span><span class="sxs-lookup"><span data-stu-id="35a7f-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="35a7f-104">Niezawodne kolekcje replikacji i utrwalić swoich elementów, aby upewnić się, że są trwałe na błędy maszyn i awarie zasilania.</span><span class="sxs-lookup"><span data-stu-id="35a7f-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="35a7f-105">Do replikacji i elementy będą się powtarzać, niezawodne kolekcje muszą serializować je.</span><span class="sxs-lookup"><span data-stu-id="35a7f-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="35a7f-106">Kolekcje niezawodnej uzyskanie odpowiedniego programu szeregującego dla danego typu niezawodnej Menedżer stanu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="35a7f-107">Menedżer stanu niezawodny zawiera wbudowane serializatorów i umożliwia niestandardowych serializatorów rejestracji dla danego typu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="35a7f-108">Wbudowane serializatorów</span><span class="sxs-lookup"><span data-stu-id="35a7f-108">Built-in Serializers</span></span>

<span data-ttu-id="35a7f-109">Menedżer stanu niezawodny obejmuje wbudowane serializatora dla niektórych typowych tak, aby serializować wydajnie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="35a7f-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="35a7f-110">Dla innych typów niezawodnej Menedżer stanu powraca do użycia [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="35a7f-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="35a7f-111">Wbudowane serializatorów są bardziej wydajne, ponieważ wiedzieli, nie można zmienić ich typów i nie muszą obejmować informacje o typie, takie jak jego nazwa typu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="35a7f-112">Menedżer stanu niezawodny ma wbudowane serializatora dla następujących typów:</span><span class="sxs-lookup"><span data-stu-id="35a7f-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="35a7f-113">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="35a7f-113">Guid</span></span>
- <span data-ttu-id="35a7f-114">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="35a7f-114">bool</span></span>
- <span data-ttu-id="35a7f-115">Bajtów</span><span class="sxs-lookup"><span data-stu-id="35a7f-115">byte</span></span>
- <span data-ttu-id="35a7f-116">sbyte —</span><span class="sxs-lookup"><span data-stu-id="35a7f-116">sbyte</span></span>
- <span data-ttu-id="35a7f-117">Byte]</span><span class="sxs-lookup"><span data-stu-id="35a7f-117">byte[]</span></span>
- <span data-ttu-id="35a7f-118">char</span><span class="sxs-lookup"><span data-stu-id="35a7f-118">char</span></span>
- <span data-ttu-id="35a7f-119">Ciąg</span><span class="sxs-lookup"><span data-stu-id="35a7f-119">string</span></span>
- <span data-ttu-id="35a7f-120">Decimal</span><span class="sxs-lookup"><span data-stu-id="35a7f-120">decimal</span></span>
- <span data-ttu-id="35a7f-121">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="35a7f-121">double</span></span>
- <span data-ttu-id="35a7f-122">Float</span><span class="sxs-lookup"><span data-stu-id="35a7f-122">float</span></span>
- <span data-ttu-id="35a7f-123">int</span><span class="sxs-lookup"><span data-stu-id="35a7f-123">int</span></span>
- <span data-ttu-id="35a7f-124">uint</span><span class="sxs-lookup"><span data-stu-id="35a7f-124">uint</span></span>
- <span data-ttu-id="35a7f-125">długa</span><span class="sxs-lookup"><span data-stu-id="35a7f-125">long</span></span>
- <span data-ttu-id="35a7f-126">ulong</span><span class="sxs-lookup"><span data-stu-id="35a7f-126">ulong</span></span>
- <span data-ttu-id="35a7f-127">krótki</span><span class="sxs-lookup"><span data-stu-id="35a7f-127">short</span></span>
- <span data-ttu-id="35a7f-128">ushort</span><span class="sxs-lookup"><span data-stu-id="35a7f-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="35a7f-129">Niestandardowej serializacji</span><span class="sxs-lookup"><span data-stu-id="35a7f-129">Custom Serialization</span></span>

<span data-ttu-id="35a7f-130">Niestandardowe serializatorów są często używane w celu zwiększenia wydajności lub do szyfrowania danych przez sieć oraz na dysku.</span><span class="sxs-lookup"><span data-stu-id="35a7f-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="35a7f-131">Wśród innych powodów serializatorów niestandardowe są często bardziej efektywne niż ogólny serializator, ponieważ nie potrzebują do serializacji informacje o typie.</span><span class="sxs-lookup"><span data-stu-id="35a7f-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="35a7f-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) służy do rejestrowania niestandardowego programu szeregującego dla danego typu T. Rejestracja powinno się zdarzyć w konstrukcji StatefulServiceBase zapewnienie przed rozpoczęciem odzyskiwania, wszystkie kolekcje niezawodny dostęp do odpowiednich serializatora do odczytania ich danych.</span><span class="sxs-lookup"><span data-stu-id="35a7f-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="35a7f-133">Niestandardowe serializatorów są pierwszeństwo nad serializatorów wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="35a7f-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="35a7f-134">Na przykład po zarejestrowaniu niestandardowego programu szeregującego dla int on jest używany do serializacji liczb całkowitych zamiast wbudowanego serializatora dla int.</span><span class="sxs-lookup"><span data-stu-id="35a7f-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="35a7f-135">Jak zaimplementować serializatora niestandardowego</span><span class="sxs-lookup"><span data-stu-id="35a7f-135">How to implement a custom serializer</span></span>

<span data-ttu-id="35a7f-136">Serializatora niestandardowego należy zaimplementować [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfejsu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="35a7f-137">IStateSerializer<T> zawiera przeciążenia dla zapisu i odczytu, która przyjmuje w dodatkowych T jako wartości podstawowej.</span><span class="sxs-lookup"><span data-stu-id="35a7f-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="35a7f-138">Ten interfejs API jest różnicowej serializacji.</span><span class="sxs-lookup"><span data-stu-id="35a7f-138">This API is for differential serialization.</span></span> <span data-ttu-id="35a7f-139">Obecnie funkcja różnicowej serializacji nie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="35a7f-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="35a7f-140">W związku z tym te dwa przeciążenia nie są nazywane, dopóki różnicowej serializacji jest widoczne i włączone.</span><span class="sxs-lookup"><span data-stu-id="35a7f-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="35a7f-141">Poniżej przedstawiono przykład typu niestandardowego o nazwie OrderKey, który zawiera cztery właściwości</span><span class="sxs-lookup"><span data-stu-id="35a7f-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="35a7f-142">Poniżej przedstawiono przykład stosowania IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="35a7f-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="35a7f-143">Należy pamiętać, że odczytywanie i zapisywanie przeciążeń, które przyjmują w baseValue, wywołania ich odpowiednich przeciążenia dla zgodności wyszukiwanie do przodu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="35a7f-144">Możliwość</span><span class="sxs-lookup"><span data-stu-id="35a7f-144">Upgradability</span></span>
<span data-ttu-id="35a7f-145">W [aplikacji uaktualnienia stopniowego](service-fabric-application-upgrade.md), uaktualnienie ma zostać zastosowane do podzbioru węzłów, domeny uaktualnienia pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="35a7f-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="35a7f-146">W trakcie tego procesu będzie niektórych domen uaktualnienia w nowszej wersji aplikacji, a niektóre domen uaktualnienia będą realizowane w starszej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35a7f-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="35a7f-147">Podczas wdrożenia nowa wersja aplikacji musi mieć możliwość odczytu starą wersję danych, a starą wersję aplikacji musi mieć możliwość odczytu nowej wersji danych.</span><span class="sxs-lookup"><span data-stu-id="35a7f-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="35a7f-148">Jeśli format danych jest niezgodny z przodu i do tyłu, uaktualnienie może się nie powieść lub gorsza, może utraty lub uszkodzenia danych.</span><span class="sxs-lookup"><span data-stu-id="35a7f-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="35a7f-149">Jeśli korzystasz z wbudowanych serializator, nie masz martwić się o zgodności.</span><span class="sxs-lookup"><span data-stu-id="35a7f-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="35a7f-150">Jednak jeśli używasz niestandardowego programu szeregującego lub elementu DataContractSerializer, dane muszą być nieograniczonej zgodne przodu i do tyłu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="35a7f-151">Innymi słowy każda wersja programu szeregującego musi być możliwe do serializacji i deserializacji dowolnej wersji tego typu.</span><span class="sxs-lookup"><span data-stu-id="35a7f-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="35a7f-152">Użytkownicy kontraktu danych powinien być zgodny reguły dobrze zdefiniowany kontroli wersji, dodawanie, usuwanie i zmiana pola.</span><span class="sxs-lookup"><span data-stu-id="35a7f-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="35a7f-153">Kontrakt danych ma również obsługę zajmujących się nieznany pól, przechwytywanie do procesu serializacji i deserializacji i zajmujących się dziedziczenia klas.</span><span class="sxs-lookup"><span data-stu-id="35a7f-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="35a7f-154">Aby uzyskać więcej informacji, zobacz [kontraktu danych przy użyciu](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="35a7f-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="35a7f-155">Użytkownicy niestandardowego programu szeregującego powinien zgodne z wytycznymi serializator, którego używają Sprawdź jest Wstecz i przekazuje zgodne.</span><span class="sxs-lookup"><span data-stu-id="35a7f-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="35a7f-156">Typowy sposób obsługi wszystkich wersji jest dodawania informacji o rozmiarze na początku i tylko właściwości opcjonalnych.</span><span class="sxs-lookup"><span data-stu-id="35a7f-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="35a7f-157">W ten sposób każdej wersji może odczytywać znacznie można i przejść w pozostałej części strumienia.</span><span class="sxs-lookup"><span data-stu-id="35a7f-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35a7f-158">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35a7f-158">Next steps</span></span>
  * [<span data-ttu-id="35a7f-159">Serializacja i uaktualniania</span><span class="sxs-lookup"><span data-stu-id="35a7f-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="35a7f-160">Dokumentacja dla deweloperów niezawodnej kolekcji</span><span class="sxs-lookup"><span data-stu-id="35a7f-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="35a7f-161">[Uaktualnianie aplikacji za pomocą Visual Studio](service-fabric-application-upgrade-tutorial.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35a7f-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="35a7f-162">[Uaktualnienie z aplikacji przy użyciu programu Powershell](service-fabric-application-upgrade-tutorial-powershell.md) przeprowadzi Cię przez proces uaktualnienia aplikacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="35a7f-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="35a7f-163">Kontrolowanie sposobu uaktualnienia aplikacji przy użyciu [uaktualnienia parametrów](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="35a7f-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="35a7f-164">Dowiedz się, jak korzystać z zaawansowanych funkcji podczas uaktualniania aplikacji, odwołując się do [Tematy zaawansowane](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="35a7f-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="35a7f-165">Rozwiązywania typowych problemów w uaktualnień aplikacji, korzystając z procedury opisanej w [Rozwiązywanie problemów z uaktualnieniami aplikacji](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="35a7f-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
