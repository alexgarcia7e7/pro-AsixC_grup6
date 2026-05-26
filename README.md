# pro-AsixC_grup6
# pro-AsixC_grup6

# 1. Proposta de CPD (Centre de Processament de Dades)

## Índex de Continguts
* [1.1 Ubicació física i Acondicionament](#11-ubicació-física-i-acondicionament)
  * [Criteris de Confidencialitat, Aïllament i Seguretat Estructural Perimetral](#criteris-de-confidencialitat-aïllament-i-seguretat-estructural-perimetral)
  * [Climatització Avançada, Gestió del Flux d'Aire i Distribució en Planta](#climatització-avançada-gestió-del-flux-daire-i-distribució-en-planta)
  * [Enginyeria i Segregació en Sòl Elevat i Sostre Tècnic](#enginyeria-i-segregació-en-sòl-elevat-i-sostre-tècnic)
* [1.2 Infraestructura IT](#12-infraestructura-it)
  * [Topologia de Xarxa Física i Flux de Comunicacions](#topologia-de-xarxa-física-i-flux-de-comunicacions)
  * [Diagrama d'Estructura de Racks (Elevació de Rack de 42U)](#diagrama-destructura-de-racks-elevació-de-rack-de-42u)
  * [Disseny i Ubicació dels Patch Panels en relació amb els Switches](#disseny-i-ubicació-dels-patch-panels-en-relació-amb-els-switches)
  * [Gestió Estructurada de Cablejat (Horitzontal i Vertical)](#gestió-estructurada-de-cablejat-horitzontal-i-vertical)
* [1.3 Infraestructura Elèctrica: Dimensionament del SAI](#13-infraestructura-elèctrica-dimensionament-del-sai)
  * [Inventari de Consum Elèctric (Estudi de Càrregues)](#inventari-de-consum-elèctric-estudi-de-càrregues)
  * [Càlcul de la Potència Requerida del SAI](#càlcul-de-la-potència-requerida-del-sai)
  * [Selecció i Justificació del Model de SAI](#selecció-i-justificació-del-model-de-sai)
  * [Càlcul d'Autonomia i Gestió d'Apagat Net](#càlcul-dautonomia-i-gestió-dapagat-net)
* [1.4 Seguretat Física](#14-seguretat-física)
  * [Control d'Accés de Doble Factor (2FA)](#control-daccés-de-doble-factor-2fa)
  * [Sistemes de Videovigilància (CCTV)](#sistemes-de-videovigilància-cctv)
  * [Prevenció i Protecció Contra Incendis](#prevenció-i-protecció-contra-incendis)
  * [Vistes generals del CPD](#vistes-generals-del-cpd)
* [Prevenció de Riscos Laborals (PRL) al CPD](#prevenció-de-riscos-laborals-prl-al-cpd)
* [1.5 Sostenibilitat i Eficiència Energètica](#15-sostenibilitat-i-eficiència-energètica)
  * [Monitorització i Consolidació Lògica](#monitorització-i-consolidació-lògica)
  * [Subministrament d'Energia Verda](#subministrament-denergia-verda)
  * [Disseny Físic i Arquitectura de Cablejat](#disseny-físic-i-arquitectura-de-cablejat)
  * [Climatització Tèrmica i Circulació d'Aire](#climatització-tèrmica-i-circulació-daire)
  * [Hardware i Components d'Alta Eficiència](#hardware-i-components-dalta-eficiència)
* [1.7 Investigar i Comparar: Solucions Cloud i Sostenibilitat](#17-investigar-i-comparar-solucions-cloud-i-sostenibilitat)
  * [Criteris Tècnics de Comparació](#criteris-tècnics-de-comparació)
  * [Anàlisi per Proveïdor](#anàlisi-per-proveïdor)
  * [Conclusió i Justificació de la Selecció d'AWS](#conclusió-i-justificació-de-la-selecció-daws)

---

## 1.1 Ubicació física i Acondicionament

El disseny arquitectònic i d'enginyeria estructural per al Centre de Processament de Dades (CPD) de **Innovate Tech** s'ha concebut sota premisses estrictes de seguretat física passiva, redundància ambiental i eficiència en la distribució de la planta. El disseny segueix les directrius internacionals de la normativa **TIA-942 (Telecommunications Infrastructure Standard for Data Centers)** i s'adaptarà fidelment a la distribució espacial reflectida en la infraestructura.

### Criteris de Confidencialitat, Aïllament i Seguretat Estructural Perimetral

* **Emplaçament Estratègic a l'Edifici:** La sala destinada al CPD s'ubica en una zona geomètrica interna de la planta de l'edifici corporatiu. S'ha evitat per complet la seva instal·lació en nivells crítics com plantes baixes o soterranis, eliminant així la vulnerabilitat davant d'inundacions per ruptures de canonades generals o filtracions d'aigües pluvials. Així mateix, es descarta l'última planta per protegir l'equipament informàtic de les inclemències tèrmiques derivades de la radiació solar directa sobre la coberta o de possibles filtracions de la teulada.
* **Absència de Perímetres Exposats a l'Exterior:** Tal com es delimita en l'esquema estructural, cap de les quatre parets de la sala tècnica llinda amb façanes o finestres orientades a la via pública. Tots els envans perimetrals són divisors interiors construïts amb panells de formigó reforçat amb certificació de resistència al foc de classe **EI-120**. Això garanteix que l'estructura mantindrà la seva integritat mecànica i el seu aïllament tèrmic durant un mínim de 120 minuts ininterromputs en cas d'un sinistre d'incendi a les oficines adjacents.
* **Principi d'Ocultació i Integració Passiva:** Per minimitzar la superfície d'atac davant d'intrusions forçades, sabotatges o espionatge industrial, l'accés al CPD està camuflat visualment. La porta exterior manca de qualsevol finestreta, logotip corporatiu o senyalització tècnica que reveli el valor dels actius que protegeix (prohibint cartells explícits com "Sala de Servidors", "Sistemes" o "CPD"). L'entrada imita el disseny estàndard de les portes de registre de manteniment o serveis generals de l'edifici, neutralitzant l'interès de personal aliè a l'organització o de visites externes.

### Climatització Avançada, Gestió del Flux d'Aire i Distribució en Planta

Per contrarestar l'alta densitat tèrmica per unitat de superfície provocada pel funcionament ininterromput dels servidors, es descarta la climatització per confort i s'implanta una distribució geomètrica basada en l'acoblament tèrmic i l'aïllament de fluxos segons les directrius de la societat **ASHRAE TC 9.9**:

* **Disseny del Passadís Fred Confinat (Cold Aisle Containment):** D'acord amb el plànol de planta de Innovate Tech, els armaris Rack de 19 polzades (Rack de Comunicacions i Rack de Servidors/Cloud) es disposen en fileres enfrontades per les seves cares davanteres. La distància de separació entre racks s'estableix en un passadís central d'1.20 metres. Aquest passadís es segella hermèticament mitjançant panells de policarbonat translúcid a la part superior (sostre fals del passadís) i mitjançant portes correderes mecàniques als extrems. Les unitats d'Aire Acondicionat per a Sales de Computadors (**CRAC**) injecten l'aire refrigerat de forma descendent cap a l'espai estanc inferior, forçant la seva sortida a pressió exclusivament a través de les rajoles perforades ubicades dins del passadís confinat.
* **Dinàmica del Passadís Calent (Hot Aisle):** Les fonts d'alimentació i els extractors posteriors dels servidors expulsen l'aire calent de desfet (que oscil·la entre els **32°C i 35°C**) cap a la zona oberta perimetral de la sala. Aquest flux d'aire calent ascendeix per convecció natural cap a les reixetes de retorn situades a la part superior, sent succionat pels mòduls de retorn de les màquines CRAC per ser refredat, deshumidificat i filtrat novament.
* **Mètriques de Control de Precisió Ambiental:** Els controladors lògics de la sala regulen de manera automàtica el sistema de climatització per mantenir uns paràmetres operatius inalterables:
  * **Temperatura del Passadís Fred:** Regulada estrictament entre **20°C i 22°C**. Desviacions de $\pm 1\text{°C}$ generen alertes preventives al programari de monitorització d'infraestructura (DCIM).
  * **Humitat Relativa:** Controlada en un rang del **40% al 55%**. Mantenir un nivell superior al 55% induiria corrosió microscòpica a les connexions dels busos de dades, mentre que un nivell inferior al 40% elevaria críticament el risc d'acumulació i descàrrega d'electricitat electrostàtica (ESD) sobre els semiconductors.

### Enginyeria i Segregació en Sòl Elevat i Sostre Tècnic

* **Infraestructura de Sòl Tècnic Sobreelevat:** S'implementa un paviment flotant modular suspès a una alçada lliure de **45 centímetres** respecte al forjat de formigó base. Les rajoles estan compostes per estructures d'acer reles de ciment alugerit (60x60 cm), amb un revestiment superior de vinil antiestàtic dissipatiu i una capacitat de càrrega estàtica de disseny superior a $1500\text{ kg/m}^2$. La càmera d'aire resultant (*plenum*) actua doblement: com a canal principal per a la instrucció de l'aire de refrigeració i com a via de trànsit per als sistemes elèctrics de força.
* **Infraestructura de Sostre Tècnic Fals:** Suspès a 50 cm del sostre real, allotja les canalitzacions de seguretat, les línies de mostratge del sistema de detecció d'incendis per aspiració, els difusors de gas inert i els retorns tèrmics de les màquines CRAC.
* **Segregació Física Absoluta contra Interferències Electromagnètiques (EMI):** Per salvaguardar la integritat de les senyals de xarxa i evitar distorsions o pèrdues de paquets de dades en els serveis web i multimèdia, el cablejat es distribueix de forma estrictament separada per plans espacials:
  * El cable de **potència i alimentació elèctrica** (línies de força procedents dels quadres i les PDUs) discorre exclusivament pel pla inferior, fixat al sòl base mitjançant banderes de reixeta d'acer galvanitzat amb presa de terra independent.
  * El cable de **dades** (mangueres U/FTP Categoria 6A d'interconexió i enllaços troncals de fibra òptica multimode OM4) es desplega pel pla superior, suportat per banderes tipus passarel·la suspeses del sostre fals. En els punts crítics on ambdues infraestructures s'han de creuar, es realitza obligatòriament en angles rectes perpendiculars de **90°** per reduir a zero l'acoblament inductiu.

<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/634ccb14-aa2f-4937-b470-00ab48fd6037" />

---

## 1.2 Infraestructura IT

L'arquitectura de xarxa i la distribució del maquinari de **Innovate Tech** s'han dissenyat seguint un model estructurat i jeràrquic reflectit en els plànols d'enginyeria de detall. Tota la infraestructura de computació, commutació i seguretat es centralitza en **dos armaris Rack de 42U** de bastidor de quatre postes i estàndard de 19 polzades (dimensions exteriors de 600 mm d'amplada per 1000 mm de profunditat), garantint una òptima gestió de l'espai, estabilitat mecànica, resiliència davant fallades i un flux elèctric i tèrmic eficient.

### Topologia de Xarxa Física i Flux de Comunicacions

D'acord amb la topologia de xarxa definida per al projecte, el mapa d'interconnexions físiques des de l'exterior cap als nodes de producció s'organitza en les següents capes consecutives:

1. **Pas de Vora i Enrutament (Edge Router):** Totes les línies de comunicacions externes (fibra òptica del proveïdor d'Internet cap a la WAN) connecten amb el mòdul de distribució de fibra òptica perimetral de la sala, encaminant el tràfic cap al nucli de xarxa perimetral.
2. **Capa de Seguretat i Commutació de Core:** El tràfic es distribueix a través de switches gestionables de Capa 3 que unifiquen les funcions de seguretat, enrutament inter-VLAN i mitigació de riscs de xarxa. Aquests equips actuen com a nexe d'alta velocitat connectats directament als servidors de producció.
3. **Capa d'Emmagatzematge i Serveis Auxiliars:** Els serveis es bifurquen cap al segon bastidor de l'arquitectura, on es processen les tasques de còpies de seguretat (Backup), serveis web secundaris i l'emmagatzematge massiu de dades en xarxes dedicades NAS/SAN.

### Diagrama d'Estructura de Racks (Elevació de Rack de 42U)

Per optimitzar la distribució del pes mecànic (evitant l'efecte de bolcat), reduir les distàncies del cablejat de parxeig i afavorir la circulació de l'aire segons el plànol del passadís fred, els components es disposen verticalment en el perfil de l'armari de la següent manera. Cada element elèctric crític disposa de connexió duplicada cap a les fonts d'alimentació redundants calentes (Hot-Swap).

<img width="816" height="1024" alt="image" src="https://github.com/user-attachments/assets/a6daeaa0-3d6a-459f-9885-fdb204b998c3" />

### Disseny i Ubicació dels Patch Panels en relació amb os Switches

La disposició dels panells de parxeig s'ha dissenyat adjacents als elements de commutació actius per minimitzar el recorregut dels cables de xarxa (*patch cords*), optimitzant la densitat de ports i maximitzant la neteja visual de la següent manera:
* **Al Rack 1 (Producció):** A la capçalera de l'armari se situa el Panell de Distribució de Fibra Òptica (U40) i un **Patch Panel de 24 ports** connectat immediatament a dalt de la unitat del Switch de Xarxa de Producció. Aquesta proximitat directa permet utilitzar cables de parxeig curts que connecten verticalment els ports de dades, eliminant els bucles excessius de coure que podrien obstruir la ventilació frontal del bastidor.
* **Al Rack 2 (Backup i Serveis Auxiliars):** S'aplica una estructura simètrica a la part superior allotjant l'Organitzador de cables i el Patch Panel de 24 ports a sobre del Switch de Xarxa de Backup i Serveis, centralitzant les línies de còpies de seguretat procedents de la cabina d'emmagatzematge i el servidor de destí.

### Gestió Estructurada de Cablejat (Horitzontal i Vertical)

* **Gestió Horitzontal:** S'instal·len mòduls organitzadors de cablejat horitzontal amb perfil de 1U directament integrats en la zona alta de comunicacions. Aquests elements permeten rebre el cablejat de coure i guiar-lo de manera neta cap els laterals de l'armari, garantint que cap cable encreuat tapi els LEDs d'estat de les interfícies d'espectre d'enllaç.
* **Gestió Vertical:** Ambdós armaris disposen de línies de distribució elèctrica verticals (**PDU Vertical - Zero-U**) instal·lades als laterals del xassís per no consumir unitats operatives de rack. Els cables d'alimentació i dades discorren per camins separats a esquerra i dreta per evitar acoblaments.
* **Administració Local (KVM):** S'integra a la unitat superior (**U41/U42**) un commutador KVM amb pantalla desplegable per permetre que els tècnics puguin interactuar físicament i fer tasques de diagnòstic i manteniment *in situ* sobre els servidors sense requerir una connexió de xarxa externa activa.
* **Consideracions de Pes i Balanç Mecànic:** Els components de mayor densitat i massa, com els mòduls de **SAI Redundant (A i B) de 2U**, s'ubiquen de forma obligatòria a la base més baixa de l'armari (unitats de la U01 a la U06). Els servidors Blade/Rack de producció (Servidor 1 i Servidor 2) i els de backup (NAS/SAN i Servidor Web) es posicionen a la zona central-mitjana del perfil de càrrega. Aquesta disposició manté el centre de gravetat global de l'armari a la part inferior, garantint una estabilitat estructural perfecta contra vibracions o possibles desplaçaments accidentals.
* **Fixació del Cablejat:** Totes les agrupacions de cables es peinen manualment i se subjecten exclusivament mitjançant **brides de velcro tècnic**, respectant un radi de curvatura mínim per evitar l'estrangulació del dielèctric dels cables de coure de categoria 6A.

---

## 1.3 Infraestructura Elèctrica: Dimensionament del SAI

El disseny elèctric del centre de dades de **Innovate Tech** s'ha calculat per garantir l'alta disponibilitat, la redundància de línia i la immunitat davant de pertorbacions de la xarxa elèctrica externa (sobretensions, pics de corrent o talls de subministrament). Per fer-ho, es disposa d'una arquitectura d'alimentació doble (Línia A i Línia B) on cada rack es nodreix d'un sistema independent de **Sistemes d'Alimentació Ininterrompuda (SAI)** de tecnologia Online de doble conversió.

### Inventari de Consum Elèctric (Estudi de Càrregues)

Per dimensionar correctament la capacitat dels SAI, s'estableix el consum nominal mitjà dels equips actius instal·lats en ambdós armaris rack:

| Component Maquinari | Quantitat | Consum Unitari Nominals (W) | Consum Total Atansat (W) |
| :--- | :---: | :---: | :---: |
| Servidor HPE ProLiant DL380 Gen10 (Rack 1) | 2 | 450 W | 900 W |
| Servidor Dell PowerEdge R540 (Rack 2) | 2 | 350 W | 700 W |
| Switch Principal Cisco Catalyst C9200L (Rack 1) | 1 | 100 W | 100 W |
| Switch de Backup Cisco Catalyst C1000L (Rack 2) | 1 | 30 W | 30 W |
| Unitat Central KVM i Pantalles de Gestió | 2 | 40 W | 80 W |
| **Càrrega Nominal Total Activa ($P_{total}$)** | - | - | **1.810 W** |

### Càlcul de la Potència Requerida del SAI

Per fer la transició de la potència activa calculada en Watts ($W$) cap a la potència aparent que defineix la capacitat de trabalho d'un SAI en Voltamperis ($VA$), s'aplica el factor de potència típic de les fonts d'alimentació informàtiques modernes amb correcció activa ($f_p = 0,9$).

A més, seguint les recomanacions de la normativa **TIA-942**, s'afegeix un **marge de seguretat i futur creixement del 25%** ($\text{Marge} = 1,25$) per evitar que el sistema operi prop del llindar de sobrecàrrega i permetre l'addició de nous nodes informàtics a mitjà termini.

La fórmula utilitzada per determinar la potència aparent mínima és:

$$S_{mínima} = \frac{P_{total} \cdot \text{Marge}}{f_p}$$

Substituint els valors calculats en l'estudi de càrregues:

$$S_{mínima} = \frac{1.810 \text{ W} \cdot 1,25}{0,9} = \frac{2.262,5}{0,9} \approx 2.514 \text{ VA}$$

### Selecció i Justificació del Model de SAI

Donat que la càrrega crítica total del projecte requereix un mínim de $2.514 \text{ VA}$ distribuïts en configuració redundant per donar servei a les línies A i B de tots dos armaris, es justifica la implementació dels mòduls ja previstos en l'esquema físic: **APC Smart-UPS X 2200VA** en paral·lel per a cada armari.

* **Capacitat Total Instal·lada:** Cada armari disposa de dues unitats APC de 2200VA cadascuna (aportant un total de 4400VA per bastidor). Això garanteix que, en condicions normals, els SAI treballen a un règim del **41% de la seva capacitat màxima**, un punt òptim que maximitza l'eficiència energètica de l'inversor i redueix l'estrès tèrmic dels components interns.
* **Redundància:** L'arquitectura opera en mode tolerant a fallades. Si un dels SAI s'ha de desconnectar per manteniment o pateix una avaria en les seves bateries, l'altre mòdul de la línia bessona assumeix immediatament el 100% de la línia de càrrega elèctrica sense cap mil·lisegon de tall (temps de transferència de 0 ms gràcies a la tecnologia *Double-Conversion Online*).

### Càlcul d'Autonomia i Gestió d'Apagat Net

Amb una corba de descàrrega típica del model seleccionat funcionant a mitja càrrega (uns 905 W per armari), el banc de bateries integrat de plom-àcid segellat (AGM) garanteix una **autonomia d'emergència de 22 minuts**.

Aquest temps d'autonomia es distribueix seguint el protocol de seguretat operacional de l'empresa:
1. **Minuts 0 a 5 (Fase d'Espera):** El sistema se manté operant amb normalitat a l'espera que el subministrament elèctric de la xarxa pública es restableixi de forma automàtica.
2. **Minuts 5 a 15 (Alerta i Pre-apagat):** Es disparen els dimonis de gestió de l'UPS a través de la xarxa (*PowerChute Network Shutdown*). Es bloquegen les noves connexions d'usuaris externs i es comença la migració o tancament dels serveis no crítics.
3. **Minuts 15 a 20 (Apagat Net / Clean Shutdown):** S'envia l'ordre de tancament segur a les màquines virtuals de producció, seguit de l'apagat dels hipervisors dels servidors HPE i Dell, evitant així la corrupció dels sistemes de fitxers de les bases de dades i pèrdues d'informació a les cabines d'emmagatzematge.

---

## 1.4 Seguretat Física

La protecció dels actius materials i de la infraestructura de dades de **Innovate Tech** es basa en l'establiment de perímetres de seguretat concèntrics per mitigar riscs d'intrusisme, sabotatge o catàstrofes ambientals a la sala de servidors.

### Control d'Accés de Doble Factor (2FA)

L'entrada a la sala de racks està restringida exclusivament al personal tècnic autoritzat mitjançant un sistema d'autenticació obligatori de doble factor:
* **Primer Factor (Posseïdor):** Lector de targetes electromagnètiques de proximitat amb tecnologia encriptada **RFID Mifare Desfire EV3**.
* **Segon Factor (Biometria):** Lector d'empremta dactilar d'alta resolució amb detecció de pols viu per evitar falsificacions.
* **Registre d'Auditoria:** Totes les obertures, intents fallits i temps de permanència queden registrats de forma inalterable en una base de dades centralitzada del sistema de control d'accessos, blindada contra modificacions.

### Sistemes de Videovigilància (CCTV)

La sala disposa de càmeres de seguretat IP com resolució 4K i visió nocturna per infrarojos. Es col·loquen de manera estratègica per cobrir l'angle de visió de l'accés principal, així com els passadissos frontal i posterior dels armaris rack. L'enregistrament de les imatges es realitza en un gravador de xarxa (NVR) dedicat i aïllat, que manté un històric de gravacions de 30 dias sota custòdia segons la normativa vigent de protecció de dades.

### Prevenció i Protecció Contra Incendis

Atès que l'aigua danyaria irreversiblement el maquinari actiu, la sala està equipada amb un sistema d'extinció automàtica mitjançant inundació de **gas net (mecanisme Agent Net FK-5-1-12)**. 
* **Funcionament:** En detectar fum o un increment anòmal de temperatura mitjançant els sensors òptics i tèrmics creuats, el sistema activa una alarma acústica de pre-avís per a l'evacuació del personal i, posteriorment, injecta el gas a la sala. Aquest compost extingeix el foc per refredament tèrmic a nivell molecular sense reduir l'oxigen dràsticament i sense deixar cap mena de residu conductor ni corrosiu sobre els circuits dels servidors.

### Vistes generals del CPD

#### Vista exterior del CPD
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/0880f022-a5ee-4732-9172-f67748662547" />

#### Vista interior del CPD
<img width="1024" height="514" alt="image" src="https://github.com/user-attachments/assets/860ef679-1932-44f0-ae1f-2244c96c358d" />

---

## Prevenció de Riscos Laborals (PRL) al CPD

La seguretat, la salut i la integritat física del personal tècnic que opera i realitza tasques de manteniment dins del CPD de **Innovate Tech** es una prioritat absoluta. Ateses les condicions particulars d'una sala de servidors (risc elèctric, càrrega tèrmica, soroll continu i ús de gasos d'extinció), s'apliquen de manera estricta les següents mesures de prevenció:

| Mesura de Prevenció | Il·lustració | Descripció Detallada |
| :--- | :---: | :--- |
| **Procediment LOTO** | <img width="235" height="150" alt="image" src="https://github.com/user-attachments/assets/852d5dd8-ed81-4ed6-8305-7ec4589e87b4" /> | **Aïllament Elèctric Segur:** Protocol obligatori de bloqueig/etiquetatge (*Lockout/Tagout*) abans de qualsevol intervenció a les línies de distribució elèctrica o PDUs. El tècnic bloqueja físicament el tall d'energia amb un cadenat personalitzat i una targeta d'avís per evitar que es restableixi el corrent accidentalment. |
| **Formació en Emergències** | <img width="126" height="175" alt="Captura de pantalla de 2026-05-21 12-56-23" src="https://github.com/user-attachments/assets/aded3901-969a-410c-bb0d-2af9412ae5ef" /> | **Simulacres i Evacuació:** Formació periòdica sobre protocols d'actuació i reconeixement de l'alarma acústica/visual de pre-avís del sistema d'extinció per gas **FK-5-1-12**, assegurant que els operadors sàpiguen que disposen d'un marge de temps segur per evacuar la sala. |
| **Protecció Auditiva** | <img width="119" height="136" alt="Captura de pantalla de 2026-05-21 12-58-49" src="https://github.com/user-attachments/assets/65002e6a-fb8e-4128-b3c2-6aa75c5d88ea" /> | **Ús Obligatori d'EPIs:** Senyalització de la sala per a la permanència prolongada. Es posen a disposició dels tècnics protectors auditius (taps o orelleres d'atenuació) a l'entrada del recinte per evitar la fatiga acústica. |
| **Gestió del Soroll** | <img width="160" height="60" alt="Captura de pantalla de 2026-05-21 12-58-55" src="https://github.com/user-attachments/assets/e8f48602-51ba-4f13-a4a8-f8c0b18cc22b" /> | **Monitorització i Atenuació:** Control continu dels nivells de decibels generats pels ventiladors d'alta pressió dels servidors i els sistemes de climatització per assegurar un entorn de treball salubre. |
| **Espais de Pas i Il·luminació** | <img width="102" height="93" alt="Captura de pantalla de 2026-05-21 13-14-43" src="https://github.com/user-attachments/assets/948e7204-6d2b-4c3b-94f0-4dce2d2f6744" />| **Vies d'Evacuació i Visibilitat:** Els passadissos (inclòs el passadís fred) es mantenen 100% lliures d'obstacles per garantir una evacuació ràpida. S'instal·len panells LED d'alta uniformitet per reduir la fatiga visual durant la manipulació de components de precisió. |
| **Primers Auxilis** | <img width="102" height="93" alt="Captura de pantalla de 2026-05-21 13-14-43" src="https://github.com/user-attachments/assets/037f2406-7082-4105-9de0-dbbc0253ae18" />| **Equipament d'Emergència:** Armari de primers auxilis clarament visible i senyalitzat amb material específic per a cremades lleus i talls, recolzat per personal de l'empresa format en reanimació cardiopulmonar (RCR). |

---

## 1.5 Sostenibilitat i Eficiència Energètica

L'objectiu prioritari del CPD de **Innovate Tech** és establir un model d'infraestructura d'alta disponibilitat que minimitzi l'impacte ambiental. Per aconseguir-ho, s'integren tecnologies d'optimització física, lògica i de subministrament energètic basades en els següents pilars:

### Monitorització i Consolidació Lògica
* **Control del PUE:** S'implementa una monitorització constant de l'eficiència en l'ús de l'energia (*Power Usage Effectiveness*), amb l'objectiu de mantenir un ràtio ideal **<1.4** mitjançant sensors intel·ligents de cabal i temperatura.
* **Virtualització Avançada:** S'aprofita al màxim la consolidació de càrregues de treball utilitzant els hipervisors **Proxmox VE** i **VMware ESXi**. Això permet reduir el *footprint* físic de la sala a només dos racks i optimitzar el consum elèctric per cada instància o servei de streaming de la companyia.
* **Polítiques de Power Capping i vMotion:** Els servidors utilitzen funcions de *Power Capping* per limitar de forma programada els pics de consum inesperats. A més, s'executen migracions en calent (*vMotion*) per reequilibrar les màquines virtuals, la qual cosa permet apagar o posar en estat de baix consum els nodes físics ociosos durant les hores de menor demanda de xarxa.

### Subministrament d'Energia Verda
* **Autoconsum Fotovoltaic:** S'integra un sistema de panells solars a la coberta de l'edifici orientat a cobrir una part significativa de la demanda elèctrica diürna del CPD, reduint dràsticament la dependència directa de la xarxa elèctrica comercial.
* **Contractació Renovable Certificada (PPA):** Per al diferencial de potència que no es pugui cobrir amb les plaques solars, es contracta el subministrament mitjançant acords PPA (*Power Purchase Agreement*) amb comercialitzadores que garanteixen un origen 100% renovable (eòlica, hidràulica o solar) recolzat per certificacions oficials de *Green Energy*.

### Disseny Físic i Arquitectura de Cablejat
* **Estalvi en Longitud de Cable:** La distribució acurada dels equips actius i dels *Patch Panels* dins dels dos racks es planifica per minimitzar la longitud necessària del cablejat de coure i fibra òptica, evitant pèrdues per atenuació i reduint l'ús de materials.
* **Backbone de Fibra Òptica:** S'utilitza de forma prioritària la fibra òptica per a les connexions de *backbone* inter-rack i enllaços d'alta velocitat cap al *core*. Això no només millora el rendiment i el rendiment per watt, sinó que disminueix el volum de coure utilitzat, material que presenta un impacte ambiental molt més elevat en la seva cadena de producció.

### Climatització Tèrmica i Circulació d'Aire
* **Contenció de Passadís Fred (CAC):** El disseny mecànic de la sala tanca completament el passadís o els servidors aspiren l'aire fresc generat pels climatitzadors. Això evita de forma radical que l'aire fred es barregi amb el flux d'aire calent expulsat per la part posterior dels racks, maximitzant el rendiment tèrmic del sistema.
* **Tecnologia Free Cooling:** El sistema de climatització reaprofita de forma intel·ligent les temperatures exteriors quan les condicions ambientals ho permeten. El refredament natural redueix al mínim les hores de funcionament dels compressors mecànics de l'aire condicionat, disminuint el consum elèctric global de la infraestructura.

### Hardware i Components d'Alta Eficiència
* **Electrònica de Xarxa Intel·ligent (EEE):** Els switches del CPD es configuren amb el protocol *Energy Efficient Ethernet* (**IEEE 802.3az**), el qual disminueix automàticament l'energia subministrada als ports de xarxa que estiguin en períodes d'inactivitat o baixa utilització de trànsit.
* **Fonts d'Alimentació Platinum i Titanium:** Tots els servidors de producció equipen fonts d'alimentació redundants amb certificació **80 Plus Platinum o Titanium**, garantint una eficiència de conversió elèctrica superior al 94%.
* **Processadors i Emmagatzematge d'Alta Eficiència per Watt:** La selecció de processadors de la gamma **Intel Xeon Silver** equilibra la potència de càlcul amb la dissipació tèrmica. Al mateix temps, l'ús exclusiu d'unitats d'estat sòlid (**SSD**) redueix el consum en comparació amb els discos mecànics clàssics i disminueix la necessitat de refrigeració interna de les cabines.
* **Certificació Energy Star:** Qualsevol equipament informàtic i elèctric de nova adquisició implementat al CPD (servidors, switches, SAIs o elements de monitorització) compta amb aquest segell regulador d'alta eficiència energètica.

---

## 1.7 Investigar i Comparar: Solucions Cloud i Sostenibilitat

Per avaluar l'eficiència energètica i les solucions de CPD en el núvol (estructures gestionades i de contingut), s'ha realitzat una investigació i comparativa tècnica d'**AWS** en relació amb els altres dos proveïdors líders del mercat global: **Microsoft Azure** i **Google Cloud Platform (GCP)**.

### Criteris Tècnics de Comparació

* **PUE (Power Usage Effectiveness):** Indicador de l'eficiència de l'ús de l'energia al CPD. Com més proper a 1.0, major és el percentatge elèctric destinat exclusivament a la potència de càlcul.
* **Ús d'Energies Renovables:** Percentatge real de subministrament provinent de fonts netes i projectes d'autoconsum lligats als seus centres de dades.
* **Certificacions i Eines de Gestió del Carboni:** Utilitats i panells (*dashboards*) operatius que els proveïdors posen a disposició de l'usuari per monitoritzar l'empremta de CO₂ dels seus serveis actius.
* **Solucions de CPD Administrats (Managed Services):** Capacitat per absorbir requeriments crítics de seguretat física, lògica, elasticitat i alta disponibilitat de xarxa per al nostre desplegament.

---

### Anàlisi per Proveïdor

#### 1. AWS (Amazon Web Services) — *Solució Seleccionada*
* **Mètriques PUE:** Registra valors d'eficiència d'entre **1.1 i 1.2** en els seus centres de dades més recents, amb un full de ruta per assolir de manera generalitzada un ràtio de 1.05.
* **Energia Renovable:** Assoliment del **100% d'energia renovable** en les seves operacions globals (fomentat per grans acords de PPAs solars i eòlics).
* **Innovació i Certificacions:** Membre de la *Clean Energy Buyers Alliance* (CEBA) i el *Green Power Partnership*. Destaca el disseny de xips propis d'alta eficiència (**AWS Graviton**) que redueixen dràsticament el consum elèctric per a entorns de computació.
* **Eines de Petjada de Carboni:** Integra la utilitat **AWS Carbon Footprint Tool**, ideal perquè l'equip d'administració de *Innovate Tech* auditi l'impacte d'emissions derivat de la computació i emmagatzematge.
* **Serveis Administrats del CPD:** Ofereix un ecosistema madur de màxima resiliència (EC2, S3, RDS, VPC) amb una xarxa perimetral global dissenyada específicament per a tasques d'alta demanda de xarxa.

#### 2. Microsoft Azure
* **Mètriques PUE:** Registra ràtios de PUE per sota de **1.25** a la seva xarxa d'infraestructures, invertint regularment en recerca de sistemes de refrigeració líquida i per immersió.
* **Energia Renovable:** Objectiu del 100% d'energia verda plenament operatiu amb grans fons de finançament per a la descarbonització.
* **Innovació i Certificacions:** Posicionat fortament en auditories sectorials com la **ISO 50001** (Sistemes de Gestió Energètica) i estàndards de sostenibilitat LEED.
* **Eines de Petjada de Carboni:** Compta amb el portal **Microsoft Cloud for Sustainability** i eines integrades a l'*Azure Cost Management* per auditar el consum de l'arquitectura.
* **Serveis Administrats del CPD:** Sòlida alternativa en configuracions IaaS i PaaS (Azure VMs, SQL Database), recolzada per una forta capa de certificacions globals de compliment de seguretat.

#### 3. Google Cloud Platform (GCP)
* **Mètriques PUE:** Líder de la indústria amb mitjanes globals de PUE de **1.1**, aconseguint ràtios inferiors gràcies a l'aplicació d'intel·ligència artificial (Machine Learning) aplicada al control dinàmic de la climatització.
* **Energia Renovable:** Opera amb un model de compensació del 100% d'energies renovables, amb el ferm compromís d'assolir energia completament lliure de carboni les 24 hores del dia, els 7 dies de la setmana per a l'any 2030.
* **Innovació i Certificacions:** Pioner en l'optimització de data centers mitjançant algorismes de DeepMind i membre actiu de l'aliança global RE100.
* **Eines de Petjada de Carboni:** Disposa del panell **Carbon Footprint** directament a la consola de GCP amb mètriques en temps real del projecte, a més d'alertes automatitzades (*Active Assist*) per eliminar recursos inactius.
* **Serveis Administrats del CPD:** Enfocament natiu en tecnologies de contenidors (GKE), emmagatzematge massiu d'objectes (Cloud Storage) i una xarxa global de fibra òptica d'alta velocitat.

---

### Conclusió i Justificació de la Selecció d'AWS

Tot i que els tres *hyperscalers* presenten compromisos mediambientals excel·lents i infraestructures altament eficients, l'elecció d'**AWS** com a proveïdor per al desplegament híbrid de **Innovate Tech** es justifica plenament sota els següents criteris clau:

1. **Ecosistema Multimedia i Streaming:** AWS compta amb serveis especialitzats i madurs que són el nucli de la nostra activitat de contingut digital, com ara **AWS Elemental MediaServices** i la xarxa de distribució de contingut de baixa latència **AWS CloudFront (CDN)**.
2. **Eficiència de Computació:** La presència d'instàncies basades en arquitectura **Graviton** ens permet llogar capacitats de càlcul cloud amb fins a un 60% menys de consum energètic respecte a les arquitectures de processadors tradicionals.
3. **Robustesa en Seguretat Administrada:** AWS encapsula i gestiona directament tots els requisits de seguretat física dels seus centres de dades (controls d'accés biomètric, vigilància 24/7) i lògica (aïllament per defecte a nivell d'hipervisor), garantint el compliment automàtic de normatives internacionals crítiques com la **ISO 27001**, **SOC 2** i **PCI-DSS**.

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

## 1.3 Infraestructura Elèctrica: Dimensionament del SAI

El disseny elèctric del centre de dades de **Innovate Tech** s'ha calculat per garantir l'alta disponibilitat, la redundància de línia i la immunitat davant de pertorbacions de la xarxa elèctrica externa (sobretensions, pics de corrent o talls de subministrament). Per fer-ho, es disposa d'una arquitectura d'alimentació doble (Línia A i Línia B) on cada rack es nodreix d'un sistema independent de **Sistemes d'Alimentació Ininterrompuda (SAI)** de tecnologia Online de doble conversió.

### Inventari de Consum Elèctric (Estudi de Càrregues)

Per dimensionar correctament la capacitat dels SAI, s'estableix el consum nominal mitjà dels equips actius instal·lats en ambdós armaris rack:

| Component Maquinari | Quantitat | Consum Unitari Nominals (W) | Consum Total Atansat (W) |
| :--- | :---: | :---: | :---: |
| Servidor HPE ProLiant DL380 Gen10 (Rack 1) | 2 | 450 W | 900 W |
| Servidor Dell PowerEdge R540 (Rack 2) | 2 | 350 W | 700 W |
| Switch Principal Cisco Catalyst C9200L (Rack 1) | 1 | 100 W | 100 W |
| Switch de Backup Cisco Catalyst C1000L (Rack 2) | 1 | 30 W | 30 W |
| Unitat Central KVM i Pantalles de Gestió | 2 | 40 W | 80 W |
| **Càrrega Nominal Total Activa ($P_{total}$)** | - | - | **1.810 W** |

### Càlcul de la Potència Requerida del SAI

Per fer la transició de la potència activa calculada en Watts ($W$) cap a la potència aparent que defineix la capacitat de treball d'un SAI en Voltamperis ($VA$), s'aplica el factor de potència típic de les fonts d'alimentació informàtiques modernes amb correcció activa ($f_p = 0,9$).

A més, seguint les recomanacions de la normativa **TIA-942**, s'afegeix un **marge de seguretat i futur creixement del 25%** ($\text{Marge} = 1,25$) per evitar que el sistema operi prop del llindar de sobrecàrrega i permetre l'addició de nous nodes informàtics a mitjà termini.

La fórmula utilitzada per determinar la potència aparent mínima és:

$$S_{mínima} = \frac{P_{total} \cdot \text{Marge}}{f_p}$$

Substituint els valors calculats en l'estudi de càrregues:

$$S_{mínima} = \frac{1.810 \text{ W} \cdot 1,25}{0,9} = \frac{2.262,5}{0,9} \approx 2.514 \text{ VA}$$

### Selecció i Justificació del Model de SAI

Donat que la càrrega crítica total del projecte requereix un mínim de $2.514 \text{ VA}$ distribuïts en configuració redundant per donar servei a les línies A i B de tots dos armaris, es justifica la implementació dels mòduls ja previstos en l'esquema físic: **APC Smart-UPS X 2200VA** en paral·lel per a cada armari.

* **Capacitat Total Instal·lada:** Cada armari disposa de dues unitats APC de 2200VA cadascuna (aportant un total de 4400VA per bastidor). Això garanteix que, en condicions normals, els SAI treballen a un règim del **41% de la seva capacitat màxima**, un punt òptim que maximitza l'eficiència energètica de l'inversor i redueix l'estrès tèrmic dels components interns.
* **Redundància:** L'arquitectura opera en mode tolerant a fallades. Si un dels SAI s'ha de desconnectar per manteniment o pateix una avaria en les seves bateries, l'altre mòdul de la línia bessona assumeix immediatament el 100% de la línia de càrrega elèctrica sense cap mil·lisegon de tall (temps de transferència de 0 ms gràcies a la tecnologia *Double-Conversion Online*).

### Càlcul d'Autonomia i Gestió d'Apagat Net

Amb una corba de descàrrega típica del model seleccionat funcionant a mitja càrrega (uns 905 W per armari), el banc de bateries integrat de plom-àcid segellat (AGM) garanteix una **autonomia d'emergència de 22 minuts**.

Aquest temps d'autonomia es distribueix seguint el protocol de seguretat operacional de l'empresa:
1. **Minuts 0 a 5 (Fase d'Espera):** El sistema es manté operant amb normalitat a l'espera que el subministrament elèctric de la xarxa pública es restableixi de forma automàtica.
2. **Minuts 5 a 15 (Alerta i Pre-apagat):** Es disparen els dimonis de gestió de l'UPS a través de la xarxa (*PowerChute Network Shutdown*). Es bloquegen les noves connexions d'usuaris externs i es comença la migració o tancament dels serveis no crítics.
3. **Minuts 15 a 20 (Apagat Net / Clean Shutdown):** S'envia l'ordre de tancament segur a les màquines virtuals de producció, seguit de l'apagat dels hipervisors dels servidors HPE i Dell, evitant així la corrupció dels sistemes de fitxers de les bases de dades i pèrdues d'informació a les cabines d'emmagatzematge.

## 1.4 Seguretat Física

La protecció dels actius materials i de la infraestructura de dades de **Innovate Tech** es basa en l'establiment de perímetres de seguretat concèntrics per mitigar riscs d'intrusisme, sabotatge o catàstrofes ambientals a la sala de servidors.

### Control d'Accés de Doble Factor (2FA)

L'entrada a la sala de racks està restringida exclusivament al personal tècnic autoritzat mitjançant un sistema d'autenticació obligatori de doble factor:
* **Primer Factor (Posseïdor):** Lector de targetes electromagnètiques de proximitat amb tecnologia encriptada **RFID Mifare Desfire EV3**.
* **Segon Factor (Biometria):** Lector d'empremta dactilar d'alta resolució amb detecció de pols viu per evitar falsificacions.
* **Registre d'Auditoria:** Totes les obertures, intents fallits i temps de permanència queden registrats de forma inalterable en una base de dades centralitzada del sistema de control d'accessos, blindada contra modificacions.

### Sistemes de Videovigilància (CCTV)

La sala disposa de càmeres de seguretat IP amb resolució 4K i visió nocturna per infrarojos. Es col·loquen de manera estratègica per cobrir l'angle de visió de l'accés principal, així com els passadissos frontal i posterior dels armaris rack. L'enregistrament de les imatges es realitza en un gravador de xarxa (NVR) dedicat i aïllat, que manté un històric de gravacions de 30 dies sota custòdia segons la normativa vigent de protecció de dades.

### Prevenció i Protecció Contra Incendio

Atès que l'aigua danyaria irreversiblement el maquinari actiu, la sala està equipada amb un sistema d'extinció automàtica mitjançant inundació de **gas net (mecanisme Agent Net FK-5-1-12)**. 
* **Funcionament:** En detectar fum o un increment anòmal de temperatura mitjançant els sensors òptics i tèrmics creuats, el sistema activa una alarma acústica de pre-avís per a l'evacuació del personal i, posteriorment, injecta el gas a la sala. Aquest compost extingeix el foc per refredament tèrmic a nivell molecular sense reduir l'oxigen dràsticament i sense deixar cap mena de residu conductor ni corrosiu sobre els circuits dels servidors.

### Vista exterior del CPD
<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/0880f022-a5ee-4732-9172-f67748662547" />

### Vista interior del CPD
<img width="1024" height="514" alt="image" src="https://github.com/user-attachments/assets/860ef679-1932-44f0-ae1f-2244c96c358d" />

## Prevenció de Riscos Laborals (PRL) al CPD

La seguretat, la salut i la integritat física del personal tècnic que opera i realitza tasques de manteniment dins del CPD de **Innovate Tech** és una prioritat absoluta. Ateses les condicions particulars d'una sala de servidors (risc elèctric, càrrega tèrmica, soroll continu i ús de gasos d'extinció), s'apliquen de manera estricta les següents mesures de prevenció:

| Mesura de Prevenció | Il·lustració | Descripció Detallada |
| :--- | :---: | :--- |
| **Procediment LOTO** | <img width="235" height="150" alt="image" src="https://github.com/user-attachments/assets/852d5dd8-ed81-4ed6-8305-7ec4589e87b4" /> | **Aïllament Elèctric Segur:** Protocol obligatori de bloqueig/etiquetatge (*Lockout/Tagout*) abans de qualsevol intervenció a les línies de distribució elèctrica o PDUs. El tècnic bloqueja físicament el tall d'energia amb un cadenat personalitzat i una targeta d'avís per evitar que es restableixi el corrent accidentalment. |
| **Formació en Emergències** | <img width="126" height="175" alt="Captura de pantalla de 2026-05-21 12-56-23" src="https://github.com/user-attachments/assets/aded3901-969a-410c-bb0d-2af9412ae5ef" /> | **Simulacres i Evacuació:** Formació periòdica sobre protocols d'actuació i reconeixement de l'alarma acústica/visual de pre-avís del sistema d'extinció per gas **FK-5-1-12**, assegurant que els operadors sàpiguen que disposen d'un marge de temps segur per evacuar la sala. |
| **Protecció Auditiva** | <img width="119" height="136" alt="Captura de pantalla de 2026-05-21 12-58-49" src="https://github.com/user-attachments/assets/65002e6a-fb8e-4128-b3c2-6aa75c5d88ea" /> | **Ús Obligatori d'EPIs:** Senyalització de la sala per a la permanència prolongada. Es posen a disposició dels tècnics protectors auditius (taps o orelleres d'atenuació) a l'entrada del recinte per evitar la fatiga acústica. |
| **Gestió del Soroll** | <img width="160" height="60" alt="Captura de pantalla de 2026-05-21 12-58-55" src="https://github.com/user-attachments/assets/e8f48602-51ba-4f13-a4a8-f8c0b18cc22b" /> | **Monitorització i Atenuació:** Control continu dels nivells de decibels generats pels ventiladors d'alta pressió dels servidors i els sistemes de climatització per assegurar un entorn de treball salubre. |
| **Espais de Pas i Il·luminació** | <img width="102" height="93" alt="Captura de pantalla de 2026-05-21 13-14-43" src="https://github.com/user-attachments/assets/948e7204-6d2b-4c3b-94f0-4dce2d2f6744" />| **Vies d'Evacuació i Visibilitat:** Els passadissos (inclòs el passadís fred) es mantenen 100% lliures d'obstacles per garantir una evacuació ràpida. S'instal·len panells LED d'alta uniformitat per reduir la fatiga visual durant la manipulació de components de precisió. |
| **Primers Auxilis** |<img width="102" height="93" alt="Captura de pantalla de 2026-05-21 13-14-43" src="https://github.com/user-attachments/assets/037f2406-7082-4105-9de0-dbbc0253ae18" />| **Equipament d'Emergència:** Armari de primers auxilis clarament visible i senyalitzat amb material específic per a cremades lleus i talls, recolzat per personal de l'empresa format en reanimació cardiopulmonar (RCR). |

## 1.5 Sostenibilitat i Eficiència Energètica

L'objectiu prioritari del CPD de **Innovate Tech** és establir un model d'infraestructura d'alta disponibilitat que minimitzi l'impacte ambiental. Per aconseguir-ho, s'integren tecnologies d'optimització física, lògica i de subministrament energètic basades en els següents pilars:

### Monitorització i Consolidació Lògica
* **Control del PUE:** S'implementa una monitorització constant de l'eficiència en l'ús de l'energia (*Power Usage Effectiveness*), amb l'objectiu de mantenir un ràtio ideal **<1.4** mitjançant sensors intel·ligents de cabal i temperatura.
* **Virtualització Avançada:** S'aprofita al màxim la consolidació de càrregues de treball utilitzant els hipervisors **Proxmox VE** i **VMware ESXi**. Això permet reduir el *footprint* físic de la sala a només dos racks i optimitzar el consum elèctric per cada instància o servei de streaming de la companyia.
* **Polítiques de Power Capping i vMotion:** Els servidors utilitzen funcions de *Power Capping* per limitar de forma programada els pics de consum inesperats. A més, s'executen migracions en calent (*vMotion*) per reequilibrar les màquines virtuals, la qual cosa permet apagar o posar en estat de baix consum els nodes físics ociosos durant les hores de menor demanda de xarxa.

### Subministrament d'Energia Verda
* **Autoconsum Fotovoltaic:** S'integra un sistema de panells solars a la coberta de l'edifici orientat a cobrir una part significativa de la demanda elèctrica diürna del CPD, reduint dràsticament la dependència directa de la xarxa elèctrica comercial.
* **Contractació Renovable Certificada (PPA):** Per al diferencial de potència que no es pugui cobrir amb les plaques solars, es contracta el subministrament mitjançant acords PPA (*Power Purchase Agreement*) amb comercialitzadores que garanteixen un origen 100% renovable (eòlica, hidràulica o solar) recolzat per certificacions oficials de *Green Energy*.

### Disseny Físic i Arquitectura de Cablejat
* **Estalvi en Longitud de Cable:** La distribució acurada dels equips actius i dels *Patch Panels* dins dels dos racks es planifica per minimitzar la longitud necessària del cablejat de coure i fibra òptica, evitant pèrdues per atenuació i reduint l'ús de materials.
* **Backbone de Fibra Òptica:** S'utilitza de forma prioritària la fibra òptica per a les connexions de *backbone* inter-rack i enllaços d'alta velocitat cap al *core*. Això no només millora el rendiment i el rendiment per watt, sinó que disminueix el volum de coure utilitzat, material que presenta un impacte ambiental molt més elevat en la seva cadena de producció.

### Climatització Tèrmica i Circulació d'Aire
* **Contenció de Passadís Fred (CAC):** El disseny mecànic de la sala tanca completament el passadís on els servidors aspiren l'aire fresc generat pels climatitzadors. Això evita de forma radical que l'aire fred es barregi amb el flux d'aire calent expulsat per la part posterior dels racks, maximitzant el rendiment tèrmic del sistema.
* **Tecnologia Free Cooling:** El sistema de climatització reaprofita de forma intel·ligent les temperatures exteriors quan les condicions ambientals ho permeten. El refredament natural redueix al mínim les hores de funcionament dels compressors mecànics de l'aire condicionat, disminuint el consum elèctric global de la infraestructura.

### Hardware i Components d'Alta Eficiència
* **Electrònica de Xarxa Intel·ligent (EEE):** Els switches del CPD es configuren amb el protocol *Energy Efficient Ethernet* (**IEEE 802.3az**), el qual disminueix automàticament l'energia subministrada als ports de xarxa que estiguin en períodes d'inactivitat o baixa utilització de trànsit.
* **Fonts d'Alimentació Platinum i Titanium:** Tots els servidors de producció equipen fonts d'alimentació redundants amb certificació **80 Plus Platinum o Titanium**, garantint una eficiència de conversió elèctrica superior al 94%.
* **Processadors i Emmagatzematge d'Alta Eficiència per Watt:** La selecció de processadors de la gamma **Intel Xeon Silver** equilibra la potència de càlcul amb la dissipació tèrmica. Al mateix temps, l'ús exclusiu d'unitats d'estat sòlid (**SSD**) redueix el consum en comparació amb els discos mecànics clàssics i disminueix la necessitat de refrigeració interna de les cabines.
* **Certificació Energy Star:** Qualsevol equipament informàtic i elèctric de nova adquisició implementat al CPD (servidors, switches, SAIs o elements de monitorització) compta amb aquest segell regulador d'alta eficiència energètica.



## 1.7 Investigar i Comparar: Solucions Cloud i Sostenibilitat

Per avaluar l'eficiència energètica i les solucions de CPD en el núvol (estructures gestionades i de contingut), s'ha realitzat una investigació i comparativa tècnica d'**AWS** en relació amb els altres dos proveïdors líders del mercat global: **Microsoft Azure** i **Google Cloud Platform (GCP)**.

### Criteris Tècnics de Comparació

* **PUE (Power Usage Effectiveness):** Indicador de l'eficiència de l'ús de l'energia al CPD. Com més proper a 1.0, major és el percentatge elèctric destinat exclusivament a la potència de càlcul.
* **Ús d'Energies Renovables:** Percentatge real de subministrament provinent de fonts netes i projectes d'autoconsum lligats als seus centres de dades.
* **Certificacions i Eines de Gestió del Carboni:** Utilitats i panells (*dashboards*) operatius que els proveïdors posen a disposició de l'usuari per monitoritzar l'empremta de CO₂ dels seus serveis actius.
* **Solucions de CPD Administrats (Managed Services):** Capacitat per absorbir requeriments crítics de seguretat física, lògica, elasticitat i alta disponibilitat de xarxa per al nostre desplegament.

---

### Anàlisi per Proveïdor

#### 1. AWS (Amazon Web Services) — *Solució Seleccionada*
* **Mètriques PUE:** Registra valors d'eficiència d'entre **1.1 i 1.2** en els seus centres de dades més recents, amb un full de ruta per assolir de manera generalitzada un ràtio de 1.05.
* **Energia Renovable:** Assoliment del **100% d'energia renovable** en les seves operacions globals (fomentat per grans acords de PPAs solars i eòlics).
* **Innovació i Certificacions:** Membre de la *Clean Energy Buyers Alliance* (CEBA) i el *Green Power Partnership*. Destaca el disseny de xips propis d'alta eficiència (**AWS Graviton**) que redueixen dràsticament el consum elèctric per a entorns de computació.
* **Eines de Petjada de Carboni:** Integra la utilitat **AWS Carbon Footprint Tool**, ideal perquè l'equip d'administració de *Innovate Tech* auditi l'impacte d'emissions derivat de la computació i emmagatzematge.
* **Serveis Administrats del CPD:** Ofereix un ecosistema madur de màxima resiliència (EC2, S3, RDS, VPC) amb una xarxa perimetral global dissenyada específicament per a tasques d'alta demanda de xarxa.

#### 2. Microsoft Azure
* **Mètriques PUE:** Registra ràtios de PUE per sota de **1.25** a la seva xarxa d'infraestructures, invertint regularment en recerca de sistemes de refrigeració líquida i per immersió.
* **Energia Renovable:** Objectiu del 100% d'energia verda plenament operatiu amb grans fons de finançament per a la descarbonització.
* **Innovació i Certificacions:** Posicionat fortament en auditories sectorials com la **ISO 50001** (Sistemes de Gestió Energètica) i estàndards de sostenibilitat LEED.
* **Eines de Petjada de Carboni:** Compta amb el portal **Microsoft Cloud for Sustainability** i eines integrades a l'*Azure Cost Management* per auditar el consum de l'arquitectura.
* **Serveis Administrats del CPD:** Sòlida alternativa en configuracions IaaS i PaaS (Azure VMs, SQL Database), recolzada per una forta capa de certificacions globals de compliment de seguretat.

#### 3. Google Cloud Platform (GCP)
* **Mètriques PUE:** Líder de la indústria amb mitjanes globals de PUE de **1.1**, aconseguint ràtios inferiors gràcies a l'aplicació d'intel·ligència artificial (Machine Learning) aplicada al control dinàmic de la climatització.
* **Energia Renovable:** Opera amb un model de compensació del 100% d'energies renovables, amb el ferm compromís d'assolir energia completament lliure de carboni les 24 hores del dia, els 7 dies de la setmana per a l'any 2030.
* **Innovació i Certificacions:** Pioner en l'optimització de data centers mitjançant algorismes de DeepMind i membre actiu de l'aliança global RE100.
* **Eines de Petjada de Carboni:** Disposa del panell **Carbon Footprint** directament a la consola de GCP amb mètriques en temps real del projecte, a més d'alertes automatitzades (*Active Assist*) per eliminar recursos inactius.
* **Serveis Administrats del CPD:** Enfocament natiu en tecnologies de contenidors (GKE), emmagatzematge massiu d'objectes (Cloud Storage) i una xarxa global de fibra òptica d'alta velocitat.

---

### Conclusió i Justificació de la Selecció d'AWS

Tot i que els tres *hyperscalers* presenten compromisos mediambientals excel·lents i infraestructures altament eficients, l'elecció d'**AWS** com a proveïdor per al desplegament híbrid de **Innovate Tech** es justifica plenament sota els següents criteris clau:

1. **Ecosistema Multimedia i Streaming:** AWS compta amb serveis especialitzats i madurs que són el nucli de la nostra activitat de contingut digital, com ara **AWS Elemental MediaServices** i la xarxa de distribució de contingut de baixa latència **AWS CloudFront (CDN)**.
2. **Eficiència de Computació:** La presència d'instàncies basades en arquitectura **Graviton** ens permet llogar capacitats de càlcul cloud amb fins a un 60% menys de consum energètic respecte a les arquitectures de processadors tradicionals.
3. **Robustesa en Seguretat Administrada:** AWS encapsula i gestiona directament tots els requisits de seguretat física dels seus centres de dades (controls d'accés biomètric, vigilància 24/7) i lògica (aïllament per defecte a nivell d'hipervisor), garantint el compliment automàtic de normatives internacionals crítiques com la **ISO 27001**, **SOC 2** i **PCI-DSS**.












# 3. Disseny i Implementació de la Base de Dades

## 3.1 Context del Projecte

**InnovateTech** disposa d'una estructura interna amb diferents departaments (vendes, suport tècnic, administració i logística). Per donar-los suport operatiu, s'ha dissenyat i implementat una **base de dades integral** sobre un servidor EC2 d'AWS que cobreix tres eixos funcionals:

- La **gestió del personal** i l'estructura organitzativa de l'empresa.
- El **sistema de comunicació interna**: registre de trucades, videotrucades i streaming.
- El **control d'accés, seguretat i auditoria** de la base de dades i els sistemes instal·lats.

### Justificació del SGBD escollit

S'ha triat **MySQL** com a sistema gestor de bases de dades per les raons següents:

- **Codi obert i sense cost de llicència**, adequat per a entorns educatius i empresarials de mida mitjana.
- **Compatibilitat total amb triggers, events i rols**, funcionalitats que el projecte exigeix.
- **Integració nativa amb Ansible** per a la seva instal·lació i configuració automatitzada.
- **Desplegament sobre EC2** sense cost addicional (s'evita RDS, que té cost elevat).
- **Àmplia comunitat i documentació**, facilitant el manteniment i la resolució d'incidències.

---

## 3.2 Disseny i Implementació de la Base de Dades

### 3.2.1 Diagrama Entitat-Relació (E/R)

El diagrama E/R reflecteix totes les entitats, atributs i relacions necessàries per cobrir els requisits funcionals del projecte:

```
┌─────────────────┐         ┌──────────────────┐
│  departaments   │◄────────│     empleats     │
│─────────────────│  1   N  │──────────────────│
│ PK id_dept      │         │ PK dni           │
│    nom_dept     │         │    nom           │
│    planta       │         │    cognoms       │
└─────────────────┘         │    correu        │
                            │    salari        │
                            │ FK id_dept       │
                            └────────┬─────────┘
                                     │ 1
                                     │
                                     │ N
                            ┌────────▼─────────┐
                            │     trucades     │
                            │──────────────────│
                            │ PK id_trucada    │
                            │ FK dni_empleat   │
                            │    destinari     │
                            │    durada_minuts │
                            │    data_trucada  │
                            └──────────────────┘

┌──────────────────────────────────────────────┐
│               taula_avisos                   │
│──────────────────────────────────────────────│
│ PK id_avis                                   │
│    usuari         (CURRENT_USER())           │
│    accio_intentada                           │
│    taula_afectada                            │
│    data_hora      (TIMESTAMP automàtic)      │
└──────────────────────────────────────────────┘
```

**Cardinalitats:**
- Un **departament** pot tenir **molts empleats** (1:N).
- Un **empleat** pot realitzar **moltes trucades** (1:N).
- La **taula_avisos** és independent: l'alimenten els triggers d'auditoria.

---

### 3.2.2 Model Relacional

A partir del diagrama E/R, s'obté l'esquema relacional:

| Taula | Atributs | PK | FK |
|-------|----------|----|----|
| `departaments` | id_dept, nom_dept, planta | id_dept | — |
| `empleats` | dni, nom, cognoms, correu, salari, id_dept | dni | id_dept → departaments |
| `trucades` | id_trucada, dni_empleat, destinari, durada_minuts, data_trucada | id_trucada | dni_empleat → empleats |
| `taula_avisos` | id_avis, usuari, accio_intentada, taula_afectada, data_hora | id_avis | — |

**Restriccions d'integritat implementades:**
- `UNIQUE (nom_dept)` — no hi pot haver dos departaments amb el mateix nom.
- `UNIQUE (correu)` — cada empleat té un correu únic.
- `CHECK (salari > 0)` — el salari ha de ser positiu.
- `CHECK (durada_minuts >= 0)` — la durada no pot ser negativa.
- `ON DELETE SET NULL` a `empleats.id_dept` — si s'elimina un departament, l'empleat queda sense departament assignat.
- `ON DELETE CASCADE` a `trucades.dni_empleat` — si s'elimina un empleat, les seves trucades s'eliminen en cascada.

---

### 3.2.3 Script de Creació de la Base de Dades

A continuació es detalla pas a pas el script SQL complet, explicant cada bloc:

#### Pas 1 — Creació de la base de dades i selecció

```sql
-- Crear la base de dades oficial
CREATE DATABASE IF NOT EXISTS innovate_tech;

-- Indicar a MySQL que treballarem dins d'ella
USE innovate_tech;
```

> S'utilitza `IF NOT EXISTS` per evitar errors si el script s'executa més d'una vegada (idempotència).

---

#### Pas 2 — Creació de les taules

```sql
-- Taula de Departaments
CREATE TABLE IF NOT EXISTS departaments (
    id_dept INT AUTO_INCREMENT,
    nom_dept VARCHAR(50) NOT NULL,
    planta INT NOT NULL,
    CONSTRAINT PK_departaments PRIMARY KEY (id_dept),
    CONSTRAINT UN_nom_dept UNIQUE (nom_dept)
);

-- Taula d'Avisos (sistema d'auditoria del Trigger)
CREATE TABLE IF NOT EXISTS taula_avisos (
    id_avis INT AUTO_INCREMENT,
    usuari VARCHAR(100) NOT NULL,
    accio_intentada VARCHAR(50) NOT NULL,
    taula_afectada VARCHAR(50) NOT NULL,
    data_hora TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT PK_taula_avisos PRIMARY KEY (id_avis)
);

-- Taula d'Empleats
CREATE TABLE IF NOT EXISTS empleats (
    dni VARCHAR(9),
    nom VARCHAR(50) NOT NULL,
    cognoms VARCHAR(100) NOT NULL,
    correu VARCHAR(100) NOT NULL,
    salari DECIMAL(10,2) NOT NULL,
    id_dept INT,
    CONSTRAINT PK_empleats PRIMARY KEY (dni),
    CONSTRAINT UN_correu UNIQUE (correu),
    CONSTRAINT CK_salari_positiu CHECK (salari > 0),
    CONSTRAINT FK_empleats_dept FOREIGN KEY (id_dept)
        REFERENCES departaments(id_dept) ON DELETE SET NULL
);

-- Taula de Trucades / Comunicacions
CREATE TABLE IF NOT EXISTS trucades (
    id_trucada INT AUTO_INCREMENT,
    dni_empleat VARCHAR(9) NOT NULL,
    destinari VARCHAR(50) NOT NULL,
    durada_minuts INT NOT NULL,
    data_trucada DATE NOT NULL,
    CONSTRAINT PK_trucades PRIMARY KEY (id_trucada),
    CONSTRAINT CK_durada_positiva CHECK (durada_minuts >= 0),
    CONSTRAINT FK_trucades_empleat FOREIGN KEY (dni_empleat)
        REFERENCES empleats(dni) ON DELETE CASCADE
);
```

**Justificació del disseny:**
- `taula_avisos` es crea **abans** que `empleats` perquè el trigger d'auditoria hi insereix registres en operacions sobre empleats.
- `departaments` es crea **abans** que `empleats` per complir la dependència de la FK.
- `trucades` es crea **al final** perquè depèn d'`empleats`.

---

#### Pas 3 — Inserció de dades de prova

```sql
-- Departaments de prova
INSERT INTO departaments (nom_dept, planta) VALUES
('Administració', 1),
('Vendes', 2),
('Sistemes', 3);

-- Empleats de prova
INSERT INTO empleats (dni, nom, cognoms, correu, salari, id_dept) VALUES
('12345678A', 'Joan',   'Garcia Perez', 'joan@innovatetech.com',   1800.00, 1),
('87654321B', 'Marta',  'Lopez Gomez',  'marta@innovatetech.com',  1500.00, 2),
('11112222C', 'Albert', 'Sanz Roca',    'albert@innovatetech.com', 2500.00, 3);

-- Trucades de prova
INSERT INTO trucades (dni_empleat, destinari, durada_minuts, data_trucada) VALUES
('87654321B', '600111222', 5,  CURDATE()),
('87654321B', '633444555', 12, CURDATE());
```

**Verificació de les dades insertades:**

```sql
SELECT * FROM departaments;
SELECT * FROM empleats;
SELECT * FROM trucades;
```

---

## 3.3 Gestió d'Usuaris, Rols i Permisos

### 3.3.1 Creació de Rols

```sql
-- Creació dels rols exigits pel projecte
CREATE ROLE IF NOT EXISTS 'admin', 'vendes', 'administracio';
```

#### Assignació de permisos per rol

**Rol `admin` — Control total:**
```sql
GRANT ALL PRIVILEGES ON innovate_tech.* TO 'admin';
```

**Rol `administracio` — Gestió de personal:**
```sql
-- Pot consultar, afegir i modificar empleats
GRANT SELECT, INSERT, UPDATE ON innovate_tech.empleats TO 'administracio';
-- Pot consultar departaments (però no modificar-los)
GRANT SELECT ON innovate_tech.departaments TO 'administracio';
```

**Rol `vendes` — Registre de trucades:**
```sql
-- Pot consultar i registrar trucades, però no modificar-les ni eliminar-les
GRANT SELECT, INSERT ON innovate_tech.trucades TO 'vendes';
```

| Rol | Taules accessibles | Operacions permeses | Restriccions |
|-----|--------------------|---------------------|--------------|
| `admin` | Totes | SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, GRANT | Cap |
| `administracio` | `empleats`, `departaments` | SELECT, INSERT, UPDATE | No pot accedir a trucades ni avisos |
| `vendes` | `trucades` | SELECT, INSERT | No pot modificar ni eliminar; no accedeix a empleats |
| `treballador` | `empleats` (lectura) | SELECT | Només lectura; cap accés a salaris ni dades sensibles |

---

### 3.3.2 Script de Creació Automatitzada d'Usuaris (Bash)

L'script `create_user.sh` automatitza la creació d'usuaris MySQL i la generació del fitxer `.sql` corresponent. Accepta múltiples usuaris en una sola execució.

```bash
#!/bin/bash
# ============================================================
# Script: create_user.sh
# Descripció: Creació automatitzada d'usuaris MySQL per a
#             la base de dades innovate_tech d'InnovateTech.
# Ús: bash create_user.sh
# ============================================================

# --- Configuració ---
DB_NAME="innovate_tech"
MYSQL_ROOT_USER="root"
OUTPUT_FILE="usuaris_creats.sql"
ROLS_VALIDS=("admin" "vendes" "administracio" "treballador")

# --- Colors per a la terminal ---
VERD='\033[0;32m'
VERMELL='\033[0;31m'
GROC='\033[1;33m'
NC='\033[0m' # Sense color

# --- Funció: validar si un rol és vàlid ---
rol_valid() {
    local rol="$1"
    for r in "${ROLS_VALIDS[@]}"; do
        [[ "$r" == "$rol" ]] && return 0
    done
    return 1
}

# --- Capçalera del fitxer SQL de sortida ---
echo "-- Fitxer SQL generat automàticament per create_user.sh" > "$OUTPUT_FILE"
echo "-- Data: $(date '+%Y-%m-%d %H:%M:%S')" >> "$OUTPUT_FILE"
echo "USE $DB_NAME;" >> "$OUTPUT_FILE"
echo "" >> "$OUTPUT_FILE"

echo -e "${GROC}=== Script de Creació d'Usuaris MySQL - InnovateTech ===${NC}"
echo ""

# --- Bucle principal: afegir usuaris ---
while true; do
    # Demanar nom d'usuari
    read -rp "Nom d'usuari MySQL (o 'fi' per acabar): " NOM_USUARI
    [[ "$NOM_USUARI" == "fi" ]] && break
    [[ -z "$NOM_USUARI" ]] && echo -e "${VERMELL}El nom no pot estar buit.${NC}" && continue

    # Demanar contrasenya
    read -rsp "Contrasenya per a '$NOM_USUARI': " CONTRASENYA
    echo ""
    [[ -z "$CONTRASENYA" ]] && echo -e "${VERMELL}La contrasenya no pot estar buida.${NC}" && continue

    # Demanar rol
    echo "Rols disponibles: ${ROLS_VALIDS[*]}"
    read -rp "Rol per a '$NOM_USUARI': " ROL
    if ! rol_valid "$ROL"; then
        echo -e "${VERMELL}Error: El rol '$ROL' no és vàlid.${NC}"
        continue
    fi

    # Comprovar si l'usuari ja existeix a MySQL
    EXISTEIX=$(mysql -u"$MYSQL_ROOT_USER" -e \
        "SELECT COUNT(*) FROM mysql.user WHERE User='$NOM_USUARI';" \
        --skip-column-names 2>/dev/null)

    if [[ "$EXISTEIX" -gt 0 ]]; then
        echo -e "${VERMELL}Error: L'usuari '$NOM_USUARI' ja existeix a MySQL.${NC}"
        continue
    fi

    # Generar i executar les sentències SQL
    SQL_CREATE="CREATE USER '${NOM_USUARI}'@'%' IDENTIFIED BY '${CONTRASENYA}';"
    SQL_GRANT="GRANT '${ROL}' TO '${NOM_USUARI}'@'%';"
    SQL_APPLY="SET DEFAULT ROLE '${ROL}' FOR '${NOM_USUARI}'@'%';"
    SQL_FLUSH="FLUSH PRIVILEGES;"

    # Permisos especials per a backups (GRANT FILE per a root i admin)
    if [[ "$ROL" == "admin" ]]; then
        SQL_FILE="GRANT FILE ON *.* TO '${NOM_USUARI}'@'%';"
    fi

    # Executar a MySQL
    mysql -u"$MYSQL_ROOT_USER" -e "$SQL_CREATE $SQL_GRANT $SQL_APPLY $SQL_FLUSH" 2>/dev/null
    if [[ $? -eq 0 ]]; then
        echo -e "${VERD}✔ Usuari '$NOM_USUARI' creat correctament amb el rol '$ROL'.${NC}"

        # Escriure al fitxer .sql
        {
            echo "-- Usuari: $NOM_USUARI | Rol: $ROL"
            echo "$SQL_CREATE"
            echo "$SQL_GRANT"
            echo "$SQL_APPLY"
            [[ -n "$SQL_FILE" ]] && echo "$SQL_FILE"
            echo "$SQL_FLUSH"
            echo ""
        } >> "$OUTPUT_FILE"
    else
        echo -e "${VERMELL}Error en crear '$NOM_USUARI'. Comprova els permisos de root.${NC}"
    fi

    SQL_FILE=""  # Resetar variable de permisos FILE
done

echo ""
echo -e "${VERD}Procés finalitzat. Fitxer SQL generat: ${OUTPUT_FILE}${NC}"
```

**Com executar l'script:**

```bash
# Donar permisos d'execució
chmod +x create_user.sh

# Executar
bash create_user.sh
```

**Exemple de fitxer `usuaris_creats.sql` generat:**

```sql
-- Fitxer SQL generat automàticament per create_user.sh
-- Data: 2026-05-20 10:30:00
USE innovate_tech;

-- Usuari: joan_vendes | Rol: vendes
CREATE USER 'joan_vendes'@'%' IDENTIFIED BY 'Passw0rd!';
GRANT 'vendes' TO 'joan_vendes'@'%';
SET DEFAULT ROLE 'vendes' FOR 'joan_vendes'@'%';
FLUSH PRIVILEGES;

-- Usuari: marta_admin | Rol: admin
CREATE USER 'marta_admin'@'%' IDENTIFIED BY 'S3cur3Pass!';
GRANT 'admin' TO 'marta_admin'@'%';
SET DEFAULT ROLE 'admin' FOR 'marta_admin'@'%';
GRANT FILE ON *.* TO 'marta_admin'@'%';
FLUSH PRIVILEGES;
```

---

### 3.3.3 Triggers per al Control d'Accés i Auditoria

#### Trigger 1 — Control de quotes de trucades (`tg_control_quotes`)

Impedeix que un empleat superi el **límit de 3 trucades diàries** o els **60 minuts mensuals** acumulats.

```sql
DELIMITER //

CREATE TRIGGER tg_control_quotes
BEFORE INSERT ON trucades
FOR EACH ROW
BEGIN
    DECLARE trucades_avui INT;
    DECLARE minuts_mes INT;

    -- 1. Comptar quantes trucades ha fet l'empleat AVUI
    SELECT COUNT(*) INTO trucades_avui
    FROM trucades
    WHERE dni_empleat = NEW.dni_empleat
      AND data_trucada = NEW.data_trucada;

    -- 2. Sumar quants minuts porta acumulats aquest MES
    SELECT IFNULL(SUM(durada_minuts), 0) INTO minuts_mes
    FROM trucades
    WHERE dni_empleat = NEW.dni_empleat
      AND MONTH(data_trucada) = MONTH(NEW.data_trucada)
      AND YEAR(data_trucada)  = YEAR(NEW.data_trucada);

    -- VALIDACIÓ 1: Màxim 3 trucades al dia
    IF trucades_avui >= 3 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Error: L''empleat ja ha superat el límit de 3 trucades diàries.';
    END IF;

    -- VALIDACIÓ 2: Màxim 60 minuts al mes (sumant la nova trucada)
    IF (minuts_mes + NEW.durada_minuts) > 60 THEN
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Error: Aquesta trucada supera el límit de 60 minuts mensuals permesos.';
    END IF;
END //

DELIMITER ;
```

**Com funciona:**

| Situació | Resultat |
|----------|---------|
| L'empleat ha fet 2 trucades avui i en fa una tercera | Permet la inserció |
| L'empleat ha fet 3 trucades avui i intenta una quarta | Bloqueja amb error |
| L'empleat porta 55 minuts al mes i fa una trucada de 4 minuts | Permet (59 min ≤ 60) |
| L'empleat porta 58 minuts al mes i fa una trucada de 5 minuts | Bloqueja (63 min > 60) |

**Prova del trigger:**

```sql
-- Inserir 3 trucades vàlides (passa el control)
INSERT INTO trucades (dni_empleat, destinari, durada_minuts, data_trucada)
VALUES ('87654321B', '611000001', 5, CURDATE());
INSERT INTO trucades (dni_empleat, destinari, durada_minuts, data_trucada)
VALUES ('87654321B', '611000002', 5, CURDATE());
INSERT INTO trucades (dni_empleat, destinari, durada_minuts, data_trucada)
VALUES ('87654321B', '611000003', 5, CURDATE());

-- La 4a trucada ha de ser bloquejada pel trigger
INSERT INTO trucades (dni_empleat, destinari, durada_minuts, data_trucada)
VALUES ('87654321B', '611000004', 5, CURDATE());
-- Resultat esperat: ERROR 1644 (45000): L'empleat ja ha superat el límit de 3 trucades diàries.
```

---

#### Trigger 2 — Auditoria de seguretat (`tg_auditoria_seguretat`)

Registra i bloqueja qualsevol intent de modificar dades d'empleats per part d'un usuari que no sigui `root`. Dissenyat per detectar accessos no autoritzats des d'Ansible o altres sistemes externs.

```sql
DELIMITER //

CREATE TRIGGER tg_auditoria_seguretat
BEFORE UPDATE ON empleats
FOR EACH ROW
BEGIN
    -- Comprovem si l'usuari actual NO és el root del sistema
    -- En AWS, controlarà l'usuari que utilitza Ansible
    IF CURRENT_USER() NOT LIKE 'root@%' THEN

        -- 1. Registrar l'intent d'infracció a la taula d'avisos
        INSERT INTO taula_avisos (usuari, accio_intentada, taula_afectada)
        VALUES (CURRENT_USER(), 'UPDATE SALARI/DADES', 'empleats');

        -- 2. Cancel·lar l'operació amb un error de seguretat
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Error de seguretat: No tens permisos per modificar dades crítiques d''empleats.';
    END IF;
END //

DELIMITER ;
```

**Com funciona:**

| Usuari que intenta l'UPDATE | Resultat |
|------------------------------|---------|
| `root@localhost` | Permet la modificació |
| `joan_vendes@%` | Bloqueja + registra a `taula_avisos` |
| `marta_admin@%` (rol admin, però no root) | Bloqueja + registra a `taula_avisos` |

**Prova del trigger:**

```sql
-- Connectat com a usuari no-root, intentar modificar un salari:
UPDATE empleats SET salari = 9999.99 WHERE dni = '12345678A';
-- Resultat esperat: ERROR 1644 (45000): Error de seguretat: No tens permisos...

-- Comprovar que el registre s'ha guardat a la taula d'avisos:
SELECT * FROM taula_avisos;
```

---

### 3.3.4 Events Periòdics — Còpia de Seguretat Automàtica

L'event `ev_backup_diari` s'executa **cada dia a les 02:00** per fer una còpia de seguretat de les taules crítiques de la base de dades.

**Activar el planificador d'events a MySQL:**

```sql
SET GLOBAL event_scheduler = ON;
```

**Creació de l'event:**

```sql
DELIMITER //

CREATE EVENT IF NOT EXISTS ev_backup_diari
ON SCHEDULE EVERY 1 DAY
STARTS (CURRENT_DATE + INTERVAL 1 DAY + INTERVAL 2 HOUR)
DO
BEGIN
    -- Backup de la taula d'empleats
    SELECT * INTO OUTFILE CONCAT('/var/backups/mysql/empleats_', DATE_FORMAT(NOW(), '%Y%m%d'), '.csv')
    FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
    LINES TERMINATED BY '\n'
    FROM empleats;

    -- Backup de la taula de departaments
    SELECT * INTO OUTFILE CONCAT('/var/backups/mysql/departaments_', DATE_FORMAT(NOW(), '%Y%m%d'), '.csv')
    FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
    LINES TERMINATED BY '\n'
    FROM departaments;

    -- Backup de la taula de trucades
    SELECT * INTO OUTFILE CONCAT('/var/backups/mysql/trucades_', DATE_FORMAT(NOW(), '%Y%m%d'), '.csv')
    FIELDS TERMINATED BY ',' OPTIONALLY ENCLOSED BY '"'
    LINES TERMINATED BY '\n'
    FROM trucades;

    -- Registrar l'event de backup a la taula de control
    INSERT INTO taula_avisos (usuari, accio_intentada, taula_afectada)
    VALUES ('EVENT_SCHEDULER', 'BACKUP_DIARI', 'empleats,departaments,trucades');
END //

DELIMITER ;
```

**Justificació de la periodicitat:**

> S'ha escollit periodicitat **diària a les 02:00** perquè és la franja horària de menor activitat d'InnovateTech. Això minimitza l'impacte en el rendiment del servidor i garanteix que les còpies inclouen totes les operacions del dia anterior.

**Verificar que l'event s'ha creat correctament:**

```sql
SHOW EVENTS FROM innovate_tech;
```

---

## 3.4 Verificació i Proves de la Base de Dades

### 3.4.1 Verificació de l'estructura de les taules

```sql
-- Llistar totes les taules de la base de dades
SHOW TABLES FROM innovate_tech;

-- Revisar l'estructura de cada taula
DESCRIBE departaments;
DESCRIBE empleats;
DESCRIBE trucades;
DESCRIBE taula_avisos;
```

### 3.4.2 Verificació dels triggers actius

```sql
-- Llistar tots els triggers de la base de dades
SHOW TRIGGERS FROM innovate_tech;
```

Resultat esperat:

| Trigger | Event | Table | Timing |
|---------|-------|-------|--------|
| `tg_control_quotes` | INSERT | trucades | BEFORE |
| `tg_auditoria_seguretat` | UPDATE | empleats | BEFORE |

### 3.4.3 Verificació dels rols i permisos

```sql
-- Veure els rols existents
SELECT user, host FROM mysql.user WHERE account_locked = 'Y';

-- Veure els permisos d'un rol concret
SHOW GRANTS FOR 'vendes';
SHOW GRANTS FOR 'administracio';
SHOW GRANTS FOR 'admin';
```

### 3.4.4 Prova completa del flux de dades

```sql
-- 1. Consultar tots els departaments
SELECT * FROM departaments;

-- 2. Consultar tots els empleats amb el nom del seu departament
SELECT e.dni, e.nom, e.cognoms, e.correu, e.salari, d.nom_dept
FROM empleats e
LEFT JOIN departaments d ON e.id_dept = d.id_dept;

-- 3. Consultar les trucades d'un empleat concret
SELECT t.id_trucada, t.destinari, t.durada_minuts, t.data_trucada
FROM trucades t
WHERE t.dni_empleat = '87654321B'
ORDER BY t.data_trucada DESC;

-- 4. Consultar els minuts acumulats per empleat aquest mes
SELECT
    e.nom,
    e.cognoms,
    COUNT(t.id_trucada) AS total_trucades,
    IFNULL(SUM(t.durada_minuts), 0) AS minuts_mes
FROM empleats e
LEFT JOIN trucades t ON e.dni = t.dni_empleat
    AND MONTH(t.data_trucada) = MONTH(CURDATE())
    AND YEAR(t.data_trucada) = YEAR(CURDATE())
GROUP BY e.dni, e.nom, e.cognoms;

-- 5. Consultar el registre d'auditoria
SELECT * FROM taula_avisos ORDER BY data_hora DESC;
```

---

## 3.5 Resum de l'Arquitectura de la Base de Dades

```
┌─────────────────────────────────────────────────────────────────────┐
│                    innovate_tech (MySQL a EC2)                       │
│─────────────────────────────────────────────────────────────────────│
│                                                                       │
│  TAULES PRINCIPALS          SEGURETAT I AUDITORIA                    │
│  ─────────────────          ──────────────────────                   │
│  ┌──────────────┐           ┌─────────────────────┐                  │
│  │ departaments │           │    taula_avisos      │                  │
│  └──────┬───────┘           │  (log d'auditoria)  │                  │
│         │ 1:N               └──────────▲──────────┘                  │
│  ┌──────▼───────┐                      │ alimenta                    │
│  │   empleats   │◄──── tg_auditoria_seguretat (BEFORE UPDATE)        │
│  └──────┬───────┘                                                     │
│         │ 1:N                                                         │
│  ┌──────▼───────┐                                                     │
│  │   trucades   │◄──── tg_control_quotes (BEFORE INSERT)             │
│  └──────────────┘                                                     │
│                                                                       │
│  ROLS D'ACCÉS               EVENT PERIÒDIC                           │
│  ────────────               ───────────────                          │
│  admin       → ALL          ev_backup_diari → cada dia 02:00        │
│  administracio → personal   (backup CSV a /var/backups/mysql/)       │
│  vendes      → trucades                                               │
│  treballador → lectura                                                │
│                                                                       │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 3.6 Incidències i Solucions

| Incidència | Causa | Solució aplicada |
|------------|-------|-----------------|
| Error en el SIGNAL del trigger per apostrofes | Les cometes simples dins de `MESSAGE_TEXT` causaven error de sintaxi | Escapar amb doble apòstrof: `''empleat''` |
| L'event no s'executava | El planificador d'events estava desactivat per defecte | Executar `SET GLOBAL event_scheduler = ON;` |
| Error de permisos en `SELECT INTO OUTFILE` | L'usuari MySQL no tenia permisos de sistema de fitxers | Afegir `GRANT FILE ON *.* TO 'root'@'localhost';` i crear el directori `/var/backups/mysql/` amb `mkdir -p` |
| El rol `treballador` no es creava | La versió de MySQL Free Tier no suportava sintaxi de rols sense `@` | Crear el rol com `CREATE ROLE 'treballador'@'%'` |
