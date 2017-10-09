## <a name="scenario"></a>Scenariusz
Maszynę Wirtualną z jednej karty Sieciowej jest tooa utworzone i połączone sieci wirtualnej. Hello maszyna wirtualna wymaga trzech różnych *prywatnej* IP adresy i dwa *publicznego* adresów IP. Witaj, adresy IP są przypisywane toohello następujące konfiguracje adresów IP:

* **IPConfig-1:** przypisuje *statycznych* prywatnego adresu IP i *statycznych* publicznego adresu IP.
* **Polecenie IPConfig-2:** przypisuje *statycznych* prywatnego adresu IP i *statycznych* publicznego adresu IP.
* **Polecenie IPConfig-3:** przypisuje *statycznych* prywatnego adresu IP i żadnego publicznego adresu IP.
  
    ![Wiele adresów IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

konfiguracje adresów IP Hello są skojarzone toohello kart interfejsu Sieciowego, gdy hello, karta sieciowa jest tworzona i hello kart interfejsu Sieciowego jest toohello dołączona maszyna wirtualna po utworzeniu hello maszyny Wirtualnej. typy Hello adresy IP używane dla scenariusza hello są ilustracyjną. Można przypisać niezależnie od adresu i przypisywania typów IP wymagane.

> [!NOTE]
> Chociaż hello kroków tym artykule przypisuje wszystkie tooa konfiguracji IP jednej karty Sieciowej, można przypisać wielu tooany konfiguracji adresu IP karty Sieciowej na maszynie Wirtualnej z wieloma kartami Sieciowymi. jak toocreate Maszynę wirtualną z wieloma kartami sieciowymi, przeczytaj toolearn hello [tworzenia maszyn wirtualnych z wieloma kartami sieciowymi](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) artykułu.
