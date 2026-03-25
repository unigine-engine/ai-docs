# IG Plugin API

> **Warning:** The functionality described in this article is not available in the Community SDK edition.
> You should upgrade to [**Sim**](https://l.unigine.com/SdhugY462) SDK edition to use it.


This section contains an incomplete set of the IG Plugin API Classes.


UNIGINE's IG is designed to be simple, easy to use and [extensible](../../../../../ig/index.md#extension) via its plug-in based architecture. The main framework plugin, that manipulates systems, entities, articulated parts, component templates and so on, is the [IG Plugin](../../../../../api/library/plugins/ig/api/index.md), it operates in terms of the UNIGINE Engine (*Nodes, NodeReferences*, etc.) and is not bound to any specific communication protocol. The IG plugin has a set of additional plugins, called **connectors**, that are used to link IG terminology with that of each specific protocol (e.g. [CIGI](../../../../../api/library/plugins/ig/cigi/index.md), [HLA](../../../../../api/library/plugins/ig/hla/index.md), [DIS](../../../../../api/library/plugins/ig/dis/index.md)). Basically, the architecture looks as follows:


![IG](../../../../../ig/ig_structure.png)


- [IG::Manager Class](../../../../../api/library/plugins/ig/api/class.managerinterface_cpp.md)
- [IG::ArticulatedPart Class](../../../../../api/library/plugins/ig/api/class.articulatedpart_cpp.md)
- [IG::CollisionSegment Class](../../../../../api/library/plugins/ig/api/class.collisionsegment_cpp.md)
- [IG::CollisionVolume Class](../../../../../api/library/plugins/ig/api/class.collisionvolume_cpp.md)
- [IG::ComponentBaseInterface Class](../../../../../api/library/plugins/ig/api/class.componentbaseinterface_cpp.md)
- [IG::Component Class](../../../../../api/library/plugins/ig/api/class.component_cpp.md)
- [IG::NEDConverter Class](../../../../../api/library/plugins/ig/api/class.nedconverter_cpp.md)
- [IG::Entity Class](../../../../../api/library/plugins/ig/api/class.entity_cpp.md)
- [IG::LightController Class](../../../../../api/library/plugins/ig/api/class.lightcontroller_cpp.md)
- [IG::Meteo Class](../../../../../api/library/plugins/weather/class.meteo_cpp.md)
- [IG::MeteoCameraEffects Class](../../../../../api/library/plugins/weather/class.meteocameraeffects_cpp.md)
- [IG::Region Class](../../../../../api/library/plugins/weather/class.region_cpp.md)
- [IG::SkyMap Class](../../../../../api/library/plugins/weather/class.skymap_cpp.md)
- [IG::Symbol Class](../../../../../api/library/plugins/ig/api/class.symbol_cpp.md)
- [IG::SymbolCircle Class](../../../../../api/library/plugins/ig/api/class.symbolcircle_cpp.md)
- [IG::SymbolText Class](../../../../../api/library/plugins/ig/api/class.symboltext_cpp.md)
- [IG::SymbolPolyline Class](../../../../../api/library/plugins/ig/api/class.symbolpolyline_cpp.md)
- [IG::SymbolsController Class](../../../../../api/library/plugins/ig/api/class.symbolscontroller_cpp.md)
- [IG::SymbolsPlane Class](../../../../../api/library/plugins/ig/api/class.symbolsplane_cpp.md)
- [IG::ViewBase Class](../../../../../api/library/plugins/ig/api/class.viewbase_cpp.md)
- [IG::View Class](../../../../../api/library/plugins/ig/api/class.view_cpp.md)
- [IG::ViewGroup Class](../../../../../api/library/plugins/ig/api/class.viewgroup_cpp.md)
- [IG::Water Class](../../../../../api/library/plugins/weather/class.water_cpp.md)
- [IG::IGIntersection Structure](../../../../../api/library/plugins/ig/api/class.igintersection_cpp.md)
