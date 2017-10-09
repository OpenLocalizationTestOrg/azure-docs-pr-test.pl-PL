## <a name="scenario"></a>Scenariusz
toobetter ilustrują sposób toocreate sieci wirtualnej i podsieci, ten dokument użyje scenariusz hello poniżej.

![Scenariusz sieci wirtualnych](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

W tym scenariuszu utworzysz sieć wirtualną o nazwie **TestVNet** z zarezerwowanym blokiem CIDR **192.168.0.0./16**. Sieci wirtualnej będzie zawierać następujące podsieci hello: 

* **FrontEnd**, używająca bloku CIDR **192.168.1.0/24**.
* **BackEnd**, używająca bloku CIDR **192.168.2.0/24**.

