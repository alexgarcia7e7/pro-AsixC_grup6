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
