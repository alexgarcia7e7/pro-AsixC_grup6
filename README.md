# pro-AsixC_grup6
# 1. Proposta de CPD (Centre de Processament de Dades)

## 1.1 Ubicació física i Acondicionament

El disseny arquitectònic i d'enginyeria estructural per al Centre de Processament de Dades (CPD) de **Innovate Tech** s'ha concebut sota premisses estrictes de seguretat física passiva, redundància ambiental i eficiència en la distribució de la planta. El disseny segueix les directrius internacionals de la normativa **TIA-942 (Telecommunications Infrastructure Standard for Data Centers)** i s'adaptarà fidelment a la distribució espacial reflectida en la infraestructura.

### Criteris de Confidencialitat, Aïllament i Seguretat Estructural Perimetral

* **Emplaçament Estratègic a l'Edifici:** La sala destinada al CPD s'ubica en una zona geomètrica interna de la planta de l'edifici corporatiu. S'ha evitat per complet la seva instal·lació en nivells crítics com plantes baixes o soterranis, eliminant així la vulnerabilitat davant d'inundacions per ruptures de canonades generals o filtracions d'aigües pluvials. Així mateix, es descarta l'última planta per protegir l'equipament informàtic de les inclemències tèrmiques derivades de la radiació solar directa sobre la coberta o de possibles filtracions de la teulada.
* **Absència de Perímetres Exposats a l'Exterior:** Tal com es delimita en l'esquema estructural, cap de les quatre parets de la sala tècnica llinda amb façanes o finestres orientades a la via pública. Tots els envans perimetrals són divisors interiors construïts amb panells de formigó reforçat amb certificació de resistència al foc de classe **EI-120**. Això garanteix que l'estructura mantindrà la seva integritat mecànica i el seu aïllament tèrmic durant un mínim de 120 minuts en cas d'un sinistre d'incendi a les oficines adjacents.
* **Principi d'Ocultació i Integració Passiva:** Per minimitzar la superfície d'atac davant d'intrusions forçades, sabotatges o espionatge industrial, l'accés al CPD està camuflat visualment. La porta exterior manca de qualsevol finestreta, logotip corporatiu o senyalització tècnica que reveli el valor dels actius que protegeix (prohibint cartells explícits com "Sala de Servidors", "Sistemes" o "CPD"). L'entrada imita el disseny estàndard de les portes de registre de manteniment o serveis generals de l'edifici, neutralitzant l'interès de personal aliè a l'organització o de visites externes.

### Climatització Avançada, Gestió del Flux d'Aire i Distribució en Planta

Per contrarestar l'alta densitat tèrmica per unitat de superfície provocada pel funcionament ininterromput dels servidors, es descarta la climatització per confort i s'implanta una distribució geomètrica basada en l'acoblament tèrmic i l'aïllament de fluxos segons les directrius de la societat **ASHRAE TC 9.9**:

* **Disseny del Passadís Fred Confinat (Cold Aisle Containment):** D'acord amb el plànol de planta de Innovate Tech, els armaris Rack de 19 polzades (Rack de Comunicacions i Rack de Servidors/Cloud) es disposen en fileres enfrontades per les seves cares davanteres. La distància de separació entre racks s'estableix en un passadís central d'1.20 metres. Aquest passadís es segella hermèticament mitjançant panells de policarbonat translúcid a la part superior (sostre fals del passadís) i mitjançant portes correderes mecàniques als extrems. Les unitats d'Aire Acondicionat per a Sales de Computadors (**CRAC**) injecten l'aire refrigerat de forma descendent cap a l'espai estanc inferior, forçant la seva sortida a pressió exclusivament a través de les rajoles perforades ubicades dins del passadís confinat.
* **Dinàmica del Passadís Calent (Hot Aisle):** Les fonts d'alimentació i els extractors posteriors dels servidors expulsen l'aire calent de desfet (que oscil·la entre els **32°C i 35°C**) cap a la zona oberta perimetral de la sala. Aquest flux d'aire calent ascendeix per convecció natural cap a les reixetes de retorn situades a la part superior, sent succionat pels mòduls de retorn de les màquines CRAC per ser refredat, deshumidificat i filtrat novament.
* **Mètriques de Control de Precisión Ambiental:** Els controladors lògics de la sala regulen de manera automàtica el sistema de climatització per mantenir uns paràmetres operatius inalterables:
    * **Temperatura del Passadís Fred:** Regulada estrictament entre **20°C i 22°C**. Desviacions de $\pm 1\text{°C}$ generen alertes preventives al programari de monitorització d'infraestructura (DCIM).
    * **Humitat Relativa:** Controlada en un rang del **40% al 55%**. Mantenir un nivell superior al 55% induiria corrosió microscòpica a les connexions dels busos de dades, mentre que un nivell inferior al 40% elevaria críticament el risc d'acumulació i descàrrega d'electricitat electrostàtica (ESD) sobre els semiconductors.

### Enginyeria i Segregació en Sòl Elevat i Sostre Tècnic

* **Infraestructura de Sòl Tècnic Sobreelevat:** S'implementa un paviment flotant modular suspès a una alçada lliure de **45 centímetres** respecte al forjat de formigó base. Les rajoles estan compostes per estructures d'acer reles de ciment alugerit (60x60 cm), amb un revestiment superior de vinil antiestàtic dissipatiu i una capacitat de càrrega estàtica de disseny superior a $1500\text{ kg/m}^2$. La càmera d'aire resultant (*plenum*) actua doblement: com a canal principal per a la impulsió de l'aire de refrigeració i com a via de trànsit per als sistemes elèctrics de força.
* **Infraestructura de Sostre Tècnic Fals:** Suspès a 50 cm del sostre real, allotja les canalitzacions de seguretat, les línies de mostratge del sistema de detecció d'incendis per aspiració, els difusors de gas inert i els retorns tèrmics de les màquines CRAC.
* **Segregació Física Absoluta contra Interferències Electromagnètiques (EMI):** Per salvaguardar la integritat de les senyals de xarxa i evitar distorsions o pèrdues de paquets de dades en els serveis web i multimèdia, el cablejat es distribueix de forma estrictament separada per plans espacials:
    * El cable de **potència i alimentació elèctrica** (línies de força procedents dels quadres i les PDUs) discorre exclusivament pel pla inferior, fixat al sòl base mitjançant banderes de reixeta d'acer galvanitzat amb presa de terra independent.
    * El cable de **dades** (mangueres U/FTP Categoria 6A d'interconexió i enllaços troncals de fibra òptica multimode OM4) es desplega pel pla superior, suportat per banderes tipus passarel·la suspeses del sostre fals. En els punts crítics on ambdues infraestructures s'han de creuar, es realitza obligatòriament en angles rectes perpendiculars de **90°** per reduir a zero l'acoblament inductiu.
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/634ccb14-aa2f-4937-b470-00ab48fd6037" />

## 1.2 Infraestructura IT

L'arquitectura de xarxa i la distribució del maquinari de **Innovate Tech** s'han dissenyat seguint un model estructurat i jeràrquic reflectit en els plànols d'enginyeria de detall. Tota la infraestructura de computació, commutació i seguretat es centralitza en **dos armaris Rack de 42U** de bastidor de quatre postes i estàndard de 19 polzades (dimensions exteriors de 600 mm d'amplada per 1000 mm de profunditat), garantint una òptima gestió de l'espai, estabilitat mecànica, resiliència davant fallades i un flux elèctric i tèrmic eficient.

### Topologia de Xarxa Física i Flux de Comunicacions

D'acord amb la topologia de xarxa definida per al projecte, el mapa d'interconnexions físiques des de l'exterior cap als nodes de producció s'organitza en les següents capes consecutives:

1. **Pas de Vora i Enrutament (Edge Router):** Totes les línies de comunicacions externes (fibra òptica del proveïdor d'Internet cap a la WAN) connecten amb el mòdul de distribució de fibra òptica perimetral de la sala, encaminant el tràfic cap al nucli de xarxa perimetral.
2. **Capa de Seguretat i Commutació de Core:** El tràfic es distribueix a través de switches gestionables de Capa 3 que unifiquen les funcions de seguretat, enrutament inter-VLAN i mitigació de riscs de xarxa. Aquests equips actuen com a nexe d'alta velocitat connectats directament als servidors de producció.
3. **Capa d'Emmagatzematge i Serveis Auxiliars:** Els serveis es bifurquen cap al segon bastidor de l'arquitectura, on es processen les tasques de còpies de seguretat (Backup), serveis web secundaris i l'emmagatzematge massiu de dades en xarxes dedicades NAS/SAN.

### Diagrama d'Estructura de Racks (Elevació de Rack de 42U)

Per optimitzar la distribució del pes mecànic (evitant l'efecte de bolcat), reduir les distàncies del cablejat de parxeig i afavorir la circulació de l'aire segons el plànol del passadís fred, os components es disposen verticalment en el perfil de l'armari de la següent manera. Cada element elèctric crític disposa de connexió duplicada cap a les fonts d'alimentació redundants calentes (Hot-Swap).

<img width="816" height="1024" alt="image" src="https://github.com/user-attachments/assets/a6daeaa0-3d6a-459f-9885-fdb204b998c3" />

### Disseny i Ubicació dels Patch Panels en relació amb els Switches

La disposició dels panells de parxeig s'ha dissenyat adjacents als elements de commutació activius per minimitzar el recorregut dels cables de xarxa (*patch cords*), optimitzant la densitat de ports i maximitzant la neteja visual de la següent manera:
* **Al Rack 1 (Producció):** A la capçalera de l'armari se situa el Panell de Distribució de Fibra Òptica (U40) i un **Patch Panel de 24 ports** connectat immediatament a dalt de la unitat del Switch de Xarxa de Producció. Aquesta proximitat directa permet utilitzar cables de parxeig curts que connecten verticalment els ports de dades, eliminant els bucles excessius de coure que podrien obstruir la ventilació frontal del bastidor.
* **Al Rack 2 (Backup i Serveis Auxiliars):** S'aplica una estructura simètrica a la part superior allotjant l'Organitzador de cables i el Patch Panel de 24 ports a sobre del Switch de Xarxa de Backup i Serveis, centralitzant les línies de còpies de seguretat procedents de la cabina d'emmagatzematge i el servidor de destí.

### Gestió Estructurada de Cablejat (Horitzontal i Vertical)

* **Gestió Horitzontal:** S'instal·len mòduls organitzadors de cablejat horitzontal amb perfil de 1U directament integrats en la zona alta de comunicacions. Aquests elements permeten rebre el cablejat de coure i guiar-lo de manera neta cap als laterals de l'armari, garantint que cap cable encreuat tapi els LEDs d'estat de les interfícies d'espectre d'enllaç.
* **Gestió Vertical:** Ambdós armaris disposen de línies de distribució elèctrica verticals (**PDU Vertical - Zero-U**) instal·lades als laterals del xassís per no consumir unitats operatives de rack. Els cables d'alimentació i dades discorren per camins separats a esquerra i dreta per evitar acoblaments.
* **Administració Local (KVM):** S'integra a la unitat superior (**U41/U42**) un commutador KVM amb pantalla desplegable per permetre que els tècnics puguin interactuar físicament i fer tasques de diagnòstic i manteniment *in situ* sobre els servidors sense requerir una connexió de xarxa externa activa.
* **Consideracions de Pes i Balanç Mecànic:** Els components de major densitat i massa, com els mòduls de **SAI Redundant (A i B) de 2U**, s'ubiquen de forma obligatòria a la base més baixa de l'armari (unitats de la U01 a la U06). Els servidors Blade/Rack de producció (Servidor 1 i Servidor 2) i els de backup (NAS/SAN i Servidor Web) es posicionen a la zona central-mitjana del perfil de càrrega. Aquesta disposició manté el centre de gravetat global de l'armari a la part inferior, garantint una estabilitat estructural perfecta contra vibracions o possibles desplaçaments accidentals.
* **Fixació del Cablejat:** Totes les agrupacions de cables es peinen manualment i se subjecten exclusivament mitjançant **brides de velcro tècnic**, respectant un radi de curvatura mínim per evitar l'estrangulació del dielèctric dels cables de coure de categoria 6a.
