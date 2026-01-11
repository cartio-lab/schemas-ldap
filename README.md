# ============================================================ #
# Projeto CARTO
# Autoria: Wagner Calazans
# Ano de criação: 2025
# Versao: 1.1
# IME - Instituto Militar de Engenharia
#
# Arquivo: README.md
# Descrição: Core documentation for LDAP schemas in identity 
#            management for Joint Operations and Disaster Response.
# ============================================================ #

# LDAP Schemas for Project CARTO

This repository contains the **core (heart)** of the identity management system for Project CARTO. It defines the LDAP schema extensions necessary to achieve interoperability between diverse agencies during Joint Operations and Disaster Response (JODR).

The primary goal is to provide a standardized directory structure that allows Military, Civil Defense, and NGOs to share identity data and access controls seamlessly.

---

## 1. Project Architecture

The schemas extend standard object classes to include operational metadata required for command and control environments. This ensures that every "Identity" carries not just personal data, but also operational context.

---

## 2. Technical Specifications

### 2.1 Custom Attributes
The following attributes have been defined to support specialized mission data:

* **`cartoMissionID`**: Unique identifier for the specific operation or theater of activities.
* **`cartoRank`**: Hierarchical position within the specific institution.
* **`cartoOrganizationID`**: Identifier for the agency or branch of origin (e.g., Army, Navy, UN, Red Cross).
* **`cartoClearanceLevel`**: Security level defining access to sensitive operational resources.

### 2.2 Custom ObjectClasses
These classes organize the attributes into logical entities:

| ObjectClass | Superior | Type | Description |
| :--- | :--- | :--- | :--- |
| `cartoPerson` | `inetOrgPerson` | Structural | Main entity for personnel in the field. |
| `cartoResource` | `top` | Structural | Used for technical assets and mobile units. |
| `cartoJointGroup` | `groupOfNames` | Structural | Cross-agency groups for resource sharing. |

---

## 3. Schema Logic Example

Below is the conceptual structure used in the `.schema` files located in this repository:

```text
attributetype ( 1.3.6.1.4.1.99999.1.1 
    NAME 'cartoMissionID' 
    DESC 'Identifier for the Joint Operation' 
    EQUALITY caseIgnoreMatch 
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.15{64} )

objectclass ( 1.3.6.1.4.1.99999.2.1 
    NAME 'cartoPerson' 
    DESC 'CARTO Project Identity' 
    SUP inetOrgPerson STRUCTURAL 
    MAY ( cartoMissionID $ cartoRank $ cartoOrganizationID ) )
```

---

## 4. Deployment and Integration

### Prerequisites
* **OpenLDAP 2.4+** or **Active Directory**.
* Basic schemas loaded: `core.schema`, `cosine.schema`, and `inetorgperson.schema`.

### Installation
1.  Copy the schema files to your LDAP configuration directory.
2.  Include the schema in your `slapd.conf`:
    ```bash
    include /etc/ldap/schema/carto.schema
    ```
3.  Restart the LDAP service to commit changes.

---

## 5. Academic Background

This research is conducted as part of the Master’s Program in Computer Engineering at the **Military Institute of Engineering (IME)**, Brazil.

* **Researcher:** Wagner Calazans
* **Institution:** IME - Instituto Militar de Engenharia
* **Research Focus:** Interoperability in Identity Management for Defense and Public Safety.
* **Timeline:** 2025 - 2026.

---

## 6. License and Usage

This project is intended for academic and defense-related purposes. All rights and distribution are governed by the policies of the Military Institute of Engineering.